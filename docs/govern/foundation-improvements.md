---
title: Mejora de una base de gobernanza de la nube inicial
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Aprenda a mejorar gradualmente la base de gobernanza de la nube inicial.
author: BrianBlanchard
ms.author: brblanch
ms.date: 01/03/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: d4a0338daa65ea4269077f15acee05cd99a5fb10
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031160"
---
# <a name="improve-your-initial-cloud-governance-foundation"></a>Mejora de una base de gobernanza de la nube inicial

En este artículo se supone que ha establecido una [base de gobernanza de la nube inicial](./initial-foundation.md). A medida que se implementa el plan de adopción de la nube, surgen riesgos tangibles a partir de los enfoques propuestos mediante los cuales los equipos quieren adoptar la nube. A medida que estos riesgos afloran en las conversaciones de planeamiento del lanzamiento, use la siguiente cuadrícula para identificar rápidamente algunos procedimientos recomendados para aprovechar el plan de adopción y evitar que los riesgos se conviertan en amenazas reales.

## <a name="maturity-vectors"></a>Vectores de madurez

En cualquier momento, se pueden aplicar las siguientes guías prescriptivas a la base de gobernanza inicial para afrontar los riesgos o necesidades que se mencionan en la siguiente tabla.

> [!IMPORTANT]
> La organización de los recursos puede afectar al modo en que se aplica esta guía prescriptiva. Es importante comenzar con las recomendaciones que mejor se adapten a la base de gobernanza de la nube inicial que implementó en el paso anterior.

|Riesgo o necesidad | Pequeña y mediana empresa | Gran empresa |
|---|---|---|
|Información confidencial en la nube|[Guía prescriptiva](./guides/standard/security-baseline-improvement.md)|[Guía prescriptiva](./guides/complex/security-baseline-improvement.md)|
|Aplicaciones críticas en la nube|[Guía prescriptiva](./guides/standard/resource-consistency-improvement.md)|[Guía prescriptiva](./guides/complex/resource-consistency-improvement.md)|
|Administración de costos de la nube|[Guía prescriptiva](./guides/standard/cost-management-improvement.md)|[Guía prescriptiva](./guides/complex/cost-management-improvement.md)|
|Nube múltiple|[Guía prescriptiva](./guides/standard/multicloud-improvement.md)|[Guía prescriptiva](./guides/complex/multicloud-improvement.md)|
|Administración de identidades compleja o heredada|         |[Guía prescriptiva](./guides/complex/identity-baseline-improvement.md)|
|Varias capas de gobernanza|         |[Guía prescriptiva](./guides/complex/multiple-layers-of-governance.md)|

## <a name="next-steps"></a>Pasos siguientes

Además de la aplicación de las guías prescriptivas, la metodología de gobernanza de Cloud Adoption Framework se puede personalizar para adaptarse a restricciones empresariales específicas. Después de seguir las recomendaciones aplicables, [evalúe las directivas corporativas para comprender los requisitos de personalización adicionales](./corporate-policy.md).

> [!div class="nextstepaction"]
> [Evaluación de las directivas corporativas](./corporate-policy.md)
