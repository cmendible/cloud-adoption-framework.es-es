---
title: Rediseño de una aplicación en un contenedor de Azure y Azure SQL Database
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información de cómo Contoso rediseña la arquitectura de una aplicación en contenedores Windows de Azure y Azure SQL Database.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 6b9d2e5f4b230358985d04aca075cb89e8214422
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70837998"
---
# <a name="rearchitect-an-on-premises-app-to-an-azure-container-and-azure-sql-database"></a>Rediseño de la arquitectura de una aplicación local en un contenedor de Azure y Azure SQL Database

En este artículo se muestra cómo la compañía ficticia Contoso rediseña una aplicación de Windows .NET de dos niveles que se ejecuta en máquinas virtuales de VMware como parte de una migración a Azure. Contoso migra la máquina virtual de front-end de la aplicación a un contenedor Windows de Azure, y la base de datos de la aplicación a una base de datos de Azure SQL.

SmartHotel360, la aplicación usada en este ejemplo, se proporciona como código abierto. Si quiere utilizarla para sus propias pruebas, puede descargarla desde [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Impulsores del negocio

El equipo directivo de TI de Contoso ha trabajado estrechamente con sus socios comerciales para comprender lo quieren lograr con esta migración:

- **Abordar el crecimiento del negocio.** Contoso está creciendo y, como resultado, sus sistemas locales e infraestructura están bajo presión.
- **Aumentar la eficacia.** Contoso debe quitar procedimientos innecesarios y optimizar los procesos para sus desarrolladores y usuarios. La empresa necesita que el departamento de TI sea rápido y no malgaste tiempo ni dinero a fin de satisfacer más rápidamente los requisitos del cliente.
- **Aumentar la agilidad.** el equipo de TI de Contoso necesita más capacidad de respuesta a las necesidades de la empresa. Debe poder reaccionar con más rapidez que los cambios del mercado para facilitar el éxito en una economía global. No se debe interponer en el camino ni bloquear el negocio.
- **Escala.** a medida que el negocio crece satisfactoriamente, el equipo de TI de Contoso debe proporcionar sistemas que puedan crecer al mismo ritmo.
- **Reducir los costos.** Contoso quiere minimizar los costos de licencia.

## <a name="migration-goals"></a>Objetivos de la migración

El equipo de la nube de Contoso ha establecido los objetivos de esta migración. Estos objetivos se usaron para determinar el mejor método de migración.

<!-- markdownlint-disable MD033 -->

**Objetivos** | **Detalles**
--- | ---
**Solicitudes de aplicación** | La aplicación de Azure seguirá siendo tan importante como lo es hoy en día.<br/><br/> Debe tener las mismas funcionalidades de rendimiento que las que tiene actualmente en VMware.<br/><br/> Contoso quiere detener la compatibilidad con Windows Server 2008 R2, donde se ejecuta actualmente la aplicación, para invertir en dicha aplicación.<br/><br/> También quiere abandonar SQL Server 2008 R2 y pasar a una plataforma de base de datos PaaS moderna, lo que minimizará la necesidad de administración.<br/><br/> Contoso quiere aprovechar su inversión en licencias de SQL Server y Software Assurance, tanto como que sea posible.<br/><br/> Contoso quiere poder escalar verticalmente la capa de aplicación web.
**Limitaciones** | La aplicación está formada por una aplicación de ASP.NET y un servicio WCF que se ejecutan en la misma máquina virtual. Contoso quiere dividirlos en dos aplicaciones web con Azure App Service.
**Solicitudes de Azure** | Contoso quiere mover la aplicación a Azure y ejecutarla en un contenedor para prolongar su duración. No quiere empezar a implementar la aplicación en Azure completamente desde cero.
**DevOps** | Contoso quiere migrar a un modelo de DevOps con Azure DevOps Services para las compilaciones de código y la canalización de versión.

<!-- markdownlint-enable MD033 -->

## <a name="solution-design"></a>Diseño de la solución

Después de fijar sus objetivos y requisitos, Contoso diseña y revisa una solución de implementación e identifica el proceso de migración, incluidos los servicios de Azure que Contoso usará para ello.

### <a name="current-app"></a>Aplicación actual

- La aplicación local de SmartHotel360 se divide en niveles entre dos VM (WEBVM y SQLVM).
- Las VM están ubicadas en el host de VMware ESXi **contosohost1.contoso.com** (versión 6.5).
- El entorno de VMware lo administra vCenter Server 6.5 (**vcenter.contoso.com**), que se ejecuta en una VM.
- Contoso tiene un centro de datos local (contoso-datacenter), con un controlador de dominio local (**contosodc1**).
- Las VM locales del centro de datos de Contoso se retirarán después de realizar la migración.

### <a name="proposed-architecture"></a>Arquitectura propuesta

- Para el nivel de base de datos de la aplicación, Contoso comparó Azure SQL Database con SQL Server con [este artículo](/azure/sql-database/sql-database-features). Se decantó por Azure SQL Database por diversas razones:
  - Azure SQL Database es un servicio administrado de base de datos relacional. Ofrece un rendimiento predecible en los diferentes niveles del servicio, con administración casi inexistente. Las ventajas incluyen escalabilidad dinámica sin tiempo de inactividad, optimización inteligente integrada y disponibilidad y escalabilidad global.
  - Contoso usa la herramienta ligera Data Migration Assistant (DMA) para evaluar y migrar la base de datos local a Azure SQL.
  - Con Software Assurance, Contoso puede intercambiar sus licencias existentes por descuentos en una instancia de SQL Database mediante la Ventaja híbrida de Azure para SQL Server. Esto puede proporcionar un ahorro de hasta un 30 %.
  - SQL Database proporciona varias características de seguridad, incluidos el enmascaramiento dinámico de datos siempre cifrados y la detección de amenazas o seguridad a nivel de fila.
- Contoso ha decidido convertir la capa de aplicación web en el contenedor de Windows con Azure DevOps Services.
  - Contoso implementará la aplicación con Azure Service Fabric y extraerá la imagen de contenedor de Windows desde Azure Container Registry (ACR).
  - Implementarán un prototipo para ampliar la aplicación con la inclusión del análisis de sentimiento, como otro servicio en Service Fabric, conectado a Cosmos DB. Esto leerá la información de Tweets y la mostrará en la aplicación.
- Para implementar una canalización de DevOps, Contoso usará Azure DevOps para la administración de código fuente (SCM) con repositorios de Git. Las compilaciones y versiones automatizadas se usarán para compilar el código e implementarlo en Azure Container Registry y Azure Service Fabric.

    ![Arquitectura del escenario](./media/contoso-migration-rearchitect-container-sql/architecture.png)

### <a name="solution-review"></a>Revisión de la solución

Contoso evalúa el diseño propuesto y crea una lista de ventajas y desventajas.

<!-- markdownlint-disable MD033 -->

**Consideración** | **Detalles**
--- | ---
**Ventajas** | No será necesario modificar el código de la aplicación SmartHotel360 para la migración a Azure Service Fabric. Sin embargo, el esfuerzo es mínimo, si se usa SDK Tools de Service Fabric para los cambios.<br/><br/> Con el paso a Service Fabric, Contoso puede empezar a desarrollar microservicios para agregarlos a la aplicación rápidamente a lo largo del tiempo, sin riesgo para el código base original.<br/><br/> Los contenedores de Windows ofrecen las mismas ventajas que los contenedores en general. Mejoran la agilidad, la portabilidad y el control.<br/><br/> Contoso puede aprovechar su inversión en Software Assurance con la Ventaja híbrida de Azure para SQL Server y Windows Server.<br/><br/> Después de la migración ya no necesitarán la compatibilidad con Windows Server 2008 R2. [Más información](https://support.microsoft.com/lifecycle).<br/><br/> Puede configurar la capa web de la aplicación con varias instancias, para que no haya un único punto de error.<br/><br/> Ya no se dependerá de la antigüedad de SQL Server 2008 R2.<br/><br/> SQL Database es compatible con los requisitos técnicos de Contoso. Los administradores de Contoso evaluaron la base de datos local con Data Migration Assistant y descubrieron que es compatible.<br/><br/> SQL Database cuenta con tolerancia a errores integrada que no es necesario que Contoso configure. Esto garantiza que la capa de datos ya no sea un único punto de conmutación por error.
**Desventajas** | Los contenedores son más complejos que otras opciones de migración. La curva de aprendizaje de los contenedores podría ser un problema para Contoso. Introducen un nuevo nivel de complejidad que proporciona un gran valor a pesar de la curva.<br/><br/> El equipo de operaciones de Contoso deberá esforzarse para comprender y ofrecer soporte técnico de Azure, los contenedores y los microservicios de la aplicación.<br/><br/> Si Contoso usa Data Migration Assistant en lugar de Azure Database Migration Service para migrar la base de datos, no tendrán la infraestructura preparada para migrar bases de datos a escala.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Proceso de migración

1. Contoso aprovisiona el clúster de Azure Service Fabric para Windows.
2. Aprovisiona una instancia de Azure SQL y migra a ella la base de datos de SmartHotel360.
3. Contoso convierte la máquina virtual de capa web en un contenedor de Docker con las herramientas del SDK de Service Fabric.
4. Conecta el clúster de Service Fabric y el ACR, e implementa la aplicación con Azure Service Fabric.

    ![Proceso de migración](./media/contoso-migration-rearchitect-container-sql/migration-process.png)

### <a name="azure-services"></a>Servicios de Azure

**Servicio** | **Descripción** | **Costee**
--- | --- | ---
[Data Migration Assistant (DMA)](/sql/dma/dma-overview?view=ssdt-18vs2017) | Evalúa y detecta problemas de compatibilidad que pueden afectar a la funcionalidad de la base de datos en Azure. DMA evalúa una paridad de características entre orígenes y destinos de SQL, y recomienda mejoras de rendimiento y confiabilidad. | Es una herramienta que se puede descargar de forma gratuita.
[Azure SQL Database](https://azure.microsoft.com/services/sql-database) | Proporcione un servicio de base de datos relacional inteligente y completamente administrado en la nube. | Costo basado en características, rendimiento y tamaño. [Más información](https://azure.microsoft.com/pricing/details/sql-database/managed).
[Azure Container Registry](https://azure.microsoft.com/services/container-registry) | Almacena imágenes para todos los tipos de implementaciones de contenedor. | Costo basado en características, almacenamiento y duración de la utilización. [Más información](https://azure.microsoft.com/pricing/details/container-registry).
[Azure Service Fabric](https://azure.microsoft.com/services/service-fabric) | Compila y usa aplicaciones escalables y distribuidas que estén siempre disponibles. | Costo basado en tamaño, ubicación y duración de los nodos de proceso. [Más información](https://azure.microsoft.com/pricing/details/service-fabric).
[Azure DevOps](/azure/azure-portal/tutorial-azureportal-devops) | Ofrece integración continua y la canalización de implementación continua (CI/CD) para el desarrollo de aplicaciones. La canalización comienza con un repositorio de Git para administrar código de aplicaciones, un sistema de compilación para producir paquetes y otros artefactos de compilación, y un sistema Release Management para implementar cambios en entornos de desarrollo, prueba y producción.

## <a name="prerequisites"></a>Requisitos previos

Esto es lo que tiene hacer Contoso para ejecutar este escenario:

<!-- markdownlint-disable MD033 -->

**Requisitos** | **Detalles**
--- | ---
**Suscripción de Azure** | Suscripciones creadas por Contoso anteriormente en esta serie de artículos. Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Si crea una cuenta gratuita, será el administrador de su suscripción y podrá realizar todas las acciones.<br/><br/> Si usa una suscripción existente y no es el administrador, tendrá que solicitar al administrador que le asigne permisos de propietario o colaborador.
**Infraestructura de Azure** | [Vea](contoso-migration-infrastructure.md) cómo Contoso configuró anteriormente una infraestructura de Azure.
**Requisitos previos para desarrolladores** | Contoso necesita las siguientes herramientas en una estación de trabajo de desarrollador:<br/><br/> - [Visual Studio 2017 Community Edition: Versión 15.5](https://www.visualstudio.com)<br/><br/> - Carga de trabajo. NET habilitada.<br/><br/> - [Git](https://git-scm.com)<br/><br/> - [SDK de Service Fabric v 3.0 o posterior](/azure/service-fabric/service-fabric-get-started)<br/><br/> - [Docker CE (Windows 10) o Docker EE (Windows Server)](https://docs.docker.com/docker-for-windows/install) configurado para usar contenedores de Windows.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Pasos del escenario

Así es cómo Contoso ejecuta la migración:

> [!div class="checklist"]
>
> - **Paso 1: Aprovisionamiento de una instancia de SQL Database en Azure.** Contoso proporciona una instancia de SQL en Azure. Después de migrar la máquina virtual web de front-end a un contenedor de Azure, la instancia de contenedor con el front-end web de la aplicación apuntará a esta base de datos.
> - **Paso 2: Crear una instancia de Azure Container Registry (ACR).** Contoso aprovisiona un registro de contenedor empresarial para las imágenes de contenedor de Docker.
> - **Paso 3: Aprovisionar Azure Service Fabric.** Aprovisiona un clúster de Service Fabric.
> - **Paso 4: Administrar los certificados de Service Fabric.** Contoso configura los certificados para el acceso de Azure DevOps Services al clúster.
> - **Paso 5: Migración de la base de datos con DMA.** Migra la base de datos de la aplicación con Data Migration Assistant.
> - **Paso 6: Configurar Azure DevOps Services.** Contoso configura un nuevo proyecto en Azure DevOps Services e importa el código al repositorio de Git.
> - **Paso 7: Convertir la aplicación.** Contoso convierte la aplicación en un contenedor con Azure DevOps Services y SDK Tools.
> - **Paso 8: Configurar la compilación y la versión.** Contoso configura las canalizaciones de compilación y versión para crear y publicar la aplicación en el ACR y un clúster de Service Fabric.
> - **Paso 9: Extensión de la aplicación.** Después de que la aplicación es pública, Contoso la extiende para aprovechar las funcionalidades de Azure y la vuelve a publicar en Azure mediante la canalización.

## <a name="step-1-provision-an-azure-sql-database"></a>Paso 1: Aprovisionar una base de datos de Azure SQL

Los administradores de Contoso aprovisionan una base de datos de Azure SQL.

1. Seleccionan **SQL Database** para crear una base de datos SQL en Azure.

    ![Aprovisionar SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql1.png)

2. Especifican un nombre de base de datos para que coincida con la base de datos que se ejecuta en la máquina virtual local (**SmartHotel.Registration**). Coloca la base de datos en el grupo de recursos ContosoRG. Este es el grupo de recursos que usa para los recursos de producción en Azure.

    ![Aprovisionar SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql2.png)

3. Configura una nueva instancia de SQL Server (**sql-smarthotel-eus2**) en la región primaria.

    ![Aprovisionar SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql3.png)

4. Establecen el plan de tarifa que mejor se adapta a las necesidades de su servidor y base de datos. Así mismo, selecciona esta opción para ahorrar dinero con la Ventaja híbrida de Azure, porque ya tiene una licencia de SQL Server.
5. Para ajustar el tamaño, realizan compras basadas en el núcleo virtual y establecen los límites para los requisitos esperados.

    ![Aprovisionar SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql4.png)

6. A continuación, Contoso crea la instancia de la base de datos.

    ![Aprovisionar SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql5.png)

7. Una vez creada la instancia, abren la base de datos y anotan los detalles que necesitarán cuando usen Data Migration Assistant para la migración.

    ![Aprovisionar SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql6.png)

**¿Necesita más ayuda?**

- [Obtenga ayuda](/azure/sql-database/sql-database-get-started-portal) para aprovisionar una instancia de SQL Database.
- [Obtenga información](/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools) acerca de los límites de recursos de núcleo virtual.

## <a name="step-2-create-an-acr-and-provision-an-azure-container"></a>Paso 2: Crear un ACR y aprovisionar un contenedor de Azure

El contenedor de Azure se crea con los archivos exportados de la máquina virtual web. El contenedor se aloja en Azure Container Registry (ACR).

1. Los administradores de Contoso crean una instancia de Container Registry en Azure Portal.

     ![Container Registry](./media/contoso-migration-rearchitect-container-sql/container-registry1.png)

2. Proporcionan un nombre para el registro (**contosoacreus2**) y lo colocan en la región primaria, en el grupo de recursos que usan para sus recursos de infraestructura. Habilitan el acceso de usuarios administradores y lo establecen como SKU premium para que puedan usar la replicación geográfica.

    ![Container Registry](./media/contoso-migration-rearchitect-container-sql/container-registry2.png)

## <a name="step-3-provision-azure-service-fabric"></a>Paso 3: Aprovisionar Azure Service Fabric

El contenedor SmartHotel360 se ejecutará en el clúster de Azure Service Fabric. Los administradores de Contoso crean el clúster de Service Fabric de la manera siguiente:

1. Cree un recurso de Service Fabric desde Azure Marketplace.

     ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric1.png)

2. En **Básico**, especifican un nombre único de DS para el clúster y las credenciales para obtener acceso a la máquina virtual local. Colocan el recurso en el grupo de recursos de producción (**ContosoRG**) en la región primaria Este de EE.UU. 2.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric2.png)

3. En **Configuración del tipo de nodo**, especifican un nombre de tipo de nodo, la configuración de durabilidad, el tamaño de máquina virtual y los puntos de conexión de la aplicación.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric3.png)

4. En **Crear Key Vault**, crean un nuevo almacén de claves en su grupo de recursos de infraestructura, para alojar el certificado.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric4.png)

5. En **Directivas de acceso**, habilitan el acceso a las máquinas virtuales para implementar el almacén de claves.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric5.png)

6. Especifican un nombre para el certificado.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric6.png)

