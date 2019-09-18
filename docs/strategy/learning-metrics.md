---
title: ¿Cómo podemos alinear el trabajo con métricas de aprendizaje significativas?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Explicación del concepto de métricas de aprendizaje
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: f761f85fa4b21b35e8428985707176624b92a5ec
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031695"
---
<!-- markdownlint-disable MD026 -->

# <a name="how-can-we-align-efforts-to-meaningful-learning-metrics"></a>¿Cómo podemos alinear el trabajo con métricas de aprendizaje significativas?

En la [información general sobre resultados empresariales](./business-outcomes/index.md) se analizaron formas de medir y comunicar cómo afectará una transformación a la empresa. Desafortunadamente, pueden pasar años antes de que algunos de esos resultados produzcan resultados mensurables. La junta y los ejecutivos de máximo rango están descontentos con los informes que muestran una diferencia del 0 % durante largos períodos de tiempo.

Las métricas de aprendizaje son métricas provisionales a más corto plazo que se pueden asociar a resultados empresariales a largo plazo. Estas métricas se alinean bien con una mentalidad de crecimiento y contribuyen a posicionar la cultura para que sea más resistente. En lugar de destacar la falta de progreso prevista para la consecución de un objetivo empresarial a largo plazo, las métricas de aprendizaje resaltan los primeros indicadores de éxito. Las métricas también resaltan los indicadores iniciales de error, que probablemente proporcionen la mejor oportunidad de aprender y ajustar el plan.

Como en muchos de los materiales de este marco, se supone que está familiarizado con el [recorrido de transformación](../govern/guides/index.md) que mejor se adapta a los resultados empresariales esperados. En este artículo se describen algunas métricas de aprendizaje para cada recorrido de transformación a fin de ilustrar el concepto.

## <a name="cloud-migration"></a>Migración a la nube

Esta transformación se centra en el costo, la complejidad y la eficacia, con énfasis en las operaciones de TI. Los datos más fáciles de medir detrás de esta transformación son los del traslado de recursos a la nube. En este tipo de transformación, el patrimonio digital se mide en máquinas virtuales (VM), bastidores o clústeres que hospedan esas máquinas virtuales, costos operativos del centro de datos, gastos de capital necesarios para mantener los sistemas y amortización de dichos recursos a lo largo del tiempo.

A medida que las máquinas virtuales se trasladan a la nube, se reduce la dependencia de los recursos heredados locales. También se reduce el costo del mantenimiento de recursos. Desafortunadamente, las empresas no pueden materializar la reducción de costos hasta que los clústeres se desaprovisionan y las concesiones de centros de datos expiran. En muchos casos, el valor completo del trabajo no se materializa hasta que se completan los ciclos de amortización.

Póngase siempre de acuerdo con el director financiero o el departamento de finanzas antes de crear informes financieros. Aunque los equipos de TI generalmente pueden calcular los valores de costo monetario actual y de costo monetario futuro para cada máquina virtual en función del consumo de CPU, memoria y almacenamiento. Luego puede aplicarse ese valor a cada máquina virtual migrada para estimar el ahorro de costos inmediato y el valor monetario futuro del trabajo.

## <a name="application-innovation"></a>Innovación en las aplicaciones

La innovación en las aplicaciones habilitadas para la nube se centra en gran medida en la experiencia del cliente y en su disposición para consumir productos y servicios ofrecidos por la empresa. Se tarda cierto tiempo para que los incrementos de cambio afecten a los comportamientos de compra del consumidor o del cliente. Pero los ciclos de innovación de las aplicaciones suelen ser mucho más cortos que en otras formas de transformación. El consejo tradicional es que se debe empezar por la comprensión de los comportamientos específicos en los que quiere influir y usar esos comportamientos como métricas de aprendizaje. Por ejemplo, en una aplicación de comercio electrónico, las compras totales o las compras de complementos podrían ser el comportamiento de destino. En el caso de una empresa de vídeo, el tiempo durante el que se ven las secuencias de vídeo podría ser el objetivo.

El desafío con las métricas de comportamiento del cliente es que pueden verse fácilmente afectadas por variables externas. Por eso suele ser importante incluir estadísticas relacionadas con las métricas de aprendizaje. Entre las estadísticas relacionadas se puede incluir la cadencia de las versiones, los errores resueltos por versión, la cobertura de código de pruebas unitarias, el número de vistas de página, el rendimiento de páginas, el tiempo de carga de página y otras métricas de rendimiento de aplicaciones. Cada una de ellas puede mostrar diferentes actividades y cambios en la base de código y la experiencia del cliente que se correlacionan con patrones de comportamiento del cliente de nivel superior.

## <a name="data-innovation"></a>Innovación en los datos

Puede tardarse años en cambiar un sector, desestabilizar mercados o transformar productos o servicios. En un trabajo de innovación de datos habilitado para la nube, la experimentación es la clave para medir el éxito. Sea transparente compartiendo las métricas de predicción, como la probabilidad porcentual, el número de experimentos con errores y la cantidad de modelos entrenados. Los errores se acumularán con mayor rapidez que los éxitos. Estas mediciones pueden ser desalentadoras y es importante que el equipo ejecutivo comprenda el tiempo y la inversión que se requieren para aprovechar los datos adecuadamente.

Por otro lado, algunos indicadores positivos suelen estar asociados al aprendizaje controlado por datos: centralización de conjuntos de datos heterogéneos, entrada de datos y democratización de los datos. Mientras el equipo aprende sobre el cliente del mañana, se pueden generar resultados reales hoy mismo. Entre las métricas de aprendizaje de apoyo se podrían incluir:

- Número de modelos disponibles
- Número de orígenes de datos de partner consumidos
- Dispositivos que producen datos de entrada
- Volumen de datos de entrada
- Tipos de datos

Una métrica aún más valiosa es el número de paneles creados a partir de orígenes de datos combinados. Este número refleja los procesos empresariales de estado actual que se ven afectados por los nuevos orígenes de datos. Al compartir nuevos orígenes de datos abiertamente, su empresa puede aprovechar los datos mediante herramientas de informes como Power BI para generar información incremental e impulsar el cambio empresarial.

## <a name="next-steps"></a>Pasos siguientes

Una vez alineadas las métricas de aprendizaje, está listo para empezar a [evaluar el patrimonio digital](../digital-estate/index.md) con respecto a esas métricas. El resultado será un [trabajo pendiente de transformación o de migración](../migrate/migration-considerations/prerequisites/technical-complexity.md).

> [!div class="nextstepaction"]
> [Evaluación del patrimonio digital](../digital-estate/index.md)
