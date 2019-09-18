---
title: Métricas, indicadores y tolerancia al riesgo de la coherencia de los recursos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Métricas, indicadores y tolerancia al riesgo de la coherencia de los recursos
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: e4ec7b4700f80a8ad7b46900ed0f3f869ccfbb94
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032272"
---
# <a name="resource-consistency-metrics-indicators-and-risk-tolerance"></a>Métricas, indicadores y tolerancia al riesgo de la coherencia de los recursos

El objetivo de este artículo es ayudar a cuantificar la tolerancia al riesgo del negocio en relación con la coherencia de los recursos. Definir las métricas y los indicadores servirá de ayuda para crear un modelo de negocio con el fin de calcular la inversión en la materia sobre la coherencia de los recursos.

## <a name="metrics"></a>Métricas

La materia sobre la coherencia de los recursos se centra en abordar los riesgos relacionados con la administración operativa de las implementaciones en la nube. Como parte del análisis de riesgos, querrá recopilar datos relativos a las operaciones de TI para determinar el riesgo al que se enfrenta y la importancia que la inversión en la gobernanza de la coherencia de los recursos tiene en sus planes de implementación en la nube.

Cada organización tiene diferentes escenarios operativos, pero los elementos siguientes son ejemplos útiles de las métricas que debe recopilar a la hora de evaluar la tolerancia a los riesgos en materia sobre la coherencia de los recursos:

- **Recursos en la nube.** Número total de recursos implementados en la nube.
- **Recursos sin etiquetar.** Número de recursos sin las etiquetas necesarias de propiedad, impacto empresarial u organizativas.
- **Recursos infrautilizados.** Número de recursos cuyas capacidades de red, CPU o memoria se infrautilizan de forma constante.
- **Agotamiento de los recursos.** Número de recursos en los que la carga agota las capacidades de red, CPU o memoria.
- **Antigüedad de los recursos.** Tiempo transcurrido desde que el recurso se implementó o se modificó por última vez.
- **Máquinas virtuales en condición crítica.** Número de máquinas virtuales implementadas en las que se ha detectado uno o varios problemas críticos que deben solucionarse para restaurar la funcionalidad normal.
- **Alertas por gravedad.** Número total de alertas en un recurso implementado, desglosado por gravedad.
- **Vínculos de subred incorrectos.** Número de recursos con problemas de conectividad de red.
- **Puntos de conexión de servicio incorrectos.** Número de problemas con los puntos de conexión de red externos.
- **Incidencias de estado de mantenimiento del servicio del proveedor de nube.** Número de interrupciones o incidencias de rendimiento causados por el proveedor de servicios en la nube.
- **Contratos de nivel de servicio.** Pueden incluir tanto los compromisos de Microsoft correspondientes al tiempo de actividad y conectividad de los servicios de Azure como los compromisos adquiridos por la empresa con sus clientes externos e internos.
- **Disponibilidad del servicio.** Porcentaje del tiempo de actividad real de las cargas de trabajo hospedadas en la nube en comparación con el tiempo de actividad esperado.
- **Objetivo de tiempo de recuperación (RTO).** El tiempo máximo aceptable que una aplicación puede estar no disponible después de un incidente.
- **Objetivo de punto de recuperación (RPO).** La duración máxima de pérdida de datos que es aceptable durante un desastre. Por ejemplo, si se almacenan datos en una única base de datos, sin replicación en otras bases de datos y se realizan copias de seguridad por hora, se podría perder hasta una hora de datos.
- **Promedio de tiempo de recuperación (MTTR).** El tiempo promedio necesario para restaurar un componente después de un error.
- **Promedio de tiempo entre errores (MTBF).** La duración razonable que se puede suponer que un componente se ejecutará entre interrupciones. Esta métrica puede ayudarle a calcular la frecuencia con la que un servicio dejará de estar disponible.
- **Estado de mantenimiento de las copias de seguridad.** Número de copias de seguridad que se están sincronizando activamente.
- **Estado de mantenimiento de la recuperación.** Número de operaciones de recuperación realizadas correctamente.

## <a name="risk-tolerance-indicators"></a>Indicadores de tolerancia al riesgo

Las plataformas de nube ofrecen un conjunto básico de características que permiten a los equipos de implementación administrar de forma eficaz pequeñas implementaciones sin necesidad de extensos planeamientos o procesos adicionales. Como resultado, las primeras cargas de trabajo experimentales o de desarrollo/pruebas que incluyan una pequeña cantidad de recursos basados en la nube representan un nivel de riesgo bajo y, probablemente, no hará falta mucho en cuanto a la directiva formal de coherencia de los recursos.

Sin embargo, a medida que crezca el tamaño de su patrimonio en la nube, la administración de los recursos se volverá más compleja. Al haber más recursos en la nube, es fundamental poder identificar quién es el propietario y controlar los recursos de forma útil. A medida que se implementan en la nube más cargas de trabajo críticas para la misión, el tiempo de actividad del servicio pasa a ser más importante y tolerancia a los posibles sobrecostos producidos por interrupciones del servicio disminuye rápidamente.

