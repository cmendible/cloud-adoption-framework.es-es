---
title: Guía de decisiones de suscripción
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información acerca de las suscripciones a la plataforma en la nube como servicio principal en las migraciones de Azure.
author: alexbuckgit
ms.author: abuck
ms.date: 06/07/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 209de4c03474a956edf629c9c24f6b29f492284b
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71023630"
---
# <a name="subscription-decision-guide"></a>Guía de decisiones de suscripción

Un diseño eficaz de suscripciones ayuda a las organizaciones a establecer una estructura para organizar los recursos de Azure durante un proceso de adopción de la nube.

Cada recurso de Azure, como una máquina virtual o una base de datos, está asociado a una suscripción. La adopción de Azure comienza con la creación de una suscripción, la asociación a una cuenta y la implementación de recursos en la suscripción. Para una introducción sobre estos conceptos, consulte [Conceptos básicos de Azure](../../ready/considerations/fundamental-concepts.md).

A medida que crece su patrimonio digital en Azure, es probable que necesite crear suscripciones adicionales para satisfacer sus necesidades. Azure le permite definir una jerarquía de grupos de administración para organizar las suscripciones y aplicar fácilmente la directiva correcta a los recursos adecuados. Para más información, consulte [Scaling with multiple Azure subscriptions](../../ready/considerations/scaling-subscriptions.md) (Escalado de varias suscripciones de Azure).

Estos son algunos ejemplos básicos del uso de grupos de administración para separar diferentes cargas de trabajo:

- **Producción frente a no producción:** Algunas empresas crean grupos de administración para separar las suscripciones de producción y las que no son de producción. Los grupos de administración permiten a estos clientes administrar roles y directivas más fácilmente. Por ejemplo, una suscripción que no es de producción puede otorgar a los desarrolladores acceso de **colaborador**, pero en producción solo tienen acceso de **lector**.
- **Servicios internos frente a servicios externos:** Al igual que sucede con las cargas de trabajo de producción en comparación con las que no son de producción, las empresas suelen tener requisitos, directivas y roles distintos para los servicios internos en comparación con los externos, orientados al cliente.

Esta guía de decisiones le ayuda a tener en cuenta diferentes métodos para organizar la jerarquía del grupo de administración.

## <a name="subscription-design-patterns"></a>Patrones de diseño de suscripciones

Como cada organización es diferente, los grupos de administración de Azure están diseñados para ser flexibles. El modelado de su entorno en la nube para reflejar la jerarquía de la organización le ayuda a definir y aplicar directivas en los niveles más altos de la jerarquía, y a confiar en la herencia para asegurarse de que esas directivas se aplicarán automáticamente a los grupos de administración situados más abajo. Aunque las suscripciones se pueden trasladar entre diferentes grupos de administración, resulta útil diseñar una jerarquía inicial de grupos de administración que refleje sus necesidades organizativas de forma anticipada.

Antes de finalizar el diseño de la suscripción, considere cómo las decisiones sobre la [coherencia de recursos](../resource-consistency/index.md) pueden influir en las opciones de diseño.

> [!NOTE]
> Los Contratos Enterprise (EA) de Azure le permiten definir otra jerarquía organizativa con fines de facturación. Esta jerarquía es distinta de la jerarquía del grupo de administración, que se centra en proporcionar un modelo de herencia para aplicar fácilmente directivas adecuadas y control de acceso a los recursos.

Los patrones de suscripción siguientes reflejan un aumento inicial de la sofisticación en el diseño de la suscripción, seguido de varias jerarquías más avanzadas que se pueden adaptar bien a su organización:

### <a name="single-subscription"></a>Suscripción única

Una sola suscripción por cuenta puede ser suficiente para las organizaciones que necesitan implementar un número pequeño de recursos hospedados en la nube. Este es el primer patrón de suscripción que se implementa cuando comienza el proceso de adopción de la nube, lo que permite implementaciones experimentales a pequeña escala o de prueba de concepto para explorar las funcionalidades de la nube.

### <a name="production-and-nonproduction-pattern"></a>Patrón de producción y de no producción

Una vez que esté listo para implementar una carga de trabajo en un entorno de producción, deberá agregar una suscripción adicional. Esto le ayuda a mantener los datos de producción y otros recursos fuera de los entornos de desarrollo y pruebas. Puede aplicar también fácilmente dos conjuntos diferentes de directivas en los recursos de las dos suscripciones.

