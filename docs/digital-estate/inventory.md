---
title: Recopilación de datos de inventario de un patrimonio digital
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Cómo recopilar el inventario de un patrimonio digital
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 6b6bbfef4f9e404433119d412cd4bf625cd3b480
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71023497"
---
# <a name="gather-inventory-data-for-a-digital-estate"></a>Recopilación de datos de inventario de un patrimonio digital

El desarrollo de un inventario es el primer paso del [planeamiento del patrimonio digital](./index.md). En este proceso, se recopila una lista de los recursos de TI que posibilitan funciones de negocio específicas para su posterior análisis y racionalización. En este artículo se da por supuesto que un análisis de abajo hacia arriba es el más adecuado para el planeamiento de las necesidades. Para más información, consulte [Enfoques para el planeamiento del patrimonio digital](./approach.md).

## <a name="take-inventory-of-a-digital-estate"></a>Realizar un inventario de un patrimonio digital

El inventario que posibilita un patrimonio digital cambia en función de la transformación digital deseada y el recorrido de transformación correspondiente.

- **Migración a la nube.**  Suele ser recomendable que, durante una migración a la nube, recopile el inventario con herramientas de análisis que crean una lista centralizada de todas las máquinas virtuales y los servidores. Algunas herramientas también pueden crear mapas de red y dependencias, lo que ayuda a definir la alineación de la carga de trabajo.

- **Innovación en las aplicaciones.** Durante un esfuerzo de innovación en aplicaciones habilitadas para la nube, el inventario comienza con el usuario. Un buen lugar para comenzar es la asignación de la experiencia del cliente de principio a fin. La alineación de dicha asignación con las aplicaciones, API, datos y otros recursos produce un inventario detallado para el análisis.

- **Innovación en los datos.** Los esfuerzos de innovación en datos habilitados para la nube se centran en el producto o servicio. Un inventario incluye también una asignación de las oportunidades para romper el mercado, así como las funcionalidades necesarias.

## <a name="accuracy-and-completeness-of-an-inventory"></a>Precisión e exhaustividad de un inventario

Un inventario rara vez se completa totalmente en su primera iteración. Es muy recomendable que el equipo de estrategia de la nube coordine a las partes interesadas y los usuarios avanzados para validar el inventario. Cuando sea posible, use herramientas adicionales, como el análisis de la red y las dependencias, para identificar los recursos a los que se está enviando tráfico, pero no están en el inventario.

## <a name="next-steps"></a>Pasos siguientes

Una vez que se recopila y valida un inventario, se puede racionalizar. La racionalización del inventario es el siguiente paso en el planeamiento del patrimonio digital.

> [!div class="nextstepaction"]
> [Racionalización del patrimonio digital](./rationalize.md)