En las primeras fases de adopción de la nube, trabaje con el equipo de seguridad de TI y las partes interesadas de la empresa para identificar los [riesgos empresariales](./business-risks.md) relativos a la coherencia de los recursos y, después, determine una base de referencia aceptable para la tolerancia al riesgo. En esta sección del Marco de adopción de la nube se proporcionan ejemplos, pero los riesgos detallados y las bases de referencia de su empresa o sus implementaciones pueden ser diferentes.

Una vez que tenga una base de referencia, establezca bancos de pruebas mínimos que representen un aumento inaceptable de los riesgos identificados. Estos bancos de pruebas actúan como desencadenadores cuando necesita tomar medidas para corregir estos riesgos. En los siguientes ejemplos, se muestra cómo las métricas operativas, como las descritas anteriormente, pueden justificar una mayor inversión en la materia sobre la coherencia de los recursos.

- **Desencadenador de etiquetado y nomenclatura.** Una empresa con más de _x_ recursos que carecen de la información necesaria de etiquetado o que no cumplen los estándares de nomenclatura debe plantearse invertir en la materia de coherencia de los recursos para ayudar a pulir estos estándares y garantizar su aplicación coherente a los recursos implementados en la nube.
- **Desencadenador de recursos sobreaprovisionados.** Si una empresa tiene más de un _x %_ de recursos que usan regularmente pequeñas cantidades de sus capacidades disponibles de memoria, CPU o red, se recomienda invertir en la materia de coherencia de los recursos para ayudar a optimizar el uso que hacen de estos elementos.
- **Desencadenador de recursos infraaprovisionados.** Si una empresa tiene más de un _x %_ de recursos que agotan regularmente la mayor parte de sus capacidades disponibles de memoria, CPU o red, se recomienda invertir en la materia de coherencia de los recursos para ayudar a garantizar que estos recursos tengan la capacidad necesaria para evitar interrupciones del servicio.
- **Desencadenador de antigüedad de los recursos.** Una empresa con más de _x_ recursos que no se han actualizado en más de _y_ meses podría beneficiarse de la inversión en la materia de coherencia de los recursos, cuyo objetivo es asegurarse de que los recursos activos estén revisados y en buen estado, y de que se retiren los recursos obsoletos o que no se usen.
- **Desencadenador de contrato de nivel de servicio.** Una empresa que no puede cumplir sus contratos de nivel de servicio con sus clientes externos o asociados internos debe invertir en la disciplina de aceleración de la implementación para reducir el tiempo de inactividad del sistema.
- **Desencadenadores de tiempo de recuperación.** Si una compañía supera los umbrales necesarios para el tiempo de recuperación tras un error del sistema, debe invertir en la mejora de la disciplina de aceleración de la implementación y el diseño de sistemas para reducir o eliminar los errores o el efecto del tiempo de inactividad de un componente individual.
- **Desencadenador de estado de mantenimiento de las máquinas virtuales.** Una empresa que tenga más de un _x %_ de máquinas virtuales con problemas de estado de mantenimiento críticos debe invertir en la materia de coherencia de los recursos para identificar los problemas y mejorar la estabilidad de las máquinas virtuales.
- **Desencadenador de estado de mantenimiento de las redes.** Una empresa que tiene más de un _x %_ de subredes o puntos de conexión con problemas de conectividad debe invertir en la materia de coherencia de los recursos para identificar y resolver los problemas de red.
- **Desencadenador de cobertura de las copias de seguridad.** Una empresa con un _x %_ de los recursos críticos sin copias de seguridad actualizadas se beneficiaría de una mayor inversión en la materia de coherencia de los recursos para garantizar una estrategia de copia de seguridad coherente.
- **Desencadenador de estado de mantenimiento de las copias de seguridad.** Una empresa con más de un _x %_ de errores en las operaciones de restauración debe invertir en la materia de coherencia de los recursos para identificar los problemas de copia de seguridad y garantizar que los recursos importantes estén protegidos.

Las métricas y los desencadenadores exactos que use para medir la tolerancia al riesgo y el nivel de inversión en la materia de coherencia de los recursos son específicos para su organización, pero los ejemplos anteriores sirven como base para las conversaciones con el equipo de gobernanza de la nube.

## <a name="next-steps"></a>Pasos siguientes

Use la [plantilla de administración de la nube](./template.md) para documentar las métricas y los indicadores de tolerancia que están en línea con el plan de adopción de la nube actual.

Revise las directivas de coherencia de los recursos como punto de partida para desarrollar directivas que aborden riesgos de negocio específicos que se alineen con los planes de adopción de la nube.

> [!div class="nextstepaction"]
> [Revise las directivas de ejemplo](./policy-statements.md)
