---
title: Protección y administración
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Protección y administración
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 7d742242f2639708914927aedbf45d1c59020c7d
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818734"
---
# <a name="secure-and-manage"></a>Proteger y administrar

Después de migrar el entorno a Azure, es importante tener en cuenta la seguridad y los métodos que se usan para administrar el entorno. Azure proporciona muchas características y funcionalidades para satisfacer estas necesidades en la solución.

# <a name="azure-monitortabmonitor"></a>[Azure Monitor](#tab/monitor)

Azure Monitor maximiza la disponibilidad y el rendimiento de las aplicaciones con una completa solución que permite recopilar, analizar y administrar datos telemétricos tanto en la nube como en entornos locales. Esta solución le ayudará a entender cómo funcionan las aplicaciones y le permitirá identificar de manera proactiva los problemas que les afectan y los recursos de los que dependen.

## <a name="use-and-configure-azure-monitor"></a>Uso y configuración de Azure Monitor

1. Vaya a **Supervisar** en Azure Portal.
2. Seleccione **Métricas**, **Registros** o **Estado del servicio** para ver información general al respecto.
3. Seleccione cualquier información pertinente.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview]" submitText="Go to Azure Monitor" :::

::: zone-end

::: zone target="docs"

## <a name="read-more"></a>Más información

- [Introducción a Azure Monitor](/azure/azure-monitor/overview).

::: zone-end

# <a name="azure-service-healthtabservicehealth"></a>[Azure Service Health](#tab/servicehealth)

Azure Service Health le proporciona orientación y soporte técnico personalizados cuando le afectan los problemas de los servicios de Azure. Puede enviarle notificaciones, ayudarle a conocer el impacto de los problemas y mantenerle actualizado con respecto a la actualización del problema. También le puede ayudar a preparar las operaciones de mantenimiento y los cambios planeados que podrían afectar a la disponibilidad de sus recursos.

Azure Service Health incluye:

- **Estado de Azure**: una vista global del estado de los servicios de Azure.
- **Estado del servicio**: una vista personalizada del estado de los servicios de Azure.
- **Estado de los recursos**: una vista más detallada del estado de los recursos individuales que aprovisionan los servicios de Azure.

En combinación, estas experiencias ofrecen una vista completa del estado de Azure, con un nivel de detalle importante para usted.

## <a name="access-service-health"></a>Acceso a Service Health

1. Vaya a **Supervisar** en Azure Portal.
2. Seleccione **Service Health**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/serviceIssues]" submitText="Go to Service Health" :::

::: zone-end

::: zone target="docs"

## <a name="read-more"></a>Más información

Para más información, consulte la [documentación de Azure Service Health](/azure/service-health).

::: zone-end

# <a name="azure-advisortabadvisor"></a>[Azure Advisor](#tab/advisor)

Asistente de Azure es un consultor en la nube personalizado que le ayudará a realizar procedimientos recomendadas para optimizar las implementaciones de Azure. Analiza la telemetría de uso y configuración de los recursos y, posteriormente, recomienda soluciones que ayudan a mejorar el rendimiento, la seguridad y la alta disponibilidad de los recursos, al mismo tiempo que busca oportunidades para reducir el gasto general de Azure.

## <a name="access-azure-advisor"></a>Acceso a Azure Advisor

1. Vaya a **Advisor** en Azure Portal o busque el recurso.
2. Seleccione **Alta disponibilidad**, **Securidad**, **Rendimiento**, **Costo**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Expert/AdvisorMenuBlade/overview]" submitText="Go to Azure Advisor" :::

::: zone-end

::: zone target="docs"

## <a name="read-more"></a>Más información

[Información general](/azure/advisor/advisor-overview).

::: zone-end

# <a name="azure-security-centertabsecurity"></a>[Azure Security Center](#tab/security)

Azure Security Center es un sistema unificado de administración de seguridad de la infraestructura que fortalece la posición de seguridad de los centros de datos y proporciona una protección contra amenazas avanzada de todas las cargas de trabajo híbridas que se encuentran en la nube&mdash;ya sea que estén en Azure o no&mdash;así como también en el entorno local.

