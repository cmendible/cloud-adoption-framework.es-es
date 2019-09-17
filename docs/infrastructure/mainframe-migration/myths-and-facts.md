---
title: 'Migración del sistema central: Mitos y verdades'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migre aplicaciones desde entornos de sistema central a Azure, una infraestructura que se ha probado de alta disponibilidad y escalable para los sistemas que se ejecutan actualmente en sistemas centrales.
author: njray
ms.author: v-nanra
ms.date: 12/27/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 7a3e1c7cd0003191838f08569b18de4626745745
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70838322"
---
# <a name="mainframe-myths-and-facts"></a>Mitos y verdades del sistema central

Los sistemas centrales aparecen de en un lugar destacado de la historia de la informática y siguen siendo viables para cargas de trabajo muy específicas. La mayoría está de acuerdo en que los sistemas centrales son una plataforma probada, con procedimientos operativos arraigados, que los convierten en entornos de confianza y sólidos. Hay ejecuciones de software basadas en el uso, medidas en millones de instrucciones por segundo (MIPS), e informes extensos del uso disponibles para anulaciones.

La confiabilidad, la disponibilidad y la capacidad de procesamiento de los sistemas centrales se han encargado de proporciones casi míticas. Para evaluar las cargas de trabajo de los sistemas centrales que son más adecuadas para Azure, primero debe distinguir entre los mitos y la realidad.

## <a name="myth-mainframes-never-go-down-and-have-a-minimum-of-five-9s-of-availability"></a>Mito: Los sistemas centrales nunca dejan de funcionar y tienen un mínimo de cinco nueves (99,999 %) de disponibilidad.

El hardware del sistema central y los sistemas operativos se perciben confiables y estables. Pero la realidad es que debe programarse un tiempo de inactividad para el mantenimiento y reinicios (denominados cargas programa inicial o IPL). Cuando se toman en consideración estas tareas, una solución de sistema central suele estar más cerca de dos o tres nueves de disponibilidad, lo que es equivalente a la de los servidores de gama alta, basados en Intel.

Los sistemas centrales también son vulnerables ante desastres como cualquier otro servidor y requieren sistemas de alimentación ininterrumpida (SAI) para controlar estos tipos de errores.

## <a name="myth-mainframes-have-limitless-scalability"></a>Mito: Los sistemas centrales gozan de una escalabilidad sin límites.

La escalabilidad de un sistema central depende de la capacidad del software del sistema, como el sistema de control de la información de clientes (CICS) y la capacidad de las nuevas instancias de motores y almacenamiento del sistema central. Algunas grandes compañías que usan sistemas centrales han personalizado el rendimiento de su CICS y han sobrepasado la capacidad de los sistemas centrales más grandes disponibles.

## <a name="myth-intel-based-servers-are-not-as-powerful-as-mainframes"></a>Mito: Los servidores basados en Intel no son tan eficaces como los sistemas centrales.

Los nuevos sistemas basados en Intel con núcleo denso tienen tanta capacidad de proceso como los sistemas centrales.

## <a name="myth-the-cloud-cant-accommodate-mission-critical-applications-for-large-companies-such-as-financial-institutions"></a>Mito: La nube no puede acomodar aplicaciones críticas de empresas grandes, como instituciones financieras.

Aunque puede haber algunos casos aislados en que las soluciones en la nube se quedan cortas, suele ser porque no se pueden distribuir los algoritmos de la aplicación. Estos pocos ejemplos son la excepción, no la regla.

## <a name="summary"></a>Resumen

En comparación, Azure proporciona una plataforma alternativa que es capaz de ofrecer unas características y una funcionalidad equivalentes a un sistema central con un costo mucho menor. Además, el costo total de propiedad (TCO) del modelo de costo controlado por el uso basado en suscripciones de la nube es mucho más económico que los sistemas centrales.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Realizar el cambio desde sistemas centrales a Azure](migration-strategies.md)
