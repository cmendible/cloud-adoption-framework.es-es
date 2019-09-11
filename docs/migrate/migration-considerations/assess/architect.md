---
title: Diseño de las cargas de trabajo antes de una migración
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Diseño de las cargas de trabajo antes de una migración
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: d62b2f5957dc5cee19f462e3c7d74c85672eadfe
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70834786"
---
# <a name="architect-workloads-prior-to-migration"></a>Diseño de las cargas de trabajo antes de una migración

En este artículo se amplía el proceso de evaluación a través de la revisión de las actividades asociadas con la definición de la arquitectura de una carga de trabajo dentro de una iteración determinada. Tal como se describe en el artículo sobre la [racionalización incremental](../../../digital-estate/rationalize.md), se realizan algunas suposiciones de diseño durante cualquier transformación empresarial que requiera una migración. En este artículo se explican estas suposiciones, se comparten algunos obstáculos que se pueden evitar y se identifican oportunidades para acelerar el valor empresarial al desafiar esas suposiciones. Este modelo incremental para la arquitectura permite que los equipos se muevan más rápido y obtengan resultados empresariales antes.

## <a name="architecture-assumptions-prior-to-migration"></a>Suposiciones de arquitectura antes de la migración

Las suposiciones siguientes son típicas para cualquier esfuerzo de migración:

- **IaaS.** Se suele suponer que la migración de cargas de trabajo implica principalmente el movimiento de máquinas virtuales desde un centro de datos físico a un centro de datos en la nube a través de una migración de IaaS, que requiere un mínimo de redesarrollo o reconfiguración. Esto se conoce como migración mediante lift-and-shift. (A continuación, se muestran algunas excepciones).
- **Coherencia de la arquitectura.** Los cambios en la arquitectura central durante una migración aumentan considerablemente la complejidad. La depuración de un sistema modificado en una plataforma nueva presenta muchas variables que pueden ser difíciles de aislar. Es por esta razón que las cargas de trabajo se deben someter solo a cambios menores durante la migración y cualquier cambio se debe probar minuciosamente.
- **Prueba de retirada.** Las migraciones y el hospedaje de recursos consumen gastos operativos y de capital potenciales. Se supone que las cargas de trabajo que se van a migrar se revisaron para validar su uso continuo. La opción de retirar los recursos no utilizados genera un ahorro de costos inmediato.
- **Cambiar el tamaño de los recursos.** Se presupone que unos pocos recursos locales están usando por completo los recursos asignados. Antes de la migración, se presupone que el tamaño de los recursos se modificará para ajustarlo mejor a los requisitos de uso reales.
- **Requisitos de continuidad empresarial y recuperación ante desastres (BCDR).** Se supone que un acuerdo de nivel de servicio acordado para la carga de trabajo se negoció con la empresa antes de planear una liberación. Es probable que estos requisitos generen cambios de arquitectura menores.
- **Tiempo de inactividad de la migración.** Del mismo modo, el tiempo de inactividad para promover la carga de trabajo al entorno de producción puede tener un efecto adverso en la empresa. A veces, las soluciones que deben realizar la transición con un tiempo de inactividad mínimo necesitan cambios de arquitectura. Se supone que se estableció una descripción general de los requisitos de tiempo de inactividad antes de planear una liberación.

## <a name="roadblocks-that-can-be-avoided"></a>Obstáculos que se pueden evitar

Las suposiciones detalladas pueden crear obstáculos que podrían ralentizar el progreso o generar más puntos críticos. A continuación, se indican algunos obstáculos que hay que supervisar antes de la liberación:

- **Pago de una deuda técnica.** Algunas cargas de trabajo antiguas tienen una gran cantidad de deuda técnica. Esto puede conducir a desafíos a largo plazo al aumentar los costos de hospedaje con cualquier proveedor de servicios en la nube. Cuando la deuda técnica aumenta de manera poco natural los costos de hospedaje, se deben evaluar arquitecturas alternativas.
- **Patrones de tráfico de usuario.** Las soluciones existentes pueden depender de los patrones de enrutamiento de red existentes. Estos patrones podrían ralentizar considerablemente el rendimiento. Además, la introducción de nuevas soluciones de red de área extensa (WAN) híbrida puede tardar semanas o incluso meses. Prepárese al inicio del proceso de arquitectura para enfrentar estos obstáculos, considerando los patrones de tráfico y los cambios en los servicios de infraestructura principales.

## <a name="accelerating-business-value"></a>Aceleración del valor empresarial

Algunos escenarios podrían requerir una arquitectura diferente a la de la estrategia de rehospedaje de IaaS supuesta. Estos son algunos ejemplos:

- Alternativas de PaaS. Las implementaciones de PaaS pueden reducir los costos de hospedaje y también el tiempo que se necesita para migrar ciertas cargas de trabajo. Para una lista de los enfoques que podrían beneficiarse de una conversión de PaaS, consulte el artículo sobre la [evaluación de los recursos](./evaluate.md).
- Implementaciones con scripts/DevOps. Si una carga de trabajo tiene una implementación de DevOps existente u otras formas de implementaciones con scripts, el costo de cambiar esos scripts podría ser menor que el costo de migrar el recurso.
- Esfuerzos de corrección. Los esfuerzos de corrección necesarios para preparar una carga de trabajo para la migración pueden ser importantes. En algunos casos, tiene más sentido modernizar la solución que corregir los problemas de compatibilidad subyacentes.

En cada uno de estos escenarios detallados, una arquitectura alternativa podría ser la mejor solución posible.

## <a name="next-steps"></a>Pasos siguientes

Una vez definida la arquitectura nueva, [se pueden calcular estimaciones de costos precisas](./estimate.md).

> [!div class="nextstepaction"]
> [Estimación del costo de la nube](./estimate.md)
