---
title: Refactorización de una aplicación del departamento de servicios de Linux a Azure App Service y Azure Database for MySQL
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información sobre cómo Contoso refactoriza la aplicación Linux local mediante la migración a Azure App Service usando GitHub para el nivel web y Azure SQL Database.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: e504d4032fc019af43ec7cb1e8513504196559a2
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024212"
---
# <a name="refactor-a-linux-app-to-multiple-regions-using-azure-app-service-traffic-manager-and-azure-database-for-mysql"></a>Refactorización de una aplicación de Linux a varias regiones con Azure App Service, Traffic Manager y Azure Database for MySQL

En este artículo se muestra cómo la empresa ficticia Contoso refactoriza una aplicación de Apache MySQL PHP (LAMP) basada en Linux de dos niveles y la migra de una ubicación local a Azure mediante Azure App Service con integración de GitHub y Azure Database for MySQL.

osTicket, la aplicación del departamento de servicios usada en este ejemplo, se proporciona como código abierto. Si quiere utilizarla para sus propias pruebas, puede descargarla desde [GitHub](https://github.com/osTicket/osTicket).

## <a name="business-drivers"></a>Impulsores del negocio

El equipo directivo de TI ha trabajado estrechamente con sus socios comerciales para comprender sus objetivos:

- **Abordar el crecimiento del negocio.** Contoso crece y se mueve a mercados nuevos. Se necesitan más agentes de servicio al cliente.
- **Escala.** se debe compilar la solución para que Contoso pueda agregar más agentes de servicio al cliente al escalar el negocio.
- **Mejora de la resistencia.**  en el pasado, los problemas del sistema afectaban solo a los usuarios internos. Con su nuevo modelo de negocio, se verán afectados los usuarios externos y Contoso necesita que la aplicación esté siempre en funcionamiento.

## <a name="migration-goals"></a>Objetivos de la migración

El equipo de la nube de Contoso ha definido los objetivos de esta migración con el fin de determinar el mejor método para llevarla a cabo:

- La aplicación debe escalar más allá de la capacidad y el rendimiento local actual. Contoso va a mover la aplicación para aprovechar las ventajas del escalado a petición de Azure.
- Contoso quiere mover el código base de la aplicación a una canalización de entrega continua. Cuando los cambios de la aplicación se inserten en GitHub, Contoso quiere implementar dichos cambios sin tareas para el personal de operaciones.
- La aplicación debe ser resistente con capacidades para el crecimiento y la conmutación por error. Contoso quiere implementar la aplicación en dos regiones de Azure diferentes y configurarla para el escalado automático.
- Contoso quiere minimizar las tareas de administración de la base de datos tras mover la aplicación a la nube.

## <a name="solution-design"></a>Diseño de la solución

Después de fijar sus objetivos y requisitos, Contoso diseña y revisa una solución de implementación e identifica el proceso de migración, incluidos los servicios de Azure que usará para la migración.

## <a name="current-architecture"></a>Arquitectura actual

- La aplicación se divide en capas entre dos VM (OSTICKETWEB y OSTICKETMYSQL).
- Las VM están ubicadas en el host de VMware ESXi **contosohost1.contoso.com** (versión 6.5).
- El entorno de VMware lo administra vCenter Server 6.5 (**vcenter.contoso.com**), que se ejecuta en una VM.
- Contoso tiene un centro de datos local (contoso-datacenter), con un controlador de dominio local (**contosodc1**).

![Arquitectura actual](./media/contoso-migration-refactor-linux-app-service-mysql/current-architecture.png)

## <a name="proposed-architecture"></a>Arquitectura propuesta

Esta es la arquitectura propuesta:

- La aplicación de nivel web en OSTICKETWEB se migrará mediante la compilación de una instancia de Azure App Service en dos regiones de Azure. Azure App Service para Linux se implementará mediante el contenedor Docker de PHP 7.0.
- El código de la aplicación se moverá a GitHub y Azure App Service Web App se configurará para la entrega continua con GitHub.
- Las instancias de Azure App Server se implementarán en las regiones primaria (Este de EE. UU. 2) y secundaria (Centro de EE. UU.).
- Traffic Manager se configurará delante de las dos aplicaciones web en ambas regiones.
- Traffic Manager se configurará en modo de prioridad para forzar el tráfico a través de la región Este de EE. UU. 2.
- Si Azure App Server en la región Este de EE. UU. 2 se queda sin conexión, los usuarios pueden obtener acceso a la aplicación de conmutación por error en la región Centro de EE. UU.
- La base de datos de la aplicación se migrará al servicio Azure Database for MySQL mediante herramientas de MySQL Workbench. La copia de seguridad de la base de datos local se realizará localmente y se restaurará de forma directa en Azure Database for MySQL.
- La base de datos residirá en la región primaria Este de EE. UU. 2, en la subred de base de datos (PROD-DB-EUS2) de la red de producción (VNET-PROD-EUS2):
- Dado que se migra una carga de trabajo de producción, los recursos de Azure para la aplicación residirán en el grupo de recursos de producción **ContosoRG**.
- El recurso Traffic Manager se implementará en el grupo de recursos de la infraestructura de Contoso **ContosoInfraRG**.
- Las VM locales del centro de datos de Contoso se retirarán después de realizar la migración.

![Arquitectura del escenario](./media/contoso-migration-refactor-linux-app-service-mysql/proposed-architecture.png)

## <a name="migration-process"></a>Proceso de migración

Contoso completará el proceso de migración como se indica a continuación:

1. Como primer paso, los administradores de Contoso configuran la infraestructura de Azure, incluido el aprovisionamiento de Azure App Service, la configuración de Traffic Manager y el aprovisionamiento de una instancia de Azure Database for MySQL.
2. Después de preparar Azure, se migra la base de datos mediante MySQL Workbench.
3. Cuando la base de datos se ejecuta en Azure, configuran un repositorio privado de GitHub para Azure App Service con entrega continua y lo cargan con la aplicación osTicket.
4. En Azure Portal, se carga la aplicación desde GitHub en el contenedor Docker que ejecuta Azure App Service.
5. Se modifica la configuración de DNS y se configura el escalado automático para la aplicación.

![Proceso de migración](./media/contoso-migration-refactor-linux-app-service-mysql/migration-process.png)

### <a name="azure-services"></a>Servicios de Azure

**Servicio** | **Descripción** | **Costee**
--- | --- | ---
[Azure App Service](https://azure.microsoft.com/services/app-service) | El servicio ejecuta y escala aplicaciones mediante el servicio PaaS de Azure para sitios web. | Los precios se basan en el tamaño de las instancias y las características necesarias. [Más información](https://azure.microsoft.com/pricing/details/app-service/windows).
[Traffic Manager](https://azure.microsoft.com/services/traffic-manager) | Un equilibrador de carga que usa DNS para dirigir los usuarios a Azure o a sitios web y servicios externos. | Los precios se basan en el número de consultas de DNS recibidas y el número de puntos de conexión supervisados. | [Más información](https://azure.microsoft.com/pricing/details/traffic-manager).
[Azure Database for MySQL](https://docs.microsoft.com/azure/mysql) | La base de datos se basa en el motor de MySQL Server de código abierto. Proporciona una base de datos MySQL de comunidad completamente administrada y lista para la empresa como un servicio para el desarrollo e implementación de aplicaciones. | Los precios se basan en los requisitos de proceso, almacenamiento y copia de seguridad. [Más información](https://azure.microsoft.com/pricing/details/mysql).

## <a name="prerequisites"></a>Requisitos previos

Esto es lo que tiene hacer Contoso para ejecutar este escenario.

<!-- markdownlint-disable MD033 -->

**Requisitos** | **Detalles**
--- | ---
**Suscripción de Azure** | Suscripciones creadas por Contoso anteriormente en esta serie de artículos. Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Si crea una cuenta gratuita, será el administrador de su suscripción y podrá realizar todas las acciones.<br/><br/> Si usa una suscripción existente y no es el administrador, tendrá que solicitar al administrador que le asigne permisos de propietario o colaborador.
**Infraestructura de Azure** | Contoso configura la infraestructura de Azure según se describe en [Infraestructura de Azure para la migración](./contoso-migration-infrastructure.md).

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Pasos del escenario

Así es como Azure realizará la migración:

> [!div class="checklist"]
>
> - **Paso 1: Aprovisionamiento de Azure App Service.** Los administradores de Contoso aprovisionarán aplicaciones web en las regiones primarias y secundarias.
> - **Paso 2: Configuración de Traffic Manager.** Configurarán Traffic Manager delante de las aplicaciones web para el enrutamiento y el equilibrio de carga del tráfico.
> - **Paso 3: Aprovisionamiento de MySQL.** En Azure, aprovisionarán una instancia de Azure Database for MySQL.
> - **Paso 4: Migración de la base de datos**. migrarán la base de datos mediante MySQL Workbench.
> - **Paso 5: Configuración de GitHub**. configurarán un repositorio de GitHub local para los sitios web y el código de la aplicación.
> - **Paso 6: Implementación de las aplicaciones web**. implementarán las aplicaciones web desde GitHub.

## <a name="step-1-provision-azure-app-service"></a>Paso 1: Aprovisionamiento de Azure App Service.

Los administradores de Contoso aprovisionan dos aplicaciones web (una en cada región) con Azure App Service.

1. Se crea un recurso de aplicación web en la región primaria Este de EE. UU. 2 (**osticket-eus2**) desde Azure Marketplace.
2. Se coloca el recurso en el grupo de recursos de producción **ContosoRG**.

    ![Azure App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app1.png)

3. Se crea una nuevo plan de App Service en la región primaria (**APP-SVP-EUS2**), con el tamaño estándar.

     ![Azure App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app2.png)

4. Seleccionan un sistema operativo Linux con la pila en tiempo de ejecución PHP 7.0, que es un contenedor de Docker.

    ![Azure App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app3.png)

5. Crean una segunda aplicación web (**osticket-cus**) y el plan de Azure App Service para la región Centro de EE. UU.

    ![Azure App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app4.png)

**¿Necesita más ayuda?**

- Más información sobre [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service/overview).
- Información sobre [Azure App Service en Linux](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).

## <a name="step-2-set-up-traffic-manager"></a>Paso 2: Configuración de Traffic Manager

Los administradores de Contoso configuran Traffic Manager para dirigir las solicitudes web entrantes a las aplicaciones web que se ejecutan en nivel web de osTicket.

1. Crean un recurso de Traffic Manager (**osticket.trafficmanager.net**) desde Azure Marketplace. Se usa el enrutamiento de prioridad para que la región Este de EE. UU. 2 sea el sitio primario. Se coloca el recurso en el grupo de recursos de la infraestructura (**ContosoInfraRG**). Tenga en cuenta que Traffic Manager es global y no está enlazado a una ubicación específica.

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager1.png)

2. Ahora, configuran Traffic Manager con puntos de conexión. Se agrega la aplicación web de la región Este de EE. UU. 2 como sitio principal (**osticket-eus2**) y la aplicación del Centro de EE. UU. como secundario (**osticket-cus**).

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager2.png)

3. Después de agregar los puntos de conexión, se pueden supervisar.

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager3.png)

**¿Necesita más ayuda?**

- Más información sobre [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview).
- Más información sobre el [enrutamiento del tráfico a un punto de conexión prioritario](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-configure-priority-routing-method).

## <a name="step-3-provision-azure-database-for-mysql"></a>Paso 3: Aprovisionamiento de Azure Database for MySQL

Los administradores de Contoso aprovisionan una instancia de base de datos MySQL en la región primaria Este de EE. UU. 2.

1. En Azure Portal, crea un recurso de Azure Database for MySQL.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-1.png)

