---
title: Refactorización de una aplicación mediante su migración a Azure App Service y Azure SQL Database
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Averigüe cómo Contoso rehospeda una aplicación local al migrarla a una aplicación web de Azure App Service y una base de datos de Azure SQL Server.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: a2798f3d3abe9c301ea35b7b8dd6b4b16cd0056b
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70835178"
---
# <a name="refactor-an-on-premises-app-to-an-azure-app-service-web-app-and-azure-sql-database"></a>Refactorización de una aplicación local a una aplicación web de Azure App Service y a una base de datos de Azure SQL

En este artículo se muestra cómo la compañía ficticia Contoso refactoriza una aplicación de Windows .NET de dos niveles que se ejecuta en máquinas virtuales de VMware como parte de una migración a Azure. Contoso migra la máquina virtual del front-end de la aplicación a una aplicación web de Azure App Service y la base de datos de la aplicación a una base de datos de Azure SQL.

SmartHotel360, la aplicación usada en este ejemplo, se proporciona como código abierto. Si quiere utilizarla para sus propias pruebas, puede descargarla desde [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Impulsores del negocio

El equipo directivo de TI ha trabajado estrechamente con sus socios comerciales para comprender lo quieren lograr con esta migración:

- **Abordar el crecimiento del negocio.** Contoso está creciendo y, como resultado, sus sistemas locales e infraestructura están bajo presión.
- **Aumentar la eficacia.** Contoso debe quitar procedimientos innecesarios y optimizar los procesos para sus desarrolladores y usuarios. La empresa necesita que el departamento de TI sea rápido y no malgaste tiempo ni dinero a fin de satisfacer más rápidamente los requisitos del cliente.
- **Aumentar la agilidad.**  el equipo de TI de Contoso necesita más capacidad de respuesta a las necesidades de la empresa. Debe poder reaccionar con más rapidez que los cambios del mercado para facilitar el éxito en una economía global. No se debe interponer en el camino ni bloquear el negocio.
- **Escala.** a medida que el negocio crece satisfactoriamente, el equipo de TI de Contoso debe proporcionar sistemas que puedan crecer al mismo ritmo.
- **Reducir los costos.** Contoso quiere minimizar los costos de licencia.

## <a name="migration-goals"></a>Objetivos de la migración

El equipo de la nube de Contoso ha establecido los objetivos de esta migración. Estos objetivos se usaron para determinar el mejor método de migración.

<!-- markdownlint-disable MD033 -->

**Requisitos** | **Detalles**
--- | ---
**Aplicación** | La aplicación de Azure seguirá siendo tan importante como lo es hoy en día.<br/><br/> Debe tener las mismas funcionalidades de rendimiento que las que tiene actualmente en VMware.<br/><br/> El equipo no quiere invertir en la aplicación. Por ahora, los administradores simplemente moverán la aplicación de forma segura a la nube.<br/><br/> El equipo quiere finalizar la compatibilidad con Windows Server 2008 R2, donde se ejecuta actualmente la aplicación.<br/><br/> El equipo también quiere abandonar SQL Server 2008 R2 y pasar a una plataforma de base de datos PaaS moderna, lo que minimizará la necesidad de administración.<br/><br/> Contoso quiere aprovechar su inversión en licencias de SQL Server y Software Assurance, tanto como que sea posible.<br/><br/> Además, Contoso quiere mitigar el único punto de error en el nivel web.
**Limitaciones** | La aplicación está formada por una aplicación de ASP.NET y un servicio WCF que se ejecutan en la misma máquina virtual. Contoso quiere dividirlos en dos aplicaciones web con Azure App Service.
**Las tablas de Azure** | Contoso quiere mover la aplicación a Azure, pero no quiere que se ejecute en VM. Quiere usar los servicios de PaaS de Azure para los niveles web y de datos.
**DevOps** | Contoso quiere migrar a un modelo DevOps, con Azure DevOps para las compilaciones y la canalización de versión.

<!-- markdownlint-enable MD033 -->

## <a name="solution-design"></a>Diseño de la solución

Después de fijar los objetivos y requisitos, Contoso diseña y revisa una solución de implementación e identifica el proceso de migración, incluidos los servicios de Azure que usará para la migración.

### <a name="current-app"></a>Aplicación actual

- La aplicación local de SmartHotel360 se divide en niveles entre dos VM (WEBVM y SQLVM).
- Las VM están ubicadas en el host de VMware ESXi **contosohost1.contoso.com** (versión 6.5).
- El entorno de VMware lo administra vCenter Server 6.5 (**vcenter.contoso.com**), que se ejecuta en una VM.
- Contoso tiene un centro de datos local (contoso-datacenter), con un controlador de dominio local (**contosodc1**).
- Las VM locales del centro de datos de Contoso se retirarán después de realizar la migración.

### <a name="proposed-solution"></a>Solución propuesta

- Para el nivel de base de datos de la aplicación, Contoso comparó Azure SQL Database con SQL Server con [este artículo](/azure/sql-database/sql-database-features). Contoso se decantó por Azure SQL Database por diversas razones:
  - Azure SQL Database es un servicio administrado de base de datos relacional. Ofrece un rendimiento predecible en los diferentes niveles del servicio, con administración casi inexistente. Las ventajas incluyen escalabilidad dinámica sin tiempo de inactividad, optimización inteligente integrada y disponibilidad y escalabilidad global.
  - Contoso puede usar la herramienta ligera Data Migration Assistant (DMA) para evaluar y migrar la base de datos local a Azure SQL.
  - Con Software Assurance, Contoso puede intercambiar las licencias existentes por descuentos en una instancia de SQL Database mediante la Ventaja híbrida de Azure para SQL Server. Esto puede proporcionar un ahorro de hasta un 30 %.
  - SQL Database proporciona características de seguridad como, por ejemplo, el enmascaramiento dinámico de datos siempre cifrados y la detección de amenazas o seguridad a nivel de fila.
- Para el nivel web de la aplicación, Contoso ha decidido usar Azure App Service. Este servicio PaaS permite implementar la aplicación con tan solo unos cambios en la configuración. Contoso deberá usar Visual Studio para realizar el cambio e implementar dos aplicaciones web. Una para el sitio web y otra para el servicio WCF.
- Para cumplir los requisitos de una canalización de DevOps, Contoso usará Azure DevOps para la administración de código fuente (SCM) con repositorios de Git. Se usarán compilaciones y versiones automatizadas para compilar el código e implementarlo en Azure App Service.

### <a name="solution-review"></a>Revisión de la solución

Contoso evalúa el diseño propuesto creando una lista de ventajas y desventajas.

<!-- markdownlint-disable MD033 -->

**Consideración** | **Detalles**
--- | ---
**Ventajas** | No será necesario modificar el código de la aplicación SmartHotel360 para la migración a Azure.<br/><br/> Contoso puede aprovechar su inversión en Software Assurance con la Ventaja híbrida de Azure para SQL Server y Windows Server.<br/><br/> Después de la migración, ya no será necesaria la compatibilidad con Windows Server 2008 R2. [Más información](https://support.microsoft.com/lifecycle).<br/><br/> Puede configurar la capa web de la aplicación con varias instancias, para que no haya un único punto de error.<br/><br/> La base de datos ya no dependerá de la antigüedad de SQL Server 2008 R2.<br/><br/> SQL Database es compatible con los requisitos técnicos. Contoso evaluó la base de datos local con Data Migration Assistant y averiguó que es compatible.<br/><br/> Azure SQL Database cuenta con tolerancia a errores integrada que no es necesario que Contoso configure. Esto garantiza que la capa de datos ya no sea un único punto de conmutación por error.
**Desventajas** | Azure App Service solo admite la implementación de una aplicación por cada aplicación web. Esto significa que deben aprovisionarse dos aplicaciones web (una para el sitio web y otra para el servicio WCF).<br/><br/> Si Contoso usa Data Migration Assistant en lugar de Azure Database Migration Service para migrar la base de datos, no tendrán la infraestructura preparada para migrar bases de datos a escala. Contoso deberá compilar otra región para garantizar la conmutación por error si la región principal no está disponible.

<!-- markdownlint-enable MD033 -->

## <a name="proposed-architecture"></a>Arquitectura propuesta

![Arquitectura del escenario](media/contoso-migration-refactor-web-app-sql/architecture.png)

### <a name="migration-process"></a>Proceso de migración

1. Contoso aprovisiona una instancia de Azure SQL y migra a ella la base de datos de SmartHotel360.
2. Contoso aprovisiona y configura las aplicaciones web e implementa la aplicación SmartHotel360 en ellas.

    ![Proceso de migración](media/contoso-migration-refactor-web-app-sql/migration-process.png)

### <a name="azure-services"></a>Servicios de Azure

**Servicio** | **Descripción** | **Costee**
--- | --- | ---
[Data Migration Assistant (DMA)](/sql/dma/dma-overview?view=ssdt-18vs2017) | Contoso usará DMA para valorar y detectar problemas de compatibilidad que podrían afectar a la funcionalidad de su base de datos en Azure. DMA evalúa una paridad de características entre orígenes y destinos de SQL, y recomienda mejoras de rendimiento y confiabilidad. | Es una herramienta que se puede descargar de forma gratuita.
[Azure SQL Database](https://azure.microsoft.com/services/sql-database) | Servicio de base de datos relacional inteligente y completamente administrado en la nube. | Costo basado en características, rendimiento y tamaño. [Más información](https://azure.microsoft.com/pricing/details/sql-database/managed).
[Azure App Service](/azure/app-service/overview) | Permite crear. aplicaciones de nube eficaces mediante una plataforma totalmente administrada | Costo según la duración de uso, la ubicación y el tamaño. [Más información](https://azure.microsoft.com/pricing/details/app-service/windows).
[Azure DevOps](/azure/azure-portal/tutorial-azureportal-devops) | Ofrece integración continua y la canalización de implementación continua (CI/CD) para el desarrollo de aplicaciones. La canalización comienza con un repositorio de Git para administrar código de aplicaciones, un sistema de compilación para producir paquetes y otros artefactos de compilación, y un sistema Release Management para implementar cambios en entornos de desarrollo, prueba y producción.

## <a name="prerequisites"></a>Requisitos previos

Esto es lo que tiene hacer Contoso para ejecutar este escenario:

<!-- markdownlint-disable MD033 -->

**Requisitos** | **Detalles**
--- | ---
**Suscripción de Azure** | En un artículo anterior, Contoso creó suscripciones. Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Si crea una cuenta gratuita, será el administrador de su suscripción y podrá realizar todas las acciones.<br/><br/> Si usa una suscripción existente y no es el administrador, tendrá que solicitar al administrador que le asigne permisos de propietario o colaborador.
**Infraestructura de Azure** | [Vea](contoso-migration-infrastructure.md) cómo Contoso configuró una infraestructura de Azure.

<!--markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Pasos del escenario

Contoso ejecutará la migración de la forma siguiente:

> [!div class="checklist"]
>
> - **Paso 1: Aprovisionamiento de una instancia de SQL Database en Azure.** Contoso proporciona una instancia de SQL en Azure. Después de migrar el sitio web de la aplicación a Azure, la aplicación web del servicio WCF apuntará a esta instancia.
> - **Paso 2: Migración de la base de datos con DMA.** Contoso migra la base de datos de la aplicación con Data Migration Assistant.
> - **Paso 3: Aprovisionamiento de aplicaciones web.** Contoso aprovisiona las dos aplicaciones web.
> - **Paso 4: Configuración de Azure DevOps.** Contoso crea un proyecto de Azure DevOps e importa el repositorio de Git.
> - **Paso 5: Configuración de cadenas de conexión.** Contoso configura las cadenas de conexión para que la instancia de SQL, la aplicación web del servicio WCF y la aplicación web de nivel de web puedan comunicarse.
> - **Paso 6: Configuración de las canalizaciones de compilación y versión.** Como último paso, Contoso configura las canalizaciones de compilación y versión para crear la aplicación y las implementa en dos aplicaciones web independientes.

## <a name="step-1-provision-an-azure-sql-database"></a>Paso 1: Aprovisionar una base de datos de Azure SQL

1. Los administradores de Contoso seleccionan para crear una instancia de SQL Database en Azure.

    ![Aprovisionar SQL](media/contoso-migration-refactor-web-app-sql/provision-sql1.png)

2. Especifican un nombre de base de datos para que coincida con la base de datos que se ejecuta en la máquina virtual local (**SmartHotel.Registration**). Coloca la base de datos en el grupo de recursos ContosoRG. Este es el grupo de recursos que usa para los recursos de producción en Azure.

    ![Aprovisionar SQL](media/contoso-migration-refactor-web-app-sql/provision-sql2.png)

3. Configura una nueva instancia de SQL Server (**sql-smarthotel-eus2**) en la región primaria.

    ![Aprovisionar SQL](media/contoso-migration-refactor-web-app-sql/provision-sql3.png)

4. Establece el plan de tarifa que mejor se adapta a las necesidades de su servidor y base de datos. Así mismo, selecciona esta opción para ahorrar dinero con la Ventaja híbrida de Azure, porque ya tiene una licencia de SQL Server.
5. Para ajustar el tamaño, realiza compras basadas en el núcleo virtual y establece los límites para los requisitos esperados.

    ![Aprovisionar SQL](media/contoso-migration-refactor-web-app-sql/provision-sql4.png)

6. A continuación, Contoso crea la instancia de la base de datos.

    ![Aprovisionar SQL](media/contoso-migration-refactor-web-app-sql/provision-sql5.png)

7. Una vez creada la instancia, abren la base de datos y anotan los detalles que necesitarán cuando usen Data Migration Assistant para la migración.

    ![Aprovisionar SQL](media/contoso-migration-refactor-web-app-sql/provision-sql6.png)

**¿Necesita más ayuda?**

- [Obtenga ayuda](/azure/sql-database/sql-database-get-started-portal) para aprovisionar una instancia de SQL Database.
- [Obtenga información](/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools) acerca de los límites de recursos de núcleo virtual.

## <a name="step-2-migrate-the-database-with-dma"></a>Paso 2: Migración de la base de datos con DMA

Un administrador de Contoso migrará la base de datos de SmartHotel360 con DMA.

### <a name="install-dma"></a>Instalar DMA

1. Descarga la herramienta desde el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=53595) en la VM local de SQL Server (**SQLVM**).
2. Ejecuta el programa de instalación (DownloadMigrationAssistant.msi) en la VM.
3. En la página **Finalizar**, selecciona **Launch Microsoft Data Migration Assistant** (Iniciar Microsoft Data Migration Assistant) antes de finalizar el asistente.

### <a name="migrate-the-database-with-dma"></a>Migración de la base de datos con DMA

1. En DMA, crean un nuevo proyecto (**SmartHotelDB**) y seleccionan **Migración**.
2. Contoso selecciona el tipo de servidor de origen como **SQL Server** y el destino como instancia de **Azure SQL Database**.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-1.png)

3. En los detalles de la migración, agrega **SQLVM** como servidor de origen y la base de datos **SmartHotel.Registration**.

     ![DMA](media/contoso-migration-refactor-web-app-sql/dma-2.png)

4. Recibe un error que parece que se asociará con la autenticación. Sin embargo, después de investigar, el problema es el punto (.) en el nombre de la base de datos. Como alternativa, decide aprovisionar una nueva base de datos SQL con el nombre **SmartHotel-Registration**, para resolver el problema. Cuando vuelve a ejecutar DMA, puede seleccionar **SmartHotel-Registration** y continuar con el asistente.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-3.png)

5. En **Seleccionar objetos**, selecciona las tablas de la base de datos y genera un script de SQL.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-4.png)

