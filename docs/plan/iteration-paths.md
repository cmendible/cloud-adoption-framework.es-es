---
title: Establecimiento de iteraciones y planes de versiones
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Establecimiento de iteraciones y planes de versiones
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 0dbef36d3909f11c1616d2e44c63227959c4ff56
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70839178"
---
# <a name="establish-iterations-and-release-plans"></a>Establecimiento de iteraciones y planes de versiones

Agile y otras metodologías iterativas se basan en los conceptos de iteraciones y versiones. En este artículo se describe la asignación de iteraciones y versiones durante el planeamiento. Dichas asignaciones impulsan la visibilidad de la escala de tiempo para facilitar las conversaciones entre los miembros del equipo de estrategia de la nube. Las asignaciones también alinean las tareas técnicas de una manera que el equipo de adopción de la nube puede administrar durante la implementación.

## <a name="establish-iterations"></a>Establecimiento de iteraciones

En un enfoque iterativo de la implementación técnica, los trabajos técnicos se planean en torno a bloques de tiempo recurrentes. Las iteraciones tienden a ser bloques de tiempo de entre una y seis semanas. El consenso sugiere que la duración media de la iteración es de dos semanas para la mayoría de los equipos de adopción de la nube. Pero la elección de la duración de la iteración depende del tipo de trabajo técnico, la sobrecarga administrativa y las preferencias del equipo.

Para empezar a alinear los trabajos con una escala de tiempo, se recomienda definir un conjunto de iteraciones que dure entre 6 y 12 meses.

## <a name="understand-velocity"></a>Descripción de la velocidad

La alineación de trabajos con iteraciones y versiones requiere un conocimiento de la velocidad. La velocidad es la cantidad de trabajo que se puede completar en una iteración determinada. Durante el planeamiento temprano, la velocidad es una estimación. Después de varias iteraciones, la velocidad se convierte en un indicador muy valioso de los compromisos que el equipo puede llevar a cabo con confianza.

Puede medir la velocidad en términos abstractos como el grado de dificultad del caso. También puede medirla en términos más tangibles; por ejemplo, horas. En la mayoría de los marcos iterativos, se recomienda usar medidas abstractas para evitar desafíos en la precisión y la percepción. Los ejemplos de este artículo representan la velocidad en horas por sprint. Esta representación hace que el tema se entienda más universalmente.

**Ejemplo:** un equipo de adopción de la nube de cinco personas se ha comprometido a realizar sprints de dos semanas. Dadas las obligaciones actuales, como las reuniones y el soporte técnico de otros procesos, cada miembro del equipo puede colaborar de forma coherente 20 horas por semana con el trabajo de adopción. Para este equipo, la estimación de velocidad inicial es de 100 horas por sprint.

## <a name="iteration-planning"></a>Planeamiento de las iteraciones

Inicialmente, las iteraciones se planean mediante la evaluación de las tareas técnicas basadas en el trabajo pendiente con prioridades. Los equipos de adopción de la nube estiman el trabajo necesario para realizar varias tareas. A continuación, esas tareas se asignan a la primera iteración disponible.

Durante el planeamiento de las iteraciones, los equipos de adopción de la nube validan y refinan las estimaciones. Lo hacen hasta que hayan alineado toda la velocidad disponible a tareas específicas. Este proceso continúa para cada carga de trabajo con prioridades hasta que todos los trabajos se alinean con una iteración prevista.

En este proceso, el equipo valida las tareas asignadas al siguiente sprint. El equipo actualiza sus estimaciones en función de las conversaciones del equipo sobre cada tarea. A continuación, el equipo agrega cada tarea estimada al siguiente sprint hasta que se alcanza la velocidad disponible. Por último, el equipo calcula las tareas adicionales y las agrega a la siguiente iteración. El equipo realiza estos pasos hasta que se agota también la velocidad de dicha iteración.

El proceso anterior continúa hasta que todas las tareas se asignan a una iteración.

**Ejemplo:** sigamos a partir del ejemplo anterior. Supongamos que cada migración de carga de trabajo requiere 40 tareas. Supongamos también que calcula que cada tarea tardará un promedio de una hora. La estimación combinada es de aproximadamente 40 horas por cada migración de carga de trabajo. Si estas estimaciones se mantienen coherentes para las 10 cargas de trabajo prioritarias, esas cargas de trabajo tardarán 400 horas.

La velocidad definida en el ejemplo anterior sugiere que la migración de las 10 primeras cargas de trabajo llevará cuatro iteraciones, lo que significa dos meses de tiempo de calendario. La primera iteración constará de 100 tareas que dan como resultado la migración de dos cargas de trabajo. En la siguiente iteración, una colección similar de 100 tareas dará como resultado la migración de tres cargas de trabajo.

> [!WARNING]
> El número de tareas anterior y las estimaciones se usan estrictamente como ejemplo. Las tareas técnicas rara vez son tan coherentes. No debería ver este ejemplo como un reflejo de la cantidad de tiempo necesaria para migrar una carga de trabajo.

## <a name="release-planning"></a>Planeamiento de la versión

En el contexto de la adopción de la nube, una versión se define como una colección de entregas que generan un valor empresarial suficiente para justificar el riesgo de interrupción de los procesos empresariales.

El lanzamiento de una versión de cualquier cambio relacionado con la carga de trabajo en un entorno de producción crea algunos cambios en los procesos empresariales. Idealmente, estos cambios no serán problemáticos y el negocio verá el valor de los cambios sin interrupciones significativas en el servicio. Pero el riesgo de interrupción del negocio está presente en cualquier cambio y no se debe tomar a la ligera.

Para asegurarse de que un cambio está justificado por su retorno potencial, el equipo de estrategia de la nube debe participar en el planeamiento de la versión. Una vez que las tareas están alineadas con los sprints, el equipo puede determinar una escala de tiempo aproximada de cuándo estará preparada para la versión de producción cada carga de trabajo. El equipo de estrategia de la nube revisaría la temporización de cada versión. El equipo identificaría entonces el punto de inflexión entre el riesgo y el valor empresarial.

**Ejemplo:** siguiendo con el ejemplo anterior, el equipo de estrategia de la nube ha revisado el plan de iteraciones. La revisión identificó dos puntos de versión. Durante la segunda iteración, estarán listas para la migración un total de cinco cargas de trabajo. Esas cinco cargas de trabajo proporcionarán un valor empresarial significativo y desencadenarán la primera versión. La siguiente versión vendrá dos iteraciones más adelante, cuando las cinco cargas de trabajo siguientes estén listas para su lanzamiento.

## <a name="assign-iteration-paths-and-tags"></a>Asignación de rutas de iteración y etiquetas

Para los clientes que administran los planes de adopción de la nube en Azure DevOps, los procesos anteriores se reflejan mediante la asignación de una ruta de iteración a cada tarea y caso de usuario. También se recomienda etiquetar cada carga de trabajo con una versión específica. El etiquetado y la asignación alimentan el rellenado automático de informes temporales.

## <a name="next-steps"></a>Pasos siguientes

[Realice una estimación de las escalas de tiempo](./timelines.md) para comunicar correctamente las expectativas.

> [!div class="nextstepaction"]
> [Estimación de escalas de tiempo](./timelines.md)
