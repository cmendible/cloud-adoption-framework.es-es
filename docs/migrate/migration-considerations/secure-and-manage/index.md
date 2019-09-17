---
title: Protección y administración
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Protección de las herramientas de administración y supervisión
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 652637905f9de09972eed199f85245e99fb60e29
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022586"
---
# <a name="secure-monitoring-and-management-tools"></a>Protección de las herramientas de administración y supervisión

Una vez completada la migración, los recursos migrados deben administrarse mediante operaciones de TI controladas. Este artículo no pretende sugerir una desviación de los procedimientos recomendados. Por el contrario, lo siguiente debe considerarse como un producto mínimamente viable para la protección y administración de los recursos migrados, ya sea desde las operaciones de TI o de forma independiente cuando estas operaciones se conecten.

## <a name="monitoring"></a>Supervisión

La *supervisión* es el acto de recopilar y analizar datos para determinar el rendimiento, el mantenimiento y la disponibilidad de su carga de trabajo empresarial y de los recursos de los que esta depende. Azure incluye varios servicios que realizan individualmente una tarea o un rol específico en el espacio de supervisión. Juntos, estos servicios ofrecen una solución completa para recopilar, analizar y actuar en la telemetría de las aplicaciones de la carga de trabajo y los recursos de Azure que las admiten. Obtenga visibilidad sobre el estado de mantenimiento y el rendimiento de sus aplicaciones, infraestructura y datos en Azure con herramientas de supervisión en la nube como Azure Monitor, Log Analytics y Application Insights. Use estas herramientas de supervisión en la nube para tomar medidas e intégrelas con sus soluciones de administración de servicios:

- **Supervisión básica.** La supervisión básica proporciona el control fundamental requerido de los recursos de Azure. Estos servicios requieren una configuración mínima y recopilan la telemetría principal que usan los servicios de supervisión premium.
- **Supervisión profunda de la aplicación y la infraestructura.** Los servicios de Azure proporcionan funcionalidades enriquecidas para recopilar y analizar datos de supervisión en profundidad. Estos servicios se basan en la supervisión básica y aprovechan las funcionalidades comunes de Azure. Proporcionan análisis eficaces con los datos recopilados y le ofrecen información única sobre sus aplicaciones e infraestructura.

Obtenga más información sobre [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) para la supervisión de los recursos migrados.

## <a name="security-monitoring"></a>Supervisión de la seguridad

Confíe en Azure Security Center para lograr una supervisión unificada de la seguridad y obtener notificaciones de amenazas avanzadas de las cargas de trabajo de su nube híbrida. Security Center aporta visibilidad total y control sobre la seguridad de sus aplicaciones en la nube de Azure. Detecte posibles amenazas y tome medidas con rapidez, y reduzca su exposición mediante la protección contra amenazas adaptable. El panel integrado proporciona información instantánea sobre alertas de seguridad y vulnerabilidades que requieren atención. Azure Security Center puede ayudarle con muchas funciones, incluidas:

- **Supervisión centralizada de directivas.** Garantice el cumplimiento de los requisitos de seguridad normativos o de la empresa administrando las directivas de seguridad de forma centralizada de las cargas de trabajo en la nube híbridas.
- **Evaluación continua de la seguridad.** Supervise la seguridad de máquinas, redes, almacenamiento y servicios de datos y aplicaciones para detectar posibles problemas de seguridad.
- **Recomendaciones prácticas.** Corrija las vulnerabilidades de seguridad antes de que los atacantes se aprovechen. Incluya recomendaciones de seguridad prácticas y prioritarias.
- **Defensas avanzadas en la nube.** Reduzca las amenazas con acceso Just-In-Time a los puertos de administración y la creación de listas seguras para controlar las aplicaciones que se ejecutan en las máquinas virtuales.
- **Alertas e incidentes clasificados por orden de prioridad.** Céntrese primero en las amenazas más críticas con la clasificación en orden de prioridad de las alertas e incidentes de seguridad.
- **Soluciones de seguridad integradas.** Recopile, busque y analice datos de seguridad de una gran variedad de orígenes, incluidas las soluciones conectadas de los asociados.

Obtenga más información sobre [Azure Security Center](https://docs.microsoft.com/azure/security-center) para la protección de los recursos migrados.

## <a name="protect-assets-and-data"></a>Protección de recursos y datos

Azure Backup proporciona un medio de protección de las máquinas virtuales, archivos y datos. Azure Backup puede ayudarle con muchas funciones, incluidas:

- La copia de seguridad de máquinas virtuales.
- La copia de seguridad de archivos.
- La copia de seguridad de bases de datos de SQL Server.
- La recuperación de recursos protegidos.

Obtenga más información sobre [Azure Backup](https://docs.microsoft.com/azure/backup) para proteger los recursos migrados.