2. Agrega el nombre **contosoosticket** para la base de datos de Azure. Agrega la base de datos al grupo de recursos de producción **ContosoRG** y especifica las credenciales.
3. La base de datos MySQL local es de la versión 5.7, por lo que selecciona esta versión por cuestiones de compatibilidad. Utiliza los tamaños predeterminados, que coinciden con los requisitos de la base de datos.

     ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-2.png)

4. Para las **opciones de redundancia de copia de seguridad**, seleccionan el uso de **redundancia geográfica**. Esta opción permite restaurar la base de datos en la región secundaria del Centro de EE. UU. si se produce una interrupción. Solo puede configurar esta opción al aprovisionar la base de datos.

    ![Redundancia](./media/contoso-migration-refactor-linux-app-service-mysql/db-redundancy.png)

5. Configuran la seguridad de conexión. En la base de datos > **Seguridad de la conexión**, se configuran las reglas de firewall para permitir que la base de datos tenga acceso a servicios de Azure.

6. Se agrega la dirección IP del cliente de la estación de trabajo local a las direcciones IP inicial y final. Esto permite que las aplicaciones web tengan acceso a la base de datos MySQL, junto con el cliente de base de datos que realiza la migración.

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-3.png)

## <a name="step-4-migrate-the-database"></a>Paso 4: Migración de la base de datos