7. En la página de resumen, copian el vínculo que se usa para descargar el certificado. Lo necesitan para conectarse al clúster de Service Fabric.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric7.png)

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric8.png)

8. Después de la validación correcta, aprovisionan el clúster.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric9.png)

9. En el Asistente para importar certificados, importan el certificado descargado a equipos de desarrollo. El certificado se usa para autenticarse en el clúster.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric10.png)

10. Después de aprovisionar el clúster, se conectan al explorador de clúster de Service Fabric.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric11.png)

11. Deben seleccionar el certificado correcto.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric12.png)

12. Se carga la instancia de Service Fabric Explorer y el administrador de Contoso puede administrar el clúster.

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric13.png)

## <a name="step-4-manage-service-fabric-certificates"></a>Paso 4: Administrar los certificados de Service Fabric

Contoso necesita certificados de clúster para permitir el acceso de Azure DevOps Services al clúster. Los administradores de Contoso se encargan de su configuración.

1. Abren Azure Portal y van hasta Key Vault.
2. Abren los certificados y copian la huella digital del certificado que se creó durante el proceso de aprovisionamiento.

    ![Copia de la huella digital](./media/contoso-migration-rearchitect-container-sql/cert1.png)

3. La copian en un archivo de texto para consultarla más adelante.
4. Ahora, agregan un certificado de cliente que se convertirá en un certificado de cliente de administrador en el clúster. Esto permite a Azure DevOps Services conectarse al clúster para la implementación de la aplicación en la canalización de versión. Para ello, abren Key Vault en el portal y seleccionan **Certificados** > **Generar/Importar**.

    ![Generación del certificado de cliente](./media/contoso-migration-rearchitect-container-sql/cert2.png)