![Patrón de suscripción de producción y de no producción](../../_images/ready/basic-subscription-model.png)

### <a name="workload-separation-pattern"></a>Patrón de separación de cargas de trabajo

A medida que una organización agrega nuevas cargas de trabajo a la nube, las diferentes propiedades de las suscripciones o una separación básica de las responsabilidades puede resultar en varias suscripciones en los grupos de administración de producción y de no producción. Aunque este enfoque proporciona una separación básica de cargas de trabajo, no aprovecha de manera significativa el modelo de herencia a la hora de aplicar automáticamente directivas en un subconjunto de las suscripciones.

![Patrón de separación de cargas de trabajo](../../_images/ready/management-group-hierarchy.png)

### <a name="application-category-pattern"></a>Patrón de categoría de aplicación

A medida que crece la superficie en la nube de la organización se crean normalmente suscripciones para admitir aplicaciones que tienen diferencias fundamentales con respecto a importancia para la empresa, requisitos de cumplimiento, controles de acceso o necesidades de protección de datos. En el patrón de suscripción de producción y de no producción, las suscripciones que admiten estas categorías de aplicaciones se organizan en el grupo de administración de producción o de no producción según corresponda. Normalmente, el personal central de operaciones de TI posee y administra estas suscripciones.

![Patrón de categoría de aplicación](../../_images/infra-subscriptions/application.png)

Cada organización categorizará las aplicaciones de forma diferente, a menudo separarán las suscripciones basadas en aplicaciones o servicios específicos o en arquetipos de aplicación. Esta categorización a menudo está diseñada para admitir cargas de trabajo que es probable que consuman la mayor parte de los límites de recursos de una suscripción o cargas de trabajo críticas independientes para asegurarse de que no compiten con otras cargas de trabajo dentro de estos límites. Entre las cargas de trabajo que pueden justificar una suscripción independiente en este patrón se incluyen:

- Cargas de trabajo críticas.
- Aplicaciones con datos protegidos.
- Aplicaciones experimentales.
- Aplicaciones sujetas a requisitos legales (como HIPAA o FedRAMP).
- Cargas de trabajo por lotes.
- Cargas de trabajo de macrodatos como Hadoop.
- Cargas de trabajo en contenedores con orquestadores de implementación, como Kubernetes.
- Cargas de trabajo de análisis.

### <a name="functional-pattern"></a>Patrón funcional

El patrón funcional organiza las suscripciones y cuentas a lo largo de líneas funcionales como finanzas, ventas o soporte técnico de TI, mediante una jerarquía de grupos de administración.

### <a name="business-unit-pattern"></a>Patrón de unidad de negocio

Este patrón agrupa las suscripciones y cuentas en función de categorías de pérdidas y ganancias, unidades de negocio, divisiones, centros de beneficios o estructuras empresariales similares mediante una jerarquía de grupo de administración.

### <a name="geographic-pattern"></a>Patrón geográfico

Para organizaciones con operaciones globales, el patrón geográfico agrupa las suscripciones y cuentas en función de las regiones geográficas mediante una jerarquía de administración de grupos.

## <a name="mixed-patterns"></a>Patrones mixtos

Las jerarquías de los grupos de administración pueden incluir hasta seis niveles de profundidad. Esto le proporciona flexibilidad para crear una jerarquía que combina varios de estos patrones para satisfacer sus necesidades organizativas. Por ejemplo, el diagrama siguiente muestra una jerarquía organizativa que combina un patrón de unidad de negocio con un patrón geográfico.

![Patrón de suscripción mixto](../../_images/infra-subscriptions/mixed.png)

## <a name="related-resources"></a>Recursos relacionados

- [Administración del acceso a recursos de Azure](../../govern/resource-consistency/resource-access-management.md)
- [Varias capas de gobernanza en grandes empresas](../../govern/guides/complex/multiple-layers-of-governance.md)
- [Varias regiones geográficas](../../migrate/expanded-scope/multiple-regions.md)

## <a name="next-steps"></a>Pasos siguientes

El diseño de suscripciones es solo uno de los principales componentes de infraestructura que requieren decisiones de arquitectura durante un proceso de adopción de la nube. Visite la [introducción a las guías de decisión](../index.md) para obtener información sobre los patrones o los modelos alternativos que se usan al tomar decisiones de diseño para otros tipos de infraestructura.

> [!div class="nextstepaction"]
> [Guías de decisiones sobre arquitectura](../index.md)
