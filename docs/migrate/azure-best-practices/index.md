---
title: Procedimientos recomendados de migración de Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introducción a los procedimientos recomendados de migración de Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: e8a7ae0af3b64a6d7e04555fe64a6189d964b3ff
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70816574"
---
# <a name="azure-migration-best-practices"></a>Procedimientos recomendados de migración de Azure

Azure proporciona varias herramientas que facilitan el proceso de migración. Esta sección de Cloud Adoption Framework está diseñada para ayudar a los lectores a implementar dichas herramientas de acuerdo con los procedimientos recomendados para la migración. Estos procedimientos recomendados se alinean con uno de los procesos del modelo de migración de Cloud Adoption Framework que se representa a continuación.

Expanda cualquier proceso de la tabla de contenido de la izquierda para ver los procedimientos recomendados que son normalmente necesarios durante dicho proceso.

![Modelo de migración de Cloud Adoption Framework](../../_images/operational-transformation-migrate.png)

> [!NOTE]
> La valoración de los recursos y la planeación del patrimonio digital representan dos niveles diferentes de valoración y planeación de la migración:
>
> - **Planeación del patrimonio digital:** El patrimonio digital se planea o racionaliza durante la planeación, con el fin de establecer un trabajo pendiente de migración global. Sin embargo, dicho plan se basa en algunas suposiciones y detalles que es preciso validar para poder migrar a una carga de trabajo.
> - **Valoración de recursos:** Los recursos individuales de una carga de trabajo se deben valorar antes de que esta se migre, con el fin de evaluar la compatibilidad de la nube y conocer las restricciones de arquitectura y tamaño. Este proceso valida las suposiciones iniciales y proporciona los detalles necesarios para migrar un recurso individual.