5. Escriben el nombre del certificado y proporcionan un nombre distintivo de X.509 en **Subject** (Asunto).

     ![Nombre del certificado](./media/contoso-migration-rearchitect-container-sql/cert3.png)

6. Una vez creado el certificado, lo descargan localmente en formato PFX.

     ![Descarga del certificado](./media/contoso-migration-rearchitect-container-sql/cert4.png)

7. Ahora, vuelven a la lista de certificados en el almacén de claves y copian la huella digital del certificado de cliente que se acaba de crear. Esta huella digital la guardan en el archivo de texto.

     ![Huella digital del certificado de cliente](./media/contoso-migration-rearchitect-container-sql/cert5.png)

8. Para la implementación de Azure DevOps Services, han de determinar el valor Base64 del certificado. Esto lo hacen en la estación de trabajo de desarrollador local mediante PowerShell. Pegan la salida en un archivo de texto para usarla en otro momento.

    ```powershell
    [System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("C:\path\to\certificate.pfx"))
    ```

     ![Valor de Base64](./media/contoso-migration-rearchitect-container-sql/cert6.png)

9. Por último, agregan el nuevo certificado al clúster de Service Fabric. Para ello, en el portal, abren el clúster y seleccionan **Seguridad**.

     ![Incorporación del certificado de cliente](./media/contoso-migration-rearchitect-container-sql/cert7.png)

