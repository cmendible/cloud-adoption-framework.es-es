---
title: Implementación de una infraestructura de migración
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información acerca de cómo Contoso puede configurar una infraestructura de Azure para la migración a Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/1/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: 35a7d62236203dd916d99aea8bf67853c86df10a
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224153"
---
# <a name="deploy-a-migration-infrastructure"></a>Implementación de una infraestructura de migración

En este artículo se muestra cómo la empresa ficticia Contoso prepara su infraestructura local para la migración, configura una infraestructura de Azure como preparación para la migración a Azure y dirige el negocio en un entorno híbrido. Cuando usa este ejemplo para ayudar a planear su propios esfuerzos de migración de infraestructura, tenga en cuenta lo siguiente:

- La arquitectura de ejemplo proporcionada es específica de Contoso. Revise las necesidades de negocio de su organización, su estructura y los requisitos técnicos cuando se tomen decisiones importantes sobre la infraestructura sobre el diseño de la suscripción o la arquitectura de la red.
- El que necesite todos los elementos que se describen en este artículo depende de su estrategia de migración. Por ejemplo, si solo va a compilar aplicaciones nativas de la nube en Azure, es posible que necesite una estructura de red menos compleja.

## <a name="overview"></a>Información general

Antes de poder migrar Contoso a Azure, es fundamental preparar una infraestructura de Azure. Por lo general, hay seis áreas generales en la que Contoso debe pensar:

> [!div class="checklist"]
>
> - **Paso 1: Suscripciones de Azure.** ¿Cómo compra Contoso Azure y cómo interactúa con la plataforma y los servicios de Azure?
> - **Paso 2: Identidad híbrida.** ¿Cómo administra y controla el acceso a recursos de Azure y locales después de la migración? ¿Cómo Contoso amplía o mueve la administración de identidades a la nube?
> - **Paso 3: Recuperación ante desastres y resistencia.** ¿Cómo garantiza Contoso que las aplicaciones y las infraestructuras son resilientes si se producen interrupciones y desastres?
> - **Paso 4: Redes.** ¿Cómo debe diseñar Contoso la infraestructura de red y establecer la conectividad entre el centro de datos local y Azure?
> - **Paso 5: Seguridad.** ¿Cómo protege Contoso la implementación híbrida o de Azure?
> - **Paso 6: Gobernanza.** ¿Cómo mantiene Contoso alineada la implementación con los requisitos de seguridad y gobernanza?

## <a name="before-you-start"></a>Antes de comenzar

Antes de empezar a trabajar con la infraestructura, debe leer información básica acerca de las capacidades de Azure que se explican en este artículo:

- Hay varias opciones disponibles para adquirir acceso a Azure, entre las que se incluyen: Pago por uso, Contratos Enterprise y licencias Open de revendedores de Microsoft o de asociados de Microsoft, también conocidos como proveedores de soluciones en la nube (CSP). Obtenga información acerca de las [opciones de compra](https://azure.microsoft.com/pricing/purchase-options) y sobre cómo [se organizan las suscripciones a Azure](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise).
- Obtenga información general acerca de la [administración de identidades y acceso](https://www.microsoft.com/trustcenter/security/identity) de Azure. En concreto, obtenga información sobre [Azure AD y la ampliación de la instancia de Active Directory local a la nube](https://docs.microsoft.com/azure/active-directory/identity-fundamentals). Tiene a su disposición un libro electrónico descargable acerca de la [administración de identidades y acceso (IAM) en un entorno híbrido](https://azure.microsoft.com/resources/hybrid-cloud-identity) que le resultará muy útil.
- Azure ofrece una sólida infraestructura de red con opciones para conectividad híbrida. Obtenga información general acerca de las [redes y el control de acceso de red](https://docs.microsoft.com/azure/security/security-network-overview).
- Obtenga una introducción a [Azure Security](https://docs.microsoft.com/azure/security/azure-security) y consiga información acerca de cómo crear un plan de [gobernanza](https://docs.microsoft.com/azure/security/governance-in-azure).

## <a name="on-premises-architecture"></a>Arquitectura local

Aquí se muestra un diagrama de la infraestructura local de Contoso en la actualidad.

 ![Arquitectura de Contoso](./media/contoso-migration-infrastructure/contoso-architecture.png)

- Contoso tiene un centro de datos principal situado en la ciudad de Nueva York, al este de los Estados Unidos.
- Asimismo, tiene tres sucursales locales más en los Estados Unidos.
- El centro de datos principal está conectado a Internet con una conexión Metro Ethernet de fibra (500 Mbps).
- Cada una de las sucursales está conectada localmente a Internet con conexiones de categoría empresarial, y con túneles VPN con IPSec hacia el centro de datos principal. Esto permite que toda la red esté conectada de forma permanente, así como optimizar la conectividad a Internet.
- El centro de datos principal está completamente virtualizado con VMware. Contoso tiene dos hosts de virtualización de ESXi 6.5, que administra vCenter Server 6.5.
- Contoso usa Active Directory para la administración de identidades y servidores DNS en la red interna.
- Los controladores de dominio del centro de datos se ejecutan en VM de VMware. Los controladores de dominio de las sucursales locales se ejecutan en servidores físicos.

## <a name="step-1-buy-and-subscribe-to-azure"></a>Paso 1: Compra y suscripción a Azure

Contoso debe averiguar cómo comprar Azure, cómo diseñar las suscripciones y cómo conceder bajo licencia servicios y recursos.

### <a name="buy-azure"></a>Comprar Azure

Contoso va a elegir un [contrato Enterprise (EA)](https://azure.microsoft.com/pricing/enterprise-agreement). Esto implica un compromiso monetario inicial con Azure, que da derecho a Contoso a disfrutar de grandes ventajas, incluidas opciones de facturación flexibles y precios optimizados.

- Contoso hizo una estimación de lo que se gastará anualmente en Azure. Cuando firmó el acuerdo, pagó por el primer año en su totalidad.
- Contoso debe usar todo lo que tiene asignado antes de que finalice el año, o perderá el valor de ese dinero.
- Si por algún motivo Contoso supera su asignación y gasta más, Microsoft le facturará la diferencia.
- Los gastos por encima de la asignación se facturarán con las mismas tarifas que las del contrato de Contoso. No hay penalizaciones por excederse.

### <a name="manage-subscriptions"></a>Administrar suscripciones

Después de pagar Azure, Contoso debe averiguar cómo administrar las suscripciones de Azure. Contoso tiene un EA y, por tanto, no hay límite en el número de suscripciones a Azure que puede configurar.

- Una inscripción Azure Enterprise define cómo una empresa da forma y usa los servicios de Azure y cómo define una estructura de gobernanza básica.
- Como primer paso, Contoso ha definido una estructura (conocida como un scaffold empresarial para la inscripción Enterprise). Usó [este artículo](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-subscription-governance) para comprender y diseñar un scaffold.
- Por ahora, Contoso ha decidido usar un enfoque funcional para administrar sus suscripciones.
  - Dentro de la empresa, tendrá un solo departamento de TI que controlará el presupuesto de Azure. Este es el único grupo con suscripciones.
  - En el futuro, Contoso podrá ampliar este modelo para que otros grupos corporativos puedan unirse como departamentos en la inscripción Enterprise.
  - Dentro del departamento de TI, Contoso ha estructurado dos suscripciones: una de desarrollo y otra de producción.
  - Si Contoso requiere suscripciones adicionales en el futuro, deberá administrar el acceso, las directivas y el cumplimiento de las suscripciones. Para ello, introducirá [grupos de administración de Azure](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview), como un nivel adicional por encima de las suscripciones.

  ![Estructura de la empresa](./media/contoso-migration-infrastructure/enterprise-structure.png)

### <a name="examine-licensing"></a>Examinar la concesión de licencias

Con las suscripciones configuradas, Contoso puede consultar sus licencias de Microsoft. Su estrategia de licencias dependerá de los recursos que quiera migrar a Azure y de cómo se seleccionan e implementan los servicios y máquinas virtuales de Azure.

#### <a name="azure-hybrid-benefit"></a>Ventaja híbrida de Azure

Al implementar VM en Azure, las imágenes estándar incluyen una licencia que se le cobrará a Contoso por minuto en función del software que se está usando. Pero Contoso ha sido un cliente de Microsoft a largo plazo y ha mantenido los contratos Enterprise y las licencias Open con Software Assurance (SA).

Ventaja híbrida de Azure proporciona un método rentable para la migración de Contoso, que le permite ahorrar en máquinas virtuales de Azure y cargas de trabajo de SQL Server mediante la conversión o la reutilización de Windows Server Datacenter o licencias Standard Edition que cubre Software Assurance. Esto permitirá que Contoso pague una tarifa de proceso más baja por las máquinas virtuales y SQL Server. [Más información](https://azure.microsoft.com/pricing/hybrid-benefit).

#### <a name="license-mobility"></a>Movilidad de licencias

Movilidad de licencias a través de Software Assurance ofrece a los clientes del Programa de licencias por volumen de Microsoft, como Contoso, la flexibilidad de implementar las aplicaciones de servidor aptas, con una instancia activa de Software Assurance en Azure. Esto elimina la necesidad de adquirir licencias nuevas. Sin costos asociados a movilidad, las licencias existentes se pueden implementar fácilmente en Azure. [Más información](https://azure.microsoft.com/pricing/license-mobility).

#### <a name="reserve-instances-for-predictable-workloads"></a>Instancias de reserva para cargas de trabajo previsibles

Las cargas de trabajo previsibles son las que siempre deben estar disponibles con VM en ejecución. Por ejemplo, las aplicaciones de línea de negocio como un sistema SAP ERP. Por otro lado, las cargas de trabajo impredecibles son las que son variables, como las máquinas virtuales que están encendidas durante los períodos de alta demanda y apagadas cuando la demanda es baja.

![Instancia reservada](./media/contoso-migration-infrastructure/reserved-instance.png)

A cambio de usar instancias reservadas en instancias específicas de VM que Contoso sabe que necesitan mantenimiento durante largos períodos de tiempo, puede obtener un descuento y una capacidad prioritaria. Al usar [Azure Reserved Instances](https://azure.microsoft.com/pricing/reserved-vm-instances) junto con la Ventaja de híbrida de Azure, Contoso puede ahorrarse hasta un 82 % del precio de pago por uso (abril de 2018).

## <a name="step-2-manage-hybrid-identity"></a>Paso 2: Administración de identidad híbrida

Otorgar y controlar el acceso de los usuarios a los recursos de Azure con la gestión de identidades y accesos (IAM) es un paso importante para unir la infraestructura de Azure.

- Contoso decide extender su instancia de Active Directory local a la nube, en lugar de crear un nuevo sistema independiente en Azure.
- Para hacer esto, crea una instancia de Active Directory basada en Azure.
- Contoso no dispone de Office 365, por lo que necesita aprovisionar una nueva instancia de Azure AD.
- Office 365 usa Azure AD para la administración de usuarios. Si Contoso usara Office 365, ya dispondría de un inquilino de Azure AD y podría usarlo como la entidad principal.
- [Obtenga más información](https://support.office.com/article/understanding-office-365-identity-and-azure-active-directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9) sobre Azure AD para Office 365 y vea [cómo agregar una suscripción](https://docs.microsoft.com/azure/active-directory/active-directory-how-subscriptions-associated-directory) a un inquilino de Azure AD existente.

### <a name="create-an-azure-ad"></a>Crear una instancia de Azure AD

Contoso usa la edición Azure AD Free que se incluye con una suscripción a Azure. Los administradores de Contoso configuran un directorio como sigue:

1. En [Azure Portal](https://portal.azure.com), van a **Crear un recurso** > **Identidad** > **Azure Active Directory**.
2. En **Crear directorio**, deberá especificarse un nombre para el directorio, un nombre de dominio inicial y la región en la que se debe crear el directorio de Azure AD.

    ![Crear una instancia de Azure AD](./media/contoso-migration-infrastructure/azure-ad-create.png)

    > [!NOTE]
    > El directorio creado tendrá un nombre de dominio inicial con el formato **nombrededominio.onmicrosoft.com**. Este nombre no se podrá modificar ni eliminar. En su lugar, deberán agregar su nombre de dominio registrado en Azure AD.

### <a name="add-the-domain-name"></a>Agregar el nombre del dominio

Para usar su nombre de dominio estándar, los administradores de Contoso tienen que agregarlo como nombre de dominio personalizado a Azure AD. Esta opción permite a los administradores asignar nombres de usuario conocidos. Por ejemplo, un usuario puede iniciar sesión con la dirección de correo electrónico billg@contoso.com, en lugar de necesitar billg@contosomigration.microsoft.com.

Para configurar un nombre de dominio personalizado, este se agrega al directorio, se agrega una entrada DNS y luego se comprueba el nombre en Azure AD.

1. En **Nombres de dominio personalizado** > **Agregar dominio personalizado**, Contoso agrega el dominio.
2. Para utilizar una entrada DNS en Azure, es necesario registrarla con el registrador de dominios.

    - En la lista **Nombres de dominio personalizado**, se tiene en cuenta la información de DNS para el nombre. Se usa una entrada MX.
    - Es necesario acceder al servidor de nombres para hacer esto. Iniciaron sesión en el dominio Contoso.com y crearon un nuevo registro MX para la entrada DNS proporcionada por Azure AD, mediante el uso de los detalles indicados.

3. Una vez propagados los registros DNS, en el nombre de los detalles del dominio, se selecciona **Comprobar** para comprobar el nombre de dominio personalizado.

     ![DNS de Azure AD](./media/contoso-migration-infrastructure/azure-ad-dns.png)

### <a name="set-up-on-premises-and-azure-groups-and-users"></a>Configurar usuarios y grupos de Azure y locales

Ahora que Azure AD ya está en funcionamiento, los administradores de Contoso deben agregar empleados a grupos de Active Directory locales que se sincronizarán con Azure Active Directory. Es recomendable que usen nombres de grupos locales que coincidan con los nombres de los grupos de recursos de Azure. Esto hace más fácil identificar las coincidencias con fines de sincronización.

#### <a name="create-resource-groups-in-azure"></a>Crear grupos de recursos en Azure

Los grupos de recursos de Azure recopilan los recursos de Azure. Usar un identificador de grupo de recursos permite que Azure realice operaciones en los recursos del grupo.

- Una suscripción a Azure puede tener varios grupos de recursos, pero un grupo de recursos solo puede existir en una única suscripción.
- Además, un único grupo de recursos puede tener varios recursos, pero un recurso solo puede pertenecer a un único grupo de recursos.

Los administradores de Contoso configuran los grupos de recursos de Azure tal como se resume en la tabla siguiente.

<!-- markdownlint-disable MD033 -->

**Grupos de recursos** | **Detalles**
--- | ---
**ContosoCobRG** | Este grupo contiene todos los recursos relacionados con la continuidad de negocio (COB). Aquí se incluyen los almacenes que Contoso usará para los servicios Azure Site Recovery y Azure Backup.<br/><br/> También se incluyen los recursos que se usaron para la migración, incluidos Azure Migrate y Azure Database Migration Service.
**ContosoDevRG** | Este grupo contiene los recursos de desarrollo y pruebas.
**ContosoFailoverRG** | Este grupo actúa como una zona de aterrizaje para los recursos conmutados por error.
**ContosoNetworkingRG** | Este grupo contiene todos los recursos de red.
**ContosoRG** | Este grupo contiene recursos relacionados con las bases de datos y aplicaciones de producción.

<!-- markdownlint-disable MD026 -->

Contoso crea los grupos de recursos de la siguiente manera:

1. En Azure Portal > **Grupos de recursos**, agrega un grupo.
2. Para cada grupo especifica un nombre, la suscripción a la que pertenece el grupo y la región.
3. Los grupos de recursos aparecen en la lista **Grupos de recursos**.

    ![Grupos de recursos](./media/contoso-migration-infrastructure/resource-groups.png)

##### <a name="scaling-resource-groups"></a>Escalado de grupos de recursos

En el futuro, Contoso agregará otros grupos de recursos según las necesidades. Por ejemplo, podrían definir un grupo de recursos para cada aplicación o servicio, para que se pueden administrar y proteger de forma independiente.

#### <a name="create-matching-security-groups-on-premises"></a>Crear grupos de seguridad coincidentes locales

1. En la instancia de Active Directory local, los administradores de Contoso configurarán los grupos de seguridad con nombres que coincidan con los nombres de los grupos de recursos de Azure.

    ![Grupos de seguridad de Active Directory locales](./media/contoso-migration-infrastructure/on-prem-ad.png)

2. Para fines de administración, se crea un grupo adicional que se agregará a todos los demás grupos. Este grupo tendrá derechos para todos los grupos de recursos de Azure. A este grupo se agregará un número ilimitado de administradores.

### <a name="synchronize-active-directory"></a>Sincronización de Active Directory

Contoso quiere proporcionar una identidad común para obtener acceso a los recursos locales y en la nube. Para ello, integrará su instancia de Active Directory local con Azure AD. Con este modelo:

- Los usuarios y las organizaciones pueden aprovechar las ventajas de una identidad única para obtener acceso a aplicaciones locales y a servicios como Office 365 y miles sitios más en Internet.
- Los administradores pueden usar los grupos de Active Directory para implementar el [Control de acceso basado en roles (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) en Azure.

Para facilitar la integración, Contoso usa la [herramienta Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect). Al instalar y configurar la herramienta en un controlador de dominio, se sincronizan las identidades locales de Active Directory en la instancia local de Active Directory.

### <a name="download-the-tool"></a>Descargar la herramienta

1. En Azure Portal, los administradores de Contoso van a **Azure Active Directory** > **Azure AD Connect** y descargan la versión más reciente de la herramienta en el servidor que se usa para la sincronización.

    ![Descarga de Azure AD Connect](./media/contoso-migration-infrastructure/download-ad-connect.png)

2. Se inicia la instalación de **AzureADConnect.msi** con **Usar la configuración rápida**. Se trata de la instalación más habitual y puede utilizarse para una topología de bosque único con sincronización de hash de contraseñas para la autenticación.

    ![Asistente para Azure AD Connect](./media/contoso-migration-infrastructure/ad-connect-wiz1.png)

3. En **Conectar con Azure AD**, se especifican las credenciales para conectarse a Azure AD (con el formato admin@contoso.com o admin@contoso.onmicrosoft.com).

    ![Asistente para Azure AD Connect](./media/contoso-migration-infrastructure/ad-connect-wiz2.png)

4. En **Conectar con AD DS**, se especifican las credenciales para la instancia local de Active Directory (con el formato CONTOSO\admin o contoso.com\admin).

     ![Asistente para Azure AD Connect](./media/contoso-migration-infrastructure/ad-connect-wiz3.png)

5. En **Listo para configurar**, se selecciona **Start the synchronization process when configuration completes** (Iniciar el proceso de sincronización cuando finalice la configuración) para iniciar de inmediato la sincronización. A continuación, se realiza la instalación.

Observe lo siguiente:

- Contoso tiene una conexión directa con Azure. Si su instancia local de Active Directory está detrás de un proxy, lea este [artículo](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-troubleshoot-connectivity).

- Después de la primera sincronización, los objetos locales de Active Directory están visibles en el directorio de Azure AD.

    ![Instancia local de Active Directory en Azure](./media/contoso-migration-infrastructure/on-prem-ad-groups.png)

- El equipo de TI de Contoso se representa en cada grupo según su rol.

    ![Miembros locales de Active Directory en Azure](./media/contoso-migration-infrastructure/on-prem-ad-group-members.png)

### <a name="set-up-rbac"></a>Configurar RBAC

El [control de acceso basado en roles (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) de Azure permite realizar una administración detallada del acceso para Azure. Con RBAC, puede conceder únicamente el grado de acceso que los usuarios necesiten para realizar sus tareas. Asigne el rol RBAC adecuado a los usuarios, grupos y aplicaciones en un nivel de ámbito. El ámbito de una asignación de roles puede ser una suscripción, un grupo de recursos o un único recurso.

Los administradores de Contoso ahora asignan roles a los grupos de Active Directory que sincronizan desde el entorno local.

1. En el grupo de recursos **ControlCobRG**, seleccione **Control de acceso (IAM)**  > **Agregar asignación de roles**.
2. En **Agregar asignación de roles** > **Rol** > **Colaborador,**  se selecciona el grupo **ContosoCobRG** de la lista. El grupo aparece entonces en la lista **Miembros seleccionados**.
3. Esto se repite con los mismos permisos para otros grupos de recursos (excepto para **ContosoAzureAdmins**), mediante la adición de los permisos de colaborador a la cuenta que coincide con el grupo de recursos.
4. Para el grupo **ContosoAzureAdmins**, se asigna el rol **Propietario**.

    ![Miembros locales de Active Directory en Azure](./media/contoso-migration-infrastructure/on-prem-ad-groups.png)

## <a name="step-3-design-for-resiliency"></a>Paso 3: Diseño para lograr resistencia

### <a name="set-up-regions"></a>Configuración de regiones

Los recursos de Azure se implementan en las regiones.

- Las regiones se organizan por zonas geográficas y, los requisitos de residencia, soberanía, cumplimiento normativo y resistencia de los datos se cumplen dentro de los límites geográficos.
- Una región se compone de un conjunto de centros de datos. Estos centros de datos se implementan dentro de un perímetro que define la latencia y se conectan a través de una red regional dedicada de baja latencia.
- Cada región de Azure se empareja con una región diferente para proporcionar resistencia.
- Obtenga información acerca de las [regiones de Azure](https://azure.microsoft.com/global-infrastructure/regions) para comprender [cómo están emparejadas](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

Contoso ha decidido que su región primaria sea Este de EE. UU. 2 (que se encuentra en Virginia) y su región secundaria, Centro de EE. UU. (que se encuentra en Iowa). Hay un par de razones para esto:

- El centro de datos de Contoso se encuentra en Nueva York, y Contoso consideró la latencia en función de del centro de datos más cercano.
- La región Este de EE. UU. 2 tiene todos los servicios y productos que Contoso necesita. No todas las regiones de Azure son iguales en cuanto a los productos y servicios disponibles. Puede consultar los [productos de Azure según la región](https://azure.microsoft.com/global-infrastructure/services).
- El Centro de EE. UU. es la región de Azure emparejada para Este de EE. UU. 2.

Cuando piensa en su entorno híbrido, Contoso debe considerar cómo compilar una estrategia de recuperación ante desastres y de resistencia en su diseño de la región. En términos generales, las estrategias van desde una implementación en una única región, que se basa en las características de la plataforma Azure, como dominios de error y emparejamiento regional de resistencia, hasta un modelo completamente activo en el que los servicios en la nube y la base de datos se implementan y ofrecen mantenimiento a los usuarios de dos regiones.

Contoso ha decidido tomar un camino intermedio. Implementará sus aplicaciones y recursos en una región principal y mantendrá una copia completa de la infraestructura en la región secundaria, para que esté lista para actuar como copia de seguridad completa en caso de un desastre total en la aplicación o de un error en la región.

### <a name="set-up-availability"></a>Configuración de la disponibilidad

**Conjuntos de disponibilidad:**

los conjuntos de disponibilidad ayudan a proteger a las aplicaciones y los datos frente a una interrupción de la red o hardware local dentro de un centro de datos.

- Los conjuntos de disponibilidad distribuyen las máquinas virtuales de Azure entre distinto hardware físico dentro de un centro de datos.
- Los dominios de error representan el hardware subyacente con una fuente de alimentación común y un conmutador de red dentro del centro de datos. Las máquinas virtuales de un conjunto de disponibilidad están distribuidas entre distintos dominios de error para minimizar las interrupciones provocadas por un solo error de la red o de hardware.
- Los dominios de actualización representan hardware subyacente que puede someterse a mantenimiento o reiniciarse al mismo tiempo. Los conjuntos de disponibilidad también distribuyen las máquinas virtuales entre varios dominios de actualización para garantizar que al menos habrá una instancia en ejecución en todo momento.

Contoso implementará los conjuntos de disponibilidad cada vez que las cargas de trabajo de VM requieran alta disponibilidad. [Más información](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability).

**Zonas de disponibilidad:**

las zonas de disponibilidad ayudan a proteger las aplicaciones y los datos frente a errores que afectan a todo un centro de datos dentro de una región.

- Cada zona de disponibilidad representa una ubicación física exclusiva dentro de una región de Azure.
- Cada zona de disponibilidad consta de uno o varios centros de datos equipados con alimentación, refrigeración y redes independientes.
- Hay tres zonas independientes como mínimo en todas las regiones habilitadas.
- La separación física de las zonas dentro de una región protege las aplicaciones y los datos frente a los errores del centro de datos.

Contoso implementará zonas de disponibilidad a medida que las aplicaciones requieran escalabilidad, alta disponibilidad y resistencia. [Más información](https://docs.microsoft.com/azure/availability-zones/az-overview).

### <a name="set-up-backup"></a>Configuración de copias de seguridad

**Azure Backup:**

Azure Backup permite crear copias de seguridad de discos de máquinas virtuales de Azure y restaurarlos.

- Azure Backup permite crear copias de seguridad automatizadas de imágenes de discos de VM, almacenadas en Azure Storage.
- Las copias de seguridad son coherentes con la aplicación, lo que garantiza que los datos con copia de seguridad son transaccionalmente coherentes y que las aplicaciones arrancarán después de la restauración.
- Azure Backup admite el almacenamiento con redundancia local (LRS) para replicar varias copias de los datos de copia de seguridad dentro de un centro de datos, en caso de un error de hardware local.
- En el evento de una interrupción regional, Azure Backup también admite el almacenamiento con redundancia geográfica (GRS), que replica los datos de copia de seguridad en una región secundaria emparejada.
- Azure Backup cifra los datos en tránsito mediante AES 256. Los datos en reposo de los que se ha realizado una copia de seguridad se cifran con [Storage Service Encryption (SSE)](https://docs.microsoft.com/azure/storage/common/storage-service-encryption?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).

Contoso usará Azure Backup con GRS en todas las máquinas virtuales de producción para garantizar que se creen copias de seguridad de los datos de cargas de trabajo y que se puedan restaurar rápidamente en caso de error o de cualquier otra interrupción. [Más información](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup).

### <a name="set-up-disaster-recovery"></a>Configuración de la recuperación ante desastres

**Azure Site Recovery:**

Azure Site Recovery ayuda a garantizar la continuidad empresarial manteniendo las aplicaciones y cargas de trabajo empresariales en funcionamiento durante las interrupciones regionales.

- Azure Site Recovery replica de manera continua las máquinas virtuales de Azure desde una región primaria a una secundaria, lo que garantiza que habrá copias funcionales en ambas ubicaciones.
- En caso de que se produzca una interrupción en la región primaria, la aplicación o el servicio conmutará por error para usar instancias de máquinas virtuales replicadas en la región secundaria, lo que minimiza la posible interrupción.
- Cuando las operaciones vuelven a la normalidad, las aplicaciones o servicios pueden conmutar por recuperación en las máquinas virtuales de la región primaria.

Contoso implementará Azure Site Recovery para todas las máquinas virtuales de producción que se usan en cargas de trabajo críticas, lo que garantiza una interrupción mínima durante un corte en la región primaria. [Más información](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)

## <a name="step-4-design-a-network-infrastructure"></a>Paso 4: Diseño de una infraestructura de red

Con el diseño de la región establecido, Contoso está listo para considerar una estrategia en la red. Debe pensar en cómo se conectan y comunican entre sí el centro de datos local y Azure, y cómo diseñar la infraestructura de red en Azure. En concreto, Contoso debe:

- **Planear la conectividad de red híbrida**: averiguar cómo van a conectarse las redes entre las instancias locales y Azure.
- **Diseñar una infraestructura de red de Azure**: decidir cómo implementar las redes en las regiones. Cómo se comunicarán las redes dentro de la misma región y entre las diferentes regiones.
- **Diseñar y configurar redes de Azure**: configurar redes y subredes de Azure, y decidir qué residirá en cada una.

### <a name="plan-hybrid-network-connectivity"></a>Planear conectividad de red híbrida

Contoso consideró un determinado [número de arquitecturas](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking) para las redes híbridas entre Azure y su centro de datos local. [Obtenga más información](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/considerations) acerca de la comparación de opciones.

Como recordatorio, la infraestructura de red local de Contoso está formada por su centro de datos de Nueva York y sucursales locales en la parte oriental de Estados Unidos. Todas las ubicaciones tienen una conexión de clase empresarial a Internet. Cada una de las sucursales está conectada al centro de datos a través de un túnel VPN con IPSec a través de Internet.

![Red de Contoso](./media/contoso-migration-infrastructure/contoso-networking.png)

Aquí se muestra cómo Contoso decidió implementar conectividad híbrida:

1. Configurar una nueva conexión VPN de sitio a sitio entre el centro de datos de Contoso en Nueva York y las dos regiones de Azure: Este de EE. UU. 2 y Centro de EE. UU.
2. El tráfico de las sucursales con destino a las redes virtuales de Azure se dirigirá a través del centro de datos principal de Contoso.
3. Al escalar verticalmente la implementación de Azure, Contoso establecerá una conexión de ExpressRoute entre su centro de datos y las regiones de Azure. Cuando esto suceda, Contoso podrá conservar la conexión VPN de sitio a sitio únicamente con fines de conmutación por error.
    - [Obtener más información](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/considerations) acerca de cómo elegir entre una solución híbrida ExpressRoute y VPN.
    - Comprobar el [soporte y las ubicaciones de ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-locations-providers).

**Solo VPN:**

![VPN de Contoso](./media/contoso-migration-infrastructure/hybrid-vpn.png)

**VPN y ExpressRoute:**

![VPN/ExpressRoute de Contoso](./media/contoso-migration-infrastructure/hybrid-vpn-expressroute.png)

### <a name="design-the-azure-network-infrastructure"></a>Diseño de la infraestructura de red de Azure

Es fundamental que Contoso cree redes de forma que su implementación híbrida sea segura y escalable. Para ello, Contoso adoptará un enfoque a largo plazo y diseñará redes virtuales resistentes y listas para la empresa. [Obtener más información](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm) acerca de cómo planear las redes virtuales.

Para conectar sus dos regiones, Contoso ha decidido implementar un modelo de red de concentrador a concentrador:

- En cada región, Contoso utilizará un modelo radial.
- Para conectar redes y concentradores, Contoso usará el emparejamiento de redes de Azure.

#### <a name="network-peering"></a>Emparejamiento de redes

Azure proporciona la opción de emparejamiento de redes para conectar redes virtuales y concentradores. El emparejamiento global permite realizar conexiones entre redes virtuales y los concentradores de regiones diferentes. El emparejamiento local conecta redes virtuales en la misma región. El emparejamiento de VNet proporciona varias ventajas:

- El tráfico de red entre redes virtuales emparejadas es privado.
- El tráfico entre redes virtuales se mantiene en la red troncal de Microsoft. No se requiere ninguna red pública de Internet, puertas de enlace ni cifrado en la comunicación entre redes virtuales.
- El emparejamiento proporciona una conexión predeterminada de gran ancho de banda y baja latencia entre los diferentes recursos de las redes virtuales.

[Obtener más información](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) acerca del emparejamiento de redes.

#### <a name="hub-to-hub-across-regions"></a>Conexiones concentrador a concentrador entre regiones

Contoso implementará un concentrador en cada región. Un concentrador es una red virtual (VNet) en Azure que actúa como punto central de conectividad para la red local. Las redes virtuales del concentrador se conectarán entre sí con el emparejamiento de VNet global. El emparejamiento de VNet global conecta las redes virtuales entre las regiones de Azure.

- El concentrador de cada región está emparejado a su concentrador asociado en la otra región.
- El concentrador está emparejado a todas las redes de la región y puede conectarse a todos los recursos de red.

    ![Emparejamiento global](./media/contoso-migration-infrastructure/global-peering.png)

#### <a name="hub-and-spoke-model-within-a-region"></a>Modelo radial dentro de una región

Dentro de cada región, Contoso implementará las redes virtuales para propósitos diferentes, como redes de radio desde el concentrador de la región. Las redes virtuales de una región usan la opción de emparejamiento para conectarse a su concentrador y entre sí.

#### <a name="design-the-hub-network"></a>Diseño de la red del concentrador

En el modelo de concentrador y radio que Contoso ha elegido, es necesario pensar en cómo se enrutará el tráfico del centro de datos local y de Internet. Le mostramos cómo Contoso decidió controlar el enrutamiento para los concentradores del Este de EE. UU. 2 y Centro de EE. UU.:

- Diseñará una red denominada "reverse c", como sucede con la ruta de acceso que siguen los paquetes desde la red de entrada a la de salida.
- Su arquitectura de red tiene dos límites, una zona de confianza perimetral front-end y una zona de confianza de back-end.
- Un firewall tendrá un adaptador de red en cada zona, para controlar el acceso a zonas de confianza.
- Desde Internet:
  - El tráfico de Internet alcanzará una dirección IP pública de carga equilibrada en la red perimetral.
  - Este tráfico se enruta a través del firewall y está sujeto a las reglas de firewall.
  - Después de implementar los controles de acceso de red, el tráfico se reenviará a la ubicación adecuada en la zona de confianza.
  - El tráfico saliente de la red virtual se enrutará a Internet mediante rutas definidas por el usuario. El tráfico se fuerza a través del firewall y se inspecciona en consonancia con las directivas de Contoso.
- Desde el centro de datos de Contoso:
  - El tráfico entrante a través del VPN de sitio a sitio (o ExpressRoute) alcanza la dirección IP pública de la puerta de enlace del VPN de Azure.
  - Este tráfico se enruta a través del firewall y está sujeto a las reglas de firewall.
  - Después de aplicar las reglas de firewall, el tráfico se reenvía a un equilibrador de carga interno (SKU estándar) en la subred de la zona interna de confianza.
  - El tráfico saliente de la subred de confianza que va al centro de datos local a través de VPN, se enruta a través del firewall, y se aplican las reglas, antes de pasar por la conexión de VPN de sitio a sitio.

### <a name="design-and-set-up-azure-networks"></a>Diseño y configuración de redes de Azure

Con una red y una topología de enrutamiento, Contoso está preparado para configurar sus redes y subredes de Azure.

- Contoso implementará una red privada de clase A en Azure (0.0.0.0 a 127.255.255.255). Esta es una buena opción, ya que en las instalaciones locales hay un espacio de direcciones privado de Clase B 172.160.0/16, por lo que Contoso puede estar seguro de que no habrá ninguna superposición entre los rangos de direcciones.
- Se implementarán redes virtuales en sus regiones primarias y secundarias.
- Contoso usará una convención de nomenclatura que incluye el prefijo **VNET** y la abreviatura de región **EUS2** o **CUS**. Con esta norma, las redes del concentrador se denominarán **VNET-HUB-EUS2** (Este de EE. UU. 2) y **VNET-HUB-CUS** (Centro de EE. UU.).
- Contoso no tiene ninguna [solución IPAM](https://docs.microsoft.com/windows-server/networking/technologies/ipam/ipam-top), por lo que es necesario planear el enrutamiento de red sin NAT.

#### <a name="virtual-networks-in-east-us-2"></a>Redes virtuales de Este de EE. UU. 2

El Este de EE. UU. 2 es la región principal que Contoso usará para implementar servicios y recursos de Contoso. Así es como Contoso diseñará sus redes:

- **Centro:** la red virtual del concentrador del Este de EE. UU. 2 es el punto de conectividad central con el centro de datos local.
- **Redes virtuales:** las redes virtuales de radios del Este de EE. UU. 2 pueden usarse para aislar las cargas de trabajo si fuera necesario. Además de la red virtual del concentrador, Contoso tendrá dos redes virtuales de radios en el Este de EE. UU. 2:
  - **VNET-DEV-EUS2**. Esta red virtual proporcionará al equipo de desarrollo y pruebas una red completamente funcional para proyectos de desarrollo. Actuará como una zona piloto de producción y dependerá de la infraestructura de producción para su funcionamiento.
    - **VNET-PROD-EUS2**. los componentes de producción de IaaS de Azure se encontrarán en esta red.
  - Cada red virtual tendrá su propio espacio de dirección única, sin superposiciones. Contoso intenta configurar el enrutamiento sin necesidad de NAT.
- **Subredes:**
  - Habrá una subred en cada red para cada nivel de aplicación
  - Cada subred de la red de producción tendrá una subred coincidente en la red virtual de desarrollo.
  - Además, la red de producción tiene una subred para controladores de dominio.

Las redes virtuales del Este de EE. UU. 2 se resumen en la tabla siguiente.

**Red virtual** | **Range** | **Peer**
--- | --- | ---
**VNET-HUB-EUS2** | 10.240.0.0/20 | VNET-HUB-CUS2, VNET-DEV-EUS2, VNET-PROD-EUS2
**VNET-HUB-EUS2** | 10.245.16.0/20 | VNET-HUB-EUS2
**VNET-PROD-EUS2** | 10.245.32.0/20 | VNET-HUB-EUS2, VNET-PROD-CUS

![Modelo radial en la región primaria](./media/contoso-migration-infrastructure/primary-hub-peer.png)

#### <a name="subnets-in-the-east-us-2-hub-network-vnet-hub-eus2"></a>Subredes de la red del concentrador del Este de EE. UU. 2 (VNET-DEV-EUS2)

**Subred/zona** | **CIDR** | **Direcciones IP que se pueden usar
--- | --- | ---
**IB-UntrustZone** | 10.240.0.0/24 | 251
**IB-TrustZone** | 10.240.1.0/24 | 251
**OB-UntrustZone** | 10.240.2.0/24 | 251
**OB-TrustZone** | 10.240.3.0/24 | 251
**GatewaySubnets** | 10.240.10.0/24 | 251

#### <a name="subnets-in-the-east-us-2-dev-network-vnet-dev-eus2"></a>Subredes de la red de desarrollo del Este de EE. UU. 2 (VNET-DEV-EUS2)

El equipo de desarrollo usa la red virtual de desarrollo como zona piloto de producción. Tiene tres subredes.

**Subred** | **CIDR** | **Direcciones** | **En la subred**
--- | --- | --- | ---
**DEV-FE-EUS2** | 10.245.16.0/22 | 1019 | Máquinas virtuales de nivel web/servidores front-end
**DEV-APP-EUS2** | 10.245.20.0/22 | 1019 | Máquinas virtuales de nivel de aplicación
**DEV-APP-EUS2** | 10.245.24.0/23 | 507 | VM de base de datos

#### <a name="subnets-in-the-east-us-2-production-network-vnet-prod-eus2"></a>Subredes de la red de producción del Este de EE. UU. 2 (VNET-PROD-EUS2)

Los componentes de IaaS de Azure se encuentran en la red de producción. Cada nivel de aplicación tiene su propia subred. Las subredes coinciden con las de la red de desarrollo, con la adición de una subred para los controladores de dominio.

**Subred** | **CIDR** | **Direcciones** | **En la subred**
--- | --- | --- | ---
**PROD-FE-EUS2** | 10.245.32.0/22 | 1019 | Máquinas virtuales de nivel web/servidores front-end
**PROD-FE-EUS2** | 10.245.36.0/22 | 1019 | Máquinas virtuales de nivel de aplicación
**PROD-FE-EUS2** | 10.245.40.0/23 | 507 | VM de base de datos
**PROD-DC-EUS2** | 10.245.42.0/24 | 251 | VM del controlador de dominio

![Arquitectura de red del concentrador](./media/contoso-migration-infrastructure/azure-networks-eus2.png)

#### <a name="virtual-networks-in-central-us-secondary-region"></a>Redes virtuales de Centro de EE. UU. (región secundaria)

El Centro de EE. UU. es la región secundaria de Contoso. Así es como Contoso diseñará sus redes:

- **Centro:** la red virtual del concentrador del Este de EE. UU. 2 es el punto central de conectividad con el centro de datos local, y las redes virtuales de radios del Este de EE. UU. 2 pueden usarse para aislar las cargas de trabajo, si es necesario, y se administran por separado de otros radios.
- **Redes virtuales:** Contoso tendrá dos redes virtuales en el Centro de EE. UU.:
  - VNET-PROD-CUS. Esta red virtual es una red de producción, similar a VNET-PROD_EUS2.
  - VNET-ASR-CUS. Esta red virtual actuará como una ubicación en la que las VM se crean después de la conmutación por error desde el entorno local, o como una ubicación para las VM de Azure que se conmuten por error desde el servidor principal en la región secundaria. Esta red es similar a las redes de producción, pero sin ningún controlador de dominio.
  - Cada red virtual de la región tendrá su propio espacio de dirección, sin superposición. Contoso configurará el enrutamiento sin NAT.
- **Subredes:** as subredes se diseñarán de una manera similar a las del Este de EE. UU. 2. La excepción es que Contoso no se necesita ninguna subred para los controladores de dominio.

Las redes virtuales del Centro de EE. UU. se resumen en la tabla siguiente.

**Red virtual** | **Range** | **Peer**
--- | --- | ---
**VNET-HUB-CUS** | 10.250.0.0/20 | VNET-HUB-EUS2, VNET-ASR-CUS, VNET-PROD-CUS
**VNET-ASR-CUS** | 10.255.16.0/20 | VNET-HUB-CUS, VNET-PROD-CUS
**VNET-PROD-CUS** | 10.255.32.0/20 | VNET-HUB-CUS, VNET-ASR-CUS, VNET-PROD-EUS2

![Modelo radial en una región emparejada](./media/contoso-migration-infrastructure/paired-hub-peer.png)

#### <a name="subnets-in-the-central-us-hub-network-vnet-hub-cus"></a>Subredes de la red del concentrador del Centro de EE. UU. (VNET-HUB-CUS)

**Subred** | **CIDR** | **Direcciones IP que se pueden usar**
--- | --- | ---
**IB-UntrustZone** | 10.250.0.0/24 | 251
**IB-TrustZone** | 10.250.1.0/24 | 251
**OB-UntrustZone** | 10.250.2.0/24 | 251
**OB-TrustZone** | 10.250.3.0/24 | 251
**GatewaySubnet** | 10.250.2.0/24 | 251

#### <a name="subnets-in-the-central-us-production-network-vnet-prod-cus"></a>Subredes de la red de producción del Centro de EE. UU. (VNET-PROD-CUS)

En paralelo con la red de producción en la región Este de EE. UU. 2 principal, hay una red de producción en la región Centro de EE. UU. secundaria.

**Subred** | **CIDR** | **Direcciones** | **En la subred**
--- | --- | --- | ---
**PROD-FE-CUS** | 10.255.32.0/22 | 1019 | Máquinas virtuales de nivel web/servidores front-end
**PROD-APP-CUS** | 10.255.36.0/22 | 1019 | Máquinas virtuales de nivel de aplicación
**PROD-DB-CUS** | 10.255.40.0/23 | 507 | VM de base de datos
**PROD-DC-CUS** | 10.255.42.0/24 | 251 | VM del controlador de dominio

#### <a name="subnets-in-the-central-us-failoverrecovery-network-in-central-us-vnet-asr-cus"></a>Subredes de la red de conmutación por error/recuperación del Centro de EE. UU. en Centro de EE. UU. (VNET-ASR-CUS)

La red VNET-ASR-CUS se usa para fines de conmutación por error entre regiones. Site Recovery se usará para replicar y conmutar por error las VM de Azure entre las regiones. También funciona como un centro de datos de Contoso para la red de Azure creada para las cargas de trabajo protegidas que se guardan de forma local, pero que conmutan por error a Azure para la recuperación ante desastres.

VNET-ASR-CUS es la misma subred básica que la de la red virtual de producción del Este de EE. UU. 2, pero sin necesidad de una subred de controlador de dominio.

**Subred** | **CIDR** | **Direcciones** | **En la subred**
--- | --- | --- | ---
**ASR-FE-CUS** | 10.255.16.0/22 | 1019 | Máquinas virtuales de nivel web/servidores front-end
**ASR-APP-CUS** | 10.255.20.0/22 | 1019 | Máquinas virtuales de nivel de aplicación
**ASR-DB-CUS** | 10.255.24.0/23 | 507 | VM de base de datos

![Arquitectura de red del concentrador](./media/contoso-migration-infrastructure/azure-networks-cus.png)

#### <a name="configure-peered-connections"></a>Configurar conexiones emparejadas

El concentrador de cada región se emparejará al concentrador en otra región, y a todas las redes virtuales de la región del concentrador. Esto permite que los concentradores se comuniquen, y también le permite ver todas las redes virtuales de una región. Observe lo siguiente:

- El emparejamiento crea una conexión con dos lados. Uno desde el mismo nivel de inicio en la primera red virtual, y otro en la segunda red virtual.
- En una implementación híbrida, el tráfico que pasa entre equipos del mismo nivel debe verse desde la conexión VPN entre el centro de datos local y Azure. Para habilitar esta opción, hay algunos parámetros específicos que deben configurarse en conexiones emparejadas.

Para las conexiones de VNet de radio que se realizan a través del concentrador al centro de datos local, Contoso debe permitir que el tráfico se reenvíe, y atraviese las puertas de enlace VPN.

##### <a name="domain-controller"></a>Controlador de dominio

Para los controladores de dominio en la red VNET-PROD-EUS2, Contoso quiere que el tráfico fluya entre la red de producción o el concentrador EUS2 y por la conexión VPN a la instancia local. Para ello, los administradores de Contoso deben permitir lo siguiente:

1. **Allow forwarded traffic (Permitir tráfico reenviado)** y **Allow gateway transit configurations (Permitir configuraciones de tránsito de puerta de enlace)** en la conexión emparejada. En nuestro ejemplo, esto sería la conexión VNET-HUB-EUS2 a la conexión VNET-PROD-EUS2.

    ![Emparejamiento](./media/contoso-migration-infrastructure/peering1.png)

2. **Allow forwarded traffic (Permitir tráfico reenviado)** y **Use remote gateways (Usar puertas de enlace remotas)** en el lado opuesto del emparejamiento, en la conexión de VNET-PROD-EUS2 a VNET-HUB-EUS2.

    ![Emparejamiento](./media/contoso-migration-infrastructure/peering2.png)

3. Configurarán localmente una ruta estática que dirige el tráfico local para enrutar a través del túnel VPN a la red virtual. La configuración se completará en la puerta de enlace que proporciona el túnel VPN desde Contoso a Azure. Para esto, utilizan RRAS.

    ![Emparejamiento](./media/contoso-migration-infrastructure/peering3.png)

##### <a name="production-networks"></a>Redes de producción

Una red del mismo nivel con radio no puede ver a través de un concentrador a otra red del mismo nivel con radio que se encuentre en otra región.

Para que las redes de producción de Contoso en ambas regiones puedan verse entre sí, los administradores de Contoso deben crear una conexión directa del mismo nivel para VNET-PROD-EUS2 y VENT-PROD-CUS.

![Emparejamiento](./media/contoso-migration-infrastructure/peering4.png)

### <a name="set-up-dns"></a>Configurar DNS

Al implementar recursos en redes virtuales, tiene un par de opciones para la resolución del nombre de dominio. Puede usar la resolución del nombre que proporciona Azure o proporcionar servidores DNS para la resolución. El tipo de resolución de nombres que tenga que usar dependerá de cómo se comuniquen los recursos entre sí. Obtenga [más información](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances#azure-provided-name-resolution) acerca del servicio Azure DNS.

Los administradores de Contoso han decidido que el servicio Azure DNS no es una buena opción en su entorno híbrido. En su lugar, se usarán los servidores DNS locales.

- Puesto que se trata de una red híbrida, todas las VM locales y en Azure deben ser capaces de resolver nombres para funcionar correctamente. Esto significa que la configuración personalizada de DNS debe aplicarse a todas las redes virtuales.
- Contoso actualmente tiene controladores de dominio implementados en el centro de datos de Contoso y en las sucursales. Sus servidores DNS principales son CONTOSODC1(172.16.0.10) y CONTOSODC2(172.16.0.1)
- Cuando se implementan las redes virtuales, los controladores de dominio locales se establecen para usarse como servidores DNS en las redes.
- Para configurar esto, al usar un DNS personalizado en la red virtual, es necesario agregar la dirección IP de las resoluciones recursivas de Azure (por ejemplo, 168.63.129.16) a la lista de DNS. Para ello, Contoso configura el servidor DNS en cada red virtual. Por ejemplo, la configuración personalizada de DNS para la red VNET-HUB-EUS2 sería como sigue:

    ![DNS personalizado](./media/contoso-migration-infrastructure/custom-dns.png)

Además de sus controladores de dominio local, Contoso va a implementar cuatro más para dar apoyo a sus redes de Azure, dos para cada región. Esto es lo que Contoso implementará en Azure.

**Región** | **DC** | **Red virtual** | **Subred** | **Dirección IP**
--- | --- | --- | --- | ---
EUS2 | CONTOSODC3 | VNET-PROD-EUS2 | PROD-DC-EUS2 | 10.245.42.4
EUS2 | CONTOSODC4 | VNET-PROD-EUS2 | PROD-DC-EUS2 | 10.245.42.5
CUS | CONTOSODC5 | VNET-PROD-CUS | PROD-DC-CUS | 10.255.42.4
CUS | CONTOSODC6 | VNET-PROD-CUS | PROD-DC-CUS | 10.255.42.4

Después de implementar los controladores de dominio local, Contoso necesita actualizar la configuración de DNS en redes en ambas regiones para incluir los nuevos controladores de dominio en su lista de servidores DNS.

#### <a name="set-up-domain-controllers-in-azure"></a>Configurar controladores de dominio de Azure

Después de actualizar la configuración de red, los administradores de Contoso están listos para crear sus controladores de dominio en Azure.

1. En Azure Portal, se implementa una nueva VM de Windows Server en la red virtual adecuada.
2. Se crean conjuntos de disponibilidad en cada ubicación para la VM. Los conjuntos de disponibilidad hacen lo siguiente:

    - Asegúrese de que el tejido de Azure separa las VM en infraestructuras diferentes en la región de Azure.
    - Permite que Contoso sea apto para el SLA de 99,95 % para las VM de Azure. [Más información](https://docs.microsoft.com/azure/virtual-machines/windows/tutorial-availability-sets).

    ![Grupo de disponibilidad](./media/contoso-migration-infrastructure/availability-group.png)

3. Una vez implementada la VM, hay que encargarse de la interfaz de red de la VM. Establecen la dirección IP privada en estático y especifican una dirección válida.

    ![NIC de la VM](./media/contoso-migration-infrastructure/vm-nic.png)

4. Ahora, conectan un nuevo disco de datos a la VM. Este disco contiene la base de datos de Active Directory y el recurso compartido Sysvol.
    - El tamaño del disco determinará el número de IOPS que admite.
    - Con el tiempo, es posible que el tamaño del disco tenga que aumentar a medida que crece el entorno.
    - La unidad no se debe establecer en lectura/escritura para el almacenamiento en caché de host. Las bases de datos de Active Directory no admiten esto.

     ![Disco de Active Directory](./media/contoso-migration-infrastructure/ad-disk.png)

5. Una vez agregado el disco, se conecta a una VM a través del Escritorio remoto y se abre el Administrador del servidor.

6. A continuación, en **Servicios de almacenamiento y archivo**, se ejecuta el asistente para el nuevo volumen; hay que asegurarse de que la unidad tiene asignada la letra F: o superior en la VM local.

     ![Asistente para nuevo volumen](./media/contoso-migration-infrastructure/volume-wizard.png)

7. En Administrador del servidor, se agrega el rol **Active Directory Domain Services**. A continuación, la máquina virtual se configura como un controlador de dominio.

      ![Rol de servidor](./media/contoso-migration-infrastructure/server-role.png)

8. Después de que la VM se configure como controlador de dominio y se reinicie, Contoso abre el Administrador de DNS y configura el solucionador DNS de Azure como el reenviador. Esto permite que el controlador de dominio reenvíe consultas DNS que no se pueden resolver en el DNS de Azure.

    ![Reenviador DNS](./media/contoso-migration-infrastructure/dns-forwarder.png)

9. Ahora, se actualiza la configuración de DNS personalizada para cada red virtual con el controlador de dominio adecuado para la región de la red virtual. La lista incluye controladores de dominio locales.

### <a name="set-up-active-directory"></a>Configuración de Active Directory

Active Directory es un servicio crítico en la red y debe estar configurado correctamente. Los administradores de Contoso compilan sitios de Active Directory para el centro de datos de Contoso y para las regiones EUS2 y CUS.

1. Crea dos nuevos sitios (AZURE-EUS2 y AZURE-CUS y AZURE PERSO) junto con el sitio del centro de datos (ContosoDatacenter).
2. Después de crear los sitios, crea subredes en los sitios, para que coincidan las redes virtuales y el centro de datos.

    ![Subredes de controlador de dominio](./media/contoso-migration-infrastructure/dc-subnets.png)

3. A continuación, crea dos vínculos a sitios para conectarlo todo. Los controladores de dominio deberán moverse a su ubicación.

    ![Vínculos del controlador de dominio](./media/contoso-migration-infrastructure/dc-links.png)

4. Una vez que todo se haya configurado, la topología de replicación de Active Directory estará lista.

    ![Replicación de controlador de dominio](./media/contoso-migration-infrastructure/ad-resolution.png)

5. Con todo completo, se muestra una lista de los sitios y los controladores de dominio en el Centro de administración de Active Directory local.

    ![Centro de administración de Active Directory](./media/contoso-migration-infrastructure/ad-center.png)

## <a name="step-5-plan-for-governance"></a>Paso 5: Planeación para la gobernanza

Azure proporciona una gama de controles de gobernanza a través de los servicios y la plataforma de Azure. [Siga leyendo](https://docs.microsoft.com/azure/security/governance-in-azure) para conocer las opciones básicas.

A medida que Contoso configura la identidad y el control de acceso, ya ha comenzado a tener en cuenta algunos aspectos acerca de la gobernanza y la seguridad. En términos generales, hay tres áreas que deben tener en cuenta:

- **Directiva:** Azure Policy aplica y hace cumplir las reglas y los efectos sobre sus recursos, de modo que los recursos cumplan con los requisitos corporativos y los SLA.
- **Bloqueos:** Azure permite el bloqueo de suscripciones, grupos de recursos y otros recursos, por lo que solo pueden modificarlos aquellas personas con autoridad para hacerlo.
- **Etiquetas:** los recursos pueden controlarse, auditarse y administrarse con etiquetas. Las etiquetas asocian metadatos a recursos, que proporcionan información acerca de los recursos o propietarios.

### <a name="set-up-policies"></a>Configurar directivas

El servicio de Azure Policy evalúa los recursos, para detectar los que no son compatibles con las definiciones de directivas definidas. Por ejemplo, podría tener una directiva que solo permite determinados tipos de máquinas virtuales o que requiere recursos que tengan una etiqueta específica.

Las directivas especifican una definición de directiva, mientras que una asignación de directiva especifica el ámbito en el que se debe aplicar una directiva. El ámbito puede ir desde un grupo de administración a un grupo de recursos. [Obtenga información](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage) acerca de cómo crear y administrar directivas.

Contoso quiere empezar a trabajar con un par de directivas:

- Quiere una directiva para asegurarse de que los recursos solo pueden implementarse en las regiones EUS2 y CUS.
- Desea limitar las SKU de VM a las SKU aprobadas. La intención es asegurarse de que no se usan SKU de VM costosas.

#### <a name="limit-resources-to-regions"></a>Limitación de recursos en las regiones

Contoso usa la definición de directiva integrada **Ubicaciones permitidas** para limitar las regiones de los recursos.

1. En Azure Portal, seleccione **Todos los servicios** y busque **Directiva**.
2. Seleccione **Asignaciones** > **Asignar directiva**.
3. En la lista de directivas, seleccione **Ubicaciones permitidas**.
4. Establezca **Ámbito** en el nombre de la suscripción a Azure y seleccione las dos regiones en la lista de permitidos.

    ![Regiones permitidas de la directiva](./media/contoso-migration-infrastructure/policy-region.png)

5. De forma predeterminada, la directiva está establecida con la opción **Denegar**, lo que significa que si alguien inicia una implementación en la suscripción que no se encuentra en EUS2 o CUS, se producirá un error en la implementación. Esto es lo que ocurre si alguien de la suscripción de Contoso intenta configurar una implementación en Oeste de EE. UU.

    ![Error de directiva](./media/contoso-migration-infrastructure/policy-failed.png)

#### <a name="allow-specific-vm-skus"></a>Permitir determinadas SKU de VM

Contoso usará la definición de la directiva integrada **Allow virtual machines SKUs** (Permitir SKU de máquinas virtuales) para limitar el tipo de VM que se pueden crear en la suscripción.

![SKU de directiva](./media/contoso-migration-infrastructure/policy-sku.png)

#### <a name="check-policy-compliance"></a>Comprobar cumplimiento de directivas

Las directivas entran inmediatamente en vigor y Contoso puede comprobar el cumplimiento de los recursos.

1. En Azure Portal, seleccione el vínculo **Cumplimiento**.
2. Aparece el panel de cumplimiento. Puede explorar esta información en profundidad para obtener más detalles.

    ![Cumplimiento de directivas](./media/contoso-migration-infrastructure/policy-compliance.png)

### <a name="set-up-locks"></a>Configurar bloqueos

Contoso lleva mucho tiempo usando el marco de ITIL para administrar sus sistemas. Uno de los aspectos más importantes del marco es el control de cambios, y Contoso quiere asegurarse de que el control de cambios se incluye en la implementación de Azure.

Contoso va a implementar bloqueos tal como se indica a continuación:

- Cualquier componente de conmutación por error o de producción debe estar en un grupo de recursos con un bloqueo de solo lectura. Esto significa que, para modificar o eliminar elementos de producción, se debe quitar el bloqueo.
- Los grupos de recursos que no son de producción tendrán bloqueos CanNotDelete. Esto significa que los usuarios autorizados pueden leer o modificar un recurso, pero no eliminarlo.

[Obtenga más información](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) acerca de los bloqueos.

### <a name="set-up-tagging"></a>Configuración del etiquetado

Para realizar el seguimiento de los recursos que se agregan, será cada vez más importante que Contoso asocie los recursos con el departamento, el cliente o el entorno adecuados.

Además de proporcionar información acerca de los recursos y propietarios, las etiquetas permitirán que Contoso agregue y agrupe recursos, y que use los datos para propósitos de anulación.

Contoso necesita visualizar los recursos de Azure de forma que tenga sentido para su empresa. Por ejemplo, por rol o departamento. Tenga en cuenta que los recursos no tienen que residir en el mismo grupo de recursos para compartir una etiqueta. Contoso creará una taxonomía de etiquetas sencilla para que todo el mundo use las mismas etiquetas.

**Nombre de etiqueta** | **Valor**
--- | ---
CostCenter | 12345: debe ser un centro de coste válido de SAP.
BusinessUnit | Nombre de unidad de negocio (de SAP). Coincide con CostCenter.
ApplicationTeam | Alias de correo electrónico del equipo que posee la compatibilidad de la aplicación.
CatalogName | Nombre de la aplicación o ShareServices, según el catálogo de servicios que es compatible con el recurso.
ServiceManager | Alias de correo electrónico del Administrador de servicios de ITIL para el recurso.
COBPriority | Prioridad que estableció la empresa para BCDR. Valores de 1 a 5.
ENV | DEV, STG y PROD son los valores posibles. Representan el desarrollo, el ensayo y la producción.

Por ejemplo:

 ![Etiquetas de Azure](./media/contoso-migration-infrastructure/azure-tag.png)

Después de crear la etiqueta, Contoso volverá atrás y creará nuevas asignaciones y definiciones de la directiva para exigir el uso de las etiquetas necesarias en toda la organización.

## <a name="step-6-consider-security"></a>Paso 6: Consideración de la seguridad

La seguridad es fundamental en la nube y Azure proporciona una amplia gama de herramientas y funcionalidades de seguridad. Esto le ayuda a crear soluciones seguras, en la plataforma segura de Azure. Lea [Seguridad en una nube confianza](https://azure.microsoft.com/overview/trusted-cloud) para obtener más información acerca de la seguridad de Azure.

Hay algunos aspectos que Contoso debe contemplar:

- **Azure Security Center:** Azure Security Center proporciona administración unificada de la seguridad y protección avanzada contra amenazas para cargas de trabajo en la nube híbrida. Con Security Center, puede aplicar directivas de seguridad en las cargas de trabajo, limitar la exposición a amenazas y detectar y responder a los ataques. [Más información](https://docs.microsoft.com/azure/security-center/security-center-intro).
- **Grupos de seguridad de red (NSG):** un grupo de seguridad de red es un filtro (firewall) que contiene una lista de reglas de seguridad que, cuando se aplican, permiten o deniegan el tráfico de red a recursos que están conectados a redes virtuales de Azure. [Más información](https://docs.microsoft.com/azure/virtual-network/security-overview).
- **Cifrado de datos:** Azure Disk Encryption es una funcionalidad que permite cifrar los discos de las máquinas virtuales IaaS con Windows y Linux. [Más información](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest).

### <a name="work-with-the-azure-security-center"></a>Trabajar con Azure Security Center.

Contoso quiere conocer rápidamente la postura de seguridad de su nueva nube híbrida y, sobre todo, de las cargas de trabajo de Azure. Como resultado, Contoso ha decidido implementar Azure Security Center a partir de las siguientes características:

- Administración de directivas centralizada
- Evaluación continua
- Recomendaciones prácticas

#### <a name="centralize-policy-management"></a>Administración de directivas centralizada

Gracias a la administración centralizada de directiva, Contoso garantizará el cumplimiento de los requisitos de seguridad administrando las directivas de seguridad de forma centralizada en todo el entorno. Puede implementar una directiva que se aplica a todos sus recursos de Azure de manera simple y rápida.

![Directiva de seguridad](./media/contoso-migration-infrastructure/security-policy.png)

#### <a name="assess-and-action"></a>Evaluar y acción

Contoso se aprovechará de una evaluación continua de la seguridad que supervisa la seguridad de las máquinas, redes, almacenamiento, datos y aplicaciones; para detectar posibles problemas de seguridad.

- Security Center analizará el estado de seguridad del proceso, la infraestructura y los recursos de Contoso, y de los servicios y aplicaciones de Azure.
- La evaluación continua ayuda al equipo de operaciones de Contoso a detectar posibles problemas de seguridad, por ejemplo, sistemas a los que les faltan actualizaciones de seguridad o puertos de red expuestos.
- En concreto, Contoso quiere asegurarse de que todas sus VM están protegidas. Security Center ayuda con esto, comprobando el estado de las VM, realizando recomendaciones con prioridad y útiles para corregir las vulnerabilidades de seguridad antes de que se exploten.

![Supervisión](./media/contoso-migration-infrastructure/monitoring.png)

### <a name="work-with-nsgs"></a>Trabajar con Grupos de seguridad de red

Contoso puede limitar el tráfico de red a los recursos de una red virtual mediante un grupo de seguridad de red.

- Un grupo de seguridad de red contiene una lista de reglas de seguridad que permiten o deniegan el tráfico de red entrante o saliente en función de las direcciones IP de origen o destino, el puerto y el protocolo.
- Cuando se aplican a una subred, las reglas se aplican a todos los recursos de la subred. Además de interfaces de red, esto incluye instancias de servicios de Azure implementados en la subred.
- Los grupos de seguridad de aplicaciones (ASG) le permiten configurar la seguridad de red como una extensión natural de la estructura de una aplicación, lo que le permite agrupar VM y directivas de seguridad de red basadas en esos grupos.
  - Los grupos de seguridad de aplicaciones implican que Contoso puede volver a usar la directiva de seguridad a escala sin mantenimiento manual de direcciones IP explícitas. La plataforma controla la complejidad de las direcciones IP explícitas y de varios conjuntos de reglas, lo que le permite centrarse en su lógica de negocios.
  - Contoso puede especificar un grupo de seguridad de aplicaciones como origen y destino de una regla de seguridad. Cuando se haya definido una directiva de seguridad, Contoso podrá crear redes virtuales y asignar las NIC de las máquinas virtuales a un grupo.

Contoso implementará una mezcla de NSG y ASG. Le preocupa la administración de NSG. así como el uso excesivo de los NSG y la mayor complejidad para el personal encargado de las operaciones. Esto es lo que Contoso hará:

- Todo el tráfico que entra y sale de todas las subredes (norte-sur) estará sujeto a una regla de NSG, excepto GatewaySubnets en las redes de concentrador.
- Cualquier controlador de dominio o firewall estará protegido por los NSG de subred y los NSG de NIC.
- Todas las aplicaciones de producción tendrán ASG aplicados.

Contoso ha compilado un modelo del aspecto de todo esto para sus aplicaciones.

![Seguridad](./media/contoso-migration-infrastructure/asg.png)

Los NSG asociados con el ASG se configurarán con privilegios mínimos para asegurarse de que solo los paquetes permitidos pueden fluir de una parte de la red a su destino.

**Acción** | **Nombre** | **Origen** | **Destino** | **Puerto**
--- | --- | --- | --- | ---
Allow | AllowiInternetToFE | VNET-HUB-EUS1/IB-TrustZone | APP1-FE 80, 443
Allow | AllowWebToApp | APP1-FE | APP1-APP | 80, 443
Allow | AllowAppToDB | APP1-APP | APP1-DB | 1433
Denegar | DenyAllInbound | Any | Any | Any

### <a name="encrypt-data"></a>Cifrado de datos

Azure Disk Encryption se integra con Azure Key Vault para controlar y administrar los secretos y las claves de cifrado de los discos en la suscripción a Key Vault. Gracias a ello, se garantiza que todos los datos de los discos de VM se cifren en reposo en Azure Storage.

- Contoso determinó que las VM específicas requieren cifrado.
- Contoso aplicará un cifrado a las VM con datos confidenciales, de clientes o de PPP.

## <a name="conclusion"></a>Conclusión

En este artículo, Contoso configuró su infraestructura y directiva para la suscripción a Azure, la identificación híbrida, la recuperación ante desastres, las redes, la gobernanza y la seguridad.

No todos los pasos que Contoso llevó a cabo aquí son necesarios para realizar una migración a la nube. En este caso, quería planear una infraestructura de red que pudiera usarse para todos los tipos de migraciones y que fuera segura, resistente y escalable.

Con esta infraestructura lista, Contoso ya puede continuar y probar la migración.

## <a name="next-steps"></a>Pasos siguientes

Después de configurar su infraestructura de Azure, Contoso está listo para empezar a migrar las cargas de trabajo a la nube. Consulte la sección de [información general sobre los patrones de migración y ejemplos](./contoso-migration-overview.md#windows-server-workloads) para ver una selección de los escenarios que usan esta infraestructura de ejemplo como destino de migración.