Los administradores de Contoso migran la base de datos mediante la copia de seguridad y la restauración con herramientas de MySQL. Instala MySQL Workbench, hace una copia de seguridad de la base de datos de OSTICKETMYSQL y, a continuación, la restaura al servidor de Azure Database for MySQL.

### <a name="install-mysql-workbench"></a>Instalación de MySQL Workbench

1. Comprueban los [requisitos previos y las descargas de MySQL Workbench](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).
2. Instala MySQL Workbench para Windows de acuerdo con las [instrucciones de instalación](https://dev.mysql.com/doc/workbench/en/wb-installing.html). El equipo en el que se instala debe ser accesible para la máquina virtual OSTICKETMYSQL y Azure a través de Internet.
3. En MySQL Workbench, crea una conexión de MySQL a OSTICKETMYSQL.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench1.png)

4. Exporta la base de datos como **osticket** a un archivo independiente local.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench2.png)

5. Después de realizar la copia de seguridad de la base de datos localmente, crea una conexión a la instancia de Azure Database for MySQL.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench3.png)

6. Ahora, pueden importar (restaurar) la base de datos en la instancia de Azure Database for MySQL desde el archivo independiente. Se crea un nuevo esquema (osticket) para la instancia.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench4.png)

7. Después de restaurar los datos, se pueden consultar mediante Workbench y aparecen en Azure Portal.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench5.png)

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench6.png)