6. Una vez que DMA crea el script, seleccionan **Implementar esquema**.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-5.png)

7. DMA confirma que la implementación se realizó correctamente.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-6.png)

8. Luego, se inicia la migración.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-7.png)

9. Una vez finalizada la migración, el administrador de Contoso puede comprobar que la base de datos se ejecuta en la instancia de Azure SQL.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-8.png)

10. Elimina la base de datos SQL adicional **SmartHotel.Registration** de Azure Portal.

    ![DMA](media/contoso-migration-refactor-web-app-sql/dma-9.png)

## <a name="step-3-provision-web-apps"></a>Paso 3: Aprovisionamiento de aplicaciones web

Con la base de datos migrada, el administrador de Contoso ya puede migrar las dos aplicaciones web.

1. Selecciona **Aplicación web** en el portal.

    ![Aplicación web](media/contoso-migration-refactor-web-app-sql/web-app1.png)

2. Proporciona un nombre a la aplicación (**SHWEB EUS2**), la ejecuta en Windows y la coloca en el grupo de recursos de producción **ContosoRG**. Crean una nueva aplicación web y un plan de Azure App Service.

    ![Aplicación web](media/contoso-migration-refactor-web-app-sql/web-app2.png)

3. Después de aprovisionar la aplicación web, repite el proceso para crear una aplicación web para el servicio WCF (**SHWCF EUS2**)

    ![Aplicación web](media/contoso-migration-refactor-web-app-sql/web-app3.png)

