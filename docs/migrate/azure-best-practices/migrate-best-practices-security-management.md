---
title: Procedimientos recomendados para la protección y administración de cargas de trabajo migradas a Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Después de migrar a Azure, consulte los procedimientos recomendados para la operación, administración y protección de las cargas de trabajo migradas.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b7d2ac8d624115c9d843ded8a045cd68f4050650
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70836742"
---
# <a name="best-practices-for-securing-and-managing-workloads-migrated-to-azure"></a>Procedimientos recomendados para la protección y administración de cargas de trabajo migradas a Azure

A medida que planea y diseña la migración, además de pensar en la migración propiamente dicha, debe tener en cuenta el modelo de seguridad y administración en Azure después de la migración. En este artículo, se describen la planeación y los procedimientos recomendados para proteger la implementación de Azure después de la migración y para las tareas en curso para mantener la implementación en ejecución en un nivel óptimo.

> [!IMPORTANT]
> Los procedimientos recomendados y las opiniones que se describen en este artículo se basan en la plataforma de Azure y las características del servicio disponibles en el momento de redactar el artículo. Las características y funcionalidades cambian con el tiempo.

## <a name="secure-migrated-workloads"></a>Protección de las cargas de trabajo migradas

Tras la migración, la tarea más crítica es proteger las cargas de trabajo migradas de amenazas internas y externas. Estos procedimientos recomendados le ayudarán a hacerlo:

- [Trabajo con Azure Security Center](#best-practice-follow-azure-security-center-recommendations): obtenga información sobre cómo trabajar con la supervisión, las valoraciones y las recomendaciones proporcionadas por Azure Security Center.
- [Cifrado de los datos](#best-practice-encrypt-data): consulte los procedimientos recomendados para cifrar los datos en Azure.
- [Configuración de antimalware](#best-practice-protect-vms-with-antimalware): proteja las máquinas virtuales frente a malware y ataques malintencionados.
- [Protección de aplicaciones web](#best-practice-secure-web-apps): proteja la información confidencial de las aplicaciones web migradas.
- [Revisión de suscripciones](#best-practice-review-subscriptions-and-resource-permissions): compruebe quién tiene acceso a las suscripciones y los recursos de Azure después de la migración.
- [Trabajo con registros](#best-practice-review-audit-and-security-logs): revise los registros de auditoría y seguridad de Azure de forma periódica.
- [Revisión de otras características de seguridad](#best-practice-evaluate-other-security-features): conozca y evalúe las características de seguridad avanzadas que ofrece Azure.

## <a name="best-practice-follow-azure-security-center-recommendations"></a>Procedimiento recomendado: seguir las recomendaciones de Azure Security Center

Microsoft realiza un gran esfuerzo para asegurarse de que los administradores de inquilinos de Azure tengan la información necesaria para habilitar las características de seguridad que protegen las cargas de trabajo frente a los ataques. Azure Security Center proporciona administración de seguridad unificada. Desde Security Center, puede aplicar directivas de seguridad en las cargas de trabajo, limitar la exposición a amenazas y detectar y responder a los ataques. Security Center analiza configuraciones y recursos de los inquilinos de Azure y hace recomendaciones de seguridad, que incluyen:

- **Administración centralizada de directivas**: garantice el cumplimiento de los requisitos de seguridad normativos o de la empresa administrando las directivas de seguridad de forma centralizada en todas las cargas de trabajo en la nube híbridas.
- **Evaluación continua de la seguridad**: supervise la situación de seguridad de máquinas, redes, almacenamiento y servicios de datos y aplicaciones para detectar posibles problemas de seguridad.
- **Recomendaciones prácticas**: corrija las vulnerabilidades de seguridad antes de que puedan ser usadas por los atacantes mediante recomendaciones de seguridad prácticas y clasificadas en orden de prioridad.
- **Prioridad de alertas e incidentes**: céntrese primero en las amenazas más críticas con la clasificación en orden de prioridad de las alertas e incidentes de seguridad.

Además de las valoraciones y recomendaciones, Azure Security Center proporciona otras características de seguridad que se pueden habilitar para recursos específicos.

- **Acceso Just-In-Time (JIT).** reduzca la superficie de la red que está expuesta a ataques mediante un acceso Just-In-Time controlado a los puertos de administración de las máquinas virtuales de Azure.
  - Tener el puerto RDP 3389 de la máquina virtual abierto en Internet expone las máquinas virtuales a la continua actividad de los actores perjudiciales. Las direcciones IP de Azure son bien conocidas y los piratas informáticos las sondean continuamente para posibles ataques en los puertos 3389 abiertos.
  - Just-In-Time utiliza grupos de seguridad de red (NSG) y reglas de entrada que limitan el tiempo que está abierto un puerto específico.
  - Con Just-In-Time habilitado, Security Center comprueba que un usuario tiene permisos de acceso de escritura de control de acceso basado en rol (RBAC) para una máquina virtual. Además, especifique reglas de cómo pueden conectarse los usuarios a las máquinas virtuales. Si los permisos son correctos, se aprueba la solicitud de acceso y Security Center configura grupos de seguridad de red (NSG) para permitir el tráfico entrante a los puertos seleccionados durante el tiempo especificado. Los grupos de seguridad de red se devuelven a su estado anterior cuando expira el tiempo.
- **Controles de aplicaciones adaptables.** Mantenga las máquinas virtuales sin malware mediante el control de las aplicaciones que se ejecutan en ellas con listas dinámicas de aplicaciones permitidas.
  - Los controles de aplicaciones adaptables le permiten aprobar aplicaciones y evitar que usuarios o administradores suplantados puedan instalar aplicaciones de software no autorizadas o en investigación en las máquinas virtuales.
    - Puede bloquear o generar alertas de los intentos de ejecución de aplicaciones malintencionadas, evitar aplicaciones no deseadas o malintencionadas y garantizar el cumplimiento de la directiva de seguridad de aplicaciones de la organización.
- **Supervisión de la integridad de los archivos.** garantice la integridad de los archivos que se ejecutan en las máquinas virtuales.
  - No es necesario instalar software para causar problemas en la máquina virtual. El cambio de un archivo del sistema también puede causar la degradación del rendimiento o errores en la máquina virtual. La funcionalidad Supervisión de la integridad de los archivos examina los archivos del sistema y la configuración del registro en busca de cambios y le notifica si se actualiza algún elemento.
  - Security Center recomienda qué archivos se deben supervisar.

**Más información:**

- [Más información](/azure/security-center/security-center-intro) sobre Azure Security Center.
- [Más información](/azure/security-center/security-center-just-in-time) sobre el acceso Just-in-Time a la máquina virtual.
- [Más información](/azure/security-center/security-center-adaptive-application) sobre la aplicación de los controles de aplicación adaptables.
- [Introducción](/azure/security-center/security-center-file-integrity-monitoring) a la supervisión de la integridad de los archivos.

## <a name="best-practice-encrypt-data"></a>Procedimiento recomendado: Cifrado de datos

El cifrado es una parte importante de los procedimientos de seguridad de Azure. Garantizar que el cifrado está habilitado en todos los niveles ayuda a prevenir que personas no autorizadas puedan tener acceso a información confidencial, incluidos los datos en tránsito y en reposo.

### <a name="encryption-for-iaas"></a>Cifrado para IaaS

- **Máquinas virtuales:** para las máquinas virtuales, puede usar Azure Disk Encryption para cifrar los discos de las máquinas virtuales de IaaS con Linux y Windows.
  - Disk Encryption usa BitLocker para Windows y DM-Crypt para Linux con la finalidad de proporcionar cifrado de volumen para discos de datos y del sistema operativo.
  - Puede usar una clave de cifrado creada por Azure o puede proporcionar sus propias claves de cifrado protegidas en Azure Key Vault.
  - Con Disk Encryption, los datos de la máquina virtual de IaaS se protegen en reposo (en el disco) y durante el arranque de la máquina virtual.
    - Azure Security Center le avisa si tiene máquinas virtuales que no están cifradas.
- **Storage:** proteja en reposo los datos almacenados en Azure Storage.
  - Los datos almacenados en cuentas de Azure Storage se pueden cifrar mediante claves AES generadas por Microsoft que cumplen con FIPS 140-2 o puede usar sus propias claves.
  - Storage Service Encryption está habilitado para todas las cuentas de almacenamiento nuevas y existentes y no se puede deshabilitar.

### <a name="encryption-for-paas"></a>Cifrado para PaaS

A diferencia de IaaS, en la que administra sus propias máquinas virtuales y la infraestructura, en un modelo PaaS el proveedor administra la plataforma y la infraestructura, lo que le permite centrarse en la lógica y las funcionalidades de la aplicación principal. Con tantos tipos distintos de servicios de PaaS, cada servicio se evalúa individualmente por motivos de seguridad. Por ejemplo, veamos cómo se puede habilitar el cifrado para Azure SQL Database.

- **Always Encrypted:** use el Asistente de Always Encrypted en SQL Server Management Studio para proteger los datos en reposo.
  - Puede crear claves de Always Encrypted para cifrar los datos de columnas individuales.
  - Las claves de Always Encrypted se pueden almacenan cifradas en los metadatos de la base de datos o se pueden almacenar en almacenes de claves de confianza, como Azure Key Vault.
  - Probablemente se necesitarán cambios en la aplicación para usar esta característica.
- **Cifrado de datos transparente (TDE)** : proteja Azure SQL Database con cifrado y descifrado en tiempo real de la base de datos, las copias de seguridad asociadas y los archivos de registro de transacciones en reposo.
  - TDE permite que las actividades de cifrado tengan lugar sin cambios en la capa de aplicación.
  - TDE puede usar claves de cifrado proporcionadas por Microsoft o puede proporcionar sus propias claves mediante la compatibilidad con Bring Your Own Key.

**Más información:**

- [Más información](/azure/security/azure-security-disk-encryption-overview) sobre Azure Disk Encryption para máquinas virtuales de IaaS.
- [Habilitación](/azure/security/azure-security-disk-encryption-windows) del cifrado para máquinas virtuales Windows de IaaS.
- [Más información](/azure/storage/common/storage-service-encryption) sobre Azure Storage Service Encryption para datos en reposo.
- [Consulte](/azure/sql-database/sql-database-always-encrypted-azure-key-vault) una introducción a Always Encrypted.
- [Más información](/azure/sql-database/transparent-data-encryption-azure-sql?view=sql-server-2017) sobre TDE para Azure SQL Database.
- [Más información](/azure/sql-database/transparent-data-encryption-byok-azure-sql) sobre TDE con Bring Your Own Key.

## <a name="best-practice-protect-vms-with-antimalware"></a>Procedimiento recomendado: protección de las máquinas virtuales con antimalware

En particular, las máquinas virtuales anteriores migradas a Azure podrían no tener instalado el nivel adecuado de antimalware. Azure proporciona una solución de punto de conexión gratuita que ayuda a proteger las máquinas virtuales frente a virus, spyware y otro malware.

- Microsoft Antimalware para Azure genera alertas cuando intenta instalarse un software malintencionado o no deseado conocido.
- Es una solución de un solo agente que se ejecuta en segundo plano sin intervención humana.
- En Azure Security Center, puede identificar fácilmente las máquinas virtuales que no tienen la protección del punto de conexión en ejecución e instalar Microsoft Antimalware según sea necesario.

![Antimalware para máquinas virtuales](./media/migrate-best-practices-security-management/antimalware.png)
*Antimalware for VMs*

**Más información:**

- [Más información](/azure/security/azure-security-antimalware) sobre Microsoft Antimalware.

## <a name="best-practice-secure-web-apps"></a>Procedimiento recomendado: protección de aplicaciones web

Las aplicaciones web migradas se enfrentan a un par de problemas:

- La mayoría de las aplicaciones web heredadas tienden a tener información confidencial dentro de los archivos de configuración. Los archivos que contienen dicha información pueden presentar problemas de seguridad cuando se realiza una copia de seguridad de las aplicaciones o cuando el código de la aplicación se confirma o extrae del control de código fuente.
- Además, al migrar aplicaciones web que residen en una máquina virtual, es probable que traslade esa máquina desde una red local y un entorno protegido mediante firewall a un entorno abierto a Internet. Asegúrese de que configura una solución que lleve a cabo el trabajo de los recursos de protección locales.

Azure proporciona un par de soluciones:

- **Azure Key Vault:** hoy en día, los desarrolladores de aplicaciones web dan pasos para asegurarse de que la información confidencial no se filtra de estos archivos. Un método para proteger la información consiste en extraerla de los archivos y colocarla en una instancia de Azure Key Vault.
  - Puede usar Key Vault para centralizar el almacenamiento de secretos de aplicación y controlar su distribución. Evita la necesidad de almacenar información de seguridad en los archivos de la aplicación.
  - Las aplicaciones pueden acceder de forma segura a la información del almacén mediante identificadores URI, sin necesidad de código personalizado.
  - Azure Key Vault le permite bloquear el acceso mediante los controles de seguridad de Azure e implementar a la perfección "claves de rotación". Microsoft no puede ver ni extraer sus datos.
- **App Service Environment:** si una aplicación que ha migrado necesita protección adicional, puede considerar la incorporación de App Service Environment y el firewall de aplicaciones web para proteger los recursos de la aplicación.
  - Azure App Service Environment proporciona un entorno completamente aislado y dedicado en el que ejecutar aplicaciones de App Service como aplicaciones web Windows y Linux, contenedores de Docker, aplicaciones móviles y funciones.
  - Es útil para aplicaciones de muy alta escala, que requieren aislamiento y un acceso a la red seguro o que tienen un uso elevado de memoria.
- **Firewall de aplicaciones web:** una característica de Azure Application Gateway que ofrece una protección centralizada para aplicaciones web.
  - Protege las aplicaciones web sin necesidad de modificaciones en el código de back-end.
  - Protege varias aplicaciones web al mismo tiempo detrás de una puerta de enlace de aplicaciones.
  - Un firewall de aplicaciones web se puede supervisar mediante Azure Monitor y se integra en Azure Security Center.

![protección de aplicaciones web](./media/migrate-best-practices-security-management/web-apps.png)

*Azure Key Vault*

**Más información:**

- [Introducción](/azure/key-vault/key-vault-overview) a Azure Key Vault.
- [Más información](/azure/application-gateway/waf-overview) sobre el firewall de aplicaciones web.
- [Introducción](/azure/app-service/environment/intro) a Azure App Service Environment.
- [Más información](/azure/key-vault/tutorial-web-application-keyvault) sobre cómo configurar una aplicación web para leer los secretos de Key Vault.
- [Más información](/azure/application-gateway/waf-overview) sobre el firewall de aplicaciones web.

## <a name="best-practice-review-subscriptions-and-resource-permissions"></a>Procedimiento recomendado: revisión de suscripciones y permisos de recursos

Al migrar las cargas de trabajo y ejecutarlas en Azure, el personal con acceso a las cargas de trabajo varía. El equipo de seguridad debe revisar el acceso a los grupos de recursos y el inquilino de Azure de forma periódica. Azure incluye ofertas de administración de identidades y seguridad de control de acceso, incluido el control de acceso basado en rol (RBAC), para autorizar los permisos para acceder a los recursos de Azure.

- RBAC asigna los permisos de acceso para las entidades de seguridad. Las entidades de seguridad representan a usuarios, grupos (un conjunto de usuarios), entidades de servicio (identidades usadas por aplicaciones y servicios) e identidades administradas (una identidad de Azure Active Directory Azure administrada automáticamente por Azure).
- RBAC puede asignar roles a las entidades de seguridad, como propietario, colaborador y lector y definiciones de rol (una colección de permisos) que definen las operaciones que pueden realizar los roles.
- RBAC también puede establecer los ámbitos que definen el límite de un rol. El ámbito se puede establecer en varios niveles, como un grupo de administración, una suscripción, un grupo de recursos o un recurso.
- Asegúrese de que los administradores con acceso a Azure solo pueden acceder a los recursos que desea permitir. Si los roles predefinidos de Azure no son lo suficientemente pormenorizados, puede crear roles personalizados para separar y limitar los permisos de acceso.

![Control de acceso](./media/migrate-best-practices-security-management/subscription.png)
*Access control - IAM*

**Más información:**

- [Acerca de](/azure/role-based-access-control/overview) RBAC.
- [Más información](/azure/role-based-access-control/role-assignments-portal) sobre la administración del acceso mediante RBAC y Azure Portal.
- [Más información](/azure/role-based-access-control/custom-roles) acerca de los roles personalizados.

## <a name="best-practice-review-audit-and-security-logs"></a>Procedimiento recomendado: revisión de los registros de auditoría y seguridad

Azure Active Directory (Azure AD) proporciona registros de actividad que aparecen en Azure Monitor. Los registros capturan las operaciones realizadas en el inquilino de Azure, cuándo se produjeron y quién las realizó.

- Los registros de auditoría muestran el historial de tareas del inquilino. Los registros de actividad de inicio de sesión registros muestran quién llevó a cabo las tareas.
- El acceso a los informes de seguridad depende de la licencia de Azure AD. En las licencias Gratis y Básica puede obtener una lista de usuarios e inicios de sesión de riesgo. En las ediciones Prémium 1 y Prémium 2 puede obtener información del evento subyacente.
- Puede enrutar los registros de actividad a varios puntos de conexión para la retención a largo plazo y obtención de conclusiones sobre los datos.
- Convierta en una práctica común la revisión de los registros o integre las herramientas de administración de eventos e información de seguridad (SIEM) para revisar automáticamente las anomalías. Si no usa Premium 1 o 2, deberá hacer una gran cantidad de análisis usted mismo o mediante el sistema SIEM. El análisis incluye la búsqueda de inicios de sesión en riesgo y eventos y otros patrones de ataque del usuario.

![Usuarios y grupos](./media/migrate-best-practices-security-management/azure-ad.png)

*Usuarios y grupos de Azure AD*

**Más información:**

- [Más información](/azure/active-directory/reports-monitoring/concept-activity-logs-azure-monitor) sobre los registros de actividad de Azure AD en Azure Monitor.
- [Más información](/azure/active-directory/reports-monitoring/concept-audit-logs) sobre la auditoría de informes de actividad en Azure Portal.

## <a name="best-practice-evaluate-other-security-features"></a>Procedimiento recomendado: evaluación de otras características de seguridad

Azure proporciona otras características de seguridad que ofrecen opciones avanzadas de seguridad. Algunos de estos procedimientos recomendados requieren licencias adicionales y opciones Prémium.

- **Implementación de unidades administrativas de Azure AD.** la delegación de derechos administrativos al personal de soporte técnico puede resultar complicada con el control de acceso básico de Azure. Otorgar al personal de soporte técnico acceso para administrar todos los grupos de Azure AD podría no ser el enfoque ideal para la seguridad de la organización. El uso de AU le permite separar los recursos de Azure en contenedores de forma similar a las unidades organizativas (OU) de un entorno local. Para utilizar AU, el administrador de AU debe tener una licencia de Azure AD Prémium. [Más información](/azure/active-directory/users-groups-roles/directory-administrative-units).
- **Uso de Multi-factor Authentication.** Si tiene una licencia de Azure AD Premium, puede habilitar y aplicar la autenticación multifactor en las cuentas de administrador. La suplantación de identidad es la manera más común de poner en peligro las credenciales de las cuentas. Una vez que un actor perjudicial consigue credenciales de cuenta de administrador, no hay ningún freno posible ante acciones de gran alcance como la eliminación de todos los grupos de recursos. Puede establecer la autenticación multifactor de varias maneras como, por ejemplo, con correo electrónico, una aplicación autenticadora y mensajes de texto de teléfono. Como administrador puede seleccionar la opción menos intrusiva. La autenticación multifactor se integra con el análisis de amenazas y las directivas de acceso condicional para solicitar aleatoriamente la respuesta a un desafío de autenticación multifactor. Más información sobre la [guía de seguridad](/azure/active-directory/authentication/multi-factor-authentication-security-best-practices) y [cómo configurar la autenticación multifactor](/azure/active-directory/authentication/multi-factor-authentication-security-best-practices).
- **Implementación del acceso condicional.** en la mayoría de las organizaciones pequeñas y medianas, los administradores de Azure y el equipo de soporte técnico probablemente se encuentran en una sola zona geográfica. En este caso, la mayoría de los inicios de sesión provienen de las mismas áreas. Si las direcciones IP de estas ubicaciones son bastante estáticas, tiene sentido que no se deberían ver inicios de sesión de administrador fuera de estas áreas. Incluso en caso de que un actor perjudicial remoto ponga en peligro las credenciales de administrador, puede implementar características de seguridad como el acceso condicional combinado con la autenticación multifactor para evitar el inicio de sesión desde ubicaciones remotas o desde ubicaciones suplantadas de direcciones IP aleatorias. [Más información](/azure/active-directory/conditional-access/overview) sobre el acceso condicional y una [revisión de los procedimientos recomendados](/azure/active-directory/conditional-access/best-practices) para el acceso condicional en Azure AD.
- **Revisión de los permisos de las aplicaciones empresariales.** Con el paso del tiempo, los administradores pueden seleccionar vínculos de Microsoft y de terceros sin conocer su impacto en la organización. Los vínculos pueden presentar pantallas de consentimiento que asignan permisos a las aplicaciones de Azure y podrían permitir acceso de lectura a los datos de Azure AD o incluso acceso total para administrar la suscripción de Azure. Debe revisar periódicamente las aplicaciones a la que los administradores y usuarios han permitido el acceso a los recursos de Azure. Asegúrese de que estas aplicaciones solo tienen los permisos necesarios. Además, trimestral o semestralmente puede enviar por correo electrónico a los usuarios un vínculo a páginas de aplicación para que sean conscientes de las aplicaciones a la que han permitido el acceso a los datos de la organización. [Más información](/azure/active-directory/manage-apps/application-types) sobre los tipos de aplicación y [cómo controlar](/azure/active-directory/manage-apps/remove-user-or-group-access-portal) las asignaciones de aplicaciones en Azure AD.

## <a name="managed-migrated-workloads"></a>Administración de las cargas de trabajo migradas

En esta sección se le recomiendan algunos procedimientos para la administración de Azure, incluidos:

- [Administración de recursos](#best-practice-name-resource-groups): procedimientos recomendados para los grupos de recursos y los recursos de Azure, como la nomenclatura inteligente, la prevención de la eliminación accidental, la administración de los permisos de recursos y el etiquetado eficaz de los recursos.
- [Uso de planos técnicos](#best-practice-implement-blueprints): obtenga una visión general rápida sobre el uso de planos técnicos para crear y administrar los entornos de implementación.
- [Revisión de las arquitecturas](#best-practice-review-azure-reference-architectures): revise arquitecturas de Azure de ejemplo para obtener información al crear las implementaciones posteriores a la migración.
- [Configuración de grupos de administración](#best-practice-manage-resources-with-azure-management-groups): si tiene varias suscripciones, puede reunirlas en grupos de administración y aplicar la configuración de gobernanza a esos grupos.
- [Configuración de directivas de acceso](#best-practice-deploy-azure-policy): aplique directivas de cumplimiento a los recursos de Azure.
- [Implementación de una estrategia de BCDR](#best-practice-implement-a-bcdr-strategy): elabore una estrategia de continuidad empresarial y recuperación ante desastres (BCDR) para mantener los datos seguros, el entorno resistente y los recursos activos y en ejecución cuando se producen interrupciones.
- [Administración de máquinas virtuales](#best-practice-use-managed-disks-and-availability-sets): agrupe las máquinas virtuales en grupos de disponibilidad para alta disponibilidad y resistencia. Use discos administrados para facilitar la administración de los discos y el almacenamiento de la máquina virtual.
- [Supervisión del uso de recursos](#best-practice-monitor-resource-usage-and-performance): habilite el registro de diagnóstico para los recursos de Azure, cree alertas y cuadernos de estrategias para la solución proactiva de problemas y use el panel de Azure para obtener una vista unificada del mantenimiento y el estado de la implementación.
- [Administración del soporte técnico y las actualizaciones](#best-practice-manage-updates): conozca el plan de soporte técnico de Azure y cómo implementarlo, consulte los procedimientos recomendados para mantener actualizadas las máquinas virtuales y ponga en marcha procesos para la administración de cambios.

## <a name="best-practice-name-resource-groups"></a>Procedimiento recomendado: nomenclatura de los grupos de recursos

Asegúrese de que los grupos de recursos tienen nombres descriptivos que los administradores y los miembros del equipo de soporte técnico puedan reconocer y utilizar fácilmente para mejorar considerablemente la productividad y la eficacia.

- Se recomienda seguir las convenciones de nomenclatura de Azure.
- Si va a sincronizar Active Directory local con Azure AD mediante Azure AD Connect, considere la posibilidad de hacer coincidir los nombres de los grupos de seguridad locales con los nombres de los grupos de recursos de Azure.

![Nomenclatura](./media/migrate-best-practices-security-management/naming.png)

*Nomenclatura del grupo de recursos*

**Más información:**

- [Más información](/azure/architecture/best-practices/naming-conventions) sobre convenciones de nomenclatura.

## <a name="best-practice-implement-delete-locks-for-resource-groups"></a>Procedimiento recomendado: implementación de bloqueos de eliminación para grupos de recursos

Lo último que necesita es que un grupo de recursos desaparezca porque se eliminó accidentalmente. Se recomienda implementar bloqueos de eliminación para que esto no suceda.

![Eliminación de bloqueos](./media/migrate-best-practices-security-management/locks.png)

*Eliminación de bloqueos*

**Más información:**

- [Más información](/azure/azure-resource-manager/resource-group-lock-resources) sobre el bloqueo de recursos para impedir cambios inesperados.

## <a name="best-practice-understand-resource-access-permissions"></a>Procedimiento recomendado: descripción de los permisos de acceso a los recursos

Un propietario de la suscripción tiene acceso a todos los grupos de recursos y recursos de la suscripción.

- Agregue personas con moderación a esta asignación valiosa. Comprender las ramificaciones de estos tipos de permisos es importante para mantener el entorno seguro y estable.
- Asegúrese de colocar los recursos en los grupos de recursos adecuados:
  - Agrupe los recursos con un ciclo de vida similar. Idealmente, no debería ser necesario mover un recurso cuando se necesita eliminar un grupo de recursos completo.
  - Los recursos que posibilitan una función o una carga de trabajo se deben colocar juntos para una administración simplificada.

**Más información:**

- [Más información](https://azure.microsoft.com/blog/organizing-subscriptions-and-resource-groups-within-the-enterprise) sobre la organización de suscripciones y grupos de recursos.

## <a name="best-practice-tag-resources-effectively"></a>Procedimiento recomendado: etiquetado eficaz de los recursos

A menudo, el uso de un nombre de grupo de recursos relacionado con los recursos no proporciona suficientes metadatos para la implementación eficaz de mecanismos como la facturación interna o la administración dentro de una suscripción.

- Como procedimiento recomendado, debería usar etiquetas de Azure para agregar metadatos útiles que se pueden consultar y sobre los que se puede informar.
- Las etiquetas proporcionan una manera de organizar lógicamente los recursos con las propiedades que defina. Las etiquetas se pueden aplicar a grupos de recursos o directamente a recursos.
- Las etiquetas se pueden aplicar en un grupo de recursos o en recursos individuales. Los recursos del grupo no heredan las etiquetas del grupo de recursos.
- Puede automatizar el etiquetado con PowerShell o Azure Automation o bien etiquetar grupos y recursos individuales. Uso de la opción -tagging o método de autoservicio. Si tiene en funcionamiento un sistema de administración de cambios y solicitudes, puede usar fácilmente la información de la solicitud para rellenar las etiquetas de recursos específicos de la empresa.

![Etiquetado](./media/migrate-best-practices-security-management/tagging.png)
*Tagging*

**Más información:**

- [Más información](/azure/azure-resource-manager/resource-group-using-tags) sobre el etiquetado y las limitaciones de las etiquetas.
- [Consulte](/azure/azure-resource-manager/resource-group-using-tags#powershell) ejemplos de PowerShell y la CLI para configurar el etiquetado y para aplicar las etiquetas de un grupo de recursos a sus recursos.
- [Consulte](https://www.azurefieldnotes.com/2016/07/18/azure-resource-tagging-best-practices) los procedimientos recomendados de etiquetado de Azure.

## <a name="best-practice-implement-blueprints"></a>Procedimiento recomendado: implementación de planos técnicos

Del mismo modo que un plano técnico permite a un ingeniero o a un arquitecto bosquejar los parámetros de diseño de un proyecto, Azure Blueprints permite a los grupos de arquitectos de la nube y de TI central definir un conjunto repetible de recursos de Azure que implementa y cumple los estándares de la organización, sus requisitos y sus patrones. Con Azure Blueprints, los equipos de desarrollo pueden crear rápidamente nuevos entornos que cumplen los requisitos de cumplimiento de la organización y que contienen un conjunto de componentes integrados, como las redes, para acelerar el desarrollo y la entrega.

- Utilice planos técnicos para organizar la implementación de grupos de recursos, plantillas de Azure Resource Manager y asignaciones de roles y directivas.
- Los planos técnicos se almacenan en una base de datos de Azure Cosmos DB distribuida globalmente. Los objetos de plano técnico se replican en varias regiones de Azure. La replicación proporciona baja latencia, alta disponibilidad y acceso coherente al plano técnico, con independencia de la región en la que implementa los recursos un plano técnico.

**Más información:**

- [Más información](/azure/governance/blueprints/overview) sobre planos técnicos.
- [Consulte](https://azure.microsoft.com/blog/customizing-azure-blueprints-to-accelerate-ai-in-healthcare) un ejemplo de plano técnico para acelerar la inteligencia artificial en la sanidad.

## <a name="best-practice-review-azure-reference-architectures"></a>Procedimiento recomendado: revisión de las arquitecturas de referencia de Azure

Crear cargas de trabajo seguras, escalables y fáciles de administrar en Azure puede ser abrumador. Con los continuos cambios, puede resultar difícil mantenerse al día con las diferentes características para un entorno óptimo. Tener una referencia de la que aprender puede ser útil al diseñar y migrar las cargas de trabajo. Azure y sus asociados han desarrollado varias arquitecturas de referencia de ejemplo para varios tipos de entornos. Estos ejemplos están diseñados para proporcionar ideas para aprender y crear a partir de ellas.

Las arquitecturas de referencia están organizadas por escenario. Contienen procedimientos recomendados y consejos sobre administración, disponibilidad, escalabilidad y seguridad.
Azure App Service Environment proporciona un entorno completamente aislado y dedicado en el que ejecutar aplicaciones de App Service, incluidas aplicaciones web Windows y Linux, contenedores de Docker, aplicaciones móviles y funciones. App Service agrega a la aplicación las funcionalidades de Azure, con seguridad, equilibrio de carga, escalabilidad automática y administración automatizada. También puede sacar partido de sus funcionalidades de DevOps, por ejemplo, la implementación continua desde Azure DevOps y GitHub, la administración de paquetes, los entornos de ensayo, el dominio personalizado y los certificados SSL. App Service es útil para aplicaciones que necesitan aislamiento y acceso a la red seguro y para aquellas que consumen gran cantidad de memoria y otros recursos que necesiten escalado.

**Más información:**

- [Más información](/azure/architecture/reference-architectures) sobre las arquitecturas de referencia de Azure.
- [Consulte](/azure/architecture/example-scenario) los escenarios de ejemplo de Azure.

## <a name="best-practice-manage-resources-with-azure-management-groups"></a>Procedimiento recomendado: Administración de recursos con grupos de administración de Azure

Si la organización tiene varias suscripciones, deberá administrar el acceso, las directivas y su cumplimiento. Los grupos de administración de Azure proporcionan un nivel de ámbito por encima de las suscripciones.

- Las suscripciones se organizan en contenedores llamados grupos de administración, a los que se aplican las condiciones de gobernanza.
- Todas las suscripciones de un grupo de administración heredan automáticamente las condiciones del grupo de administración.
- Los grupos de administración proporcionan capacidad de administración de nivel empresarial a gran escala con independencia del tipo de suscripciones que tenga.
- Por ejemplo, puede aplicar una directiva de grupo de administración que limita las regiones en las que se pueden crear máquinas virtuales. Esta directiva se aplica a todos los grupos de administración, las suscripciones y los recursos de ese grupo de administración.
- Puede crear una estructura flexible de grupos de administración y suscripciones para organizar los recursos en una jerarquía para la administración unificada de las directivas y el acceso.

El siguiente diagrama muestra un ejemplo de creación de una jerarquía para la gobernanza mediante grupos de administración.

![Grupos de administración](./media/migrate-best-practices-security-management/management-groups.png)
*Management groups*

**Más información:**

- [Más información](/azure/governance/management-groups/index) acerca de la organización de recursos en grupos de administración.

## <a name="best-practice-deploy-azure-policy"></a>Procedimiento recomendado: implementación de Azure Policy

Azure Policy es un servicio de Azure que se usa para crear, asignar y administrar directivas.

- Las directivas aplican distintas reglas y efectos a los recursos, con el fin de que estos sigan siendo compatibles con los estándares corporativos y los acuerdos de nivel de servicio.
- Azure Policy evalúa los recursos y los examina en busca de los que no son compatibles con las directivas.
- Por ejemplo, podría crear una directiva que permita solo un tamaño específico de SKU para las máquinas virtuales del entorno. Azure Policy evaluará esta configuración al crear y actualizar los recursos y al buscar los recursos existentes.
- Azure proporciona algunas directivas integradas que puede asignar o bien puede crear las suyas propias.

![Azure Policy](./media/migrate-best-practices-security-management/policy.png)
*Azure Policy*

**Más información:**

- [Introducción](/azure/governance/policy/overview) a Azure Policy.
- [Más información](/azure/governance/policy/tutorials/create-and-manage) acerca de cómo crear y administrar directivas para exigir el cumplimiento.

## <a name="best-practice-implement-a-bcdr-strategy"></a>Procedimiento recomendado: implementación de una estrategia de BCDR

El planeamiento de la continuidad empresarial y recuperación ante desastres (BCDR) es un ejercicio crítico que se debe realizar como parte del proceso de planeación de la migración a Azure. En términos legales, los contratos incluyen una cláusula de fuerza mayor que exime de las obligaciones debidas a una fuerza mayor, como los huracanes o los terremotos. Sin embargo, también tiene obligaciones en torno a la capacidad para garantizar que los servicios seguirán en ejecución y se recuperarán en caso necesario cuando se produzca un desastre. La capacidad de hacer esto puede crear o interrumpir el futuro de su empresa.

En general, la estrategia de BCDR debe tener en cuenta:

- **Copia de seguridad de datos:** cómo mantener seguros los datos para una recuperación sencilla si se producen interrupciones.
- **Recuperación ante desastres:** cómo mantener las aplicaciones resistentes y disponibles si se producen interrupciones.

### <a name="set-up-bcdr"></a>Configuración de BCDR

Al migrar a Azure, es importante comprender que, aunque la plataforma Azure proporciona estas funcionalidades de resistencia integradas, debe diseñar la implementación en Azure para aprovechar las ventajas de las características y los servicios de Azure que proporcionan alta disponibilidad, recuperación ante desastres y copia de seguridad.

- La solución de BCDR dependerá de los objetivos de la empresa y estará influida por la estrategia de implementación en Azure. Las implementaciones de infraestructura como servicio (IaaS) y plataforma como servicio (PaaS) presentan diversos desafíos para BCDR.
- Una vez en funcionamiento, las soluciones de BCDR se deben probar con regularidad para comprobar que la estrategia sigue siendo viable.

### <a name="back-up-an-iaas-deployment"></a>Copia de seguridad de una implementación de IaaS

En la mayoría de los casos, una carga de trabajo local se retira tras la migración y la estrategia local para copias de seguridad se debe extender o reemplazar. Si migra todo el centro de datos a Azure, necesitará diseñar e implementar una solución de copia de seguridad completa con tecnologías de Azure o soluciones de terceros integradas.

Para cargas de trabajo que se ejecutan en máquinas virtuales de IaaS de Azure, tenga en cuenta estas soluciones de copia de seguridad:

- **Azure Backup:** proporciona copias de seguridad coherentes con la aplicación para máquinas virtuales Windows y Linux de Azure.
- **Instantáneas de almacenamiento:** tome instantáneas del almacenamiento de blobs.

#### <a name="azure-backup"></a>Azure Backup

Azure Backup crea puntos de recuperación de datos que se almacenan en Azure Storage. Azure Backup puede hacer una copia de seguridad de discos de máquina virtual de Azure y de Azure Files (versión preliminar). Azure Files proporciona recursos compartidos de archivos en la nube, accesibles mediante SMB.

Puede usar Azure Backup para realizar una copia de seguridad de las máquinas virtuales de varias maneras.

- **Copia de seguridad directa desde la configuración de la máquina virtual**: puede realizar copias de seguridad de máquinas virtuales con Azure Backup directamente desde las opciones de la máquina virtual en Azure Portal. Puede realizar una copia de seguridad de la máquina virtual una vez al día y restaurar el disco de la máquina virtual cuando sea necesario. Azure Backup toma instantáneas de datos basadas en la aplicación (VSS) y no se instala ningún agente en la máquina virtual.
- **Copia de seguridad directa en un almacén de Recovery Services**: puede realizar copias de seguridad de las máquinas virtuales de IaaS mediante la implementación de un almacén de Azure Backup Recovery Services. Esto proporciona una ubicación única para realizar el seguimiento y la administración de las copias de seguridad así como opciones de copia de seguridad y restauración pormenorizadas. La copia de seguridad se realiza hasta tres veces al día, en el nivel de archivo o carpeta. No son copias basadas en la aplicación y no es compatible con Linux. Instale el agente de Microsoft Azure Recovery Services (MARS) en cada máquina virtual de la que quiera realizar copias de seguridad mediante este método.
- **Protección de la máquina virtual en Azure Backup Server.** Azure Backup Server se proporciona de forma gratuita con Azure Backup. La máquina virtual se copia en el almacenamiento de Azure Backup Server local. A continuación, se copia Azure Backup Server en Azure en un almacén. Es una copia de seguridad basada en la aplicación, con una granularidad completa en la frecuencia y la retención de la copia de seguridad. Puede realizar una copia de seguridad en el nivel de la aplicación. Por ejemplo, la copia de seguridad de SQL Server o SharePoint.

Por motivos de seguridad, Azure Backup cifra los datos sobre la marcha con AES 256 y los envía mediante HTTPS a Azure. Los datos de la copia en reposo en Azure se cifran con [Storage Service Encryption (SSE)](/azure/storage/common/storage-service-encryption?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) y los datos de transmisión y almacenamiento.

![Azure Backup](./media/migrate-best-practices-security-management/iaas-backup.png)
*Azure Backup*

**Más información:**

- [Más información](/azure/backup/backup-introduction-to-azure-backup) sobre los diferentes tipos de copias de seguridad.
- [Planeación de una infraestructura de copia de seguridad](/azure/backup/backup-azure-vms-introduction) para máquinas virtuales de Azure.

#### <a name="storage-snapshots"></a>Instantáneas de almacenamiento

Las máquinas virtuales de Azure se almacenan como blobs en páginas en Azure Storage.

- Dichas instantáneas capturan el estado del blob en un momento específico del tiempo.
- Como un método de copia de seguridad alternativo para discos de máquina virtual de Azure, puede tomar una instantánea de los blobs de almacenamiento y copiarlos en otra cuenta de almacenamiento.
- Puede copiar un blob completo o utilizar una copia de instantánea incremental para copiar solo los cambios incrementales y reducir el espacio de almacenamiento.
- Como precaución adicional, puede habilitar la eliminación temporal para las cuentas de almacenamiento de blobs. Con esta característica habilitada, un blob que se elimina es marcado para su eliminación, pero no se purga inmediatamente. Durante el período transitorio, se puede restaurar el blob.

**Más información:**

- [Más información](/azure/storage/blobs/storage-blobs-introduction) acerca de Azure Blob Storage.
- [Más información](/azure/storage/blobs/storage-blob-snapshots) sobre cómo crear una instantánea de blob.
- [Consulte un escenario de ejemplo](https://azure.microsoft.com/blog/microsoft-azure-block-blob-storage-backup) para la copia de seguridad del almacenamiento de blobs.
- [Más información](/azure/storage/blobs/storage-blob-soft-delete) sobre la eliminación temporal.
- [Recuperación ante desastres y conmutación por error forzada (versión preliminar) en Azure Storage](/azure/storage/common/storage-disaster-recovery-guidance?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

#### <a name="third-party-backup"></a>Copia de seguridad de terceros

Además, puede usar soluciones de terceros para realizar copias de seguridad de máquinas virtuales de Azure y contenedores de almacenamiento en el almacenamiento local u otros proveedores en la nube. [Más información](https://azuremarketplace.microsoft.com/marketplace/apps?search=backup&page=1) sobre las soluciones de copia de seguridad de Azure Marketplace.

### <a name="set-up-disaster-recovery-for-iaas-apps"></a>Configuración de la recuperación ante desastres para aplicaciones de IaaS

Además de proteger los datos, la planeación de BCDR debe considerar cómo mantener las aplicaciones y las cargas de trabajo disponibles en caso de desastre. Para cargas de trabajo que se ejecutan en máquinas virtuales de IaaS de Azure y Azure Storage, tenga en cuenta estas soluciones:

#### <a name="azure-site-recovery"></a>Azure Site Recovery

Azure Site Recovery es el principal servicio de Azure para garantizar que las máquinas virtuales de Azure se pueden poner en línea y las aplicaciones de la máquina virtual estarán disponibles cuando se produzcan interrupciones.

Site Recovery replica las máquinas virtuales de una región principal en la región de Azure secundaria. Cuando se produce un desastre, se realiza una conmutación por error de las máquinas virtuales de la región primaria y el acceso a las mismas se produce con normalidad en la región secundaria. Cuando las operaciones vuelven al estado normal, puede realizar una conmutación por recuperación de las máquinas virtuales a la región primaria.

![Azure Site Recovery](./media/migrate-best-practices-security-management/site-recovery.png)

*Recuperación de sitios*

**Más información:**

- [Consulte](/azure/virtual-machines/virtual-machines-disaster-recovery-guidance) los escenarios de recuperación ante desastres para máquinas virtuales de Azure.
- [Más información](/azure/site-recovery/azure-to-azure-replicate-after-migration) sobre la configuración de la recuperación ante desastres de una máquina virtual de Azure tras la migración.

## <a name="best-practice-use-managed-disks-and-availability-sets"></a>Procedimiento recomendado: uso de discos administrados y conjuntos de disponibilidad

Azure usa conjuntos de disponibilidad para agrupar lógicamente las máquinas virtuales y para aislar las máquinas virtuales de un conjunto de otros recursos. Las máquinas virtuales de un conjunto de disponibilidad están repartidas entre varios dominios de error con subsistemas independientes para protegerse contra errores locales y también están repartidas entre varios dominios de actualización para que no se reinicien todas las máquinas virtuales de un conjunto al mismo tiempo.

Los discos administrados de Azure simplifican la administración de discos para las máquinas virtuales de IaaS de Azure, ya que administran las cuentas de almacenamiento asociadas a los discos de la máquina virtual.

- Se recomienda usar discos administrados siempre que sea posible. Solo tiene que especificar el tipo de almacenamiento que desea usar y el tamaño del disco que necesita y Azure crea y administra el disco automáticamente.
- Puede convertir discos existentes en administrados.
- Debe crear las máquinas virtuales en conjuntos de disponibilidad para alta resistencia y disponibilidad. Cuando se producen errores previstos e imprevistos, los conjuntos de disponibilidad garantizan que al menos una de las máquinas virtuales del conjunto sigue estando disponible.

![Discos administrados](./media/migrate-best-practices-security-management/managed-disks.png)

*Discos administrados*

**Más información:**

- [Introducción](/azure/virtual-machines/windows/managed-disks-overview) a los discos administrados.
- [Más información](/azure/virtual-machines/windows/convert-unmanaged-to-managed-disks) sobre cómo convertir discos en administrados.
- [Más información](/azure/virtual-machines/windows/manage-availability) sobre la administración de la disponibilidad de las máquinas virtuales Windows en Azure.

## <a name="best-practice-monitor-resource-usage-and-performance"></a>Procedimiento recomendado: supervisión del uso de recursos y el rendimiento

Puede que haya trasladado las cargas de trabajo a Azure por sus grandes funcionalidades de escalado. Sin embargo, el traslado de la carga de trabajo no significa que Azure implementará automáticamente el escalado sin la intervención del usuario. Por ejemplo:

- Si una organización de marketing inserta un nuevo anuncio de televisión que aumenta el tráfico en más de un 300%, esto podría provocar problemas de disponibilidad del sitio. La carga de trabajo recién migrada podría alcanzar los límites asignados y bloquearse.
- Otro ejemplo podría ser un ataque de denegación de servicio distribuido (DDoS) sobre la carga de trabajo migrada. En este caso no es probable que desee escalar, sino evitar que el origen de los ataques alcance los recursos.

Estos dos casos tienen resoluciones diferentes, pero en ambos se necesita información sobre lo que sucede con la supervisión del rendimiento y el uso.

- Azure Monitor puede ayudar a sacar estas métricas a la superficie y proporcionar respuesta con alertas, escalabilidad automática, centros de eventos, aplicaciones lógicas y mucho más.
- Además de la supervisión de Azure, puede integrar una aplicación de SIEM de terceros para supervisar los registros de Azure en busca de eventos de auditoría y rendimiento.

![Azure Monitor](./media/migrate-best-practices-security-management/monitor.png)
*Azure Monitor*

**Más información:**

- [Más información](/azure/azure-monitor/overview) acerca de Azure Monitor.
- [Procedimientos recomendados](/azure/architecture/best-practices/monitoring) para supervisión y diagnóstico.
- [Más información](/azure/architecture/best-practices/auto-scaling) sobre la escalabilidad automática.
- [Más información](/azure/security-center/security-center-export-data-to-siem) sobre cómo enrutar datos de Azure a una herramienta de SIEM.

## <a name="best-practice-enable-diagnostic-logging"></a>Procedimiento recomendado: Activación del registro de diagnóstico

Los recursos de Azure generan un número razonable de métricas de registro y datos de telemetría.

- De forma predeterminada, la mayoría de los tipos de recursos no tienen el registro de diagnóstico habilitado.
- Al habilitar el registro de diagnóstico en los recursos, puede consultar los datos de registro y crear alertas y cuadernos de estrategias en función de los mismos.
- Cuando se habilita el registro de diagnóstico, cada recurso tendrá un conjunto específico de categorías. Seleccione una o varias categorías de registro y una ubicación para los datos de registro. Los registros se pueden enviar a una cuenta de almacenamiento, un centro de eventos o a los registros de Azure Monitor.

![Registro de diagnóstico](./media/migrate-best-practices-security-management/diagnostics.png)
*Diagnostic logging*

**Más información:**

- [Más información](/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) sobre la recopilación y consumo de datos de registro.
- [Más información sobre lo que se admite](/azure/monitoring-and-diagnostics/monitoring-diagnostic-logs-schema) para el registro de diagnóstico.

## <a name="best-practice-set-up-alerts-and-playbooks"></a>Procedimiento recomendado: configuración de alertas y cuadernos de estrategias

Con el registro de diagnóstico habilitado para los recursos de Azure, puede empezar a usar los datos de registro para crear alertas personalizadas.

- Las alertas le informan de forma proactiva cuando se detectan condiciones en los datos que supervisa. A continuación, puede solucionar problemas antes de que los usuarios del sistema puedan experimentarlos. Puede alertar de aspectos tales como los valores de las métricas, las consultas de búsqueda de registros, los eventos del registro de actividad, el mantenimiento de la plataforma y la disponibilidad del sitio web.
- Cuando se desencadenan alertas, puede ejecutar un cuaderno de estrategias de aplicación lógica. Un cuaderno de estrategias le ayuda a automatizar y coordinar una respuesta a una alerta específica. Los cuadernos de estrategias se basan en Azure Logic Apps. Puede usar plantillas de aplicación lógica para crear cuadernos de estrategias o crear los suyos propios.
- Por ejemplo, puede crear una alerta que se desencadena cuando se produce un examen de puertos en un grupo de seguridad de red. Puede configurar un cuaderno de estrategias que se ejecuta y bloquea la dirección IP de origen del examen.
- Otro ejemplo podría ser una aplicación con una fuga de memoria. Cuando el uso de memoria llega a un punto determinado, un cuaderno de estrategias puede reciclar el proceso.

![Alertas](./media/migrate-best-practices-security-management/alerts.png)
*Alerts*

**Más información:**

- [Más información](/azure/monitoring-and-diagnostics/monitoring-overview-alerts) sobre las alertas.
- [Más información](/azure/security-center/security-center-playbooks) sobre cuadernos de estrategias de seguridad que responden a alertas de Security Center.

## <a name="best-practice-use-the-azure-dashboard"></a>Procedimiento recomendado: uso del panel de Azure

Azure Portal es una consola unificada basada en web que le permite crear, administrar y supervisar cualquier elemento, desde aplicaciones web sencillas a aplicaciones complejas en la nube. Incluye un panel personalizable y opciones de accesibilidad.

- Puede crear varios paneles y compartirlos con otras personas que tengan acceso a sus suscripciones de Azure.
- Con este modelo compartido, el equipo tiene visibilidad sobre el entorno de Azure, lo que les permite ser proactivos al administrar los sistemas en la nube.

![Panel de Azure](./media/migrate-best-practices-security-management/dashboard.png)
*Azure dashboard*

**Más información:**

- [Más información](/azure/azure-portal/azure-portal-dashboards) sobre cómo crear un panel.
- [Más información](/azure/azure-portal/azure-portal-dashboards-structure) sobre la estructura del panel.

## <a name="best-practice-understand-support-plans"></a>Procedimiento recomendado: información de los planes de soporte técnico

En algún momento necesitará colaborar con el personal de soporte técnico o el personal de soporte técnico de Microsoft. Es fundamental contar con un conjunto de directivas y procedimientos para obtener soporte técnico durante escenarios como la recuperación ante desastres. Además, se debe formar a los administradores y al personal de soporte técnico sobre la implementación de esas directivas.

- En el improbable caso de que un problema en un servicio de Azure afecte a la carga de trabajo, los administradores deben saber cómo enviar una incidencia de soporte técnico a Microsoft de la manera más adecuada y eficaz.
- Familiarícese con los diversos planes de soporte técnico que ofrece Azure. Abarcan desde tiempos de respuesta dedicados para instancias de Desarrollador hasta soporte técnico Premier con un tiempo de respuesta de menos de 15 minutos.

![Planes de soporte técnico](./media/migrate-best-practices-security-management/support.png)
*Support plans*

**Más información:**

- [Introducción](https://azure.microsoft.com/support/options) a los planes de soporte técnico de Azure.
- [Más información](https://azure.microsoft.com/support/legal/sla) sobre los Acuerdos de Nivel de Servicio (SLA).

## <a name="best-practice-manage-updates"></a>Procedimiento recomendado: Administración de actualizaciones

Mantener las máquinas virtuales de Azure actualizadas con el sistema operativo y las actualizaciones de software más recientes es una tarea rutinaria masiva. La capacidad de exponer todas las máquinas virtuales para determinar qué actualizaciones se necesitan y la inserción automática de esas actualizaciones son algo extremadamente valioso.

- Puede usar Update Management de Azure Automation para administrar las actualizaciones del sistema operativo de los equipos Windows y Linux implementados en Azure, en entornos locales o en otros proveedores en la nube.
- Utilice Update Management para evaluar rápidamente el estado de las actualizaciones disponibles en todos los equipos agente y administrar la instalación de las actualizaciones.
- Update Management se puede habilitar en máquinas virtuales directamente desde una cuenta de Azure Automation. También puede actualizar una sola máquina virtual en la página de la máquina virtual en Azure Portal.
- Además, se pueden registrar máquinas virtuales de Azure con System Center Configuration Manager. A continuación, podría migrar la carga de trabajo de Configuration Manager a Azure y realizar informes y actualizaciones de software desde una única interfaz web.

![Actualizaciones de máquinas virtuales](./media/migrate-best-practices-security-management/updates.png)
*Updates*

**Más información:**

- [Más información](/azure/automation/automation-update-management) sobre Update Management en Azure.
- [Más información](/azure/automation/oms-solution-updatemgmt-sccmintegration) sobre la integración de Configuration Manager con Update Management.
- [Preguntas más frecuentes](/sccm/core/understand/configuration-manager-on-azure) acerca de Configuration Manager en Azure.

## <a name="implement-a-change-management-process"></a>Implementación de un proceso de administración de cambios

Al igual que con cualquier sistema de producción, cualquier tipo de cambio puede afectar al entorno. Un proceso de administración de cambios que requiere que se envíen solicitudes para realizar cambios en los sistemas de producción es una adición valiosa en el entorno migrado.

- Puede crear marcos de procedimientos recomendados para la administración de cambios para aumentar el conocimiento de los administradores y personal de soporte técnico.
- Puede usar Azure Automation para ayudar con la administración de configuración y el seguimiento de cambios para los flujos de trabajo migrados.
- Al forzar el proceso de administración de cambios, puede usar los registros de auditoría para vincular los registros de cambios de Azure con las solicitudes de cambio supuestamente existentes (o no). Por lo que, si ve un cambio realizado sin una solicitud de cambio correspondiente, puede investigar qué salió mal en el proceso.

Azure tiene una solución de seguimiento de cambios en Azure Automation:

- La solución realiza un seguimiento de los cambios efectuados en el software de Windows y Linux, en los archivos y las claves del Registro de Windows, en los servicios de Windows y en los demonios de Linux.
- Los cambios en los servidores supervisados se envían al servicio Azure Monitor en la nube para su procesamiento.
- Se aplica la lógica a los datos recibidos y el servicio de nube registra los datos.
- En el panel de Change Tracking, puede ver fácilmente los cambios realizados en la infraestructura de servidores.

![Administración de cambios](./media/migrate-best-practices-security-management/change.png)
*Change management*

**Más información:**

- [Más información](/azure/automation/automation-change-tracking) sobre Change Tracking.
- [Más información](/azure/automation/automation-intro) sobre las funcionalidades de Azure Automation.

## <a name="next-steps"></a>Pasos siguientes

Examine otros procedimientos recomendados:

- [Procedimientos recomendados](migrate-best-practices-networking.md) para las redes después de la migración.
- [Procedimientos recomendados](migrate-best-practices-costs.md) para la administración de costos después de la migración.
