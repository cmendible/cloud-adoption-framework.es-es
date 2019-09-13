---
title: Guía de gobernanza para empresas estándar
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Guía de gobernanza para empresas estándar
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 82467948ae3141ef1f961ab07a503be485a1bc6f
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70908462"
---
# <a name="standard-enterprise-governance-guide"></a>Guía de gobernanza para empresas estándar

## <a name="overview-of-best-practices"></a>Introducción sobre los procedimientos recomendados

Esta guía de gobernanza muestra las experiencias de una empresa ficticia a través de diversas fases de madurez del proceso de gobernanza. Se basa en experiencias reales de los clientes. Los procedimientos recomendados se basan en las restricciones y necesidades de la empresa ficticia.

Como punto de inicio rápido, esta información general define un producto viable mínimo (MVP) para la gobernanza basado en una guía preceptiva. También proporciona vínculos a algunas mejoras de gobernanza que agregan más procedimientos recomendados a medida que surgen nuevos riesgos técnicos o empresariales.

> [!WARNING]
> Este MVP es un punto de inicio de la base de referencia, basado en un conjunto de suposiciones. Incluso este conjunto mínimo de procedimientos recomendados se basa en directivas corporativas controladas por tolerancias al riesgo y riesgos empresariales únicos. Para ver si estas suposiciones se aplican a usted, lea la [narrativa más larga](./narrative.md) que sigue este artículo.

### <a name="governance-best-practices"></a>Procedimientos recomendados sobre gobernanza

Estos procedimientos recomendados sirven como punto de partida para que una organización agregue barreras de seguridad de gobernanza de forma rápida y coherente a las suscripciones.

### <a name="resource-organization"></a>Organización de recursos

En el siguiente diagrama se muestra la jerarquía de MVP de gobernanza para organizar recursos.

![Diagrama de organización de los recursos](../../../_images/governance/resource-organization.png)

Todas las aplicaciones deben implementarse en el área adecuada de la jerarquía de grupos de recursos, suscripción y grupos de administración. Durante el planeamiento de la implementación, el equipo de gobernanza en la nube creará los nodos necesarios en la jerarquía para capacitar a los equipos de adopción de la nube.

1. Un grupo de administración para cada tipo de entorno (por ejemplo, producción, desarrollo y pruebas).
2. Dos suscripciones, una para producción y otra para fines no relacionados con producción.
3. Grupos de recursos adecuados con aplicación del control de acceso basado en rol en estas suscripciones.
4. Debe aplicarse una [nomenclatura coherente](../../../ready/considerations/name-and-tag.md) en cada nivel de esta jerarquía de agrupación.

A continuación, se indica un ejemplo de este patrón de uso:

![Ejemplo de organización de los recursos para una empresa mediana](../../../_images/governance/mid-market-resource-organization.png)

Estos patrones proporcionan espacio para el crecimiento sin complicar la jerarquía de forma innecesaria.

[!INCLUDE [governance-of-resources](../../../../includes/caf-governance-of-resources.md)]

## <a name="iterative-governance-improvements"></a>Mejoras de gobernanza iterativas

Una vez que se ha implementado este MVP, se pueden incorporar capas de gobernanza rápidamente en el entorno. Estas son algunas formas de mejorar el MVP para satisfacer necesidades empresariales específicas:

- [Base de referencia de seguridad para datos protegidos](./security-baseline-evolution.md)
- [Configuraciones de recursos para aplicaciones críticas](./resource-consistency-evolution.md)
- [Controles de administración de costos](./cost-management-evolution.md)
- [Controles de evolución en varias nubes](./multicloud-evolution.md)

<!-- markdownlint-disable MD026 -->

## <a name="what-does-this-guidance-provide"></a>¿Qué proporciona esta guía?

En el MVP, prácticas y herramientas de la materia de [aceleración de la implementación](../../deployment-acceleration/index.md) se establecen para aplicar rápidamente la directiva corporativa. En concreto, el MVP usa Azure Blueprints, Azure Policy y grupos de administración de Azure para aplicar algunas directivas corporativas básicas, tal como se define en la narrativa de esta empresa ficticia. Dichas directivas corporativas se aplican mediante plantillas de Resource Manager y directivas de Azure para establecer una base de referencia pequeña para la identidad y la seguridad.

![Ejemplo de un MVP de gobernanza incremental](../../../_images/governance/governance-mvp.png)

## <a name="incremental-improvement-of-governance-practices"></a>Mejora incremental de las prácticas de gobernanza

Con el tiempo, este MVP de gobernanza se usará para mejorar las prácticas de gobernanza. A medida que avanza la adopción, aumenta el riesgo empresarial. Para administrar esos riesgos, se cambiarán varias materias dentro del modelo de gobernanza de Cloud Adoption Framework. En artículos posteriores de esta serie se explica la mejora incremental de la directiva corporativa que afecta a la empresa ficticia. Estas mejoras se producen en tres materias:

- Administración de costos, a medida que la adopción se escala.
- Base de referencia de seguridad, a medida que los datos protegidos se implementan.
- Coherencia de recursos, a medida que las operaciones de TI empiezan a admitir cargas de trabajo críticas.

![Ejemplo de un MVP de gobernanza incremental](../../../_images/governance/governance-evolution.png)

## <a name="next-steps"></a>Pasos siguientes

Ahora que se ha familiarizado con el MVP de gobernanza y tiene una idea de las mejoras de gobernanza que se deben seguir, lea la narrativa de apoyo para obtener contexto adicional.

> [!div class="nextstepaction"]
> [Lectura de la narrativa de apoyo](./narrative.md)