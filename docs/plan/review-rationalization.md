---
title: Revisión de las decisiones de racionalización
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Revisión de las decisiones de racionalización
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 8d374fdc5df4589e58b890ae5c169d26d0b1f206
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70839170"
---
# <a name="review-rationalization-decisions"></a>Revisión de las decisiones de racionalización

Durante las fases de estrategia y planeamiento inicial, se recomienda aplicar un enfoque de [racionalización incremental](../digital-estate/rationalize.md#incremental-rationalization) al patrimonio digital. Pero este enfoque inserta algunas suposiciones en las decisiones resultantes. Se recomienda que los equipos de adopción y estrategia de la nube revisen esas decisiones en función de la documentación de la carga de trabajo ampliada. Esta revisión también es un buen momento para involucrar a las partes interesadas del negocio y al patrocinador ejecutivo en futuras decisiones sobre el patrimonio.

> [!IMPORTANT]
> Se realizará una validación adicional de las decisiones de racionalización durante la fase de evaluación de la migración. Esta validación se centra en la revisión empresarial de la racionalización para alinear los recursos de forma adecuada.

Para validar las decisiones de racionalización, utilice las siguientes preguntas para facilitar una conversación con el negocio. Las preguntas se agrupan por la alineación de racionalización probable.

## <a name="innovation-indicators"></a>Indicadores de innovación

Si la revisión conjunta de las siguientes preguntas da como resultado una respuesta afirmativa, una carga de trabajo podría ser una buena candidata para la innovación. Este tipo de carga de trabajo no se migrará con un modelo de tipo "levantar y mover" o de modernización. En su lugar, las estructuras de datos o la lógica del negocio se volverán a crear como una aplicación nueva o rediseñada. Este enfoque puede ser más intensivo y requiere mucho tiempo. Pero para una carga de trabajo que representa retornos empresariales significativos, se justifica la inversión.

- ¿Las aplicaciones de esta carga de trabajo crean diferenciación en el mercado?
- ¿Hay una inversión propuesta o aprobada destinada a mejorar las experiencias asociadas a las aplicaciones de esta carga de trabajo?
- ¿Los datos de esta carga de trabajo hacen posibles nuevas ofertas de productos o servicios?
- ¿Hay una inversión propuesta o aprobada destinada a aprovechar los datos asociados a esta carga de trabajo?
- ¿Se puede cuantificar el efecto de la diferenciación en el mercado o de las nuevas ofertas? En caso afirmativo, ¿el retorno justifica el aumento del costo de la innovación durante la adopción de la nube?

Las dos preguntas siguientes pueden ayudarle a incluir escenarios técnicos generales en la revisión de la racionalización. Una respuesta afirmativa a una de ellas puede identificar formas de contabilizar o reducir el costo asociado con la innovación.

- ¿Cambiarán las estructuras de datos o la lógica del negocio durante el transcurso de la adopción de la nube?
- ¿Se usa una canalización de implementación existente para implementar esta carga de trabajo en producción?

Si la respuesta a cualquiera de las preguntas es afirmativa, el equipo debería considerar incluir esta carga de trabajo como candidata para la innovación. Como mínimo, el equipo debe marcar esta carga de trabajo para la revisión de la arquitectura con el fin de identificar oportunidades de modernización.

## <a name="migration-indicators"></a>Indicadores de migración

La migración es una forma rápida y económica de adoptar la nube. Pero no aprovecha las oportunidades de innovación. Antes de invertir en innovación, responda a las siguientes preguntas. Pueden ayudarle a determinar si un modelo de migración es más aplicable para una carga de trabajo.

- ¿El código fuente de esta aplicación es estable? ¿Espera que permanezca estable y sin cambios durante el período de tiempo de este ciclo de versión?
- ¿Esta carga de trabajo es compatible actualmente con los procesos empresariales de producción? ¿Lo será a lo largo del curso de este ciclo de versión?
- ¿Es una prioridad que este trabajo de adopción de la nube mejore la estabilidad y el rendimiento de esta carga de trabajo?
- ¿La reducción de costos asociada a esta carga de trabajo es un objetivo durante este trabajo?
- ¿La reducción de la complejidad operativa de esta carga de trabajo es un objetivo durante este trabajo?
- ¿La innovación está limitada por la arquitectura actual o los procesos de operación de TI?

Si la respuesta a alguna de estas preguntas es afirmativa, debe considerar un modelo de migración para esta carga de trabajo. Esta recomendación se mantiene incluso si la carga de trabajo es candidata para la innovación.

Los desafíos de la complejidad operativa, los costos, el rendimiento o la estabilidad pueden afectar a los retornos del negocio. Puede usar la nube para generar rápidamente mejoras relacionadas con estos desafíos. Cuando sea aplicable, se recomienda usar el enfoque de migración para estabilizar primero la carga de trabajo. A continuación, amplíe oportunidades de innovación en el entorno estable y ágil de la nube. Este enfoque proporciona retornos a corto plazo y reduce el costo necesario para impulsar el cambio a largo plazo.

> [!IMPORTANT]
> Los modelos de migración incluyen la modernización incremental. El uso de arquitecturas de plataforma como servicio (PaaS) es un aspecto común de las actividades de migración. También hay cambios de configuración menores que usan esos servicios de plataforma. El límite de la migración se define como un cambio material en la lógica del negocio o en las estructuras empresariales de apoyo. Dicho cambio se considera un trabajo de innovación.

## <a name="update-the-project-plan"></a>Actualización del plan del proyecto

Las aptitudes necesarias para un trabajo de migración son diferentes de las aptitudes necesarias para un trabajo de innovación. Durante la implementación de un plan de adopción de la nube, se recomienda asignar los trabajos de migración e innovación a distintos equipos. Cada equipo tiene su propio ritmo de iteración, versiones y planeamiento. La asignación de equipos independientes proporciona la flexibilidad del proceso de mantenimiento de un plan de adopción de la nube, además de la contabilización de los trabajos de innovación y migración.

Cuando administra el plan de adopción de la nube en Azure DevOps, esa administración se refleja mediante el cambio del elemento de trabajo primario (o epopeya) desde la migración a la nube a la innovación en la nube. Este cambio sutil ayuda a garantizar que todos los participantes en el plan de adopción de la nube puedan realizar rápidamente el seguimiento del trabajo necesario y de los cambios en los trabajos de corrección. Este seguimiento también ayuda a alinear las asignaciones adecuadas al equipo de adopción de la nube correspondiente.

En el caso de planes de adopción complejos y de gran tamaño con varios proyectos distintos, considere la posibilidad de actualizar la ruta de iteración. Cambiar la ruta de área hace que la carga de trabajo sea visible solo para el equipo asignado a esa ruta de área. Este cambio puede facilitar el trabajo al equipo de adopción de la nube al reducir el número de tareas visibles. Pero agrega complejidad a los procesos de administración del proyecto.

## <a name="next-steps"></a>Pasos siguientes

[Defina las iteraciones y versiones](./iteration-paths.md) para empezar a planear el trabajo.

> [!div class="nextstepaction"]
> [Defina las iteraciones y versiones](./iteration-paths.md) para empezar a planear el trabajo.
