---
title: 'Guía de gobernanza para empresas complejas: directiva corporativa inicial que está detrás de la estrategia de gobernanza'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Guía de gobernanza para empresas complejas: directiva corporativa inicial que está detrás de la estrategia de gobernanza'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 2d8c2923820883561f75902830425b1bd81eb846
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032532"
---
# <a name="governance-guide-for-complex-enterprises-initial-corporate-policy-behind-the-governance-strategy"></a>Guía de gobernanza para empresas complejas: directiva corporativa inicial que está detrás de la estrategia de gobernanza

La siguiente directiva corporativa define la posición inicial de gobernanza, que es el punto de inicio de esta guía. En este artículo se definen riesgos incipientes, las declaraciones de directiva iniciales y los procesos iniciales para aplicar las declaraciones de directiva.

> [!NOTE]
>La directiva corporativa no es un documento técnico, pero promueve muchas decisiones técnicas. El producto mínimo viable de gobernanza descrito en la [información general](./index.md) deriva, en última instancia, de esta directiva. Antes de implementar un producto mínimo viable de gobernanza, su organización debe desarrollar una directiva corporativa en función de sus propios objetivos y riesgos empresariales.

## <a name="cloud-governance-team"></a>Equipo de gobernanza de la nube

El CIO recientemente ha mantenido una reunión con el equipo de gobernanza de TI para conocer el historial de información personal y las directivas críticas, y revisar el impacto que podría tener cambiar esas directivas. También ha analizado el potencial general de la nube tanto para TI como para la empresa.

Después de la reunión, dos miembros del equipo de gobernanza de TI solicitaron permiso para investigar y dar soporte técnico a los trabajos de planeamiento de la nube. Al reconocer la necesidad de gobernanza y una oportunidad para limitar la TI en la sombra, la directora de gobernanza de TI apoyó la idea. Así nació el equipo de gobernanza de la nube. En los próximos meses heredarán la limpieza de la gran cantidad de errores cometidos durante la exploración en la nube desde una perspectiva de gobernanza. Esto les valdrá el sobrenombre de _custodios de la nube_. En posteriores iteraciones, esta guía mostrará los cambios sufridos por sus roles con el paso del tiempo.

[!INCLUDE [business-risk](../../../../includes/business-risks.md)]

## <a name="tolerance-indicators"></a>Indicadores de tolerancia

La tolerancia al riesgo actual es alta y el apetito por invertir en la gobernanza de la nube es bajo. Como tales, los indicadores de tolerancia actúan como sistema de advertencia anticipado para desencadenar la inversión de tiempo y energía. Si se observan los indicadores siguientes, es aconsejable cambiar la estrategia de gobernanza.

- **Administración de costos:** la escala de implementación supera los 1000 recursos en la nube, o bien los gastos mensuales superan los 10 000 dólares al mes.
- **Línea de base de identidad:** inclusión de aplicaciones con requisitos de autenticación multifactor de terceros o heredados.
- **Base de referencia de la seguridad:** inclusión de datos protegidos en planes de adopción de la nube definidos.
- **Coherencia de los recursos:** inclusión de cualquier aplicación crítica en planes de adopción de la nube definidos.

[!INCLUDE [policy-statements](../../../../includes/policy-statements.md)]

## <a name="next-steps"></a>Pasos siguientes

Esta directiva corporativa prepara el equipo de gobernanza de la nube para implementar el producto viable mínimo de gobernanza, que será la base para la adopción. El siguiente paso es implementar dicho producto mínimo viable.

> [!div class="nextstepaction"]
> [Guías prescriptivas explicadas](./prescriptive-guidance.md)
