---
title: 'Guía para empresa estándar: directiva corporativa inicial que está detrás de la estrategia de gobernanza'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Guía para empresa estándar: directiva corporativa inicial que está detrás de la estrategia de gobernanza'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 4da4899038ca86bec2f1d003f9eaaee293119a09
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031737"
---
# <a name="standard-enterprise-guide-initial-corporate-policy-behind-the-governance-strategy"></a>Guía para empresa estándar: directiva corporativa inicial que está detrás de la estrategia de gobernanza

La siguiente directiva corporativa define una posición de gobernanza inicial, que es el punto de inicio de esta guía. En este artículo se definen riesgos incipientes, las declaraciones de directiva iniciales y los procesos iniciales para aplicar las declaraciones de directiva.

> [!NOTE]
>La directiva corporativa no es un documento técnico, pero promueve muchas decisiones técnicas. El producto mínimo viable de gobernanza descrito en la [información general](./index.md) deriva, en última instancia, de esta directiva. Antes de implementar un producto mínimo viable de gobernanza, su organización debe desarrollar una directiva corporativa en función de sus propios objetivos y riesgos empresariales.

## <a name="cloud-governance-team"></a>Equipo de gobernanza de la nube

En esta narración, el equipo de gobernanza de la nube consta de dos administradores de sistemas que han reconocido la necesidad de gobernanza. Durante los próximos meses, tendrán que hacerse cargo de limpiar la gobernanza de la presencia en la nube de la empresa, lo cual les hará merecedores del sobrenombre de _custodios de la nube_. En iteraciones posteriores, es probable que este sobrenombre cambie.

[!INCLUDE [business-risk](../../../../includes/business-risks.md)]

## <a name="tolerance-indicators"></a>Indicadores de tolerancia

La tolerancia al riesgo actual es alta y el apetito por invertir en la gobernanza de la nube es bajo. Como tales, los indicadores de tolerancia actúan como sistema de advertencia anticipado para desencadenar una mayor inversión de tiempo y energía. Si se observan los indicadores siguientes, debe mejorar de forma iterativa la estrategia de gobernanza.

- **Administración de costos:** la escala de implementación supera los 100 recursos en la nube, o bien los gastos mensuales superan los 1000 USD al mes.
- **Base de referencia de la seguridad:** inclusión de datos protegidos en planes de adopción de la nube definidos.
- **Coherencia de los recursos:** inclusión de cualquier aplicación crítica en planes de adopción de la nube definidos.

[!INCLUDE [policy-statements](../../../../includes/policy-statements.md)]

## <a name="next-steps"></a>Pasos siguientes

Esta directiva corporativa prepara el equipo de gobernanza de la nube para implementar el producto viable mínimo de gobernanza, que será la base para la adopción. El siguiente paso es implementar dicho producto mínimo viable.

> [!div class="nextstepaction"]
> [Guías prescriptivas explicadas](./prescriptive-guidance.md)