## <a name="access-azure-security-center"></a>Uso de Azure Security Center

1. Vaya al **Centro de seguridad** de Azure Portal o busque el recurso.
2. Seleccione **Recomendaciones**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/0]" submitText="Go to Security Center" :::

::: zone-end

::: zone target="docs"

## <a name="read-more"></a>Más información

[Información general](/azure/security-center/security-center-intro)

::: zone-end

# <a name="azure-backuptabbackup"></a>[Azure Backup](#tab/backup)

Azure Backup es el servicio de Azure que puede usar para hacer una copia de seguridad de los datos (protegerlos) y restaurarlos en Microsoft Cloud. Azure Backup reemplaza su solución de copia de seguridad local o remota existente por una solución confiable, segura y rentable basada en la nube.

## <a name="enable-backup-for-an-azure-vm"></a>Habilitación de la copia de seguridad de una máquina virtual de Azure

1. En Azure Portal, seleccione **Máquinas virtuales** y la máquina virtual que desea replicar.
1. En **Operaciones**, seleccione **Copia de seguridad**.
1. Cree un almacén de Recovery Services o seleccione uno existente.
1. Seleccione **Crear una nueva directiva (o editar una)** .
1. Configure la programación y el período de retención.
1. Seleccione **Aceptar**.
1. Seleccione **Habilitar copia de seguridad**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

[Información general](/azure/backup/backup-introduction-to-azure-backup)

::: zone-end

# <a name="azure-site-recoverytabsiterecovery"></a>[Azure Site Recovery](#tab/siterecovery)

Anteriormente en esta guía, analizamos cómo se puede usar Azure Site Recovery como parte de la ejecución de la migración. Pero también forma parte de un componente crítico en la estrategia de recuperación ante desastres una vez que se completa la migración.

El servicio Azure Site Recovery le permite replicar máquinas virtuales y cargas de trabajo hospedadas en una región primaria de Azure en una copia hospedada en una región secundaria. Cuando se produce una interrupción en la región primaria, puede conmutar por error en la copia que se ejecuta en la región secundaria y seguir accediendo a sus aplicaciones y servicios desde allí. Una vez que se soluciona la interrupción en la copia primaria de la máquina virtual, puede conmutar por recuperación en ella.

## <a name="replicate-an-azure-vm-to-another-region-with-site-recovery-service"></a>Replicación de una máquina virtual de Azure en otra región con el servicio Site Recovery

En los pasos siguientes se describe el proceso para usar Site Recovery servicio para replicar una máquina virtual de Azure en otra región (de Azure a Azure):

>
> [!TIP]
> Los pasos exactos pueden diferir ligeramente según el escenario.
>

## <a name="enable-replication-for-the-azure-vm"></a>Habilitación de la replicación para la máquina virtual de Azure

1. En Azure Portal, seleccione **Máquinas virtuales** y la máquina virtual que desea replicar.
1. En **Operaciones**, seleccione **Recuperación ante desastres**.
1. En **Configurar recuperación ante desastres** > **Región de destino**, seleccione la región de destino en la que quiere realizar la replicación.
1. En esta guía de inicio rápido, acepte los restantes valores predeterminados.
1. Seleccione **Habilitar replicación**. Esto inicia un trabajo para habilitar la replicación de la máquina virtual.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

## <a name="verify-settings"></a>Comprobación de la configuración

Cuando haya finalizado el trabajo de replicación, puede comprobar el estado de la replicación y probar la implementación.

1. En el menú de la máquina virtual, seleccione **Recuperación ante desastres**.
2. Compruebe el estado de la replicación, los puntos de recuperación que se crearon y las regiones de origen y destino en el mapa.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Compute%2FVirtualMachines]" submitText="Go to Virtual Machines" :::

::: zone-end

::: zone target="docs"

## <a name="learn-more"></a>Más información

- [Información general sobre Azure Site Recovery](/azure/site-recovery/site-recovery-overview)
- [Replicación de una máquina virtual de Azure en otra región](/azure/site-recovery/azure-to-azure-quickstart)

::: zone-end
