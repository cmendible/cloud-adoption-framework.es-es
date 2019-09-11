---
title: Evaluación de los recursos antes de la migración
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Evaluación de los recursos antes de la migración
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 7aac08981375a3fcbbd658d6e14564a07e06795e
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70816302"
---
# <a name="assess-assets-prior-to-migration"></a>Evaluación de los recursos antes de la migración

Muchas de sus cargas de trabajo ya existentes son candidatas ideales para la migración a la nube, pero no todos los recursos son compatibles con plataformas en la nube y no todas las cargas de trabajo se pueden beneficiar del hospedaje en la nube. El [planeamiento del patrimonio digital](../../../digital-estate/index.md) le permite generar un completo [trabajo pendiente de migración](../prerequisites/technical-complexity.md#migration-backlog-aligning-business-priorities-and-timing) con posibles cargas de trabajo que se pueden migrar. Sin embargo, este esfuerzo de planeamiento es de alto nivel. Se basa en suposiciones realizadas por el equipo de estrategia en la nube y no analiza en profundidad las consideraciones técnicas.

Por tanto, antes de migrar una carga de trabajo a la nube es fundamental evaluar los recursos individuales asociados a esa carga de trabajo para determinar su idoneidad para la migración. Durante esta valoración, su equipo de adopción de la nube deberá evaluar la compatibilidad técnica, la arquitectura necesaria, las expectativas de rendimiento y tamaño, y las dependencias para asegurarse de que la carga de trabajo migrada se puede implementar eficazmente en la nube.

El proceso de *valoración* constituye la primera de las cuatro actividades incrementales que se producen en una iteración. Como ya se ha descrito en el artículo de requisitos previos acerca de la [complejidad técnica y la administración de cambios](../prerequisites/technical-complexity.md), se debe tomar una decisión de antemano para determinar cómo se ejecuta esta fase. Concretamente, ¿será el equipo de adopción de la nube el que complete las valoraciones durante el mismo sprint que el esfuerzo de migración real? O, por el contrario, ¿se usará una oleada o modelo de fábrica para completar las valoraciones en una iteración independiente? Si no todos los miembros del equipo pueden dar una respuesta a esta pregunta básica sobre el proceso, es recomendable que revisen la sección de [Requisitos previos](../prerequisites/index.md).

## <a name="objective"></a>Objetivo

Valorar a una candidata a la migración mediante la evaluación de la carga de trabajo, los recursos y las dependencias asociados antes de realizar la migración.

## <a name="definition-of-done"></a>Definición de *Listo*

Este proceso termina cuando se realizan las siguientes tareas relacionadas con una carga de trabajo candidata a la migración:

- Se ha definido la ruta de acceso del entorno local a la nube, incluida la decisión sobre el método de promoción de la producción.
- Se han completado las aprobaciones, cambios, estimaciones de costos o procesos de validación necesarios para permitir al equipo de adopción de la nube ejecutar la migración.

## <a name="accountability-during-assessment"></a>Responsabilidad durante la valoración

El equipo de adopción de la nube es responsable de todo el proceso de valoración. No obstante, los miembros del equipo de estrategia en la nube también tienen algunas responsabilidades como se indica en la siguiente sección.

## <a name="responsibilities-during-assessment"></a>Responsabilidades durante la valoración

Además de la responsabilidad de alto nivel, hay acciones de las que un individuo o grupo se deben hacer responsables directamente. Estas son algunas de las actividades que se tienen que asignar a las partes responsables:

- **Prioridad empresarial.** El equipo comprende perfectamente la finalidad de la migración de esta carga de trabajo, incluyendo cualquier impacto previsto en la empresa.
  - Un miembro del equipo de estrategia en la nube se debe hacer cargo de la responsabilidad final de esta actividad, bajo la dirección del equipo de adopción de la nube.
- **Acuerdo con las partes interesadas.** El equipo ha acordado las expectativas y prioridades con las partes interesadas internas identificando los factores para lograr el éxito de la migración. ¿Cómo identificar el éxito después de la migración?
- **Costo.** Se ha estimado el costo de la arquitectura de destino y se ha ajustado el presupuesto total.
- **Compatibilidad con la migración.** El equipo ha decidido cómo se llevará a cabo el trabajo técnico de la migración, incluidas las decisiones relacionadas con el soporte de los asociados o de Microsoft.
- **Evaluación.** Se evalúa la compatibilidad y las dependencias de la carga de trabajo.
  - Esta actividad debe asignarse a un experto en la materia que esté familiarizado con la arquitectura y las operaciones de la carga de trabajo candidata.
- **Arquitecto.** El equipo ha acordado la arquitectura final de la carga de trabajo migrada.
- **Acuerdo sobre el trabajo pendiente.** El equipo de adopción de la nube revisa los requisitos y se compromete a la migración de la carga de trabajo candidata. Después de este compromiso, se debe actualizar el trabajo pendiente de publicación y el de iteración según corresponda.
- **Estructura de descomposición del trabajo o programación del trabajo.** El equipo define una programación con los hitos más importantes identificando los objetivos que determinan cuándo finalizar los procesos de planeamiento, implementación y revisión.
- **Aprobación final.** Todos los aprobadores necesarios han revisado el plan y han aprobado el enfoque para migrar el recurso.
  - Para evitar sorpresas más adelante en el proceso, al menos un representante de la empresa debe participar en el proceso de aprobación.

> [!CAUTION]
> Esta lista completa de responsabilidades y acciones puede admitir migraciones grandes y complejas que implican varios roles con distintos niveles de responsabilidad y que requieren un proceso de aprobación detallado. Puede que otros esfuerzos de migración más sencillos y pequeños no necesiten todos los roles y acciones que se describen aquí. Para determinar cuál de estas actividades agrega valor y cuál es una sobrecarga innecesaria, se recomienda que el equipo de adopción de la nube y el de estrategia en la nube usen todo este proceso como parte de la migración de su primera carga de trabajo. Después de haber comprobado y probado la carga de trabajo, el equipo puede evaluar este proceso y elegir qué acciones desea usar más adelante.

## <a name="next-steps"></a>Pasos siguientes

Si comprende el proceso de valoración, está listo para comenzar el proceso de [alineación de las prioridades empresariales](./business-priorities.md).

> [!div class="nextstepaction"]
> [Alineación de las prioridades empresariales](./business-priorities.md)