4. Una vez que haya terminado, se dirigirá a la dirección de las aplicaciones para comprobar si se crearon correctamente.

## <a name="step-4-set-up-azure-devops"></a>Paso 4: Configurar Azure DevOps

Contoso necesita compilar la infraestructura y las canalizaciones de DevOps para la aplicación. Para ello, los administradores de Contoso crean un proyecto de DevOps, importan el código y luego configuran las canalizaciones de compilación y versión.

1. En la cuenta de Azure DevOps de Contoso, crean un proyecto (**ContosoSmartHotelRefactor**) y seleccionan **Git** como control de versiones.

    ![Nuevo proyecto](./media/contoso-migration-refactor-web-app-sql/vsts1.png)

2. Importa el repositorio de Git que actualmente contiene su código de la aplicación. Se encuentra en un [repositorio público](https://github.com/Microsoft/SmartHotel360-internal-booking-apps) y puede descargarlo.

    ![Descarga del código de la aplicación](./media/contoso-migration-refactor-web-app-sql/vsts2.png)

3. Una vez importado el código, conecta Visual Studio al repositorio y clona el código mediante Team Explorer.

    ![Conectarse al proyecto](./media/contoso-migration-refactor-web-app-sql/devops1.png)

4. Después de clonar el repositorio en la máquina del desarrollador, abren el archivo de la solución para la aplicación. La aplicación web y el servicio WCF tienen cada uno proyectos separados dentro del archivo.

    ![Archivo de soluciones](./media/contoso-migration-refactor-web-app-sql/vsts4.png)

## <a name="step-5-configure-connection-strings"></a>Paso 5: Configurar cadenas de conexión

El administrador de Contoso necesita asegurarse de que las aplicaciones web y la base de datos pueden comunicarse. Para ello, configura las cadenas de conexión en el código y en las aplicaciones web.

1. En la aplicación web para el servicio WCF (**SHWCF EUS2**) > **Configuración** > **Configuración de la aplicación**, agrega una nueva cadena de conexión denominada **DefaultConnection**.
2. La cadena de conexión se extrae de la base de datos **SmartHotel-Registration** y debe actualizarse con las credenciales correctas.

    ![Cadena de conexión](media/contoso-migration-refactor-web-app-sql/string1.png)

3. En Visual Studio, abre el proyecto **SmartHotel.Registration.wcf** desde el archivo de la solución. La sección **connectionStrings** del archivo web.config para el servicio WCF SmartHotel.Registration.Wcf debe actualizarse con la cadena de conexión.

     ![Cadena de conexión](media/contoso-migration-refactor-web-app-sql/string2.png)

4. La sección de **cliente** del archivo web.config para SmartHotel.Registration.Web debe cambiarse para que apunte a la nueva ubicación del servicio WCF. Se trata de la dirección URL de la aplicación web WCF que hospeda el punto de conexión de servicio.

    ![Cadena de conexión](media/contoso-migration-refactor-web-app-sql/strings3.png)

5. Después de hacer los cambios en el código, el administrador debe confirmar los cambios. Con Team Explorer en Visual Studio, confirman y sincronizan.

## <a name="step-6-set-up-build-and-release-pipelines-in-azure-devops"></a>Paso 6: Configurar canalizaciones de compilación y versión en Azure DevOps

Los administradores de Contoso configuran ahora Azure DevOps para ejecutar el proceso de compilación y versión.

1. En Azure DevOps, seleccionan **Compilación y versión** > **Nueva canalización**.

    ![Nueva canalización](./media/contoso-migration-refactor-web-app-sql/pipeline1.png)

2. Seleccionan **Repositorio GIT de Azure Repos** y el repositorio correspondiente.

    ![GIT y el repositorio](./media/contoso-migration-refactor-web-app-sql/pipeline2.png)

3. En **Seleccionar una plantilla**, selecciona la plantilla de ASP.NET para su compilación.

     ![Plantilla de ASP.NET](./media/contoso-migration-refactor-web-app-sql/pipeline3.png)

4. Se utiliza el nombre **ContosoSmartHotelRefactor-ASP.NET-CI** para la compilación. Seleccionan **Guardar y poner en cola**.

     ![Guardar y poner en cola](./media/contoso-migration-refactor-web-app-sql/pipeline4.png)

5. Así se inicia la primera compilación. Seleccionan el número de compilación para ver el proceso. Cuando terminan, pueden ver los comentarios del proceso y seleccionar **Artifacts** para revisar los resultados de la compilación.

    ![Revisión](./media/contoso-migration-refactor-web-app-sql/pipeline5.png)

6. La carpeta de **entrega** contiene los resultados de la compilación.

    - Los dos archivos ZIP son los paquetes que contienen las aplicaciones.
    - Estos archivos se usan en la canalización de versión para la implementación en Azure App Service.

     ![Artefacto](./media/contoso-migration-refactor-web-app-sql/pipeline6.png)

7. Seleccionan **Versiones** >  **+Nueva canalización**.

    ![Nueva canalización](./media/contoso-migration-refactor-web-app-sql/pipeline7.png)

8. Seleccionan la plantilla de implementación de Azure App Service.

    ![Plantilla de implementación de Azure App Service](./media/contoso-migration-refactor-web-app-sql/pipeline8.png)

9. Asignan a la canalización de versión el nombre **ContosoSmartHotel360Refactor** y especifican el nombre de la aplicación web WCF (SHWCF-EUS2) como nombre de **Fase**.

    ![Entorno](./media/contoso-migration-refactor-web-app-sql/pipeline9.png)

10. En las fases, seleccionan **1 phase, 1 task** (1 fase, 1 tarea) para configurar la implementación del servicio WCF.

    ![Implementar WCF](./media/contoso-migration-refactor-web-app-sql/pipeline10.png)

11. Comprueba que la suscripción esté seleccionada y autorizada, y selecciona el **Nombre de App Service**.

     ![Selección del nombre de App Service](./media/contoso-migration-refactor-web-app-sql/pipeline11.png)

12. En la compilación > **Artifacts**, seleccionan **+Add an artifact** (+Agregar un artefacto) y optan por compilar con la canalización **ContosoSmarthotel360Refactor**.

     ![Compilación](./media/contoso-migration-refactor-web-app-sql/pipeline12.png)

13. Seleccionan el icono de rayo en el artefacto para habilitar el desencadenador de implementación continua.

     ![Rayo](./media/contoso-migration-refactor-web-app-sql/pipeline13.png)

14. El desencadenador de implementación continua debe estar establecido en **Habilitado**.

    ![Implementación continua habilitada](./media/contoso-migration-refactor-web-app-sql/pipeline14.png)

15. Ahora, vuelven a la fase 1 trabajo, 1 tarea y seleccionan **Implementar Azure App Service**.

    ![Implementar Azure App Service](./media/contoso-migration-refactor-web-app-sql/pipeline15.png)

16. En **Seleccione un archivo o carpeta**, ubican el archivo **SmartHotel.Registration.Wcf.zip** que se ha creado durante la compilación y seleccionan **Guardar**.

    ![Guardar WCF](./media/contoso-migration-refactor-web-app-sql/pipeline16.png)

17. Seleccionan **Canalización** > **Fases** **+Agregar** para agregar un entorno para **SHWEB EUS2**. Seleccionan otra implementación de Azure App Service.

    ![Agregar entorno](./media/contoso-migration-refactor-web-app-sql/pipeline17.png)

18. Repite el proceso para publicar el archivo de aplicación web (**SmartHotel.Registration.Web.zip**) en la aplicación web correcta.

    ![Publicar aplicación web](./media/contoso-migration-refactor-web-app-sql/pipeline18.png)

19. Después de guardarla, la canalización de versión se mostrará como sigue.

     ![Resumen de la canalización de versión](./media/contoso-migration-refactor-web-app-sql/pipeline19.png)

20. Vuelven a **Compilar** y seleccionan **Desencadenadores** > **Habilitar la integración continua**. Esto habilita la canalización para que, cuando se confirmen los cambios en el código, se produzcan la compilación y el lanzamiento completos.

    ![Habilitar la integración continua](./media/contoso-migration-refactor-web-app-sql/pipeline20.png)

21. Seleccionan **Guardar y poner en cola** para ejecutar la canalización completa. Se desencadena una nueva compilación que, a su vez, crea la primera versión de la aplicación en Azure App Service.

    ![Guardar la canalización](./media/contoso-migration-refactor-web-app-sql/pipeline21.png)

22. Los administradores de Contoso pueden seguir el proceso de canalización de compilación y versión en Azure DevOps. Una vez finalizada la compilación, se iniciará el lanzamiento.

    ![Compilar y lanzar la aplicación](./media/contoso-migration-refactor-web-app-sql/pipeline22.png)

23. Una vez finalizada la canalización, se han implementado ambos sitios, y la aplicación está funcionamiento en línea.

    ![Finalizar el lanzamiento](./media/contoso-migration-refactor-web-app-sql/pipeline23.png)

En este momento, la aplicación se ha migrado correctamente a Azure.

## <a name="clean-up-after-migration"></a>Limpiar después de la migración

Después de la migración, Contoso debe completar estos pasos de limpieza:

- Quitar las VM locales del inventario de vCenter.
- Quitar las VM de los trabajos de copia de seguridad locales.
- Actualizar la documentación interna para que muestre las nuevas ubicaciones para la aplicación SmartHotel360. Mostrar la base de datos en ejecución en Azure SQL Database y el front-end en ejecución en dos aplicaciones web.
- Revisar los recursos que interactúan con las VM retiradas y actualizar los valores de configuración pertinentes o la documentación para reflejar la nueva configuración.

## <a name="review-the-deployment"></a>Revisar la implementación

Con los recursos migrados de Azure, Contoso debe proteger la infraestructura nueva y ponerla totalmente en marcha.

### <a name="security"></a>Seguridad

- Contoso debe asegurarse de que su nueva base de datos **SmartHotel-Registration** es segura. [Más información](/azure/sql-database/sql-database-security-overview).
- En concreto, Contoso debe actualizar las aplicaciones web para usar SSL con certificados.

### <a name="backups"></a>Copias de seguridad

- Contoso necesita revisar los requisitos de copia de seguridad para Azure SQL Database. [Más información](/azure/sql-database/sql-database-automated-backups).
- Contoso también necesita aprender a administrar las copias de seguridad y restauraciones SQL Database. [Más información](/azure/sql-database/sql-database-automated-backups) sobre las copias de seguridad automáticas.
- Contoso debe considerar la implementación de grupos de conmutación por error para proporcionar conmutación por error regional para la base de datos. [Más información](/azure/sql-database/sql-database-geo-replication-overview).
- Contoso debe considerar la implementación de la aplicación web en las regiones principales Este de EE. UU. 2 y Centro de EE. UU. a fin de obtener resistencia. Contoso podría configurar Traffic Manager para garantizar la conmutación por error en caso de que se produzcan interrupciones regionales.

### <a name="licensing-and-cost-optimization"></a>Optimización de los costos y licencias

- Una vez implementados todos los recursos, Contoso debe asignar etiquetas de Azure según la [planificación de su infraestructura](contoso-migration-infrastructure.md#set-up-tagging).
- Todas las licencias se integran en el costo de los servicios de PaaS que consume Contoso. Esto se deducirá del contrato Enterprise.
- Contoso habilitará Azure Cost Management bajo licencia de Cloudyn, una subsidiaria de Microsoft. Se trata de una solución de administración de costos en varias nubes que le permitirá utilizar y administrar Azure y otros recursos en la nube. [Más información](/azure/cost-management/overview) sobre Azure Cost Management.

## <a name="conclusion"></a>Conclusión

En este artículo, Contoso refactorizó la aplicación SmartHotel360 en Azure mediante la migración de la máquina virtual de front-end de la aplicación a dos aplicaciones web de Azure App Service. La base de datos de la aplicación se migró a una base de datos de Azure SQL.
