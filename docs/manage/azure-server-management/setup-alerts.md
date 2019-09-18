---
title: Configuración de alertas básicas
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Configuración de alertas básicas
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 5b11a97e78d5fcd1b2a2cc866f5a7062bc6a2977
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032301"
---
# <a name="set-up-basic-alerts"></a>Configuración de alertas básicas

Una parte clave de la administración de recursos es la recepción de notificaciones cuando se producen problemas; las alertas le notifican proactivamente de las condiciones críticas. Pueden basarse en desencadenadores a partir de métricas, registros o problemas de estado del servicio. Como parte de la incorporación a los servicios de administración de servidores de Azure, puede configurar alertas y notificaciones que ayuden a los equipos de TI a mantenerse informados de los problemas que se produzcan.

## <a name="azure-monitor-alerts"></a>Alertas de Azure Monitor

Azure Monitor ofrece funcionalidades de [alerta](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview) para enviar notificaciones por correo electrónico o mensajería cuando se producen errores. Estas funcionalidades se basan en una plataforma común de supervisión de datos que incluye registros y métricas generados por los servidores y otros recursos. Esta plataforma permite analizar los datos combinados procedentes de varios recursos mediante un conjunto común de herramientas en Azure Monitor, que puede usar para desencadenar alertas. Estos desencadenadores pueden incluir:

- Valores de métrica
- Consultas de búsqueda de registros
- Eventos del registro de actividad
- Estado de la plataforma Azure subyacente
- Pruebas de disponibilidad del sitio web

Consulte la [lista de orígenes de datos de Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/data-sources) para obtener una descripción más detallada de los orígenes de los datos de supervisión que recopila este servicio.

Para más información sobre la creación y la administración manuales de alertas mediante el portal, consulte la [documentación de Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric).

## <a name="automated-deployment-of-recommended-alerts"></a>Implementación automatizada de alertas recomendadas

En esta guía se recomienda habilitar un conjunto de 15 alertas para la supervisión básica de la infraestructura. Puede encontrar los scripts de implementación en el [kit de herramientas de alerta de Azure del repositorio de GitHub](https://github.com/Microsoft/manageability-toolkits).

Este paquete crea alertas para advertir sobre poco espacio en disco, poca memoria disponible, uso intensivo de la CPU, apagados inesperados, sistemas de archivos dañados y errores de hardware comunes. El paquete usa hardware de servidor de HP como ejemplo. Debe cambiar la configuración del archivo de configuración asociado para reflejar su hardware OEM. También puede agregar más contadores de rendimiento al archivo de configuración. Para implementar el paquete, ejecute el archivo New-CoreAlerts.ps1.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información sobre las operaciones y los mecanismos de seguridad que admiten las operaciones en curso.

> [!div class="nextstepaction"]
> [Administración y seguridad en curso](./ongoing-management-overview.md)