8. Por último, deben actualizar la información de base de datos en las aplicaciones web. En la instancia de MySQL, se abre **Cadenas de conexión**.

     ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench7.png)

9. En la lista de cadenas, se busca la configuración de la aplicación web y se selecciona para copiarla.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench8.png)

10. Se abre una ventana del Bloc de notas, se pega la cadena en un archivo nuevo y se actualiza para que coincida con la base de datos de osticket, la instancia de MySQL y la configuración de credenciales.

     ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench9.png)

11. Pueden comprobar el nombre del servidor y el inicio de sesión en **Información general** en la instancia de MySQL en Azure Portal.

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench10.png)

## <a name="step-5-set-up-github"></a>Paso 5: Configuración de GitHub

Los administradores de Contoso crean un repositorio de GitHub privado y configuran una conexión a la base de datos osTicket en Azure Database for MySQL. Después, cargan la aplicación web en Azure App Service.

1. Se busca el repositorio GitHub público de software OsTicket y se bifurca a la cuenta de GitHub de Contoso.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github1.png)

2. Después de realizar la bifurcación, vaya a la carpeta **include** y busque el archivo **ost-config.php**.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github2.png)

3. Se abre el archivo en el explorador y se edita.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github3.png)

4. En el editor, actualizan los detalles de la base de datos, específicamente **DBHOST** y **DBUSER**.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github4.png)

5. Se confirman los cambios.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github5.png)

6. Para cada aplicación web (**osticket-eus2** y **osticket-cus**), modifican el valor de **Configuración de la aplicación** en Azure Portal.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github6.png)

7. Se especifica la cadena de conexión con el nombre **osticket** y se copia la cadena desde el Bloc de notas en el **área de valores**. Se selecciona **MySQL** en la lista desplegable junto a la cadena y se guarda la configuración.

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github7.png)

## <a name="step-6-configure-the-web-apps"></a>Paso 6: Configuración de las aplicaciones web

Como último paso del proceso de migración, los administradores de Contoso configuran las aplicaciones web con los sitios web de osTicket.

1. En la aplicación web principal (**osticket-eus2**), abren **Opción de implementación** y establecen el origen en **GitHub**.

    ![Configuración de la aplicación](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app1.png)

2. Se seleccionan las opciones de implementación.

    ![Configuración de la aplicación](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app2.png)

3. Después de establecer las opciones, la configuración aparece como pendiente en Azure Portal.

    ![Configuración de la aplicación](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app3.png)

4. Después de actualizar la configuración y cargar la instancia de Web App osTicket desde GitHub en el contenedor Docker que ejecuta Azure App Service, el sitio se muestra como activo.

    ![Configuración de la aplicación](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app4.png)

