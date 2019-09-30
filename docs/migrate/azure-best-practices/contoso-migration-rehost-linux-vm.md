---
title: Rehospedaje de una aplicación local Linux en Azure Virtual Machines
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información sobre cómo Contoso rehospeda una aplicación de Linux local mediante la migración a VM de Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 579f6eb761a6e59ab179e99c4c607f87897b4215
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224176"
---
# <a name="rehost-an-on-premises-linux-app-to-azure-vms"></a>Rehospedaje de una aplicación local Linux en Azure Virtual Machines

En este artículo se muestra cómo la empresa ficticia Contoso rehospeda una aplicación de Apache MySQL PHP (LAMP) basada en Linux y de dos niveles mediante máquinas virtuales de IaaS de Azure.

osTicket, la aplicación del departamento de servicios usada en este ejemplo, se proporciona como código abierto. Si quiere utilizarla para sus propias pruebas, puede descargarla desde [GitHub](https://github.com/osTicket/osTicket).

## <a name="business-drivers"></a>Impulsores del negocio

El equipo directivo de TI ha trabajado estrechamente con sus socios comerciales para comprender lo quieren lograr con esta migración:

- **Abordar el crecimiento del negocio.** Contoso está creciendo y, como resultado, sus sistemas locales e infraestructura están bajo presión.
- **Limitar el riesgo.** la aplicación de consola de servicio es fundamental para el negocio de Contoso. Contoso quiere moverla a Azure sin ningún riesgo.
- **Extensión.** Contoso no quiere cambiar ahora mismo la aplicación. Solo quiere asegurarse de que la aplicación es estable.

## <a name="migration-goals"></a>Objetivos de la migración

El equipo de la nube de Contoso ha definido los objetivos de esta migración con el fin de determinar el mejor método para llevarla a cabo:

- Tras la migración, la aplicación de Azure debe tener las mismas funcionalidades de rendimiento que las que tiene actualmente en su entorno de VMware local. La aplicación seguirá siendo tan imprescindible en la nube como lo es en el entorno local.
- Contoso no quiere hacer inversiones en esta aplicación. Es importante para la empresa, pero, en su formato actual, Contoso solo quiere moverla a la nube de modo seguro.
- Contoso no quiere cambiar el modelo de operaciones de esta aplicación. Quiere interactuar con la aplicación en la nube de la misma manera que lo hace ahora.
- Contoso no quiere cambiar la funcionalidad de la aplicación. Solo cambiará su ubicación.
- Una vez completadas un par de migraciones de aplicaciones de Windows, Contoso quiere aprender a usar una infraestructura basada en Linux en Azure.

## <a name="solution-design"></a>Diseño de la solución

Después de fijar sus objetivos y requisitos, Contoso diseña y revisa una solución de implementación e identifica el proceso de migración, incluidos los servicios de Azure que Contoso usará para ello.

### <a name="current-app"></a>Aplicación actual

- La aplicación OSTicket se divide en capas entre dos máquinas virtuales (**OSTICKETWEB** y **OSTICKETMYSQL**).
- Las VM se encuentran en el host de VMware ESXi **contosohost1.contoso.com** (versión 6.5).
- El entorno de VMware lo administra vCenter Server 6.5 (**vcenter.contoso.com**), que se ejecuta en una VM.
- Contoso tiene un centro de datos local (**contoso-datacenter**), con un controlador de dominio local (**contosodc1**).

### <a name="proposed-architecture"></a>Arquitectura propuesta

- Dado que la aplicación es una carga de trabajo de producción, las máquinas virtuales de Azure residirán en el grupo de recursos de producción **ContosoRG**.
- Las VM migrarán a la región principal (Este de EE. UU. 2) y se colocarán en la red de producción (VNET-PROD-EUS2):
  - La VM web residirá en la subred de front-end (PROD-FE-EUS2).
  - La VM de la base de datos residirá en la subred de la base de datos (PROD-DB-EUS2).
- Las VM locales del centro de datos de Contoso se retirarán después de realizar la migración.

![Arquitectura del escenario](./media/contoso-migration-rehost-linux-vm/architecture.png)

### <a name="solution-review"></a>Revisión de la solución

Contoso evalúa el diseño propuesto y crea una lista de ventajas y desventajas.

<!-- markdownlint-disable MD033 -->

**Consideración** | **Detalles**
--- | ---
**Ventajas** | Las dos máquinas virtuales de la aplicación se moverán a Azure sin cambios, de forma que se simplifica la migración.<br/><br/> Dado que Contoso usa lift-and-shift con ambas máquinas virtuales de la aplicación, no se necesitan configuraciones ni herramientas de migración especiales para la base de datos de la aplicación.<br/><br/> Contoso conservará el control total de las máquinas virtuales de la aplicación en Azure. <br/><br/> Las máquinas virtuales de la aplicación ejecutan Ubuntu 16.04-TLS, que es una distribución de Linux aprobada. [Más información](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros).
**Desventajas** | La capa de datos y la capa web de la aplicación seguirán siendo un único punto de conmutación por error. <br/><br/> Contoso deberá seguir admitiendo la aplicación en las máquinas virtuales de Azure en lugar de moverla a un servicio administrado como Azure App Service y Azure Database for MySQL.<br/><br/> Contoso sabe que al simplificar las cosas con una migración de máquinas virtuales mediante lift-and-shift, no están aprovechando al máximo las características proporcionadas por [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) (alta disponibilidad integrada, rendimiento predecible, escalado sencillo, copias de seguridad automáticas y seguridad integrada).

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Proceso de migración

Contoso realizará la migración como se indica a continuación:

- Primero, Contoso prepara y configura los componentes de Azure para Azure Migrate Server Migration y prepara la infraestructura local de VMware.
- Ya tienen la [infraestructura de Azure](./contoso-migration-infrastructure.md) en su lugar, por lo que Contoso solo tiene que configurar la replicación de las máquinas virtuales con la herramienta de Azure Migrate Server Migration.
- Con todo preparado, Contoso puede comenzar a replicar las máquinas virtuales.
- Una vez que se haya habilitado la replicación y esta se encuentre en funcionamiento, Contoso migrará la máquina virtual, haciendo que conmute por error en Azure.

![Proceso de migración](./media/contoso-migration-rehost-linux-vm/migration-process-az-migrate.png)

### <a name="azure-services"></a>Servicios de Azure

**Servicio** | **Descripción** | **Costee**
--- | --- | ---
[Azure Migrate Server Migration](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm) | El servicio orquesta y administra la migración de las aplicaciones y cargas de trabajo locales, y las instancias de máquina virtual de AWS/GCP. | Durante la replicación en Azure, se incurre en gastos de Azure Storage. Las máquinas virtuales de Azure se crean, e incurren en gastos, cuando se produce una conmutación por error. [Más información](https://azure.microsoft.com/pricing/details/azure-migrate) sobre cargos y precios.

## <a name="prerequisites"></a>Requisitos previos

Esto es lo que Contoso necesita para este escenario.

<!-- markdownlint-disable MD033 -->

**Requisitos** | **Detalles**
--- | ---
**Suscripción de Azure** | En un artículo anterior de esta serie, Contoso creó suscripciones. Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Si crea una cuenta gratuita, será el administrador de su suscripción y podrá realizar todas las acciones.<br/><br/> Si usa una suscripción existente y no es el administrador, tendrá que solicitar al administrador que le asigne permisos de propietario o colaborador.<br/><br/> Si necesita permisos más específicos, consulte [este artículo](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Infraestructura de Azure** |  [Vea](./contoso-migration-infrastructure.md) cómo Contoso configuró una infraestructura de Azure.<br/><br/> Más información sobre los [requisitos previos](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm#prerequisites) específicos para Azure Migrate Server Migration.
**Servidores locales** | La instancia local de vCenter Server debe ejecutarse en las versiones 5.5, 6.0 o 6.5.<br/><br/> Un host ESXi que ejecute la versión 5.5, 6.0 o 6.5<br/><br/> Una o más máquinas virtuales VMware que se ejecuten en el host ESXi.
**Máquinas virtuales locales** | [Revise las máquinas Linux](https://docs.microsoft.com/azure/virtual-machines/linux/endorsed-distros) que se han aprobado para ejecutarse en Azure.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Pasos del escenario

Así es como Azure realizará la migración:

> [!div class="checklist"]
>
> - **Paso 1: Preparación de Azure para Azure Migrate Server Migration.** Se agrega la herramienta Azure Migrate Server Migration al proyecto de Azure Migrate.
> - **Paso 2: Preparación del entorno de VMware local para Azure Migrate Server Migration.** Se preparan las cuentas para la detección de VM y se prepara la conexión a las VM de Azure tras la conmutación por error.
> - **Paso 3: Replicación de máquinas virtuales.** Se configura la replicación y se comienzan a replicar las VM en Azure Storage.
> - **Paso 4: Migración de las máquinas virtuales con Azure Migrate Server Migration.** se ejecuta una conmutación por error de prueba para asegurarse de que todo funciona y, luego, se ejecuta una conmutación por error completa para migrar las VM a Azure.

## <a name="step-1-prepare-azure-for-the-azure-migrate-server-migration-tool"></a>Paso 1: Preparación de Azure para Azure Migrate Server Migration

Estos son los componentes de Azure que Contoso necesita para migrar las VM a Azure:

- Una red virtual en la que se encontrarán las VM de Azure cuando se creen durante la conmutación por error.
- Herramienta Azure Migrate Server Migration aprovisionada.

Se deben configurar como se muestra a continuación:

1. **Configuración de una red:** Contoso ya configuró una red que se puede usar para Azure Migrate Server Migration cuando [implementó la infraestructura de Azure](./contoso-migration-infrastructure.md).

    - La aplicación SmartHotel360 es una aplicación de producción, y las VM se migrarán a la red de producción de Azure (VNET-PROD-EUS2) en la región principal Este de EE. UU. 2.
    - Ambas VM se colocarán en el grupo de recursos ContosoRG, que se usa para los recursos de producción.
    - La máquina virtual de front-end de la aplicación (WEBVM) se migrará a la subred de front-end (PROD-FE-EUS2), en la red de producción.
    - La base de datos de la aplicación (SQLVM) se migrará a la subred de base de datos (PROD-DB-EUS2), en la red de producción.

2. **Aprovisionamiento de la herramienta de migración de Azure Migrate Server:** Con la cuenta de almacenamiento y de red implementada, Contoso ahora crea un almacén de Recovery Services (ContosoMigrationVault) y lo coloca en el grupo de recursos ContosoFailoverRG de la región principal Este de EE. UU. 2.

    ![Herramienta Azure Migrate Server Migration](./media/contoso-migration-rehost-linux-vm/server-migration-tool.png)

**¿Necesita más ayuda?**

[Más información](https://docs.microsoft.com/azure/migrate) sobre cómo configurar la herramienta Azure Migrate Server Migration.

### <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Preparación para la conexión a las máquinas virtuales de Azure después de la conmutación por error

Después de la conmutación por error en Azure, Contoso quiere poder conectarse a las VM replicadas de Azure. Para ello, hay un par de cosas que los administradores de Contoso deben hacer:

- Para acceder a las máquinas virtuales de Azure a través de Internet, habilitan SSH en la máquina virtual Linux local antes de la migración. En el caso de Ubuntu, puede realizarse mediante el siguiente comando: **Sudo apt-get ssh install -y**.
- Después de ejecutar la migración (conmutación por error), pueden comprobar los **diagnósticos de arranque** para ver una captura de pantalla de la máquina virtual.
- Si esto no funciona, deberán comprobar que la máquina virtual está en ejecución y revisar estas [sugerencias de solución de problemas](https://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

**¿Necesita más ayuda?**

- [Más información](https://docs.microsoft.com/azure/migrate/contoso-migration-rehost-linux-vm#prepare-vms-for-migration) sobre cómo preparar las máquinas virtuales para la migración.

## <a name="step-3-replicate-the-on-premises-vms"></a>Paso 3: Replicar máquinas virtuales locales

Para que los administradores de Contoso puedan ejecutar una migración a Azure, tienen que configurar y habilitar la replicación.

Una vez finalizada la detección, puede comenzar la replicación de máquinas virtuales de VMware en Azure.

1. En el proyecto de Azure Migrate > **Servidores**, **Azure Migrate: Migración del servidor**, haga clic en **Replicar**.

    ![Replicación de máquinas virtuales](./media/contoso-migration-rehost-linux-vm/select-replicate.png)

2. En **Replicar** > **Configuración de origen** >  **¿Las máquinas están virtualizadas?** , seleccione **Sí, con VMware vSphere Hypervisor**.
3. En **Dispositivo local**, seleccione el nombre del dispositivo de Azure Migrate que configuró > **OK**.

    ![Configuración de origen](./media/contoso-migration-rehost-linux-vm/source-settings.png)

4. En **Máquinas virtuales**, seleccione las máquinas que desea replicar.
    - Si ha ejecutado una evaluación para las máquinas virtuales, puede aplicar las recomendaciones de tamaño y tipo de disco (Premium/estándar) de máquina virtual que sugieren los resultados de dicha evaluación. Para ello, en **¿Quiere importar la configuración de migración de evaluación de Azure Migrate?** , seleccione la opción **Sí**.
    - Si no ha ejecutado una evaluación o no desea usar la configuración de evaluación, seleccione la opción **No**.
    - Si ha decidido usar la evaluación, seleccione el grupo de máquinas virtuales y el nombre de la evaluación.

    ![Seleccionar evaluación](./media/contoso-migration-rehost-linux-vm/select-assessment.png)

5. En **Máquinas virtuales**, busque las máquinas virtuales que necesite y compruebe todas las que desee migrar. A continuación, haga clic en **Siguiente: Configuración de destino**.

6. En **Configuración de destino**, seleccione la suscripción y la región de destino a la que va a migrar, y especifique el grupo de recursos en el que residirán las máquinas virtuales de Azure después de la migración. En **Red virtual**, seleccione la red virtual o la subred de Azure a la que se unirán las máquinas virtuales de Azure después de la migración.
7. En **Ventaja híbrida de Azure**:

    - Seleccione **No** si no desea aplicar la Ventaja híbrida de Azure. A continuación, haga clic en **Siguiente**.
    - Seleccione **Sí** si tiene equipos con Windows Server que están incluidos en suscripciones activas de Software Assurance o Windows Server y desea aplicar el beneficio a las máquinas que va a migrar. A continuación, haga clic en **Siguiente**.

8. En **Proceso**, revise el nombre de la máquina virtual, el tamaño, el tipo de disco del sistema operativo y el conjunto de disponibilidad. Las máquinas virtuales deben cumplir los [requisitos de Azure](https://docs.microsoft.com/azure/migrate/migrate-support-matrix-vmware#agentless-migration-vmware-vm-requirements).

    - **Tamaño de VM**: si usa las recomendaciones de la evaluación, el menú desplegable de tamaño de VM contendrá el tamaño recomendado. De lo contrario, Azure Migrate elige un tamaño en función de la coincidencia más cercana en la suscripción de Azure. También puede elegir un tamaño de manera manual en **Tamaño de la máquina virtual de Azure**.
    - **Disco del sistema operativo**: especifique el disco del sistema operativo (arranque) de la máquina virtual. Este es el disco que tiene el cargador de arranque y el instalador del sistema operativo.
    - **Conjunto de disponibilidad**: si la máquina virtual debe estar incluida en un conjunto de disponibilidad de Azure después de la migración, especifique el conjunto. El conjunto debe estar en el grupo de recursos de destino que especifique para la migración.

9. En **Discos**, especifique si los discos de la máquina virtual se deben replicar en Azure y seleccione el tipo de disco (discos SSD o HDD estándar, o bien discos administrados prémium) en Azure. A continuación, haga clic en **Siguiente**.
    - Puede excluir discos de la replicación.
    - Si excluye discos, no estarán incluidos en la máquina virtual de Azure después de la migración.

10. En **Revisar e iniciar la replicación**, revise la configuración y haga clic en **Replicar** para iniciar la replicación inicial de los servidores.

> [!NOTE]
> Puede actualizar la configuración de replicación en cualquier momento antes de que esta comience; para ello, vaya a **Administrar** > **Replicación de máquinas**. Una vez iniciada la replicación, su configuración no se puede cambiar.

## <a name="step-4-migrate-the-vms"></a>Paso 4: Migrar las VM

Los administradores de Contoso ejecutan una conmutación por error de prueba rápida y, luego, una conmutación por error completa para migrar las máquinas virtuales.

### <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba

1. En **Objetivos de migración** > **Servidores** > **Azure Migrate: Server Migration**, haga clic en **Probar servidores migrados**.

     ![Probar servidores migrados](./media/contoso-migration-rehost-linux-vm/test-migrated-servers.png)

2. Haga clic con el botón derecho en la máquina virtual que va a probar y haga clic en **Migración de prueba**.

    ![Migración de prueba](./media/contoso-migration-rehost-linux-vm/test-migrate.png)

3. En **Migración de prueba**, seleccione la red virtual de Azure en la que se ubicará la máquina virtual de Azure después de la migración. Se recomienda usar una red virtual que no sea de producción.
4. Comienza el trabajo de **Migración de prueba**. Supervise el trabajo en las notificaciones del portal.
5. Una vez finalizada la migración, la máquina virtual de Azure migrada se puede ver en **Máquinas virtuales** en Azure Portal. El nombre de la máquina tiene el sufijo **-Test**.
6. Una vez finalizada la prueba, haga clic con el botón derecho en la máquina virtual de Azure, en **Replicación de máquinas**, y haga clic en **Limpiar la migración de prueba**.

    ![Limpiar la migración](./media/contoso-migration-rehost-linux-vm/clean-up.png)

### <a name="migrate-the-vms"></a>Migrar las VM

Ahora, los administradores de Contoso ejecutan una conmutación por error completa para completar la migración.

1. En el proyecto de Azure Migrate > **Servidores** > **Azure Migrate: Server Migration**, haga clic en **Replicando servidores**.

    ![Replicando servidores](./media/contoso-migration-rehost-linux-vm/replicating-servers.png)

2. En **Replicación de máquinas**, haga clic con el botón derecho en la máquina virtual > **Migrar**.
3. En **Migrar** >  **¿Quiere apagar las máquinas virtuales y realizar una migración planificada sin perder datos?** , seleccione **Sí** > **Aceptar**.
    - De forma predeterminada, Azure Migrate apaga la máquina virtual local y ejecuta una replicación a petición para sincronizar los cambios que se han producido en la máquina virtual desde la última replicación. De esta forma se garantiza que no se pierden datos.
    - Si no desea apagar la máquina virtual, seleccione **No**
4. Se inicia un trabajo de migración de la máquina virtual. Realice un seguimiento del trabajo en las notificaciones de Azure.
5. Una vez finalizado el trabajo, la máquina virtual puede ver y administrar desde la página **Máquinas virtuales**.

### <a name="connect-the-vm-to-the-database"></a>Conexión de la VM a la base de datos

Como último paso del proceso de migración, los administradores de Contoso actualizan la cadena de conexión de la aplicación para que apunte a la base de datos de la aplicación que se ejecuta en la máquina virtual **OSTICKETMYSQL**.

1. Realiza una conexión SSH a la VM **OSTICKETWEB** mediante Putty u otro cliente SSH. La VM es privada, por lo que se conecta mediante la dirección IP privada.

    ![Conexión a la base de datos](./media/contoso-migration-rehost-linux-vm/db-connect.png)

    ![Conexión a la base de datos](./media/contoso-migration-rehost-linux-vm/db-connect2.png)

2. Contoso debe asegurarse de que la VM **OSTICKETWEB** puede comunicarse con la base de datos **OSTICKETMYSQL**. Actualmente, la configuración está codificada de forma rígida con la dirección IP local 172.16.0.43.

    **Antes de la actualización:**

    ![Actualización de la IP](./media/contoso-migration-rehost-linux-vm/update-ip1.png)

    **Después de la actualización:**

    ![Actualización de la IP](./media/contoso-migration-rehost-linux-vm/update-ip2.png)

3. Reinicia el servicio con **systemctl restart apache2**.

    ![Reinicio](./media/contoso-migration-rehost-linux-vm/restart.png)

4. Por último, actualiza los registros DNS de **OSTICKETWEB** y **OSTICKETMYSQL** en uno de los controladores de dominio de Contoso.

    ![Actualización de DNS](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

    ![Actualización de DNS](./media/contoso-migration-rehost-linux-vm-mysql/update-dns.png)

**¿Necesita más ayuda?**

- [Más información](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#run-a-test-migration) sobre la ejecución de una conmutación por error de prueba.
- [Más información](https://docs.microsoft.com/azure/migrate/tutorial-migrate-vmware#migrate-vms) sobre cómo migrar máquinas virtuales a Azure.

## <a name="clean-up-after-migration"></a>Limpiar después de la migración

Al finalizar la migración, los niveles de la aplicación osTicket se ejecutan en VM de Azure.

Ahora, Contoso debe realizar la siguiente limpieza:

- Quitar las VM locales del inventario de vCenter.
- Quitar las VM locales de los trabajos de copia de seguridad locales.
- Actualizar la documentación interna para mostrar la nueva ubicación, así como las direcciones IP de OSTICKETWEB y OSTICKETMYSQL.
- Revisar los recursos que interactúan con las VM y actualizar las opciones de configuración pertinentes o la documentación para reflejar la nueva configuración.
- Contoso usaba el servicio de Azure Migrate con la asignación de dependencia para obtener acceso a las VM para la migración. Los administradores deben quitar de la máquina virtual los componentes Microsoft Monitoring Agent y Microsoft Dependency Agent que se instalaron con este fin.

## <a name="review-the-deployment"></a>Revisión de la implementación

Con la aplicación en ejecución, Contoso debe proteger y poner totalmente en marcha la infraestructura nueva.

### <a name="security"></a>Seguridad

El equipo de seguridad de Contoso revisa las VM OSTICKETWEB y OSTICKETMYSQL para determinar cualquier problema de seguridad.

- El equipo revisa los grupos de seguridad de red de las máquinas virtuales para controlar el acceso. Los NSG se usan para garantizar que solo el tráfico permitido puede pasar a la aplicación.
- El equipo también considera la posibilidad de proteger los datos de los discos de la máquina virtual mediante el cifrado de discos y Azure Key Vault.

Obtenga [más información](https://docs.microsoft.com/azure/security/azure-security-best-practices-vms) sobre los procedimientos de seguridad recomendados de las VM.

### <a name="bcdr"></a>BCDR

Para la continuidad empresarial y la recuperación ante desastres, Contoso realiza las siguientes acciones:

- **Mantener seguros los datos.** Contoso realiza la copia de seguridad de los datos de las VM mediante el servicio Azure Backup. [Más información](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
- **Mantener las aplicaciones en funcionamiento.** Contoso replica las máquinas virtuales de la aplicación de Azure en una región secundaria mediante Site Recovery. [Más información](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

### <a name="licensing-and-cost-optimization"></a>Optimización de los costos y licencias

- Después de implementar los recursos, Contoso asigna etiquetas de Azure según lo definido durante la [implementación de la infraestructura de Azure](./contoso-migration-infrastructure.md#set-up-tagging).
- Contoso no tiene problemas relacionados con las licencias con sus servidores de Ubuntu.
- Contoso habilitará Azure Cost Management bajo licencia de Cloudyn, una subsidiaria de Microsoft. Se trata de una solución de administración de costos en varias nubes que le permitirá utilizar y administrar Azure y otros recursos en la nube. [Más información](https://docs.microsoft.com/azure/cost-management/overview) sobre Azure Cost Management.