10. Seleccionan **Agregar** > **Cliente de administración** y pegan la huella digital del nuevo certificado de cliente. Luego, seleccionan **Agregar**. Esta operación puede tardar hasta 15 minutos.

     ![Incorporación del certificado de cliente](./media/contoso-migration-rearchitect-container-sql/cert8.png)

## <a name="step-5-migrate-the-database-with-dma"></a>Paso 5: Migración de la base de datos con DMA

Los administradores de Contoso ahora pueden migrar la base de datos SmartHotel360 con DMA.

### <a name="install-dma"></a>Instalar DMA

1. Descarga la herramienta desde el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=53595) en la VM local de SQL Server (**SQLVM**).
2. Ejecuta el programa de instalación (DownloadMigrationAssistant.msi) en la VM.
3. En la página **Finalizar**, selecciona **Launch Microsoft Data Migration Assistant** (Iniciar Microsoft Data Migration Assistant) antes de finalizar el asistente.

### <a name="configure-the-firewall"></a>Configuración del firewall

Para conectarse a Azure SQL Database, los administradores de Contoso configuran una regla de firewall para permitir el acceso.

1. En las propiedades de **Firewall y redes virtuales** para la base de datos, permiten el acceso a servicios de Azure y agregan una regla para la dirección IP del cliente de la máquina virtual de SQL Server local.
2. Se crea una regla de firewall de nivel de servidor.

    ![Firewall](./media/contoso-migration-rearchitect-container-sql/sql-firewall.png)