5. Repiten los pasos anteriores para la aplicación web secundaria (**osticket-cus**).
6. Tras configurar el sitio, es accesible a través del perfil de Traffic Manager. El nombre DNS es la nueva ubicación de la aplicación osTicket. [Más información](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain#map-a-cname-record).

    ![Configuración de la aplicación](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app5.png)

7. Contoso quiere un nombre DNS que sea fácil de recordar. Se crea un registro de alias (CNAME) **osticket.contoso.com** que apunta al nombre de Traffic Manager, en el DNS de sus controladores de dominio.

    ![Configuración de la aplicación](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app6.png)

8. Se configuran ambas aplicaciones web, **osticket-eus2** y **osticket-cu** para permitir los nombres de host personalizados.

    ![Configuración de la aplicación](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app7.png)

### <a name="set-up-autoscaling"></a>Configurar el escalado automático

Por último, se configura el escalado automático para la aplicación. Esto garantiza que, a medida que los agentes usan la aplicación, las instancias de aplicación aumentan y disminuyen en función de las necesidades empresariales.

1. En App Service **APP-SRV-EUS2**, abren **Unidad de escalado**.
2. Se configura una nueva opción de escalado automático con una única regla que aumenta el recuento de instancias en uno cuando el porcentaje de CPU para la instancia actual es superior al 70 % durante 10 minutos.

    ![Escalado automático](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale1.png)

3. Se configura la misma opción en **APP-SRV-CUS** para asegurarse de que se aplica el mismo comportamiento si la aplicación conmuta por error a la región secundaria. La única diferencia es que se establece la instancia predeterminada en 1, ya que solo es para las conmutaciones por error.

   ![Escalado automático](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale2.png)

## <a name="clean-up-after-migration"></a>Limpiar después de la migración

Al completar la migración, se refactoriza la aplicación osTicket para que se ejecute en una instancia de Azure Web App con entrega continua mediante un repositorio GitHub privado. La aplicación se ejecuta en dos regiones para aumentar la resistencia. La base de datos osTicket se ejecuta en Azure Database for MySQL después de la migración a la plataforma PaaS.

Para realizar la limpieza, Contoso debe hacer lo siguiente:

- Quitar las VM de VMware del inventario de vCenter.
- Quitar las VM locales de los trabajos de copia de seguridad locales.
- Actualizar la documentación interna para que muestre las nuevas ubicaciones y las direcciones IP.
- Revisar los recursos que interactúan con las VM locales y actualizar los valores de configuración pertinentes o la documentación para reflejar la nueva configuración.
- Volver a configurar la supervisión para que apunte a la dirección URL osticket-trafficmanager.net, para realizar un seguimiento de que la aplicación está en funcionamiento.

## <a name="review-the-deployment"></a>Revisión de la implementación

Con la aplicación en ejecución, Contoso debe proteger y poner totalmente operativa la infraestructura nueva.

### <a name="security"></a>Seguridad

El equipo de seguridad de Contoso revisa la aplicación para determinar si existe algún problema de seguridad. Se identifica que la comunicación entre la aplicación osTicket y la instancia de MySQL Database no está configurada para SSL. Deberá realizar esta acción para garantizar que el tráfico de la base de datos no pueda piratearse. [Más información](https://docs.microsoft.com/azure/mysql/howto-configure-ssl).

### <a name="backups"></a>Copias de seguridad

- Las aplicaciones web de osTicket no contienen datos de estado y, por tanto, no es necesario hacer copias de seguridad.
- No deberá configurar la copia de seguridad de la base de datos. Azure Database for MySQL crea automáticamente copias de seguridad del servidor y las almacena. Contoso optó por utilizar la redundancia geográfica para la base de datos para que sea resistente y esté lista para la producción. Las copias de seguridad pueden utilizarse para restaurar el servidor a un momento dado. [Más información](https://docs.microsoft.com/azure/mysql/concepts-backup).

### <a name="licensing-and-cost-optimization"></a>Optimización de los costos y licencias

- No hay ningún problema relacionado con las licencias para la implementación de PaaS.
- Contoso habilitará Azure Cost Management bajo licencia de Cloudyn, una subsidiaria de Microsoft. Se trata de una solución de administración de costos en varias nubes que le permitirá utilizar y administrar Azure y otros recursos en la nube. [Más información](https://docs.microsoft.com/azure/cost-management/overview) sobre Azure Cost Management.
