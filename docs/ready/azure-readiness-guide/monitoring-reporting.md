---
title: Supervisión e informes en Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Aprenda a configurar la supervisión, los informes y las alertas para el entorno de administración de Azure.
author: timleyden
ms.author: tileyden
ms.date: 04/09/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: dc2df86dae7e820527d5f4b1d26fa69366b55b59
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022073"
---
# <a name="monitoring-and-reporting-in-azure"></a>Supervisión e informes en Azure

Azure proporciona muchos servicios que ofrecen una solución completa para recopilar, analizar y actuar en la telemetría de la aplicación y los recursos de Azure que las admiten. Además, estos recursos se pueden ampliar para que incluyan la supervisión de recursos locales críticos para proporcionar un entorno de supervisión híbrido.

# <a name="azure-monitortabazuremonitor"></a>[Azure Monitor](#tab/AzureMonitor)

Azure Monitor proporciona un único centro unificado para todos los datos de supervisión y diagnóstico en Azure. Puede usarlo para obtener visibilidad sobre los recursos. Con Azure Monitor, puede buscar y corregir problemas y optimizar el rendimiento. También puede comprender el comportamiento de los clientes.

- **Supervise y visualice las métricas:** las métricas son valores numéricos que están disponibles en los recursos de Azure que le ayudan a comprender el estado de los sistemas. Personalice los gráficos de los paneles y use los libros para los informes.

- **Consulte y analice los registros:** los registros incluyen los registros de actividad y los registros de diagnóstico de Azure. Recopile registros adicionales de otras soluciones de supervisión y administración para los recursos de nube o locales. Log Analytics proporciona un repositorio central para agregar todos estos datos. Desde allí, puede ejecutar consultas para ayudar a solucionar problemas o para visualizar los datos.

- **Configure alertas y acciones:** las alertas le notifican proactivamente de las condiciones críticas. Las acciones correctivas se pueden tomar basándose en los desencadenadores de las métricas, los registros o los problemas de estado del servicio. Puede configurar diferentes notificaciones y acciones, y enviar datos a las herramientas de administración de servicios de TI.

::: zone target="docs"

 Comience a supervisar lo siguiente:

- [Aplicaciones](https://docs.microsoft.com/azure/application-insights/app-insights-overview)
- [Contenedores](https://docs.microsoft.com/azure/monitoring/monitoring-container-overview)
- [Máquinas virtuales](https://docs.microsoft.com/azure/monitoring/monitoring-service-map)
- [Redes](https://docs.microsoft.com/azure/networking/network-monitoring-overview)

Para supervisar otros recursos, busque soluciones adicionales en Azure Marketplace.

Para explorar Azure Monitor, vaya a [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview).

## <a name="learn-more"></a>Más información

Para más información, consulte [Documentación sobre Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics).

::: zone-end

::: zone target="chromeless"

## <a name="action"></a>.

::: form action="OpenBlade[#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/overview]" submitText="Explore Azure Monitor" :::

::: zone-end

# <a name="azure-service-healthtabazureservicehealth"></a>[Azure Service Health](#tab/AzureServiceHealth)

Azure Service Health proporciona una vista personalizada del estado de los servicios y regiones de Azure que se usan. La información acerca de los problemas activos se publica en Service Health lo cual le ayudará a comprender el impacto de estos en los recursos. Las actualizaciones periódicas le mantendrán informado sobre la resolución del problema.

También se publican los eventos de mantenimiento planeado en Service Health para proporcionarle información sobre los cambios que podrían afectar a la disponibilidad de los recursos. Configure alertas de Service Health para que le envíen notificaciones cuando se produzcan problemas del servicio, mantenimientos planeados o cualquier otro cambio que pueda afectar a los servicios y regiones de Azure que usa.

Azure Service Health incluye:

- **Estado de Azure:** una vista global del estado de los servicios de Azure.
- **Estado del servicio:** una vista personalizada del estado de los servicios de Azure.
- **Estado de los recursos:** una vista más detallada del estado de cada uno de los recursos individuales.

::: zone target="chromeless"

<!-- markdownlint-disable MD024 -->

## <a name="action"></a>.

Para configurar una alerta de Service Health:

1. Vaya a **Service Health**.
2. Seleccione **Alertas de estado**.
3. Cree una alerta de estado del servicio.

::: form action="OpenBlade[#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts]" submitText="Go to Service Health" :::

::: zone-end

::: zone target="docs"

Para configurar una alerta de Service Health, vaya a [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Health/AzureHealthBrowseBlade/healthalerts).

## <a name="learn-more"></a>Más información

Para más información, consulte la [documentación de Azure Service Health](https://docs.microsoft.com/azure/service-health).

::: zone-end

# <a name="azure-advisortabazureadvisor"></a>[Azure Advisor](#tab/AzureAdvisor)

Azure Advisor es un consultor gratuito y personalizado en la nube que le ayuda a seguir e implementar los procedimientos recomendados para las implementaciones de Azure. Analiza la configuración de los recursos y la telemetría de uso y luego recomienda soluciones que pueden ayudarlo a optimizar el entorno. Las recomendaciones se dividen en cuatro categorías:

- **Alta disponibilidad:** para mejorar la continuidad de las aplicaciones críticas para la empresa. Las recomendaciones pueden incluir la adición de máquinas virtuales a un conjunto de disponibilidad o la adición de puntos de conexión con redundancia geográfica.
- **Seguridad:** ayuda a detectar amenazas y vulnerabilidades que podrían dar lugar a infracciones de seguridad. Las recomendaciones pueden incluir la aplicación de cifrado de disco o la habilitación de grupos de seguridad de red.
- **Rendimiento:** ayuda a mejorar la velocidad de las aplicaciones. Las recomendaciones pueden incluir el aumento del rendimiento de las consultas SQL mediante la creación de índices o la reconfiguración de los valores del administrador de tráfico.
- **Costo:** ayuda a optimizar y reducir el gasto general de Azure. Las recomendaciones pueden incluir el cambio de tamaño o el apagado de máquinas virtuales poco usadas o el cambio a reservas de Azure para reducir el costo total de propiedad.

Las recomendaciones de Advisor se basan en los recursos que se implementan y en las acciones que se realizan en Azure. Puede consultar regularmente Advisor para conocer las últimas recomendaciones.

::: zone target="chromeless"

## <a name="action"></a>.

::: form action="OpenBlade[#blade/Microsoft_Azure_Expert/AdvisorBlade]" submitText="Explore Azure Advisor" :::

::: zone-end

::: zone target="docs"

Para explorar Azure Advisor, vaya a [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Expert/AdvisorBlade).

## <a name="learn-more"></a>Más información

Para más información, consulte [Documentación de Azure Advisor](https://docs.microsoft.com/azure/advisor).

::: zone-end

# <a name="azure-security-centertabazuresecuritycenter"></a>[Azure Security Center](#tab/AzureSecurityCenter)

Azure Security Center también desempeña un papel importante en su estrategia de supervisión. Le permite supervisar la seguridad de las máquinas, las redes, el almacenamiento, los servicios de datos y las aplicaciones. Security Center proporciona detección de amenazas avanzada mediante análisis del comportamiento y aprendizaje automático para ayudar a identificar las amenazas activas dirigidas a los recursos de Azure. También proporciona protección contra amenazas que bloquea el malware u otro código no deseado y reduce la superficie expuesta a los ataques por fuerza bruta y a otros ataques a la red.

Cuando Security Center identifica una amenaza, desencadena una alerta de seguridad con los pasos que debe seguir para responder a un ataque. También proporciona un informe con datos sobre la amenaza detectada.

Azure Security Center se ofrece en dos niveles: gratis y estándar. Características como las recomendaciones de seguridad están disponibles gratis. El nivel estándar proporciona protección adicional, como detección de amenazas avanzada y protección en las cargas de trabajo de nube híbrida.

::: zone target="chromeless"

## <a name="action"></a>.

**Pruebe el nivel estándar gratis durante los primeros 30 días.**

Después de activar y configurar directivas de seguridad para los recursos de una suscripción, puede ver el estado de seguridad de los recursos y cualquier problema en la sección **Prevención**. Una lista de dichos problemas también se puede encontrar en el icono **Recomendaciones**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0]" submitText="Explore Azure Security Center" :::

::: zone-end

::: zone target="docs"

Para explorar Azure Security Center, vaya a [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0).

## <a name="learn-more"></a>Más información

Para más información, consulte la [documentación de Azure Security Center](https://docs.microsoft.com/azure/security-center).

::: zone-end
