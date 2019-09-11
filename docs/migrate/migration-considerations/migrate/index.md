---
title: Ejecución de una migración
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ejecución de una migración
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 21520edecc7ba874713561672cd0bd38aa96c0a2
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818240"
---
# <a name="execute-a-migration"></a>Ejecución de una migración

Una vez que se haya valorado una carga de trabajo, se puede migrar a la nube. Esta serie de artículos explica las diversas actividades que pueden estar implicadas en la ejecución de una migración.

## <a name="objective"></a>Objetivo

El objetivo de una migración es migrar una sola carga de trabajo a la nube.

## <a name="definition-of-done"></a>Definición de *Listo*

La fase de migración está completa cuando la carga de trabajo está almacenada provisionalmente y lista para las pruebas en la nube, incluidos todos los recursos dependientes necesarios para que la carga de trabajo funcione. Durante el proceso de optimización, la carga de trabajo se prepara para su uso en producción.

Esta definición de *listo* puede variar en función de los procesos de pruebas y migración. El siguiente artículo de esta serie trata sobre la [elección de un modelo de promoción](./promotion-models.md) y puede ayudarle a entender cuándo sería mejor promover una carga de trabajo migrada a producción.

## <a name="accountability-during-migration"></a>Responsabilidad durante la migración

El equipo de adopción de la nube es responsable de todo el proceso de migración. No obstante, los miembros del equipo de estrategia en la nube también tienen algunas responsabilidades como se analiza en la siguiente sección.

## <a name="responsibilities-during-migration"></a>Responsabilidades durante la migración

Además de la responsabilidad de alto nivel, hay acciones de las que un individuo o grupo se deben hacer responsables directamente. Estas son algunas de las actividades que se tienen que asignar a las partes responsables:

- **Corrección.** Resuelva los problemas de compatibilidad que impidan que la carga de trabajo se migre a la nube.
  - Como ya se ha descrito en el artículo de requisitos previos acerca de la [complejidad técnica y la administración de cambios](../prerequisites/technical-complexity.md), se debe tomar una decisión de antemano para determinar cómo se ejecuta esta actividad. Concretamente, ¿será el equipo de adopción de la nube el que complete la corrección durante el mismo sprint que el esfuerzo de migración real? O, por el contrario, ¿se usará una oleada o modelo de fábrica para completar la corrección en una iteración independiente? Si no todos los miembros del equipo pueden dar una respuesta a esta pregunta básica sobre el proceso, es recomendable que revisen la sección sobre [Requisitos previos](../prerequisites/index.md).
- **Replicación.** Cree una copia de cada recurso en la nube para sincronizar las máquinas virtuales, los datos y las aplicaciones con recursos en la nube.
  - Según el modelo de promoción, puede que se necesiten herramientas diferentes para completar esta actividad.
- **Almacenamiento provisional.** Una vez que todos los recursos de una carga de trabajo se han replicado y comprobado, se puede almacenar provisionalmente la carga de trabajo para pruebas empresariales y para la ejecución de un plan de cambios en la empresa.

## <a name="next-steps"></a>Pasos siguientes

Con una comprensión general del proceso de migración, está listo para [decidir sobre un modelo de promoción](./promotion-models.md).

> [!div class="nextstepaction"]
> [Decidir sobre un modelo de promoción](./promotion-models.md)
