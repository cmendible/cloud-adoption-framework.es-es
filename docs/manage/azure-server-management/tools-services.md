---
title: Servicios y herramientas de administración de servidores de Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Servicios y herramientas de administración de servidores de Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: dbb00a411eb7905ad557e1acdc2a98d4d03cff49
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221424"
---
# <a name="azure-server-management-tools-and-services"></a>Servicios y herramientas de administración de servidores de Azure

Como se describe en la [introducción](./index.md) de esta sección, el conjunto de servicios de administración de servidores de Azure cubre estas áreas:

- [Migrar](#migrate)
- [Protección](#secure)
- [Protección](#protect)
- [Supervisión](#monitor)
- [Configuración](#configure)
- [Gobernanza](#govern)

En las secciones siguientes se describen sucintamente estas áreas de administración y se proporcionan vínculos a información detallada acerca de los principales servicios de Azure compatibles con ellas.

## <a name="migrate"></a>Migrar

Los servicios de migración pueden ayudarle a migrar sus cargas de trabajo a Azure. Para proporcionar la mejor orientación, el servicio Azure Migrate comienza midiendo el rendimiento del servidor local y evaluando la idoneidad para la migración. Una vez que Azure Migrate completa la evaluación, puede usar [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) y [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview) para migrar las máquinas locales a Azure.

## <a name="secure"></a>Seguridad

[Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) es una aplicación de administración de seguridad completa. Al incorporarse a Security Center, puede obtener rápidamente una evaluación de la seguridad y el estado de cumplimiento normativo de su entorno. Para obtener instrucciones sobre la incorporación de los servidores a Azure Security Center, consulte [Configuración de los servicios de administración de Azure para una suscripción](./onboard-at-scale.md#azure-security-center).

## <a name="protect"></a>Protección

Para proteger los datos, debe planear la copia de seguridad, la alta disponibilidad, el cifrado, la autorización y los problemas operativos relacionados. Estos temas se tratan ampliamente en línea, por lo que aquí nos centraremos en la creación de un plan de continuidad empresarial y recuperación ante desastres (BCDR). Incluiremos referencias a la documentación que describe en detalle cómo implementar este tipo de plan.

Cuando crea estrategias de protección de datos, antes debe considerar la posibilidad de dividir las aplicaciones de carga de trabajo en sus distintos niveles, porque por lo general cada nivel requiere su propio plan de protección único. Para obtener más información sobre el diseño de las aplicaciones para que sean resistentes, consulte [Diseño de aplicaciones resistentes para Azure](https://docs.microsoft.com/azure/architecture/resiliency).

La protección de datos más básica es la copia de seguridad. Para acelerar el proceso de recuperación en caso de pérdida del servidor, debe hacer una copia de seguridad no solo de los datos sino también de las configuraciones de servidor. La copia de seguridad es un mecanismo eficaz para controlar la eliminación accidental de datos y los ataques de ransomware. [Azure Backup](https://docs.microsoft.com/azure/backup) puede ayudarle a proteger los datos en Azure y en los servidores locales que ejecutan Windows o Linux. Para obtener más información sobre las funcionalidades de este servicio y acceder a procedimientos, consulte la [documentación de Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview).

La recuperación a través de una copia de seguridad puede tardar mucho tiempo. El estándar del sector suele ser un día. Si una carga de trabajo requiere continuidad empresarial ante errores de hardware o una interrupción del centro de datos, considere la posibilidad de usar la replicación de datos. [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) proporciona una replicación continua de las máquinas virtuales, una solución que proporciona una pérdida mínima de datos. Site Recovery también admite varios escenarios de replicación, como la replicación de máquinas virtuales de Azure entre dos regiones de Azure, entre servidores locales y entre el entorno local y Azure. Para más información, consulte la [matriz completa de replicación de Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview#what-can-i-replicate).

En el caso de los datos del servidor de archivos, otro servicio que se puede tener en cuenta es [Azure File Sync](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning). Este servicio permite centralizar los recursos compartidos de archivos de su organización en Azure Files sin renunciar a la flexibilidad, el rendimiento y la compatibilidad de un servidor de archivos local. Para usar este servicio, siga las instrucciones para implementar Azure File Sync.

## <a name="monitor"></a>Supervisión

[Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) proporciona una vista de varios recursos, como aplicaciones, contenedores y máquinas virtuales. También recopila datos de varios orígenes.

- Azure Monitor para VM ([información](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)) proporciona una visión detallada del estado, las tendencias de rendimiento y las dependencias de las máquinas virtuales. El servicio supervisa el estado del sistema operativo de las máquinas virtuales de Azure, los conjuntos de escalado de máquinas virtuales y las máquinas en el entorno local.
- Log Analytics ([registros](https://docs.microsoft.com/azure/azure-monitor/platform/data-collection#logs)) es una característica de Azure Monitor. Su rol es fundamental para la función global de administración de Azure. Sirve como almacén de datos para el análisis de registros y para muchos otros servicios de Azure. Ofrece un lenguaje de consulta completo y un motor de análisis que proporciona información sobre el funcionamiento de las aplicaciones y los recursos.
- El [registro de actividad de Azure](https://docs.microsoft.com/azure/azure-monitor/platform/activity-logs-overview) es también una característica de Azure Monitor. Proporciona información sobre los eventos de nivel de suscripción que se producen en Azure.

## <a name="configure"></a>Configuración

En esta categoría se ajustan varios servicios. Pueden ayudarle a automatizar las tareas operativas, administrar configuraciones de servidores, medir el cumplimiento de las actualizaciones, programar actualizaciones y detectar cambios en los servidores. Estos servicios son esenciales para la compatibilidad con las operaciones en curso.

- [Update Management](https://docs.microsoft.com/azure/automation/automation-update-management#viewing-update-assessments) automatiza la implementación de revisiones en el entorno, incluida la implementación en instancias del sistema operativo que se ejecutan fuera de Azure. Es compatible con sistemas operativos Windows y Linux, y realiza un seguimiento de las vulnerabilidades clave del sistema operativo y el incumplimiento provocados por la falta de revisiones.
- [Change Tracking e Inventario](https://docs.microsoft.com/azure/automation/change-tracking) proporciona información sobre el software que se ejecuta en el entorno y permite ver los cambios que se han producido.
- [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) permite ejecutar scripts o runbooks de Python y PowerShell para automatizar tareas en el entorno. Cuando se usa con [Hybrid Runbook Worker](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker), también se pueden ampliar los runbooks a los recursos locales.
- [Azure Automation State Configuration](https://docs.microsoft.com/azure/automation/automation-dsc-overview) permite insertar configuraciones de Desired State Configuration (DSC) de PowerShell directamente desde Azure. A su vez, DSC permite supervisar y conservar las configuraciones del sistema operativo invitado y de la carga de trabajo.

## <a name="govern"></a>Control

La adopción de la nube y el traslado a ella crea nuevos desafíos de administración y requiere una mentalidad diferente a medida que pasa de la carga de una administración operativa a la supervisión y la gobernanza. Cloud Adoption Framework para Azure comienza con la [gobernanza](../../govern/index.md). En ella se explica cómo migrar a la nube, cómo será el recorrido y quién debe estar implicado.

El diseño de la gobernanza para organizaciones estándar es, a menudo, diferente del de las empresas complejas. Para más información sobre los procedimientos recomendados de gobernanza para una organización estándar, consulte [Guía de gobernanza estándar](../../govern/guides/standard/index.md). Para más información sobre los procedimientos recomendados de gobernanza para una empresa compleja, consulte [Guía de gobernanza para empresas complejas](../../govern/guides/complex/index.md).

## <a name="billing-information"></a>Información de facturación

Para obtener información sobre los precios de los servicios de administración de Azure, vaya a estas páginas:

- [Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery)

- [Azure Backup](https://azure.microsoft.com/pricing/details/backup)

- [Azure Monitor](https://azure.microsoft.com/pricing/details/monitor)

- [Azure Security Center](https://azure.microsoft.com/pricing/details/security-center)

- [Azure Update Management](https://azure.microsoft.com/pricing/details/automation)

- [Azure Change Tracking e Inventario](https://azure.microsoft.com/pricing/details/automation)

- [Desired State Configuration](https://azure.microsoft.com/pricing/details/automation)

- [Azure Automation](https://azure.microsoft.com/pricing/details/automation)

- [Azure Policy](https://azure.microsoft.com/pricing/details/azure-policy)

- [Azure File Sync](https://azure.microsoft.com/pricing/details/storage/blobs)

> [!NOTE]
> La solución Azure Update Management es gratuita, pero hay un pequeño costo relacionado con la ingesta de datos. Como regla general, los primeros 5 GB al mes de ingesta de datos son gratuitos. Hemos observado que habitualmente cada equipo usa unos 25 MB al mes. Por lo tanto, se incluyen de forma gratuita 200 máquinas al mes. Para cada servidor adicional, multiplique el número de servidores adicionales por 25 MB al mes. Multiplique esto por el costo de almacenamiento para la cantidad total de almacenamiento necesaria. [Los costos de almacenamiento están disponibles aquí](https://azure.microsoft.com/pricing/details/storage). Cada servidor adicional debe tener un impacto nominal en el costo.
