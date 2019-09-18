---
title: Escalas de tiempo de un plan de adopción de la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Escalas de tiempo de un plan de adopción de la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 4e095dd90711f201935e88ea5f2712e881a8574b
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70837626"
---
# <a name="timelines-in-a-cloud-adoption-plan"></a>Escalas de tiempo de un plan de adopción de la nube

En el artículo anterior de esta serie, las cargas de trabajo y las tareas se asignaron a [versiones e iteraciones](./iteration-paths.md). Estas asignaciones alimentan las estimaciones de la escala de tiempo en este artículo.

Las estructuras de descomposición del trabajo (WBS) se usan normalmente en herramientas de administración de proyectos secuenciales. Representan cómo se completarán las tareas dependientes durante un período de tiempo. Estas estructuras funcionan bien cuando las tareas son secuenciales por naturaleza. Las interdependencias de las tareas que se encuentran en la adopción de la nube hacen que estas estructuras sean difíciles de administrar. Para rellenar esta brecha, puede hacer una estimación de las escalas de tiempo en función de las asignaciones de rutas de iteración ocultando la complejidad.

## <a name="estimate-timelines"></a>Estimación de escalas de tiempo

Para desarrollar una escala de tiempo, empiece con las versiones. Estos objetivos de versión crean una fecha objetivo para cualquier impacto empresarial. Las iteraciones ayudan a alinear esas versiones con períodos de tiempo específicos.

Si se necesitan hitos más granulares en la escala de tiempo, utilice la asignación de iteraciones para indicar los hitos. Para realizar esta asignación, supongamos que la última instancia de una tarea relacionada con la carga de trabajo puede servir como el hito final. Los equipos también etiquetan normalmente la tarea final como un hito.

Para cualquier nivel de granularidad, use el último día de la iteración como la fecha de cada hito. Esto vincula la finalización de la adopción de la carga de trabajo a una fecha específica. Puede realizar un seguimiento de la fecha en una hoja de cálculo o una herramienta de administración de proyectos secuenciales como Microsoft Project.

## <a name="delivery-plans-in-azure-devops"></a>Planes de entrega en Azure DevOps

Si usa Azure DevOps para administrar el plan de adopción de la nube, considere la posibilidad de usar la extensión [Microsoft Delivery Plans](https://marketplace.visualstudio.com/items?itemName=ms.vss-plans). Esta extensión puede crear rápidamente una representación visual de la escala de tiempo en función de las asignaciones de versiones y de iteraciones.
