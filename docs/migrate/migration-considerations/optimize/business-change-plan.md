---
title: Instrucciones para desarrollar un plan de cambio empresarial
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Un proceso de la migración a la nube que se centra en las tareas de migración de cargas de trabajo.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 44296faa9b5be56988babe9e0a847564d51148c3
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70839062"
---
# <a name="business-change-plan"></a>Plan de cambio de negocio

Tradicionalmente, TI supervisaba la publicación de nuevas cargas de trabajo. Durante una transformación principal, como la migración de un centro de datos o una migración en la nube, se podría aplicar un patrón similar de adopción de liderazgo por parte del departamento de TI. Sin embargo, el enfoque tradicional podría pasar por alto oportunidades para obtener un valor empresarial adicional. Por este motivo, antes de que una carga de trabajo migrada se promocione a producción, se recomienda implementar un enfoque más amplio para la adopción de los usuarios. En este artículo se describen las formas en que un plan de cambio empresarial se agrega a un plan estándar de adopción de los usuarios.

## <a name="traditional-user-adoption-approach"></a>Enfoque tradicional de adopción de los usuarios

Los planes de adopción de los usuarios se centran en cómo adoptarán los usuarios una nueva tecnología o cambio en una tecnología determinada. Este enfoque es de eficacia probada a la hora de presentar nuevas herramientas a los usuarios. En un plan de adopción de los usuarios típico, el departamento de TI se centra en la instalación, configuración, mantenimiento y entrenamiento asociados a los cambios técnicos que se van a introducir en el entorno empresarial.

Aunque los enfoques pueden variar, los temas generales están presentes en la mayoría de los planes de adopción de los usuarios. Estos temas se basan normalmente en un enfoque de control de riesgos y de facilitación que se adapta a las mejoras incrementales. La matriz Eason, que se muestra en la ilustración siguiente, representa los controladores que se encuentran detrás de estos temas en un espectro de tipos de adopción.

![Matriz Eason de preocupaciones relacionadas con la adopción por parte de los usuarios](../../../_images/eason-matrix.jpg)

*Matriz Eason de tipos de adopción por parte de los usuarios.*

Estos temas suelen basarse en la suposición de que la introducción de nuevas soluciones para los usuarios debe centrarse en gran medida en el control de riesgos y en facilitar el cambio. Además, el equipo de TI se suele centrar principalmente en el riesgo de ese cambio tecnológico y en facilitar dicho cambio.

## <a name="creating-business-change-plans"></a>Creación de planes de cambio empresarial

Un plan de cambio empresarial va más allá del cambio técnico y presupone que cada fase de un esfuerzo de migración promueve un cierto grado de cambio en el proceso empresarial. Analiza la situación previa y posterior de los cambios técnicos. Las siguientes preguntas ayudan a los participantes a pensar en el proceso de adopción por parte de los usuarios desde una perspectiva de cambio empresarial para maximizar el impacto en la empresa:

**Preguntas previas.** Las preguntas previas analizan los impactos o cambios que se producen antes de que se produzca la adopción por parte del usuario:

- ¿Se ha cuantificado un [resultado empresarial](../../../business-strategy/business-outcomes/index.md) previsible?
- ¿Se asigna el impacto empresarial a [métricas de aprendizaje](../../../business-strategy/learning-metrics.md) definidas?
- ¿Qué procesos y equipos empresariales podrán aprovechar esta solución técnica?
- ¿Qué persona de la empresa puede preparar mejor a los usuarios avanzados para realizar pruebas y enviar comentarios?
- ¿Se ha implicado a los directivos en el planeamiento de las prioridades y de la migración?
- ¿Hay eventos o fechas críticas para la empresa que pudieran verse afectados por este cambio?
- ¿Es un plan de cambio empresarial que maximiza el impacto pero minimiza la interrupción del negocio?
- ¿Se prevé algún tiempo de inactividad? ¿Se ha comunicado algún período de tiempo de inactividad a los usuarios finales?

**Preguntas posteriores.** Una vez completada la fase de adopción, puede comenzar el cambio empresarial. Desafortunadamente, aquí es donde acaban muchos planes de adopción por parte de los usuarios. Las preguntas posteriores ayudan al equipo de estrategia en la nube a centrarse en la transformación una vez completado el cambio técnico:

- ¿Están respondiendo bien los usuarios empresariales a los cambios?
- ¿Se ha mantenido la previsión del rendimiento ahora que se ha adoptado el cambio técnico?
- ¿Están cambiando los procesos empresariales o las experiencias de los clientes de la manera prevista?
- ¿Se requieren cambios adicionales para conseguir las métricas de aprendizaje?
- ¿Se alinearon los cambios con los resultados empresariales que se querían conseguir? Si no es así, ¿por qué no?
- ¿Es necesario algún cambio adicional para contribuir a conseguir los resultados empresariales?
- ¿Se ha observado algún efecto negativo como resultado de este cambio?

El plan de cambio empresarial varía de una empresa a otra. El objetivo de estas preguntas es ayudar a integrar mejor la empresa en el cambio asociado a cada nuevo lanzamiento. Al considerar cada lanzamiento no como un cambio de tecnología que se debe adoptar sino como un plan de cambio empresarial, se puede lograr que los resultados de la empresa sean más viables.

## <a name="next-steps"></a>Pasos siguientes

Una vez que el cambio empresarial está documentado y planeado, pueden comenzar las [pruebas empresariales](./business-test.md).

> [!div class="nextstepaction"]
> [Guía sobre las pruebas empresariales (UAT) durante la migración](./business-test.md)

## <a name="references"></a>Referencias

- Eason, K. (1988) _Information technology and organizational change_, New York: Taylor and Francis.
