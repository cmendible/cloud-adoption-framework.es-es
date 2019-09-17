---
title: Trabajo pendiente de iteración y liberación
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Creación de un trabajo pendiente de iteración y liberación
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: dc567c80b6193d651c8bf3884476728a8d3daa7f
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70839086"
---
# <a name="manage-change-in-an-incremental-migration-effort"></a>Administración de los cambios en un esfuerzo de migración incremental

En este artículo se presupone que los procesos de migración son incrementales por naturaleza y que se ejecutan en paralelo al [proceso de control](../../../governance/index.md). Sin embargo, se podría usar la misma guía para rellenar las tareas iniciales en una estructura de descomposición del trabajo para los enfoques tradicionales de administración de cambios en cascada.

## <a name="release-backlog"></a>Trabajo pendiente de liberación

Un *trabajo pendiente de liberación* consta de una serie de recursos (máquinas virtuales, bases de datos, archivos y aplicaciones, entre otros) que se deben migrar antes de que se pueda liberar una carga de trabajo para su uso de producción en la nube. Durante cada iteración, el equipo de adopción de la nube documenta y calcula los esfuerzos necesarios para trasladar cada recurso a la nube. Consulte la sección "Trabajo pendiente de iteración" que aparece a continuación.

## <a name="iteration-backlog"></a>Trabajo pendiente de iteración

Un *trabajo pendiente de iteración* es una lista del trabajo detallado que se necesita para migrar un número específico de recursos desde el patrimonio digital existente a la nube. Las entradas de esta lista se suelen almacenar en una herramienta de administración ágil, como Azure DevOps, como elementos de trabajo.

Antes de iniciar la primera iteración, el equipo de adopción de la nube especifica su duración, que habitualmente va de dos a cuatro semanas. Este tiempo asignado es importante para crear un período de tiempo de inicio y finalización para cada conjunto de actividades confirmadas. Mantener ventanas de ejecución coherentes facilita la medición de la velocidad (el ritmo de la migración) y la alineación con las necesidades empresariales en constante evolución.

Antes de cada iteración, el equipo revisa el trabajo pendiente de liberación, calculando el esfuerzo y las prioridades de los recursos que se van a migrar. A continuación, se confirma para ofrecer un número específico de migraciones acordadas. Una vez que el equipo de adopción de la nube la acepta, la lista de actividades se convierte en el *trabajo pendiente de iteración actual*.

Durante cada iteración, los miembros del equipo trabajan como un equipo de organización automática para cumplir con los compromisos existentes en el trabajo pendiente de iteración actual.

## <a name="next-steps"></a>Pasos siguientes

Una vez que se define el trabajo pendiente de iteración y el equipo de adopción de la nube lo acepta, se pueden finalizar las [aprobaciones de administración de cambios](./approve.md).

> [!div class="nextstepaction"]
> [Aprobación de los cambios de arquitectura antes de la migración](./approve.md)
