---
title: Rehospedaje de una aplicación del departamento de servicios de Linux en Azure y Azure Database for MySQL
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información sobre cómo Contoso vuelve a hospedar una aplicación de Linux local mediante la migración de VM de Azure y Azure Database for MySQL.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: d4681f372038b5c78d4b0793aac1a2b47e9f2c91
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70835038"
---
# <a name="rehost-an-on-premises-linux-app-to-azure-vms-and-azure-database-for-mysql"></a>Rehospedaje de una aplicación Linux local en máquinas virtuales de Azure y en Azure Database for MySQL

En este artículo se muestra cómo la empresa ficticia Contoso rehospeda una aplicación de Apache MySQL PHP (LAMP) basada en Linux de dos niveles y la migra de una ubicación local a Azure mediante máquinas virtuales de Azure y Azure Database for MySQL.

osTicket, la aplicación del departamento de servicios usada en este ejemplo, se proporciona como código abierto. Si quiere utilizarla para sus propias pruebas, puede descargarla desde [GitHub](https://github.com/osTicket/osTicket).

## <a name="business-drivers"></a>Impulsores del negocio

El equipo directivo de TI ha trabajado estrechamente con sus socios comerciales para comprender sus objetivos:

- **Abordar el crecimiento del negocio.** Contoso está creciendo y, como resultado, sus sistemas locales e infraestructura están bajo presión.
- **Limitar el riesgo.** la aplicación del departamento de servicios es fundamental para la empresa. Contoso quiere moverla a Azure sin ningún riesgo.
- **Extensión.** Contoso no quiere cambiar la aplicación en este momento. Simplemente desea mantener la aplicación estable.

## <a name="migration-goals"></a>Objetivos de la migración

El equipo de la nube de Contoso ha definido los objetivos de esta migración con el fin de determinar el mejor método para llevarla a cabo:

- Tras la migración, la aplicación de Azure debe tener las mismas funcionalidades de rendimiento que las que tiene actualmente en su entorno de VMware local. La aplicación seguirá siendo tan imprescindible en la nube como lo es en el entorno local.
- Contoso no quiere hacer inversiones en esta aplicación. Es importante para la empresa, pero, en su estado actual, Contoso solo quiere moverla a la nube de modo seguro.
- Una vez completadas un par de migraciones de aplicaciones de Windows, Contoso quiere aprender a usar una infraestructura basada en Linux en Azure.
- Quiere minimizar las tareas de administración de la base de datos tras mover la aplicación a la nube.

## <a name="proposed-architecture"></a>Arquitectura propuesta

En este escenario:

- La aplicación se divide en niveles entre dos máquinas virtuales (`OSTICKETWEB` y `OSTICKETMYSQL`).
- Las máquinas virtuales se encuentran en el host de VMware ESXi `contosohost1.contoso.com` (versión 6.5).
- El entorno de VMware lo administra vCenter Server 6.5 (`vcenter.contoso.com`) que se ejecuta en una máquina virtual.
- Contoso tiene un centro de datos local (`contoso-datacenter`), con un controlador de dominio local (`contosodc1`).
- La aplicación de nivel de web en `OSTICKETWEB` se migrará a una máquina virtual IaaS de Azure.
- La base de datos de la aplicación se migrará al servicio PaaS de Azure Database for MySQL.
- Dado que Contoso va a migrar una carga de trabajo de producción, los recursos residirán en el grupo de recursos de producción `ContosoRG`.
- Los recursos se replicarán en la región principal (Este de EE. UU. 2) y se colocarán en la red de producción (`VNET-PROD-EUS2`):
  - La máquina virtual web residirá en la subred de front-end (`PROD-FE-EUS2`).
  - La instancia de la base de datos residirá en la subred de la base de datos (`PROD-DB-EUS2`).
- La base de datos de la aplicación se migrará a Azure Database for MySQL con herramientas de MySQL.
- Las VM locales del centro de datos de Contoso se retirarán después de realizar la migración.

![Arquitectura del escenario](./media/contoso-migration-rehost-linux-vm-mysql/architecture.png)

## <a name="migration-process"></a>Proceso de migración

Contoso completará el proceso de migración como se indica a continuación:

Para migrar la VM web:

1. Como primer paso, Contoso configura la infraestructura local y de Azure necesaria para implementar Site Recovery.
2. Después de preparar los componentes locales y de Azure, Contoso configura y habilita la replicación de las máquinas virtuales web.
3. Con la replicación en ejecución, Contoso migra la máquina virtual mediante la conmutación por error en Azure.

Migración de la base de datos:

1. Contoso proporciona una instancia de MySQL en Azure.
2. Contoso configura MySQL Workbench y hace una copia de seguridad local de la base de datos.
3. A continuación, restaura la base de datos desde la copia de seguridad local en Azure.

![Proceso de migración](./media/contoso-migration-rehost-linux-vm-mysql/migration-process.png)

### <a name="azure-services"></a>Servicios de Azure

**Servicio** | **Descripción** | **Costee**
--- | --- | ---
[Azure Site Recovery](/azure/site-recovery) | El servicio orquesta y administra la migración y la recuperación ante desastres de las máquinas virtuales de Azure, así como las máquinas virtuales y servidores físicos locales. | Durante la replicación en Azure, se incurre en gastos de Azure Storage. Las máquinas virtuales de Azure se crean, e incurren en gastos, cuando se produce una conmutación por error. [Más información](https://azure.microsoft.com/pricing/details/site-recovery) sobre cargos y precios.
[Azure Database for MySQL](/azure/mysql) | La base de datos se basa en el motor de MySQL Server de código abierto. Proporciona una base de datos MySQL de comunidad completamente administrada y lista para la empresa como un servicio para el desarrollo e implementación de aplicaciones.

## <a name="prerequisites"></a>Requisitos previos

Esto es lo que Contoso necesita para este escenario.

<!-- markdownlint-disable MD033 -->

**Requisitos** | **Detalles**
--- | ---
**Suscripción de Azure** | En un artículo anterior, Contoso creó suscripciones. Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Si crea una cuenta gratuita, será el administrador de su suscripción y podrá realizar todas las acciones.<br/><br/> Si usa una suscripción existente y no es el administrador, tendrá que solicitar al administrador que le asigne permisos de propietario o colaborador.<br/><br/> Si necesita permisos más específicos, consulte [este artículo](/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Infraestructura de Azure** | Contoso configura la infraestructura de Azure según se describe en la [infraestructura de Azure para la migración](contoso-migration-infrastructure.md).<br/><br/> Obtenga más información sobre los requisitos específicos de la [red](/azure/site-recovery/vmware-physical-azure-support-matrix#network) y el [almacenamiento](/azure/site-recovery/vmware-physical-azure-support-matrix#storage) para Site Recovery.
**Servidores locales** | La instancia local de vCenter Server debe ejecutarse en las versiones 5.5, 6.0 o 6.5.<br/><br/> Un host ESXi que ejecute la versión 5.5, 6.0 o 6.5<br/><br/> Una o más máquinas virtuales VMware que se ejecuten en el host ESXi.
**Máquinas virtuales locales** | [Revise los requisitos de VM Linux](/azure/site-recovery/vmware-physical-azure-support-matrix#replicated-machines) que se admiten para la migración con Site Recovery.<br/><br/> Verifique los [sistemas de almacenamiento y archivos de Linux](/azure/site-recovery/vmware-physical-azure-support-matrix#linux-file-systemsguest-storage) que se admiten.<br/><br/> Las máquinas virtuales tienen que cumplir los [requisitos de Azure](/azure/site-recovery/vmware-physical-azure-support-matrix#azure-vm-requirements).

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Pasos del escenario

Así es como los administradores de Contoso realizarán la migración:

> [!div class="checklist"]
>
> - **Paso 1: Preparación de Azure Site Recovery.** se crea una cuenta de Azure Storage que contiene los datos replicados, así como un almacén de Recovery Services.
> - **Paso 2: Preparación de VMware local para Site Recovery.** se prepararán las cuentas para la detección de VM y la instalación del agente para conectarse a las VM de Azure tras la conmutación por error.
> - **Paso 3: Aprovisionamiento de la base de datos.** En Azure, aprovisionarán una instancia de Azure Database for MySQL.
> - **Paso 4: Replicación de máquinas virtuales.** el entorno de origen y de destino de Site Recovery se configura, así como una directiva de replicación, y se empiezan a replicar las máquinas virtuales en Azure Storage.
> - **Paso 5: Migración de la base de datos.** se configura la migración con herramientas de MySQL.
> - **Paso 6: Migración de las máquinas virtuales mediante Site Recovery.** por último, se ejecuta una conmutación por error de prueba para asegurarse de que todo funciona y, luego, se ejecuta una conmutación por error completa para migrar las VM a Azure.

## <a name="step-1-prepare-azure-for-the-site-recovery-service"></a>Paso 1: Preparación de Azure para el servicio Site Recovery

Contoso necesita un par de componentes de Azure para Site Recovery:

- Una red virtual para colocar los recursos tras la conmutación por error. Contoso ha creado la red virtual durante la [implementación de la infraestructura de Azure](contoso-migration-infrastructure.md)
- Una cuenta de Azure Storage para almacenar los datos replicados.
- Un almacén de Recovery Services en Azure.

Los administradores de Contoso crean una cuenta de almacenamiento y un almacén de la manera siguiente:

1. Se crea una cuenta de almacenamiento (**contosovmsacc20180528**) en la región Este de EE. UU. 2.

    - La cuenta de almacenamiento debe estar en la misma región que el almacén de Recovery Services.
    - Se usa una cuenta de uso general, con almacenamiento estándar y replicación de LRS.

    ![Almacenamiento de Site Recovery](./media/contoso-migration-rehost-linux-vm-mysql/asr-storage.png)

2. Con la red y la cuenta de almacenamiento implementadas, crean un almacén (ContosoMigrationVault) y lo colocan en el grupo de recursos **ContosoFailoverRG**, en la región primaria Este de EE. UU. 2.

    ![Almacén de Recovery Services](./media/contoso-migration-rehost-linux-vm-mysql/asr-vault.png)

**¿Necesita más ayuda?**

[Más información](/azure/site-recovery/tutorial-prepare-azure) sobre cómo configurar Azure para Site Recovery.

## <a name="step-2-prepare-on-premises-vmware-for-site-recovery"></a>Paso 2: Preparación de VMware local para Site Recovery

Los administradores de Contoso preparan la infraestructura de VMware local de la manera siguiente:

- Se crea una cuenta en vCenter Server para automatizar la detección de máquinas virtuales.
- Se crea una cuenta que permite la instalación automática de Mobility Service en las máquinas virtuales de VMware que se van a replicar.
- Se preparan las máquinas virtuales locales para que puedan conectarse a las de Azure cuando se creen tras la migración.

### <a name="prepare-an-account-for-automatic-discovery"></a>Preparación de una cuenta de detección automática

Site Recovery necesita acceso a los servidores de VMware para:

- Detectar automáticamente las máquinas virtuales. Se requiere al menos una cuenta de solo lectura.
- Coordinar la replicación, la conmutación por error y la conmutación por recuperación. Necesita una cuenta que pueda ejecutar operaciones como la creación y eliminación de discos, así como la activación de máquinas virtuales.

Los administradores de Contoso configuran la cuenta de la manera siguiente:

1. Se crea un rol en el nivel de vCenter.
2. Asignan a ese rol los permisos necesarios.

### <a name="prepare-an-account-for-mobility-service-installation"></a>Preparación de una cuenta para la instalación de Mobility Service

Mobility Service debe instalarse en todas las VM que Contoso quiera migrar.

- Site Recovery puede hacer una instalación de inserción automática de este componente cuando habilita la replicación para las VM.
- Para la instalación automática. Site Recovery necesita una cuenta con permisos para tener acceso a la VM.
- Los detalles de la cuenta se especifican durante la configuración de la replicación.
- La cuenta puede ser una cuenta de dominio o local, siempre y cuando tenga permisos de instalación.

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Preparación para la conexión a las máquinas virtuales de Azure después de la conmutación por error

Después de la conmutación por error en Azure, Contoso quiere poder conectarse a las VM de Azure. Para ello, los administradores de Contoso deben realizar lo siguiente:

- Para obtener acceso a través de Internet, habilita SSH en la VM Linux local antes de la migración. En el caso de Ubuntu, puede realizarse mediante el siguiente comando: **Sudo apt-get ssh install -y**.
- Después de la conmutación por error, comprueba los **Diagnósticos de arranque** para ver una captura de pantalla de la VM.
- Si no funciona, debe comprobar que se está ejecutando la VM, así como revisar estas [sugerencias de solución de problemas](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

**¿Necesita más ayuda?**

- [Averigüe](/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-automatic-discovery) cómo puede crear y asignar un rol para la detección automática.
- [Más información](/azure/site-recovery/vmware-azure-tutorial-prepare-on-premises#prepare-an-account-for-mobility-service-installation) sobre cómo crear una cuenta para la instalación de inserción de Mobility Service.

## <a name="step-3-provision-azure-database-for-mysql"></a>Paso 3: Aprovisionamiento de Azure Database for MySQL

Los administradores de Contoso aprovisionan una instancia de base de datos MySQL en la región primaria Este de EE. UU. 2.

1. En Azure Portal, crea un recurso de Azure Database for MySQL.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-1.png)

2. Agrega el nombre **contosoosticket** para la base de datos de Azure. Agrega la base de datos al grupo de recursos de producción **ContosoRG** y especifica las credenciales.
3. La base de datos MySQL local es de la versión 5.7, por lo que selecciona esta versión por cuestiones de compatibilidad. Utiliza los tamaños predeterminados, que coinciden con los requisitos de la base de datos.

     ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-2.png)

4. Para las **opciones de redundancia de copia de seguridad**, seleccionan el uso de **redundancia geográfica**. Esta opción permite restaurar la base de datos en la región secundaria del Centro de EE. UU. si se produce una interrupción. Solo puede configurar esta opción al aprovisionar la base de datos.

     ![Redundancia](./media/contoso-migration-rehost-linux-vm-mysql/db-redundancy.png)

5. En la red **VNET-PROD-EUS2** > **Puntos de conexión de servicio**, agrega un punto de conexión de servicio (una subred de la base de datos) para el servicio SQL.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-3.png)

6. Tras agregar la subred, crea una regla de red virtual que permite obtener acceso desde la subred de la base de datos de la red de producción.

    ![MySQL](./media/contoso-migration-rehost-linux-vm-mysql/mysql-4.png)

## <a name="step-4-replicate-the-on-premises-vms"></a>Paso 4: Replicar máquinas virtuales locales

Para poder migrar la máquina virtual web a Azure, los administradores de Contoso configuran y habilitan la replicación.

### <a name="set-a-protection-goal"></a>Establecimiento de un objetivo de protección

1. En el nombre del almacén (ContosoVMVault), establece un objetivo de replicación (**Introducción** > **Site Recovery** > **Preparar infraestructura**.
2. Especifica que las máquinas se encuentran en el entorno local, que son VM de VMware y que quieren replicarse en Azure.

    ![Objetivo de replicación](./media/contoso-migration-rehost-linux-vm-mysql/replication-goal.png)

### <a name="confirm-deployment-planning"></a>Confirmación del planeamiento de la implementación

Para continuar, confirma que se ha completado la planificación de implementación mediante la selección de la opción **Sí, ya lo hice**. Contoso solo va a migrar una única VM en este escenario, por lo que no es necesario planear la implementación.

### <a name="set-up-the-source-environment"></a>Configuración del entorno de origen

Los administradores de Contoso configuran en ese momento el entorno de origen. Para ello, mediante una plantilla OVF, implementa un servidor de configuración de Site Recovery como una VM local de VMware de alta disponibilidad. Una vez que el servidor de configuración se encuentra en funcionamiento, lo registra en el almacén.

El servidor de configuración ejecuta varios componentes:

- El componente del servidor de configuración que coordina las comunicaciones entre el entorno local y Azure y administra la replicación de datos.
- El servidor de procesos que actúa como puerta de enlace de replicación. Recibe datos de replicación, los optimiza con almacenamiento en caché, compresión y cifrado, y los envía a Azure Storage.
- El servidor de procesos también instala Mobility Service en las máquinas virtuales que quiere replicar, además de realizar la detección automática de las máquinas virtuales de VMware locales.

Los administradores de Contoso lo hacen como sigue:

1. Descarga la plantilla OVF desde **Preparar infraestructura** > **Origen** > **Servidor de configuración**.

    ![Descarga de OVF](./media/contoso-migration-rehost-linux-vm-mysql/add-cs.png)

2. Importa la plantilla en VMware para crear la VM e implementa la VM.

    ![Plantilla de OVF](./media/contoso-migration-rehost-linux-vm-mysql/vcenter-wizard.png)

3. Al activar la VM por primera vez, se inicia en una experiencia de instalación de Windows Server 2016. Acepta el contrato de licencia e introduce una contraseña de administrador.
4. Una vez finalizada la instalación, inicia sesión en la VM como administrador. Cuando se inicia sesión por primera vez, se ejecuta la herramienta de configuración de Azure Site Recovery de manera predeterminada.
5. En la herramienta, especifica un nombre que se usará para registrar el servidor de configuración en el almacén.
6. La herramienta comprueba que la máquina virtual pueda conectarse a Azure.
7. Una vez establecida la conexión, inicia sesión en la suscripción a Azure. Las credenciales deben tener acceso al almacén donde registrará el servidor de configuración.

    ![Registrar servidor de configuración](./media/contoso-migration-rehost-linux-vm-mysql/config-server-register2.png)

8. La herramienta realiza algunas tareas de configuración y, a continuación, se reinicia.
9. Vuelve a iniciar sesión en la máquina y el Asistente para administración del servidor de configuración se inicia automáticamente.
10. En el asistente, selecciona la NIC para recibir tráfico de replicación. Una vez configurada, esta opción no se puede cambiar.
11. Selecciona la suscripción, el grupo de recursos y el almacén en el que se va a registrar el servidor de configuración.

    ![almacén](./media/contoso-migration-rehost-linux-vm-mysql/cswiz1.png)

12. Ahora, descargan e instalan MySQL Server y VMware PowerCLI.
13. Después de la validación, especifica la dirección IP o el FQDN del host de vSphere o vCenter Server. Deja el puerto predeterminado y especifica un nombre descriptivo para vCenter Server.
14. Introduce la cuenta que ha creado para la detección automática, así como las credenciales que utilizará Site Recovery para instalar automáticamente Mobility Service.

    ![vCenter](./media/contoso-migration-rehost-linux-vm-mysql/cswiz2.png)

15. Cuando finaliza el registro, en Azure Portal, comprueban que el servidor de configuración y el servidor VMware aparecen en la página **Origen** del almacén. La detección puede tardar 15 minutos o más.
16. Cuando esté todo listo, Site Recovery se conecta a los servidores de VMware y detecta VM.

### <a name="set-up-the-target"></a>Configuración del destino

Ahora, los administradores de Contoso indican la configuración de replicación de destino.

1. En **Preparar infraestructura** > **Destino**, selecciona la configuración de destino.
2. Site Recovery comprueba si existe una red y una cuenta de almacenamiento de Azure en el destino especificado.

### <a name="create-a-replication-policy"></a>Creación de una directiva de replicación

Con el origen y destino configurados, los administradores de Contoso están listos para crear una directiva de replicación.

1. En **Preparar infraestructura** > **Configuración de la replicación** > **Directiva de replicación** >  **Crear y asociar**, crea una directiva denominada **ContosoMigrationPolicy**.

2. Usa la configuración predeterminada:
    - **Umbral de RPO:** el valor predeterminado es de 60 minutos. Este valor define la frecuencia de creación de puntos de recuperación. Se genera una alerta cuando la replicación continua supera este límite.
    - **Retención de punto de recuperación:** Valor predeterminado de 24 horas. Este valor especifica cuánto tiempo dura el período de retención para cada punto de recuperación. Las máquinas virtuales replicadas se pueden recuperar a cualquier momento de un período.
    - **Frecuencia de las instantáneas coherentes con la aplicación:** Valor predeterminado de una hora. Este valor especifica la frecuencia con la que se crean instantáneas coherentes con la aplicación.

        ![Creación de la directiva de replicación](./media/contoso-migration-rehost-linux-vm-mysql/replication-policy.png)

3. La directiva se asocia automáticamente al servidor de configuración.

    ![Asociación de la directiva de replicación](./media/contoso-migration-rehost-linux-vm-mysql/replication-policy2.png)

**¿Necesita más ayuda?**

- Puede leer un tutorial completo de todos estos pasos en [Configurar la recuperación ante desastres para VM de VMware locales](/azure/site-recovery/vmware-azure-tutorial).
- Puede encontrar instrucciones detalladas que le ayudarán a [configurar el entorno de origen](/azure/site-recovery/vmware-azure-set-up-source), [implementar el servidor de configuración](/azure/site-recovery/vmware-azure-deploy-configuration-server) y [establecer la configuración de replicación](/azure/site-recovery/vmware-azure-set-up-replication).
- [Más información](/azure/virtual-machines/extensions/agent-linux) sobre el agente invitado de Azure para Linux.

### <a name="enable-replication-for-the-web-vm"></a>Habilitación de la replicación de la VM web

Los administradores de Contoso ya pueden empezar a replicar la máquina virtual **OSTICKETWEB**.

1. En **Replicar aplicación** > **Origen** >  **+Replicar**, selecciona la configuración de origen.
2. Indica que quiere habilitar las máquinas virtuales y selecciona la configuración de origen, incluidos vCenter Server y el servidor de configuración.

    ![Habilitar replicación](./media/contoso-migration-rehost-linux-vm-mysql/enable-replication-source.png)

3. Ahora, especifica las opciones de configuración de destino. Entre otras, se incluye el grupo de recursos y una red en la que la VM de Azure se ubicará después de la conmutación por error, así como una cuenta de almacenamiento en la que se almacenarán los datos replicados.

     ![Habilitar replicación](./media/contoso-migration-rehost-linux-vm-mysql/enable-replication2.png)

4. Se selecciona **OSTICKETWEB** para la replicación.

    ![Habilitar replicación](./media/contoso-migration-rehost-linux-vm-mysql/enable-replication3.png)

5. En las propiedades de la VM, selecciona la cuenta que se debe usar para instalar automáticamente Mobility Service en la VM.

     ![Mobility Service](./media/contoso-migration-rehost-linux-vm-mysql/linux-mobility.png)

6. En **Configuración de la replicación** > **Establecer configuración de replicación**, comprueban que se haya aplicado la directiva de replicación correcta y seleccionan **Habilitar replicación**. Mobility Service se instalará automáticamente.
7. Realiza un seguimiento del progreso de la replicación en **Trabajos**. La máquina estará preparada para la conmutación por error después de que finalice el trabajo **Finalizar la protección**.

**¿Necesita más ayuda?**

Puede leer un tutorial completo de todos estos pasos en [Habilitar replicación](/azure/site-recovery/vmware-azure-enable-replication).

## <a name="step-5-migrate-the-database"></a>Paso 5: Migración de la base de datos

Los administradores de Contoso migran la base de datos mediante la copia de seguridad y la restauración con herramientas de MySQL. Instala MySQL Workbench, hace una copia de seguridad de la base de datos de OSTICKETMYSQL y, a continuación, la restaura al servidor de Azure Database for MySQL.

### <a name="install-mysql-workbench"></a>Instalación de MySQL Workbench

1. Comprueban los [requisitos previos y las descargas de MySQL Workbench](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).
2. Instala MySQL Workbench para Windows de acuerdo con las [instrucciones de instalación](https://dev.mysql.com/doc/workbench/en/wb-installing.html).
3. En MySQL Workbench, crea una conexión de MySQL a OSTICKETMYSQL.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench1.png)

4. Exporta la base de datos como **osticket** a un archivo independiente local.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench2.png)

5. Después de realizar la copia de seguridad de la base de datos localmente, crea una conexión a la instancia de Azure Database for MySQL.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench3.png)

6. Ahora, pueden importar (restaurar) la base de datos en la instancia de Azure Database for MySQL desde el archivo independiente. Se crea un nuevo esquema (osticket) para la instancia.

    ![MySQL Workbench](./media/contoso-migration-rehost-linux-vm-mysql/workbench4.png)

## <a name="step-6-migrate-the-vms-with-site-recovery"></a>Paso 6: Migración de las máquinas virtuales mediante Site Recovery

Por último, los administradores de Contoso ejecutan una conmutación por error de prueba rápida y migran la máquina virtual.

### <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba

La ejecución de una conmutación por error de prueba ayuda a comprobar que todo funciona según lo previsto antes de la migración.

1. Ejecutan una conmutación por error de prueba en el punto más reciente en el tiempo disponible (**Procesado más recientemente**).
2. Selecciona **Apague la máquina antes de comenzar con la conmutación por error**, por lo que Site Recovery intenta apagar la VM de origen antes de desencadenar la conmutación por error. La conmutación por error continúa aunque se produzca un error de cierre.
3. Se ejecuta la conmutación por error de prueba:

    - Se ejecuta una comprobación de requisitos previos para garantizar que todas las condiciones necesarias para la conmutación por error están correctamente establecidas.
    - La conmutación por error procesa los datos, de modo que se pueda crear una máquina virtual de Azure. Si se selecciona el último punto de recuperación, se crea un punto de recuperación a partir de los datos.
    - Se crea una VM de Azure mediante los datos procesados en el paso anterior.

4. Una vez finalizada la conmutación por error, la VM de Azure de réplica aparece en Azure Portal. Contoso comprueba si la VM tiene el tamaño adecuado, si está conectada a la red correspondiente y si se está ejecutando.
5. Después, limpia la conmutación por error y registra y guarda las observaciones.

### <a name="migrate-the-vm"></a>Migración de la VM

Para migrar la máquina virtual, los administradores de Contoso crean un plan de recuperación que incluye la máquina virtual y conmutan el plan por error en Azure.

1. Se crea un plan y se agrega **OSTICKETWEB** a él.

    ![Plan de recuperación](./media/contoso-migration-rehost-linux-vm-mysql/recovery-plan.png)

2. Ejecuta una conmutación por error en el plan. Selecciona el punto de recuperación más reciente y especifica que Site Recovery debe intentar apagar la VM local antes de desencadenar la conmutación por error. Puede seguir el progreso de la conmutación por error en la página **Trabajos**.

    ![Conmutación por error](./media/contoso-migration-rehost-linux-vm-mysql/failover1.png)

3. Durante la conmutación por error, vCenter Server emite comandos para detener las dos VM que se ejecutan en el host ESXi.

    ![Conmutación por error](./media/contoso-migration-rehost-linux-vm-mysql/vcenter-failover.png)

4. Después de la conmutación por error, Contoso comprueba si la VM de Azure aparece según lo esperado en Azure Portal.

    ![Conmutación por error](./media/contoso-migration-rehost-linux-vm-mysql/failover2.png)

5. Después de comprobar la VM, completa la migración. Con esta acción se detienen la replicación de la VM y la facturación de Site Recovery para la VM.

    ![Conmutación por error](./media/contoso-migration-rehost-linux-vm-mysql/failover3.png)

**¿Necesita más ayuda?**

- [Más información](/azure/site-recovery/tutorial-dr-drill-azure) sobre la ejecución de una conmutación por error de prueba.
- [Más información](/azure/site-recovery/site-recovery-create-recovery-plans) sobre cómo crear un plan de recuperación.
- [Más información](/azure/site-recovery/site-recovery-failover) sobre cómo crear una conmutación por error en Azure.

### <a name="connect-the-vm-to-the-database"></a>Conexión de la VM a la base de datos

Como último paso del proceso de migración, los administradores de Contoso actualizan la cadena de conexión de la aplicación para que apunte a Azure Database for MySQL.

1. Realiza una conexión SSH a la VM OSTICKETWEB mediante Putty u otro cliente SSH. La VM es privada, por lo que se conecta mediante la dirección IP privada.

    ![Conexión a la base de datos](./media/contoso-migration-rehost-linux-vm-mysql/db-connect.png)

    ![Conexión a la base de datos](./media/contoso-migration-rehost-linux-vm-mysql/db-connect2.png)

2. Actualiza la configuración para que la VM **OSTICKETWEB** pueda comunicarse con la base de datos **OSTICKETMYSQL**. Actualmente, la configuración está codificada de forma rígida con la dirección IP local 172.16.0.43.

    **Antes de la actualización:**

    ![Actualización de la IP](./media/contoso-migration-rehost-linux-vm-mysql/update-ip1.png)

    **Después de la actualización:**

    ![Actualización de la IP](./media/contoso-migration-rehost-linux-vm-mysql/update-ip2.png)

    ![Actualización de la IP](./media/contoso-migration-rehost-linux-vm-mysql/update-ip3.png)

3. Reinicia el servicio con **systemctl restart apache2**.

    ![Reinicio](./media/contoso-migration-rehost-linux-vm-mysql/restart.png)

4. Por último, actualiza los registros DNS de **OSTICKETWEB** en uno de los controladores de dominio de Contoso.

    ![Actualización de DNS](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

## <a name="clean-up-after-migration"></a>Limpiar después de la migración

Al finalizar la migración, los niveles de la aplicación osTicket se ejecutan en VM de Azure.

Ahora, Contoso debe hacer lo siguiente:

- Quitar las VM de VMware del inventario de vCenter.
- Quitar las VM locales de los trabajos de copia de seguridad locales.
- Actualizar la documentación interna para que muestre las nuevas ubicaciones y las direcciones IP.
- Revisar los recursos que interactúan con las VM locales y actualizar los valores de configuración pertinentes o la documentación para reflejar la nueva configuración.
- Contoso usaba el servicio de Azure Migrate con la asignación de dependencia para evaluar la VM **OSTICKETWEB** para la migración. Ahora, debe quitar de la VM los agentes (Microsoft Monitoring Agent o Dependency Agent) que se instalaron con este propósito.

## <a name="review-the-deployment"></a>Revisión de la implementación

Con la aplicación en ejecución, Contoso debe proteger y poner totalmente operativa la infraestructura nueva.

### <a name="security"></a>Seguridad

El equipo de seguridad de Contoso revisa la VM y la base de datos para determinar cualquier problema de seguridad.

- Revisan los grupos de seguridad de red de la máquina virtual con el fin de controlar el acceso. Los NSG se usan para garantizar que solo el tráfico permitido puede pasar a la aplicación.
- Considera la posibilidad de proteger los datos en los discos de la máquina virtual mediante el cifrado de discos y Azure Key Vault.
- La comunicación entre la instancia de la base de datos y la VM no está configurada para SSL. Deberá realizar esta acción para garantizar que el tráfico de la base de datos no pueda piratearse.

Obtenga [más información](/azure/security/azure-security-best-practices-vms) sobre los procedimientos de seguridad recomendados de las VM.

### <a name="bcdr"></a>BCDR

Para la continuidad empresarial y la recuperación ante desastres, Contoso realiza las siguientes acciones:

- **Mantener seguros los datos.** Contoso realiza la copia de seguridad de los datos de la VM de la aplicación mediante el servicio Azure Backup. [Más información](/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). No deberá configurar la copia de seguridad de la base de datos. Azure Database for MySQL crea automáticamente copias de seguridad del servidor y las almacena. Contoso optó por utilizar la redundancia geográfica para la base de datos para que sea resistente y esté lista para la producción.
- **Mantener las aplicaciones en funcionamiento.** Contoso replica las máquinas virtuales de la aplicación de Azure en una región secundaria mediante Site Recovery. [Más información](/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Optimización de los costos y licencias

- Después de implementar los recursos, Contoso asigna etiquetas de Azure de acuerdo con las decisiones que se tomaron durante la implementación de la [infraestructura de Azure](contoso-migration-infrastructure.md#set-up-tagging).
- No hay ningún problema relacionado con las licencias para los servidores de Ubuntu de Contoso.
- Contoso habilitará Azure Cost Management bajo licencia de Cloudyn, una subsidiaria de Microsoft. Se trata de una solución de administración de costos en varias nubes que le permitirá utilizar y administrar Azure y otros recursos en la nube. [Más información](/azure/cost-management/overview) sobre Azure Cost Management.