**¿Necesita más ayuda?**

[Obtenga información sobre](/azure/sql-database/sql-database-firewall-configure) la creación y la administración de reglas de firewall para Azure SQL Database.

### <a name="migrate"></a>Migrar

Los administradores de Contoso ahora migran la base de datos.

1. En DMA, crea un nuevo proyecto (**SmartHotelDB**) y selecciona **Migración**.
2. Contoso selecciona el tipo de servidor de origen como **SQL Server** y el destino como instancia de **Azure SQL Database**.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-1.png)

3. En los detalles de la migración, agrega **SQLVM** como servidor de origen y la base de datos **SmartHotel.Registration**.

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-2.png)

4. Recibe un error que parece que se asociará con la autenticación. Sin embargo, después de investigar, el problema es el punto (.) en el nombre de la base de datos. Como alternativa, decide aprovisionar una nueva base de datos SQL con el nombre **SmartHotel-Registration**, para resolver el problema. Cuando vuelve a ejecutar DMA, puede seleccionar **SmartHotel-Registration** y continuar con el asistente.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-3.png)

5. En **Seleccionar objetos**, selecciona las tablas de la base de datos y genera un script de SQL.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-4.png)

6. Una vez que DMA crea el script, seleccionan **Implementar esquema**.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-5.png)

7. DMA confirma que la implementación se realizó correctamente.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-6.png)

8. Luego, se inicia la migración.

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-7.png)

9. Una vez finalizada la migración, Contoso puede comprobar que la base de datos se ejecuta en la instancia de SQL Azure.

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-8.png)

10. Elimina la base de datos SQL adicional **SmartHotel.Registration** de Azure Portal.

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-9.png)

## <a name="step-6-set-up-azure-devops-services"></a>Paso 6: Configurar Azure DevOps Services

Contoso necesita compilar la infraestructura y las canalizaciones de DevOps para la aplicación. Para ello, los administradores de Contoso crean un proyecto de Azure DevOps, importan el código y luego las canalizaciones de compilación y versión.

1. En la cuenta de Azure DevOps de Contoso, crean un proyecto (**ContosoSmartHotelRearchitect**) y seleccionan **Git** como control de versiones.
![Nuevo proyecto](./media/contoso-migration-rearchitect-container-sql/vsts1.png)

