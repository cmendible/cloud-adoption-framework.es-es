---
title: Rehospedaje de una aplicación local mediante la migración a máquinas virtuales de Azure e Instancia administrada de Azure SQL Database
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Aprenda cómo Contoso vuelve a hospedar una aplicación local en máquinas virtuales de Azure y mediante Instancia administrada de Azure SQL Database.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 4b9f6bcb8ce2732cda094e83b832c0e4c920c665
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024170"
---
# <a name="rehost-an-on-premises-app-on-an-azure-vm-and-sql-database-managed-instance"></a>rehospedar una aplicación local en una máquina virtual de Azure e Instancia administrada de Azure SQL Database

En este artículo se muestra cómo la empresa ficticia Contoso migra una aplicación front-end de Windows .NET de dos niveles que se ejecuta en máquinas virtuales de VMware a una máquina virtual de Azure mediante el servicio Azure Site Recovery. También se muestra cómo Contoso migra la base de datos de la aplicación a Instancia administrada de Azure SQL Database.

> [!NOTE]
> Instancia administrada de Azure SQL Database está actualmente en versión preliminar.

SmartHotel360, la aplicación usada en este ejemplo, se proporciona como código abierto. Si quiere utilizarla para sus propias pruebas, puede descargarla desde [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Impulsores del negocio

El equipo directivo de TI de Contoso ha trabajado estrechamente con sus asociados comerciales para comprender lo que quiere lograr la empresa con esta migración:

- **Abordar el crecimiento del negocio.** Contoso está creciendo. Como resultado, ha aumentado la presión sobre los sistemas locales y la infraestructura de la empresa.
- **Aumentar la eficacia.** Contoso debe quitar procedimientos innecesarios y optimizar los procesos para sus desarrolladores y usuarios. La empresa necesita que el departamento de TI sea rápido y no malgaste tiempo ni dinero a fin de satisfacer más rápidamente los requisitos del cliente.
- **Aumentar la agilidad.** el equipo de TI de Contoso necesita más capacidad de respuesta a las necesidades de la empresa. Debe ser capaz de anticiparse a los cambios que se producen en el mercado para que la empresa tenga éxito en una economía global. No debe ser un obstáculo ni convertirse en un inhibidor del negocio.
- **Escala.** a medida que el negocio crece satisfactoriamente, el equipo de TI de Contoso debe proporcionar sistemas que puedan crecer al mismo ritmo.

## <a name="migration-goals"></a>Objetivos de la migración

El equipo de la nube de Contoso ha establecido los objetivos de esta migración. La empresa usa los objetivos de migración para determinar el mejor método de migración.

- Tras la migración, la aplicación de Azure debe tener las mismas funcionalidades de rendimiento que las que tiene actualmente en su entorno de VMware local. Pasar a la nube no significa que el rendimiento de la aplicación sea menos crítico.
- Contoso no quiere invertir en la aplicación. La aplicación es crítica e importante para la empresa, pero Contoso solo quiere mover la aplicación en su formato actual a la nube.
- Después de migrar la aplicación, las tareas administrativas de la base de datos deberían ser menores.
- Contoso no quiere usar una base de datos de Azure SQL para esta aplicación. Busca alternativas.

## <a name="solution-design"></a>Diseño de la solución

Después de fijar sus objetivos y requisitos, Contoso diseña y revisa una solución de implementación e identifica el proceso de migración, incluidos los servicios de Azure que usará para la migración.

### <a name="current-architecture"></a>Arquitectura actual

- Contoso tiene un centro de datos principal (**contoso-datacenter**). El centro de datos está situado en la ciudad de Nueva York, al este de los Estados Unidos.
- Contoso tiene tres sucursales locales más en los Estados Unidos.
- El centro de datos principal está conectado a Internet con una conexión Metro Ethernet de fibra (500 Mbps).
- Cada una de las sucursales está conectada localmente a Internet mediante conexiones de categoría empresarial, y con túneles VPN con IPSec hacia el centro de datos principal. Esta configuración permite que la red entera de Contoso esté conectada de forma permanente, y además optimiza la conectividad a Internet.
- El centro de datos principal está completamente virtualizado con VMware. Contoso tiene dos hosts de virtualización ESXi 6.5 que están administrados por vCenter Server 6.5.
- Contoso usa Active Directory para la administración de identidades. Contoso usa servidores DNS en la red interna.
- Contoso tiene un controlador de dominio local (**contosodc1**).
- Los controladores de dominio se ejecutan en las máquinas virtuales de VMware. Los controladores de dominio de las sucursales locales se ejecutan en servidores físicos.
- La aplicación SmartHotel360 se divide en capas en dos VM (**WEBVM** y **SQLVM**) que se encuentran en un host de VMware ESXi versión 6.5 (**contosohost1.contoso.com**).
- El entorno de VMware lo administra vCenter Server 6.5 (**vcenter.contoso.com**), que se ejecuta en una máquina virtual.

![Arquitectura actual de Contoso](./media/contoso-migration-rehost-vm-sql-managed-instance/contoso-architecture.png)

### <a name="proposed-architecture"></a>Arquitectura propuesta

En este escenario, Contoso quiere migrar su aplicación de viajes local de dos capas como se indica a continuación:

- Migrar la base de datos de la aplicación (**SmartHotelDB**) a una instancia administrada de Azure SQL Database.
- Migrar la **WebVM** de front-end a una máquina virtual de Azure.
- Las máquinas virtuales locales del centro de datos de Contoso se retirarán cuando finalice la migración.

![Arquitectura del escenario](media/contoso-migration-rehost-vm-sql-managed-instance/architecture.png)

### <a name="database-considerations"></a>Consideraciones sobre la base de datos

Como parte del proceso de diseño de la solución, Contoso hizo una comparación de características entre Instancia administrada de Azure SQL Database y de SQL Server. Las siguientes consideraciones les ayudaron a decidirse por Instancia administrada.

- El objetivo de Instancia administrada es proporcionar casi un 100 % de compatibilidad con la versión de SQL Server local más reciente. Microsoft recomienda Instancia administrada para los clientes que ejecutan SQL Server de forma local o en una máquina virtual de IaaS que desean migrar sus aplicaciones a un servicio totalmente administrado con cambios mínimos en el diseño.
- Contoso planea migrar un gran número de aplicaciones locales a IaaS. Muchas de ellas las proporciona el fabricante de software independiente. Contoso se da cuenta de que el uso de Instancia administrada le ayudará a garantizar la compatibilidad de la base de datos con estas aplicaciones, en lugar de utilizar SQL Database, que podría no ser compatible.
- Contoso simplemente puede realizar una migración mediante lift-and-shift a Instancia administrada con Azure Database Migration Service totalmente automatizado. Con este servicio, Contoso puede reutilizarla para las migraciones futuras de la base de datos.
- Instancia administrada de SQL es compatible con el Agente SQL Server, lo que es un problema importante para la aplicación SmartHotel360. Contoso necesita esta compatibilidad, ya que si carece de ella tendrá que volver a diseñar los planes de mantenimiento que requiere la aplicación.
- Con Software Assurance, Contoso puede intercambiar sus licencias existentes para obtener descuentos en una instancia administrada de SQL Database mediante Ventaja híbrida de Azure para SQL Server. Esto puede permitir a Contoso ahorrar hasta un 30 % en Instancia administrada.
- Instancia administrada de SQL se incluye totalmente en la red virtual, por lo que ofrece un mayor nivel de aislamiento y seguridad para los datos de Contoso. Contoso puede obtener las ventajas de la nube pública y, al mismo tiempo, mantener el entorno aislado de la red Internet pública.
- Instancia administrada admite muchas características de seguridad, incluidos el enmascaramiento dinámico de datos siempre cifrados, la seguridad a nivel de fila y la detección de amenazas.

### <a name="solution-review"></a>Revisión de la solución

Contoso evalúa el diseño propuesto y crea una lista de ventajas y desventajas.

<!-- markdownlint-disable MD033 -->

**Consideración** | **Detalles**
--- | ---
**Ventajas** | WEBVM se moverá a Azure sin cambios, por lo que la migración será sencilla.<br/><br/> Instancia administrada de SQL admite los requisitos técnicos y los objetivos de Contoso.<br/><br/> Instancia administrada proporcionará compatibilidad total con su implementación actual, mientras Contoso deja de usar SQL Server 2008 R2.<br/><br/> Puede aprovechar su inversión en Software Assurance y usar la Ventaja híbrida de Azure para SQL Server y Windows Server.<br/><br/> Puede volver a usar Azure Database Migration Service para futuras migraciones adicionales.<br/><br/> Instancia administrada de SQL tiene la tolerancia a errores integrada que Contoso no necesita configurar. Esto garantiza que la capa de datos ya no sea un único punto de conmutación por error.
**Desventajas** | WEBVM ejecuta Windows Server 2008 R2. Aunque este sistema operativo es compatible con Azure, ha dejado de ser una plataforma compatible. [Más información](https://support.microsoft.com/help/956893).<br/><br/> El nivel web sigue siendo un único punto de conmutación por error en el que WEBVM es el único que proporciona servicios.<br/><br/> Contoso tendrá que seguir dando soporte al nivel web de la aplicación como una máquina virtual, en lugar de pasarse a un servicio administrado, como Azure App Service.<br/><br/> Para la capa de datos, es posible que Instancia administrada no sea la mejor solución si Contoso desea personalizar el sistema operativo o el servidor de base de datos, o si desea ejecutar aplicaciones de terceros junto con SQL Server. La ejecución de SQL Server en una máquina virtual IaaS puede proporcionar esta flexibilidad.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Proceso de migración

Contoso migrará la capas web y de datos de su aplicación SmartHotel360 a Azure mediante estos pasos:

1. Contoso ya tiene su infraestructura de Azure, por lo que solo necesita agregar un par de componentes de Azure específicos a este escenario.
2. La capa de datos se migrará con Azure Database Migration Service. Este servicio se conecta a la VM con SQL Server local mediante una conexión VPN de sitio a sitio entre el centro de datos de Contoso y Azure. Después, el servicio migra la base de datos.
3. La capa web se migrará con una migración mediante lift-and-shift por medio de Site Recovery. Este proceso supone la preparación del entorno local de VMware, la configuración y habilitación de la replicación y la migración de las máquinas virtuales mediante su conmutación por error a Azure.

     ![Arquitectura de migración](media/contoso-migration-rehost-vm-sql-managed-instance/migration-architecture.png)

### <a name="azure-services"></a>Servicios de Azure

Servicio | DESCRIPCIÓN | Coste
--- | --- | ---
[Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) | Azure Database Migration Service permite migraciones completas de varios orígenes de base de datos a plataformas de datos de Azure, con un tiempo de inactividad mínimo. | Información acerca de las [regiones admitidas](https://docs.microsoft.com/azure/dms/dms-overview#regional-availability) y los [precios de Database Migration Service](https://azure.microsoft.com/pricing/details/database-migration).
[Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) | Instancia administrada es un servicio de base de datos administrada que representa una instancia de SQL Server completamente administrada en la nube de Azure. Usa el mismo código que la versión más reciente del motor de base de datos de SQL Server y tiene las características, mejoras de rendimiento y revisiones de seguridad más recientes. | El uso de una instancia administrada de Azure SQL Database en Azure conlleva unos gastos basados en la capacidad. Más información sobre los [precios de Instancia administrada](https://azure.microsoft.com/pricing/details/sql-database/managed).
[Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery) | El servicio Site Recovery orquesta y administra la migración y la recuperación ante desastres de las máquinas virtuales de Azure y de las máquinas virtuales locales y los servidores físicos. | Durante la replicación en Azure, se incurre en gastos de Azure Storage. Las máquinas virtuales de Azure se crean, y generan gastos, cuando se produce una conmutación por error. Más información sobre las [tarifas y precios de Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery).

## <a name="prerequisites"></a>Requisitos previos

Contoso y otros usuarios deben cumplir los siguientes requisitos previos en este escenario:

<!-- markdownlint-disable MD033 -->

Requisitos | Detalles
--- | ---
**Inscribirse en la versión preliminar de Instancia administrada** | Es necesario estar inscrito en la versión preliminar pública limitada de Instancia administrada de SQL Database. También necesita una suscripción a Azure para [registrarse](https://portal.azure.com#create/Microsoft.SQLManagedInstance). El registro puede tardar unos días en completarse, así que asegúrese de hacerlo antes de empezar a implementar este escenario.
**Suscripción de Azure** | Ya debería haber creado una suscripción cuando realizó la valoración en el primer artículo de esta serie. Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Si crea una cuenta gratuita, será el administrador de su suscripción y podrá realizar todas las acciones.<br/><br/> Si usa una suscripción existente y no es el administrador de ella, tendrá que solicitar al administrador que le asigne permisos de propietario o colaborador.<br/><br/> Si necesita permisos más específicos, consulte [Uso del control de acceso basado en roles para administrar el acceso a Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Infraestructura de Azure** | Contoso configura la infraestructura de Azure según se describe en [Infraestructura de Azure para la migración](./contoso-migration-infrastructure.md).
**Site Recovery (local)** | Su instancia local de vCenter Server debe ejecutarse en las versiones 5.5, 6.0 o 6.5.<br/><br/> Un host ESXi que ejecute la versión 5.5, 6.0 o 6.5<br/><br/> Una o más máquinas virtuales VMware que se ejecuten en el host ESXi.<br/><br/> Las máquinas virtuales tienen que cumplir los [requisitos de Azure](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#azure-vm-requirements).<br/><br/> Configuración de [red](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#network) y [almacenamiento](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix#storage) compatible.
**Database Migration Service** | Para Azure Database Migration Service, necesita un [dispositivo VPN local compatible](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices).<br/><br/> Tiene que poder configurar el dispositivo VPN local. Debe tener una dirección IPv4 pública de uso externo. Esta dirección no puede estar situada detrás de un dispositivo NAT.<br/><br/> Asegúrese de que tiene acceso a la base de datos local de SQL Server.<br/><br/> Firewall de Windows debe poder acceder al motor de base de datos de origen. Aprenda a [configurar Firewall de Windows para el acceso al motor de base de datos](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access).<br/><br/> Si hay un firewall delante de la máquina de base de datos, agregue reglas para permitir el acceso a la base de datos y a los archivos a través del puerto 445 de SMB.<br/><br/> Las credenciales usadas para conectar con la instancia de SQL Server de origen y la instancia administrada de destino deben ser miembros del rol de servidor sysadmin.<br/><br/> Es necesario tener un recurso compartido de red en la base de datos local que Azure Database Migration Service pueda usar para realizar una copia de seguridad de la base de datos de origen.<br/><br/> Asegúrese de que la cuenta de servicio que ejecuta la instancia de SQL Server de origen tenga permisos de escritura sobre el recurso compartido de red.<br/><br/> Anote un nombre de usuario y una contraseña de Windows que tengan permisos de control completos sobre el recurso compartido de red. Azure Database Migration Service suplanta estas credenciales de usuario para cargar los archivos de copia de seguridad en el contenedor de Azure Storage.<br/><br/> El proceso de instalación de SQL Server Express establece el protocolo TCP/IP en **deshabilitado** de forma predeterminada. Asegúrese de que esté habilitado.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Pasos del escenario

A continuación se indica cómo Contoso configura la implementación:

> [!div class="checklist"]
>
> - **Paso 1: Configuración de una Instancia administrada de SQL Database.** Contoso necesita una instancia administrada existente a la que se migrará la base de datos de SQL Server local.
> - **Paso 2: Preparación de Azure Database Migration Service.** Contoso tiene que registrar al proveedor de migración de base de datos, crear una instancia y, luego, crear un proyecto de Azure Database Migration Service. Contoso también tiene que configurar un identificador de recursos uniforme (URI) de una firma de acceso compartido (SAS) para Azure Database Migration Service. Un URI de SAS proporciona acceso delegado a recursos de la cuenta de almacenamiento de Contoso, así Contoso puede conceder permisos limitados a los objetos de almacenamiento. Contoso configura un URI de SAS, así Azure Database Migration Service puede acceder al contenedor de cuenta de almacenamiento en el que el servicio carga los archivos de copia de seguridad de SQL Server.
> - **Paso 3: Preparación de Azure para Site Recovery.** Contoso debe crear una cuenta de almacenamiento para almacenar los datos replicados de Site Recovery. También debe crear un almacén de Azure Recovery Services.
> - **Paso 4: Preparación de VMware local para Site Recovery.** Contoso preparará las cuentas para la detección de máquinas virtuales y la instalación del agente para conectarse a las máquinas virtuales de Azure tras la conmutación por error.
> - **Paso 5: Replicación de máquinas virtuales.** para configurar la replicación, Contoso configura los entornos de origen y destino de Site Recovery, configura una directiva de replicación y empieza a replicar las máquinas virtuales en Azure Storage.
> - **Paso 6: Migración de la base de datos mediante Azure Database Migration Service.** Contoso migra la base de datos.
> - **Paso 7: Migración de la máquina virtual mediante Site Recovery.** Contoso ejecuta una conmutación por error de prueba para asegurarse de que todo funciona. A continuación, Contoso ejecuta una conmutación por error completa para migrar las máquinas virtuales a Azure.

## <a name="step-1-prepare-a-sql-database-managed-instance"></a>Paso 1: Preparación de una instancia administrada de Azure SQL Database

Para configurar una instancia administrada de Azure SQL Database, Contoso necesita una subred que cumpla los requisitos siguientes:

- La subred debe estar dedicada. Debe estar vacía y no puede contener ningún otro servicio en la nube. La subred no puede ser una subred de puerta de enlace.
- Una vez creada la instancia administrada, Contoso no puede agregar recursos a la subred.
- La subred no puede tener asociado un grupo de seguridad de red.
- La subred debe tener una tabla de rutas definida por el usuario. La única ruta asignada debe ser 0.0.0.0/0, con Internet como próximo salto.
- DNS personalizado opcional: si se especifica un DNS personalizado en la red virtual de Azure, es necesario agregar a la lista la dirección IP de las resoluciones recursivas de Azure (por ejemplo, 168.63.129.16). Más información sobre cómo [configurar DNS personalizado para una instancia administrada](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-custom-dns).
- La subred no puede tener un punto de conexión de servicio (de almacenamiento o SQL) asociado a ella. Los puntos de conexión de servicio se deben deshabilitar en la red virtual.
- La subred tiene que tener como mínimo 16 direcciones IP. Más información sobre cómo [cambiar el tamaño de la subred de Instancia administrada](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-vnet-configuration).
- En el entorno híbrido de Contoso, se requiere la configuración de DNS personalizada. Contoso configura los valores de DNS para usar uno o varios de los servidores de Azure DNS de la empresa. Más información sobre la [personalización de DNS](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-custom-dns).

### <a name="set-up-a-virtual-network-for-the-managed-instance"></a>Configuración de una red virtual para una instancia administrada

Los administradores de Contoso configuran la red virtual de la forma siguiente:

1. Crean una red virtual (**SQLMI-VNET-EU2**) en la región primaria Este de EE. UU. 2. Agrega a la red virtual al grupo de recursos **ContosoNetworkingRG**.
2. Asignan el espacio de direcciones 10.235.0.0/24. Garantizan que el intervalo no se solapa con otras redes de su empresa.
3. Se agregan dos subredes a la red:
    - **SQLMI-DS-EUS2** (10.235.0.0.25)
    - **SQLMI-SAW-EUS2** (10.235.0.128/29). Esta subred se usa para asociar un directorio a la instancia administrada.

      ![Instancia administrada: creación de una red virtual](media/contoso-migration-rehost-vm-sql-managed-instance/mi-vnet.png)

4. Después de implementar la red virtual y las subredes, emparejan las redes como se indica a continuación:

    - Empareja **VNET-SQLMI-EUS2** con **VNET-HUB-EUS2** (la red virtual central de Este de EE. UU. 2).
    - Empareja **VNET-SQLMI-EUS2** con **VNET-PROD-EUS2** (la red de producción).

      ![Emparejamiento de redes](media/contoso-migration-rehost-vm-sql-managed-instance/mi-peering.png)

5. Establecen una configuración de DNS personalizada. DNS primero apunta a los controladores de dominio de Azure de Contoso. Azure DNS es secundario. Los controladores de dominio de Azure de Contoso están ubicados de la manera siguiente:

    - Ubicado en la subred **PROD-DC-EUS2**, en la red de producción de Este de EE. UU. 2 (**VNET-PROD-EUS2**).
    - Dirección de **CONTOSODC3**: 10.245.42.4
    - Dirección de **CONTOSODC4**: 10.245.42.5
    - Resolución de Azure DNS: 168.63.129.16

      ![Servidores DNS de red](media/contoso-migration-rehost-vm-sql-managed-instance/mi-dns.png)

**¿Necesita más ayuda?**

- Más información general sobre [Instancia administrada de SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).
- Más información sobre cómo [crear una red virtual para una instancia administrada de SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-vnet-configuration).
- Más información sobre cómo [configurar el emparejamiento](https://docs.microsoft.com/azure/virtual-network/virtual-network-manage-peering).
- Más información sobre cómo [actualizar la configuración de DNS de Azure Active Directory](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-getting-started-dns).

### <a name="set-up-routing"></a>Configuración del enrutamiento

La instancia administrada se coloca en una red privada virtual. Contoso necesita una tabla de rutas para que la red virtual se comunique con Azure Management Service. Si la red virtual no puede comunicarse con el servicio que la administra, se vuelve inaccesible.

Contoso tiene en cuenta estos factores:

- La tabla de rutas contiene un conjunto de reglas (rutas) que especifican cómo se deben enrutar los paquetes enviados en la red virtual.
- La tabla de redirección se asocia con subredes en las que se implementan Instancias administradas. Cada paquete que sale de una subred se controla en función de la tabla de rutas asociada.
- Una subred puede asociarse con una sola tabla de rutas.
- No hay ningún cargo adicional por la creación de tablas de redirección en Microsoft Azure.

 Para configurar el enrutamiento de Contoso, los administradores siguen estos pasos:

1. Se crea una tabla de ruta definida por el usuario en el grupo de recursos **ContosoNetworkingRG**.

    ![Tabla de rutas](media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table.png)

2. Para cumplir los requisitos de Instancia administrada, tras implementar la tabla de rutas (**MIRouteTable**) agregan una ruta que tiene el prefijo de dirección 0.0.0.0/0. La opción **Tipo de próximo salto** está establecida en **Internet**.

    ![Prefijo de tabla de enrutamiento](media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-prefix.png)

3. Se asocia la tabla de rutas a la subred **SQLMI-DB-EUS2** (en la red **VNET-SQLMI-EUS2**).

    ![Subred de tabla de enrutamiento](media/contoso-migration-rehost-vm-sql-managed-instance/mi-route-table-subnet.png)

**¿Necesita más ayuda?**

Más información sobre cómo [configurar rutas para una instancia administrada](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-create-tutorial-portal).

### <a name="create-a-managed-instance"></a>Creación de una instancia administrada

Ahora, los administradores de Contoso pueden aprovisionar una instancia administrada de SQL Database:

1. Como la instancia administrada atiende una aplicación empresarial, implementan la instancia administrada en la región primaria Este de EE. UU. 2 de la empresa. Agregan la instancia administrada al grupo de recursos **ContosoRG**.
2. Seleccionan un plan de tarifa y el tamaño de los recursos de tamaño y almacenamiento de la instancia. Más información sobre los [precios de Instancia administrada](https://azure.microsoft.com/pricing/details/sql-database/managed).

    ![Instancia administrada](media/contoso-migration-rehost-vm-sql-managed-instance/mi-create.png)

3. Una vez implementada la instancia administrada, dos nuevos recursos aparecen en el grupo de recursos **ContosoRG**:

    - Un clúster virtual en caso de que Contoso tenga varias instancias administradas.
    - La instancia administrada de SQL Server Database.

      ![Instancia administrada](media/contoso-migration-rehost-vm-sql-managed-instance/mi-resources.png)

**¿Necesita más ayuda?**

Más información sobre cómo [aprovisionar una instancia administrada](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-create-tutorial-portal).

## <a name="step-2-prepare-the-azure-database-migration-service"></a>Paso 2: Preparación de Azure Database Migration Service

Para preparar Azure Database Migration Service, los administradores de Contoso tienen que hacer varias operaciones:

- Registrar al proveedor de Azure Database Migration Service en Azure.
- Proporcionar a Azure Database Migration Service acceso a Azure Storage para cargar los archivos de copia de seguridad que se usan para migrar una base de datos. Para proporcionar acceso a Azure Storage, crean un contenedor de Azure Blob Storage. Generan un identificador URI de SAS para el contenedor de Blob Storage.
- Crear un proyecto de Azure Database Migration Service.

Después, realizan los siguientes pasos:

1. Registran el proveedor de migración de base de datos en su suscripción.
    ![Database Migration Service: registro](media/contoso-migration-rehost-vm-sql-managed-instance/dms-subscription.png)

2. Crean un contenedor de Blob Storage. Contoso genera un URI de SAS para que Azure Database Migration Service pueda acceder a él.

    ![Database Migration Service: generación de un URI de SAS](media/contoso-migration-rehost-vm-sql-managed-instance/dms-sas.png)

3. Se crea una instancia de Azure Database Migration Service.

    ![Database Migration Service: creación de una instancia](media/contoso-migration-rehost-vm-sql-managed-instance/dms-instance.png)

4. Se coloca la instancia de Azure Database Migration Service en la subred **PROD-DC-EUS2** de la red virtual **VNET-PROD-DC-EUS2**.
    - Azure Database Migration Service se coloca ahí porque el servicio tiene que estar en una red virtual que pueda acceder a la máquina virtual de SQL Server local mediante una puerta de enlace VPN.
    - **VNET-PROD-EUS2** está emparejada con **VNET-HUB-EUS2** y puede usar puertas de enlace remotas. La opción **Usar puertas de enlace remotas** garantiza que Azure Database Migration Service pueda comunicarse cuando sea necesario.

        ![Database Migration Service: configuración de la red](media/contoso-migration-rehost-vm-sql-managed-instance/dms-network.png)

**¿Necesita más ayuda?**

- Aprenda a [configurar Azure Database Migration Service](https://docs.microsoft.com/azure/dms/quickstart-create-data-migration-service-portal).
- Más información sobre cómo [crear y usar SAS](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-shared-access-signature-part-2).

## <a name="step-3-prepare-azure-for-the-site-recovery-service"></a>Paso 3: Preparación de Azure para el servicio Site Recovery

Contoso necesita varios elementos de Azure para configurar Site Recovery para la migración de su máquina virtual de capa web (**WEBMV**):

- Una red virtual en la que ubicar los recursos de conmutación por error.
- Una cuenta de almacenamiento para almacenar los datos replicados.
- Un almacén de Recovery Services en Azure.

Los administradores de Contoso configuran como se indica a continuación:

1. Como la VM es un front-end web de la aplicación SmartHotel360, Contoso conmuta por error la VM a su red de producción existente (**VNET-PROD-EUS2**) y a la subred (**PROD-FE-EUS2**). La red y la subred se encuentran en la región primaria Este de EE. UU. 2. Contoso configura la red cuando [implementa la infraestructura de Azure](./contoso-migration-infrastructure.md).
2. Crean una cuenta de almacenamiento (**contosovmsacc20180528**). Contoso usa una cuenta de fin general. Contoso selecciona almacenamiento estándar y replicación de almacenamiento con redundancia local.

    ![Site Recovery: creación de la cuenta de almacenamiento](media/contoso-migration-rehost-vm-sql-managed-instance/asr-storage.png)

3. Con la red y la cuenta de almacenamiento, crean un almacén (**ContosoMigrationVault**). Contoso coloca el almacén en el grupo de recursos **ContosoFailoverRG**, en la región primaria Este de EE. UU. 2.

    ![Recovery Services: creación del almacén](media/contoso-migration-rehost-vm-sql-managed-instance/asr-vault.png)

**¿Necesita más ayuda?**

Más información sobre cómo [configurar Azure para Site Recovery](https://docs.microsoft.com/azure/site-recovery/tutorial-prepare-azure).

## <a name="step-4-prepare-on-premises-vmware-for-site-recovery"></a>Paso 4: Preparación de VMware local para Site Recovery

Para preparar VMware para Site Recovery, los administradores de Contoso deben realizar estas tareas:

- Preparar una cuenta en la instancia de vCenter Server o en el host de vSphere ESXi. La cuenta automatiza la detección de máquinas virtuales.
- Preparar una cuenta que permita la instalación automática de Mobility Service en máquinas virtuales de VMware que Contoso quiera replicar.
- Preparar las máquinas virtuales locales para conectarse a las máquinas virtuales de Azure cuando se creen tras la conmutación por error.

### <a name="prepare-an-account-for-automatic-discovery"></a>Preparación de una cuenta de detección automática

Site Recovery necesita acceso a los servidores de VMware para:

- Detectar automáticamente las máquinas virtuales. Se requiere al menos una cuenta de solo lectura.
- Coordinar la replicación, la conmutación por error y la conmutación por recuperación. Contoso necesita una cuenta que pueda ejecutar operaciones como la creación y eliminación de discos, así como la activación de máquinas virtuales.

Los administradores de Contoso configuran la cuenta mediante estas tareas:

1. Crea un rol en el nivel de vCenter.
2. Se asignan a ese rol los permisos necesarios.

**¿Necesita más ayuda?**

Más información sobre cómo [crear y asignar un rol para la detección automática](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-automatic-discovery).

### <a name="prepare-an-account-for-mobility-service-installation"></a>Preparación de una cuenta para la instalación de Mobility Service

Mobility Service debe instalarse en la máquina virtual que Contoso quiera replicar. Contoso tiene en cuenta estos factores sobre Mobility Service:

- Site Recovery puede realizar una instalación de inserción automática de este componente cuando Contoso permite la replicación de la máquina virtual.
- Para la instalación de inserción automática, Contoso debe preparar una cuenta que Site Recovery use para acceder a la máquina virtual.
- Esta cuenta se especifica cuando se configura la replicación en la consola de Azure.
- Contoso debe tener un dominio o una cuenta local con permisos para instalar en la máquina virtual.

**¿Necesita más ayuda?**

Más información sobre cómo [crear una cuenta para la instalación de inserción de Mobility Service](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-mobility-service-installation).

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Preparación para la conexión a las máquinas virtuales de Azure después de la conmutación por error

Después de la conmutación por error en Azure, Contoso quiere poder conectarse a las VM replicadas de Azure. Para conectarse a las máquinas virtuales replicadas en Azure, los administradores de Contoso debe realizar algunas tareas en la máquina virtual local antes de la migración:

1. Para acceder a través de Internet, habilitan RDP en la máquina virtual local antes de la conmutación por error. Se aseguran de que se han agregado las reglas de TCP y UDP para el perfil **Público** y que RDP se permite en **Firewall de Windows** > **Aplicaciones permitidas** para todos los perfiles.
2. Para acceder a través de la VPN de sitio a sitio de Contoso, habilitan RDP en el equipo local. Permiten RDP en **Firewall de Windows** > **Aplicaciones y características permitidas** para las redes de **dominio y privadas**.
3. Se establece la directiva de SAN del sistema operativo en la VM local en **OnlineAll**.

Los administradores de Contoso también deben comprobar estos elementos cuando ejecutan una conmutación por error:

- No debe haber actualizaciones de Windows pendientes en la máquina virtual cuando se desencadene una conmutación por error. Si hay actualizaciones de Windows pendientes, los usuarios de Contoso no puede iniciar sesión en la máquina virtual hasta que la actualización finalice.
- Después de la conmutación por error, los administradores deben comprobar los **diagnósticos de arranque** para ver una captura de pantalla de la máquina virtual. Si no pueden ver los diagnósticos de arranque, deben comprobar que la máquina virtual se está ejecutando y, después, revisar las [sugerencias para la solución de problemas](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

## <a name="step-5-replicate-the-on-premises-vms-to-azure"></a>Paso 5: Replicar VM locales en Azure

Antes de ejecutar una migración a Azure, los administradores de Contoso deben configurar la replicación y habilitarla en la máquina virtual local.

### <a name="set-a-replication-goal"></a>Establecer un objetivo de replicación

1. En el almacén, en el nombre de este (**ContosoVMVault**), establecen un objetivo de replicación (**Introducción** > **Site Recovery** > **Preparar infraestructura**).
2. Especifican que los equipos se encuentran en las instalaciones locales, que son máquinas virtuales de VMware, y se replican en Azure.

    ![Preparación de la infraestructura: objetivo de protección](./media/contoso-migration-rehost-vm-sql-managed-instance/replication-goal.png)

### <a name="confirm-deployment-planning"></a>Confirmación del planeamiento de la implementación

Para continuar, los administradores de Contoso confirman que han completado la planeación de la implementación. Seleccionan **Sí, ya lo hice**. En esta implementación, Contoso migra solo una máquina virtual, por lo que no es necesario planear la implementación.

### <a name="set-up-the-source-environment"></a>Configuración del entorno de origen

Ahora, los administradores de Contoso configuran el entorno de origen. Para configurar su entorno de origen, descargan una plantilla OVF y la usan para implementar el servidor de configuración y sus componentes asociados, como una máquina virtual local de VMware altamente disponible. Entre los componentes del servidor se encuentran los siguientes:

- El servidor de configuración que coordina las comunicaciones entre la infraestructura local y Azure. El servidor de configuración administra la replicación de datos.
- El servidor de procesos que actúa como puerta de enlace de replicación. El servidor de procesos:
  - Recibe datos de replicación.
  - Optimiza la fecha de la replicación mediante almacenamiento en caché, compresión y cifrado.
  - Envía la fecha de replicación a Azure Storage.
- El servidor de procesos también instala Mobility Service en las máquinas virtuales que se van a replicar. El servidor de procesos realiza la detección automática de máquinas virtuales de VMware locales.
- Después de crear e iniciar la máquina virtual del servidor de configuración, Contoso registra el servidor en el almacén.

Para configurar el entorno de origen de los administradores de Contoso haga lo siguiente:

1. Se descarga la plantilla OVF de Azure Portal (**Preparar infraestructura** > **Origen** > **Servidor de configuración**).

    ![Agregar un servidor de configuración](./media/contoso-migration-rehost-vm-sql-managed-instance/add-cs.png)

2. Importa la plantilla en VMware para crear e implementar la VM.

    ![Implementación de la plantilla de OVF](./media/contoso-migration-rehost-vm-sql-managed-instance/vcenter-wizard.png)

3. La primera vez que activan la máquina virtual se inicia en una experiencia de instalación de Windows Server 2016. Aceptan el contrato de licencia y escriben una contraseña de administrador.
4. Cuando finaliza la instalación, inician sesión en la máquina virtual como administrador. La primera vez que se inicia sesión, se ejecuta automáticamente la herramienta de configuración de Azure Site Recovery.
5. En la herramienta de configuración de Site Recovery, escriben un nombre que usarán para registrar el servidor de configuración en el almacén.
6. La herramienta comprueba la conexión de la máquina virtual a Azure. Una vez establecida la conexión, seleccionan **Iniciar sesión** para iniciar sesión en la suscripción a Azure. Las credenciales deben tener acceso al almacén donde se registra el servidor de configuración.

    ![Registro del servidor de configuración](./media/contoso-migration-rehost-vm-sql-managed-instance/config-server-register2.png)

7. La herramienta realiza algunas tareas de configuración y, a continuación, se reinicia. Vuelven a iniciar sesión en el equipo. El Asistente para administración del servidor de configuración se inicia automáticamente.
8. En el asistente, selecciona la NIC para recibir tráfico de replicación. Una vez configurada, esta opción no se puede cambiar.
9. Seleccionan la suscripción, el grupo de recursos y el almacén de Recovery Services en el que se va a registrar el servidor de configuración.

    ![Selección del almacén de Recovery Services](./media/contoso-migration-rehost-vm-sql-managed-instance/cswiz1.png)

10. Se descarga e instala el Servidor MySQL y VMware PowerCLI. Luego, validan la configuración del servidor.
11. Tras la validación, escriben el nombre de dominio completo (FQDN) o la dirección IP de la instancia de vCenter Server o del host de vSphere. Dejan el puerto predeterminado y escriben el nombre para mostrar de la instancia de vCenter Server en Azure.
12. Especifican la cuenta que se creó anteriormente para que Site Recovery pueda detectar automáticamente las máquinas virtuales de VMware disponibles para la replicación.
13. Escriben las credenciales, por lo que Mobility Service se instala automáticamente cuando se habilita la replicación. En máquinas Windows, la cuenta necesita permisos de administrador local en las máquinas virtuales.

    ![Configuración de vCenter Server](./media/contoso-migration-rehost-vm-sql-managed-instance/cswiz2.png)

14. Cuando finaliza el registro, en Azure Portal, vuelven a comprobar si el servidor de configuración y el servidor de VMware aparecen en la página **Origen** del almacén. La detección puede tardar 15 minutos o más.
15. Site Recovery se conecta a los servidores de VMware mediante la configuración especificada y detecta las máquinas virtuales.

### <a name="set-up-the-target"></a>Configuración del destino

Ahora, los administradores de Contoso configuran el entorno de la replicación de destino:

1. En **Preparar infraestructura** > **Destino**, selecciona la configuración de destino.
2. Site Recovery comprueba si existe una red y una cuenta de almacenamiento en el destino especificado.

### <a name="create-a-replication-policy"></a>Creación de una directiva de replicación

Después de configurar el origen y el destino, los administradores de Contoso crean una directiva de replicación y la asocian con el servidor de configuración:

1. En **Preparar infraestructura** > **Configuración de la replicación** > **Directiva de replicación** >  **Crear y asociar**, se crea la directiva **ContosoMigrationPolicy**.
2. Usa la configuración predeterminada:
    - **Umbral de RPO:** el valor predeterminado es de 60 minutos. Este valor define la frecuencia de creación de puntos de recuperación. Se genera una alerta cuando la replicación continua supera este límite.
    - **Retención de punto de recuperación:** Valor predeterminado de 24 horas. Este valor especifica cuánto tiempo dura el período de retención para cada punto de recuperación. Las máquinas virtuales replicadas se pueden recuperar a cualquier momento de un período.
    - **Frecuencia de las instantáneas coherentes con la aplicación:** el valor predeterminado es de 1 hora. Este valor especifica la frecuencia con la que se crean instantáneas coherentes con la aplicación.

    ![Directiva de replicación: creación](./media/contoso-migration-rehost-vm-sql-managed-instance/replication-policy.png)

3. La directiva se asocia automáticamente al servidor de configuración.

    ![Directiva de replicación: asociación](./media/contoso-migration-rehost-vm-sql-managed-instance/replication-policy2.png)

**¿Necesita más ayuda?**

- Puede leer un tutorial completo de estos pasos en [Configurar la recuperación ante desastres para máquinas virtuales de VMware locales](https://docs.microsoft.com/azure/site-recovery/vmware-azure-tutorial).
- Puede encontrar instrucciones detalladas que le ayudarán a [configurar el entorno de origen](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-source), [implementar el servidor de configuración](https://docs.microsoft.com/azure/site-recovery/vmware-azure-deploy-configuration-server) y [establecer la configuración de replicación](https://docs.microsoft.com/azure/site-recovery/vmware-azure-set-up-replication).

### <a name="enable-replication"></a>Habilitar replicación

Ahora, los administradores de Contoso pueden empezar a replicar WebVM.

1. En **Replicar aplicación** > **Origen** >  **+Replicar**, seleccionan la configuración de origen.
2. Indican que quiere habilitar las máquinas virtuales, seleccionan la instancia de vCenter Server y establecen el servidor de configuración.

    ![Habilitación de la replicación: origen](./media/contoso-migration-rehost-vm-sql-managed-instance/enable-replication1.png)

3. Contoso especifica la configuración de destino, incluido el grupo de recursos y la red donde se ubicará la máquina virtual de Azure después de la conmutación por error. Especifican la cuenta de almacenamiento en la que se almacenarán los datos replicados.

    ![Habilitación de la replicación: destino](./media/contoso-migration-rehost-vm-sql-managed-instance/enable-replication2.png)

4. Seleccionan **SQLVM** para la replicación. Site Recovery instala Mobility Service en cada máquina virtual cuando la replicación está habilitada.

    ![Habilitación de la replicación: selección de la máquina virtual](./media/contoso-migration-rehost-vm-sql-managed-instance/enable-replication3.png)

5. Comprueban que la directiva de replicación correcta está seleccionada y habilitan la replicación para **WEBVM**. Realiza un seguimiento del progreso de la replicación en **Trabajos**. La máquina estará preparada para la conmutación por error después de que finalice el trabajo **Finalizar la protección**.

6. En **Información esencial**, en Azure Portal, pueden ver la estructura de las máquinas virtuales que se replican en Azure:

    ![Vista de la infraestructura](./media/contoso-migration-rehost-vm-sql-managed-instance/essentials.png)

**¿Necesita más ayuda?**

Puede leer un tutorial completo de estos pasos en [Habilitación de la replicación](https://docs.microsoft.com/azure/site-recovery/vmware-azure-enable-replication).

## <a name="step-6-migrate-the-database"></a>Paso 6: Migración de la base de datos

Los administradores de Contoso tienen que crear un proyecto de Azure Database Migration Service y luego migrar la base de datos.

### <a name="create-an-azure-database-migration-service-project"></a>Creación de un proyecto de Azure Database Migration Service

1. Se crea un proyecto de Azure Database Migration Service. Seleccionan el tipo de servidor de origen de **SQL Server** y la **instancia administrada de Azure SQL Database** como destino.

     ![Database Migration Service: nuevo proyecto de migración](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-project.png)

2. Se abre el Asistente para migración.

### <a name="migrate-the-database"></a>Migración de la base de datos

1. En el Asistente para migración, especifican la máquina virtual de origen en la que se encuentra la base de datos local. Escriben las credenciales para acceder a la base de datos.

    ![Database Migration Service: detalles de origen](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-wizard-source.png)

2. Se selecciona la base de datos que se migrará (**SmartHotel.Registration**):

    ![Database Migration Service: selección de base de datos de origen](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-wizard-sourcedb.png)

3. Como destino, escriben el nombre de la instancia administrada de Azure y las credenciales de acceso.

    ![Database Migration Service: detalles de destino](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-target-details.png)

4. En **+Nueva actividad** > **Ejecutar migración**, especifican la configuración para ejecutar la migración:
    - Credenciales de origen y destino.
    - La base de datos para migrar.
    - El recurso compartido de red creado en la máquina virtual local. Azure Database Migration Service lleva las copias de seguridad de origen a este recurso compartido.
        - La cuenta de servicio que ejecuta la instancia de SQL Server de origen debe tener permisos de escritura sobre este recurso compartido.
        - Se debe usar la ruta de acceso del nombre de dominio completo (FQDN) al recurso compartido.
    - El URI de SAS que proporciona a Azure Database Migration Service acceso al contenedor de cuentas de almacenamiento en el que el servicio carga los archivos de copia de seguridad para la migración.

        ![Database Migration Service: configuración de la migración](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-migration-settings.png)

5. Guardan la configuración de migración y, después, ejecutan la migración.
6. En **Introducción**, supervisa el estado de la migración.

    ![Database Migration Service: seguimiento](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-monitor1.png)

7. Cuando ha finalizado la migración, comprueban que las bases de datos de destino existen en la instancia administrada.

    ![Database Migration Service: comprobación de la migración de la base de datos](./media/contoso-migration-rehost-vm-sql-managed-instance/dms-monitor2.png)

## <a name="step-7-migrate-the-vm"></a>Paso 7: Migración de la VM

Los administradores de Contoso ejecutan una conmutación por error rápida de prueba y, después, migran la máquina virtual.

### <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba

Antes de migrar WEBVM, una conmutación por error de prueba ayuda a asegurarse de que todo funciona según lo esperado. Los administradores completan los siguientes pasos:

1. Ejecutan una conmutación por error de prueba en el punto más reciente en el tiempo disponible (**el último que se ha procesado**).
2. Seleccionan **Shut down machine before beginning failover** (Apagar equipo antes de comenzar la conmutación por error). Con esta opción seleccionada, Site Recovery intenta apagar la máquina virtual de origen antes de desencadenar la conmutación por error. La conmutación por error continúa aunque se produzca un error de cierre.
3. Se ejecuta la conmutación por error de prueba: a. Se ejecuta una comprobación de requisitos previos para garantizar que todas las condiciones necesarias para la migración están correctamente establecidas.
    b. La conmutación por error procesa los datos, de modo que se pueda crear una máquina virtual de Azure. Si se selecciona el último punto de recuperación, se crea un punto de recuperación a partir de los datos.
    c. Se crea una máquina virtual de Azure mediante los datos procesados en el paso anterior.
4. Una vez finalizada la conmutación por error, la máquina virtual de Azure de réplica aparece en Azure Portal. Se comprueba que todo funciona correctamente: la máquina virtual tiene el tamaño adecuado, está conectada a la red correcta y está en ejecución.
5. Después de comprobar la conmutación por error de prueba, limpian la conmutación por error y registran las observaciones.

### <a name="migrate-the-vm"></a>Migración de la VM

1. Después de comprobar que la conmutación por error de prueba ha funcionado según lo esperado, los administradores de Contoso crean un plan de recuperación para la migración y agregan WEBVM al plan:

     ![Creación del plan de recuperación: selección de los elementos](./media/contoso-migration-rehost-vm-sql-managed-instance/recovery-plan.png)

2. Ejecutan una conmutación por error en el plan y seleccionan el punto de recuperación más reciente. Especifican que Site Recovery debe intentar cerrar la máquina virtual local antes de desencadenar la conmutación por error.

    ![Conmutación por error](./media/contoso-migration-rehost-vm-sql-managed-instance/failover1.png)

3. Después de la conmutación por error, Contoso comprueba si la VM de Azure aparece según lo esperado en Azure Portal.

   ![Detalles de plan de recuperación](./media/contoso-migration-rehost-vm-sql-managed-instance/failover2.png)

4. Después de la comprobación completan la migración para finalizar el proceso de migración, detiene la replicación para la VM y detiene la facturación de Site Recovery de la VM.

    ![Conmutación por error: migración completada](./media/contoso-migration-rehost-vm-sql-managed-instance/failover3.png)

### <a name="update-the-connection-string"></a>Actualización de la cadena de conexión

Como último paso del proceso de migración, los administradores de Contoso actualizan la cadena de conexión de la aplicación para que apunte a la base de datos migrada que se ejecuta en la instancia administrada de Contoso.

1. En Azure Portal, buscan la cadena de conexión, para lo que seleccionan **Configuración** > **Cadenas de conexión**.

    ![Cadenas de conexión](./media/contoso-migration-rehost-vm-sql-managed-instance/failover4.png)

2. Actualizan la cadena con el nombre de usuario y la contraseña de la instancia administrada de SQL Database.
3. Una vez configurada la cadena, reemplazan la cadena de conexión actual en el archivo web.config de su aplicación.
4. Después de actualizar el archivo y guardarlo, reinician IIS en WEBVM, para lo que ejecutan `IISRESET /RESTART` en una ventana del símbolo del sistema.
5. Después de reiniciar IIS, la aplicación usa la base de datos que se ejecuta en la instancia administrada de SQL Database.
6. En este momento, ya pueden apagar el equipo de SQLVM local. La migración se ha completado.

**¿Necesita más ayuda?**

- Más información sobre cómo [ejecutar una conmutación por error de prueba](https://docs.microsoft.com/azure/site-recovery/tutorial-dr-drill-azure).
- Más información sobre cómo [crear un plan de recuperación](https://docs.microsoft.com/azure/site-recovery/site-recovery-create-recovery-plans).
- Más información sobre cómo [conmutar por error a Azure](https://docs.microsoft.com/azure/site-recovery/site-recovery-failover).

## <a name="clean-up-after-migration"></a>Limpiar después de la migración

Una vez completada la migración, la aplicación SmartHotel360 se ejecuta en una VM de Azure y la base de datos de SmartHotel360 está disponible en la Instancia administrada de Azure SQL Database.

Ahora, Contoso debe realizar las siguientes tareas de limpieza:

- Quitar la máquina WEBVM del inventario de vCenter Server.
- Quitar la máquina SQLVM del inventario de vCenter Server.
- Quitar WEBVM y SQLVM de los trabajos de copia de seguridad locales.
- Actualice la documentación interna para mostrar la nueva ubicación y la dirección IP de WEBVM.
- Quite SQLVM de la documentación interna. Como alternativa, Contoso puede revisar la documentación para mostrar SQLVM como eliminada y ya no aparecerá en el inventario de máquinas virtuales.
- Revise todos los recursos que interactúan con las máquinas virtuales fuera de servicio. Actualice la configuración o la documentación pertinentes para que reflejen la nueva configuración.

## <a name="review-the-deployment"></a>Revisión de la implementación

Con los recursos migrados de Azure, Contoso debe proteger la infraestructura nueva y ponerla totalmente en marcha.

### <a name="security"></a>Seguridad

El equipo de seguridad de Contoso revisa las máquinas virtuales de Azure e Instancia administrada de SQL Database para determinar cualquier problema de seguridad con su implementación:

- El equipo revisa los grupos de seguridad de red que se usan para controlar el acceso de la máquina virtual. Los grupos de seguridad de red ayudan a garantizar que solo pueda pasar el tráfico que se permite para la aplicación.
- El equipo de seguridad de Contoso también está pensando en proteger los datos en el disco mediante Azure Disk Encryption y Azure Key Vault.
- El equipo permite la detección de amenazas en la instancia administrada. La detección de amenazas envía una alerta al sistema del equipo o departamento de seguridad de Contoso para abrir una incidencia si se detecta una amenaza. Más información sobre la [detección de amenazas para Instancia administrada](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-threat-detection).

     ![Seguridad de Instancia administrada: detección de amenazas](./media/contoso-migration-rehost-vm-sql-managed-instance/mi-security.png)

Para más información sobre los procedimientos de seguridad para máquinas virtuales, consulte [Procedimientos de seguridad recomendados para cargas de trabajo de IaaS de Azure](https://docs.microsoft.com/azure/security/azure-security-best-practices-vms).

### <a name="bcdr"></a>BCDR

Para la continuidad empresarial y la recuperación ante desastres (BCDR), Contoso realiza las siguientes acciones:

- Mantener seguros los datos: Contoso realiza la copia de seguridad de los datos de las VM mediante el servicio Azure Backup. [Más información](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
- Mantener las aplicaciones en funcionamiento: Contoso replica las máquinas virtuales de la aplicación de Azure en una región secundaria mediante Site Recovery. [Más información](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).
- Contoso aprende más acerca de cómo administrar la Instancia administrada de SQL, incluidas las [copias de seguridad de la base de datos](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).

### <a name="licensing-and-cost-optimization"></a>Optimización de los costos y licencias

- Contoso ya tiene una licencia de WEBVM. Para aprovechar las ventajas de precios con Ventaja híbrida de Azure, Contoso convierte la máquina virtual de Azure existente.
- Contoso habilita Azure Cost Management, con licencia de Cloudyn, una subsidiaria de Microsoft. Cost Management es una solución de administración de costos de varias nubes que ayuda a Contoso a usar y administrar recursos de Azure y otros recursos de nube. Más información sobre [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview).

## <a name="conclusion"></a>Conclusión

En este artículo, Contoso vuelve a hospedar la aplicación SmartHotel360 en Azure mediante la migración de la VM front-end de la aplicación a Azure con el servicio Site Recovery. Contoso migra la base de datos local a una instancia administrada de Azure SQL Database mediante Azure Database Migration Service.
