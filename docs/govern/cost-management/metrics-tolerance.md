---
title: Métricas, indicadores y tolerancia al riesgo de la administración de costos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Explicación de la administración de costos en relación con la gobernanza de la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: be1d4456ac8924c87241089c637fa3aacc38fb47
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031692"
---
# <a name="cost-management-metrics-indicators-and-risk-tolerance"></a>Métricas, indicadores y tolerancia al riesgo de la administración de costos

Este artículo está pensado para ayudarle a cuantificar la tolerancia al riesgo del negocio en relación con la administración de costos. Definir las métricas y los indicadores servirá de ayuda para crear un modelo de negocio con el fin de calcular la inversión en la materia sobre la administración de costos.

## <a name="metrics"></a>Métricas

Normalmente, la administración de costos se centra en las métricas relacionadas con los costos. Como parte del análisis de riesgos, querrá recopilar datos relativos a los gastos actuales y planeados en cargas de trabajo en la nube, con el fin de determinar el riesgo al que se enfrenta y la importancia que la inversión en la gobernanza de los costos tiene en su estrategia de adopción de la nube.

A continuación encontrará varios ejemplos de métricas útiles que debe recopilar para evaluar la tolerancia al riesgo en la materia de administración de costos:

- **Gastos anuales.** El costo total anual de los servicios que presta un proveedor de nube.
- **Gastos mensuales.** El costo total mensual de los servicios que presta un proveedor de nube.
- **Relación entre costos previstos y reales.** La relación que compara los gastos previstos con los reales (mensuales o anuales).
- **Relación del ritmo de la adopción (MOM).** El porcentaje de la diferencia de los costos de la nube de un mes a otro.
- **Costo acumulado.** Total de gastos diarios acumulados desde principios de mes.
- **Tendencias de los gastos.** Tendencias de los gastos con respecto al presupuesto.

## <a name="risk-tolerance-indicators"></a>Indicadores de tolerancia al riesgo

Durante las primeras implementaciones a pequeña escala, como desarrollo/pruebas o las primeras cargas de trabajo experimentales, es probable que la administración de costos tenga un riesgo relativamente bajo. A medida que se implementan más activos aumenta el riesgo y la tolerancia de la empresa hacia el riesgo es probable que se rechace. Además, a medida que más equipos de la adopción de la nube tienen la capacidad de configurar o implementar recursos en la nube, el riesgo aumenta y la tolerancia se reduce. Por el contrario, la expansión de una materia sobre la administración de costos hará que las personas pasen de la fase de adopción de la nube a implementar tecnologías más innovadoras.

En las primeras fases de la adopción de la nube, trabajará con su empresa para determinar una base de referencia para la tolerancia al riesgo. Una vez que la tenga, deberá determinar los criterios que desencadenarán una inversión en la materia sobre la administración de costos. Es probable que dichos criterios sean diferentes para cada organización.

Una vez que haya identificado los [riesgos empresariales](./business-risks.md), trabajará con su empresa para identificar las pruebas comparativas que puede usar para detectar los desencadenadores que podrían aumentar dichos riesgos. A continuación verá algunos ejemplos de la forma en que varias métricas, como las que se han mencionado, se pueden comparar con la tolerancia de la base de referencia de riesgo, con el fin de conocer el grado de necesidad que tiene su empresa en invertir más en administración de costos.

- **Movido por el compromiso (más habitual).** Una empresa que tiene un compromiso de gasto de X 000 000 euros este año en un proveedor de nube. Necesita una materia sobre la administración de costos para asegurarse de que el negocio no supere sus objetivos de gasto en más del 20 % y que van a usar al menos el 90 % del gasto al que se han comprometido.
- **Desencadenador por porcentaje.** Una empresa con gastos en la nube estables en sus sistemas de producción. Si esas cifras cambian más de un _x %_ , la materia de administración de costos será una inversión inteligente.
- **Desencadenador por sobreaprovisionamiento.** Una empresa que cree que sus soluciones implementadas están sobreaprovisionadas. La administración de costos es una inversión prioritaria hasta que puedan demostrar que la relación entre aprovisionamiento y uso los recursos es adecuada.
- **Desencadenador por gastos mensuales.** una compañía que gasta más de X 000 euros al mes se considera un costo considerable. Si los gastos superan esa cantidad en un mes dado, necesitarán invertir en la administración de costos.
- **Desencadenador por gastos anuales.** una empresa con un presupuesto para I+D en TI que permita gastar X 000 euros al año en la experimentación en la nube. Puede ejecutar las cargas de trabajo de producción en la nube, pero seguirán considerándolas soluciones experimentales si el presupuesto no supera dicha cantidad. Una vez que las supere, tendrán que tratar el presupuesto como si fuera una inversión de producción y administrar los gastos atentamente.
- **Gastos de explotación, adversos (no habituales):** como empresa, están en contra de los gastos de explotación y necesitarán instaurar controles de administración de costos antes de implementar una carga de trabajo de desarrollo/pruebas.

## <a name="next-steps"></a>Pasos siguientes

Use la [plantilla de administración de la nube](./template.md) para documentar las métricas y los indicadores de tolerancia que están en línea con el plan de adopción de la nube actual.

Revise las directivas de administración de costos como punto de partida para desarrollar directivas que aborden los riesgos empresariales específicos en línea con los planes de adopción de la nube.

> [!div class="nextstepaction"]
> [Revisión de las directivas de ejemplo](./policy-statements.md)