2. Importa el repositorio de Git que actualmente contiene su código de la aplicación. Se encuentra en un [repositorio público](https://github.com/Microsoft/SmartHotel360-internal-booking-apps) y puede descargarlo.

    ![Descarga del código de la aplicación](./media/contoso-migration-rearchitect-container-sql/vsts2.png)

3. Una vez importado el código, conecta Visual Studio al repositorio y clona el código mediante Team Explorer.

4. Después de clonar el repositorio en la máquina del desarrollador, abre el archivo de la solución para la aplicación. La aplicación web y el servicio WCF tienen cada uno proyectos separados dentro del archivo.

    ![Archivo de soluciones](./media/contoso-migration-rearchitect-container-sql/vsts4.png)

## <a name="step-7-convert-the-app-to-a-container"></a>Paso 7: Convertir la aplicación en un contenedor

La aplicación local es una aplicación tradicional de tres niveles:

- Contiene WebForms y un Servicio WCF que conecta a SQL Server.
- Utiliza Entity Framework para integrarse con los datos de la base de datos SQL y los expone a través de un Servicio WCF.
- La aplicación WebForms interactúa con el servicio WCF.

Los administradores de Contoso convertirán la aplicación en un contenedor con Visual Studio y SDK Tools, de la manera siguiente:

1. Con Visual Studio, revisan el archivo de la solución (SmartHotel.Registration.sln) abierto en el directorio **SmartHotel360-interno-reserva-apps\src\Registration** del repositorio local. Se muestran dos aplicaciones. El front-end web SmartHotel.Registration.Web y la aplicación de servicio WCF SmartHotel.Registration.WCF.

    ![Contenedor](./media/contoso-migration-rearchitect-container-sql/container2.png)

2. Hacen clic con el botón derecho en la aplicación web > **Agregar** > **Container Orchestrator Support** (Compatibilidad con el orquestador de contenedores).
3. En **Add Container Orchestra Support** (Agregar compatibilidad con el orquestador de contenedores), seleccionan **Service Fabric**.

    ![Contenedor](./media/contoso-migration-rearchitect-container-sql/container3.png)

4. Repiten el proceso para la aplicación SmartHotel.Registration.WCF.
5. Ahora, comprueban cómo ha cambiado la solución.

    - La nueva aplicación es **SmartHotel.RegistrationApplication/**
    - Contiene dos servicios: **SmartHotel.Registration.WCF** y **SmartHotel.Registration.Web**.

    ![Contenedor](./media/contoso-migration-rearchitect-container-sql/container4.png)

6. Visual Studio creó el archivo de Docker y extrajo localmente las imágenes necesarias en el equipo del desarrollador.

    ![Contenedor](./media/contoso-migration-rearchitect-container-sql/container5.png)

7. Visual Studio crea y abre un archivo de manifiesto (**ServiceManifest.xml**). Este archivo indica a Service Fabric cómo configurar el contenedor cuando se implementa en Azure.

    ![Contenedor](./media/contoso-migration-rearchitect-container-sql/container6.png)

8. Otro archivo de manifiesto (**ApplicationManifest.xml) contiene las aplicaciones de configuración para los contenedores.

    ![Contenedor](./media/contoso-migration-rearchitect-container-sql/container7.png)

9. Abren el archivo **ApplicationParameters/Cloud.xml** y actualizan la cadena de conexión para conectar la aplicación a la base de datos de Azure SQL. La cadena de conexión puede encontrarse en la base de datos en Azure Portal.

    ![Cadena de conexión](./media/contoso-migration-rearchitect-container-sql/container8.png)

10. Confirman el código actualizado y lo insertan en Azure DevOps Services.

    ![Confirmación](./media/contoso-migration-rearchitect-container-sql/container9.png)

## <a name="step-8-build-and-release-pipelines-in-azure-devops-services"></a>Paso 8: Canalizaciones de compilación y versión en Azure DevOps Services

Los administradores de Contoso configuran ahora Azure DevOps Services para realizar el proceso de compilación y versión a fin de poner en marcha las prácticas de DevOps.

1. En Azure DevOps Services, seleccionan **Compilación y versión** > **Nueva canalización**.

    ![Nueva canalización](./media/contoso-migration-rearchitect-container-sql/pipeline1.png)

2. Seleccione **Azure DevOps Services Git** (Git de Azure DevOps Services) y el repositorio correspondiente.

    ![GIT y el repositorio](./media/contoso-migration-rearchitect-container-sql/pipeline2.png)

3. En **Seleccionar una plantilla**, seleccionan Fabric con compatibilidad con Docker.

     ![Fabric y Docker](./media/contoso-migration-rearchitect-container-sql/pipeline3.png)

4. Cambian las imágenes de etiqueta de acción a **Build an image** (Compilar una imagen) y configuran la tarea para usar el ACR aprovisionado.

     ![Registro](./media/contoso-migration-rearchitect-container-sql/pipeline4.png)

5. En la tarea **Insertar imágenes**, configuran la imagen para insertarla en el ACR y seleccionan incluir la etiqueta más reciente.
6. En **Desencadenadores**, habilitan la integración continua y agregan la rama maestra.

    ![Desencadenadores](./media/contoso-migration-rearchitect-container-sql/pipeline5.png)

7. Seleccionan **Guardar y poner en cola** para iniciar una compilación.
8. Después de que la compilación se ha realizado correctamente, siguen con la canalización de versión. En Azure DevOps Services, seleccionan **Versiones** > **Nueva canalización**.

    ![Canalización de versión](./media/contoso-migration-rearchitect-container-sql/pipeline6.png)

9. Seleccionan la plantilla **Implementación de Azure Service Fabric** y asignan nombre (**SmartHotelSF**) a la fase.

    ![Entorno](./media/contoso-migration-rearchitect-container-sql/pipeline7.png)

10. Especifican un nombre de canalización (**ContosoSmartHotel360Rearchitect**). En la fase, seleccionan **1 job, 1 task** (1 trabajo, 1 tarea) para configurar la implementación de Service Fabric.

    ![Fase y tarea](./media/contoso-migration-rearchitect-container-sql/pipeline8.png)

11. Ahora, seleccionan **Nuevo** para agregar una nueva conexión de clúster.

    ![Nueva conexión](./media/contoso-migration-rearchitect-container-sql/pipeline9.png)

12. En **Add Service Fabric service connection** (Agregar conexión del servicio Service Fabric), configuran la conexión y las opciones de autenticación que se usarán en Azure DevOps Services para implementar la aplicación. El punto de conexión del clúster puede encontrarse en Azure Portal. Los administradores agregan **tcp://** como prefijo.

13. La información del certificado que recopilan se introduce en **Huella digital de certificado de servidor** y **Certificado de cliente**.

    ![Certificate](./media/contoso-migration-rearchitect-container-sql/pipeline10.png)

14. Seleccionan la canalización > **Agregar un artefacto**.

     ![Artefacto](./media/contoso-migration-rearchitect-container-sql/pipeline11.png)

15. Seleccionan el proyecto y la canalización de compilación, usando la versión más reciente.

     ![Compilación](./media/contoso-migration-rearchitect-container-sql/pipeline12.png)

16. Observe que se marca el rayo en el artefacto.

     ![Estado del artefacto](./media/contoso-migration-rearchitect-container-sql/pipeline13.png)

17. Además, observe que se habilita el desencadenador de implementación continua.
   ![Implementación continua habilitada](./media/contoso-migration-rearchitect-container-sql/pipeline14.png)

18. Seleccionan **Guardar** > **Crear una versión**.

    ![Release](./media/contoso-migration-rearchitect-container-sql/pipeline15.png)

19. Una vez finalizada la implementación, SmartHotel360 ejecutará Service Fabric.

    ![Publicar](./media/contoso-migration-rearchitect-container-sql/publish4.png)

20. Para conectarse a la aplicación, dirigen el tráfico a la dirección IP pública del equilibrador de carga de Azure delante de los nodos de Service Fabric.

    ![Publicar](./media/contoso-migration-rearchitect-container-sql/publish5.png)

## <a name="step-9-extend-the-app-and-republish"></a>Paso 9: Extender la aplicación y volver a publicar

Después de que la aplicación SmartHotel360 y la base de datos están en ejecución en Azure, Contoso quiere ampliar la aplicación.

- Los desarrolladores de Contoso crean el prototipo de una nueva aplicación de .NET Core que se ejecutará en el clúster de Service Fabric.
- La aplicación se usará para extraer datos de opiniones de CosmosDB.
- Estos datos estarán en formato de tweets que se procesan mediante una instancia de Azure Functions sin servidor y Azure Cognitive Services Text Analysis API.

### <a name="provision-azure-cosmos-db"></a>Aprovisionar Azure Cosmos DB

En primer lugar, los administradores de Contoso aprovisionan una base de datos de Azure Cosmos.

1. Crean un recurso de Azure Cosmos DB en Azure Marketplace.

    ![Extend](./media/contoso-migration-rearchitect-container-sql/extend1.png)

2. Proporcionan un nombre de base de datos (**contososmarthotel**), seleccionan la API de SQL y colocan el recurso en el grupo de recursos de producción, en la región primaria Este de EE.UU. 2.

    ![Extend](./media/contoso-migration-rearchitect-container-sql/extend2.png)

3. En **Introducción**, seleccionan **Explorador de datos** y agregan una nueva colección.
4. En **Agregar colección** proporcionan identificadores y establecen la capacidad de almacenamiento y rendimiento.

    ![Extend](./media/contoso-migration-rearchitect-container-sql/extend3.png)

5. En el portal, abren la nueva base de datos > **Colección** > **Documentos** y seleccionan **Nuevo documento**.
6. Pegan el siguiente código JSON en la ventana de documento. Se trata de datos de ejemplo en forma de un tweet único.

    ```json
    {
            "id": "2ed5e734-8034-bf3a-ac85-705b7713d911",
            "tweetId": 927750234331580911,
            "tweetUrl": "https://twitter.com/status/927750237331580911",
            "userName": "CoreySandersWA",
            "userAlias": "@CoreySandersWA",
            "userPictureUrl": "",
            "text": "This is a tweet about #SmartHotel360",
            "language": "en",
            "sentiment": 0.5,
            "retweet_count": 1,
            "followers": 500,
            "hashtags": [
                ""
            ]
    }
    ```

    ![Extend](./media/contoso-migration-rearchitect-container-sql/extend4.png)

7. Localizan el punto de conexión de Cosmos DB y la clave de autenticación. Se usan en la aplicación para conectarse a la colección. En la base de datos, seleccionan **Claves** y copian el URI y la clave principal en el Bloc de notas.

    ![Extend](./media/contoso-migration-rearchitect-container-sql/extend5.png)

### <a name="update-the-sentiment-app"></a>Actualizar la aplicación de opiniones

Después de aprovisionar Cosmos DB, los administradores de Contoso pueden configurar la aplicación para conectarse a ella.

1. En Visual Studio, abren el archivo ApplicationModern\ApplicationParameters\cloud.xml en el Explorador de soluciones.

    ![Aplicación de opiniones](./media/contoso-migration-rearchitect-container-sql/sentiment1.png)

2. Rellenan los dos parámetros siguientes:

   ```xml
   <Parameter Name="SentimentIntegration.CosmosDBEndpoint" Value="[URI]" />
   ```

   ```xml
   <Parameter Name="SentimentIntegration.CosmosDBAuthKey" Value="[Key]" />
   ```

    ![Aplicación de opiniones](./media/contoso-migration-rearchitect-container-sql/sentiment2.png)

### <a name="republish-the-app"></a>Volver a publicar la aplicación

Después de extender la aplicación, los administradores de Contoso vuelven a publicarla en Azure mediante la canalización.

1. Confirman el código y lo insertan en Azure DevOps Services. Esto inicia las canalizaciones de compilación y versión.

2. Una vez finalizada la implementación y la compilación, SmartHotel360 ejecutará Service Fabric. La consola de administración de Service Fabric muestra ahora tres servicios.

    ![Volver a publicar](./media/contoso-migration-rearchitect-container-sql/republish3.png)

3. Los administradores de Contoso pueden hacer clic para recorrer los servicios y ver que la aplicación SentimentIntegration está en funcionamiento.

    ![Volver a publicar](./media/contoso-migration-rearchitect-container-sql/republish4.png)

## <a name="clean-up-after-migration"></a>Limpiar después de la migración

Después de la migración, Contoso debe completar estos pasos de limpieza:

- Quitar las VM locales del inventario de vCenter.
- Quitar las VM de los trabajos de copia de seguridad locales.
- Actualizar la documentación interna para que muestre las nuevas ubicaciones para la aplicación SmartHotel360. Mostrar la base de datos en ejecución en Azure SQL Database y el front-end en ejecución en Service Fabric.
- Revisar los recursos que interactúan con las VM retiradas y actualizar los valores de configuración pertinentes o la documentación para reflejar la nueva configuración.

## <a name="review-the-deployment"></a>Revisar la implementación

Con los recursos migrados de Azure, Contoso debe proteger la infraestructura nueva y ponerla totalmente en marcha.

### <a name="security"></a>Seguridad

- Los administradores de Contoso deben asegurarse de que su nueva base de datos **SmartHotel-Registration** sea segura. [Más información](/azure/sql-database/sql-database-security-overview).
- En concreto, deben actualizar el contenedor para usar SSL con certificados.
- Debería considerarse el uso de Key Vault para proteger los secretos de las aplicaciones de Service Fabric. [Más información](/azure/service-fabric/service-fabric-application-secret-management).

### <a name="backups"></a>Copias de seguridad

- Contoso necesita revisar los requisitos de copia de seguridad para Azure SQL Database. [Más información](/azure/sql-database/sql-database-automated-backups).
- Los administradores de Contoso deben considerar la implementación de grupos de conmutación por error para proporcionar conmutación por error regional para la base de datos. [Más información](/azure/sql-database/sql-database-geo-replication-overview).
- Pueden aprovechar la replicación geográfica para la SKU premium de ACR. [Más información](/azure/container-registry/container-registry-geo-replication).
- Contoso debe considerar la implementación de la aplicación web en las regiones principales Este de EE. UU. 2 y Centro de EE. UU. cuando Web App for Containers esté disponible. Los administradores de Contoso podrían configurar Traffic Manager para garantizar la conmutación por error en caso de que se produzcan interrupciones regionales.
- Cosmos DB realiza la copia de seguridad automáticamente. Contoso [lea acerca de](/azure/cosmos-db/online-backup-and-restore) este proceso para obtener más información.

### <a name="licensing-and-cost-optimization"></a>Optimización de los costos y licencias

- Una vez implementados todos los recursos, Contoso debe asignar etiquetas de Azure según el [planeamiento de su infraestructura](contoso-migration-infrastructure.md#set-up-tagging).
- Todas las licencias se integran en el costo de los servicios de PaaS que consume Contoso. Esto se deducirá del contrato Enterprise.
- Contoso habilitará Azure Cost Management bajo licencia de Cloudyn, una subsidiaria de Microsoft. Se trata de una solución de administración de costos en varias nubes que le permitirá utilizar y administrar Azure y otros recursos en la nube. [Más información](/azure/cost-management/overview) sobre Azure Cost Management.

## <a name="conclusion"></a>Conclusión

En este artículo, Contoso refactorizó la aplicación SmartHotel360 en Azure mediante la migración de la VM de front-end de la aplicación a Service Fabric. La base de datos de la aplicación se migró a una base de datos de Azure SQL.
