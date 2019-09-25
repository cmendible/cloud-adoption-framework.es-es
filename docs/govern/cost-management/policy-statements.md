---
title: Declaraciones de directivas de ejemplo de administración de costos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Declaraciones de directivas de ejemplo de administración de costos
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: efc105298462afa9dfac76f0505854fdc157c17d
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71220947"
---
# <a name="cost-management-sample-policy-statements"></a>Declaraciones de directivas de ejemplo de administración de costos

Las declaraciones individuales de directiva de nube son directrices para abordar los riesgos específicos identificados durante el proceso de evaluación de riesgos. Estas declaraciones deben proporcionar un breve resumen de los riesgos y los planes para resolverlos. La definición de cada declaración debe incluir estos fragmentos de información:

- **Riesgo empresarial.** Un resumen del riesgo que esta directiva abordará.
- **Declaración de directiva**. Una explicación clara que resuma los requisitos de la directiva.
- **Opciones de diseño**. Recomendaciones que requieren acción, especificaciones u otras instrucciones que los equipos de TI y los desarrolladores pueden usar al implementar la directiva.

Las siguientes declaraciones de la directiva de ejemplo abordan algunos riesgos empresariales comunes relacionados con los costos. Estas declaraciones son ejemplos a los que se puede hacer referencia al elaborar el borrador de las declaraciones de directiva para satisfacer las necesidades de su organización. Estos ejemplos no pretenden ser excluyentes y hay varias opciones posibles de directiva para solucionar cada riesgo concreto identificado. Trabaje estrechamente con los equipos de TI y de dirección para identificar las mejores directivas para su conjunto de riesgos en particular.

## <a name="future-proofing"></a>Perdurabilidad

**Riesgo empresarial**: Criterios actuales que no garantizan una inversión en una materia de administración de costos por parte del equipo de gobernanza. Sin embargo, rentabilizará la inversión en el futuro.

**Declaración de directiva**: debe asociar todos los recursos implementados en la nube con una unidad de facturación, una aplicación y una carga de trabajo. Esta directiva garantizará la rentabilidad de los futuros esfuerzos de administración de costos.

**Opciones de diseño**: para obtener información sobre cómo establecer una base orientada al futuro, consulte los artículos relacionados con la creación de un producto viable mínimo de gobernanza en las [guías prácticas sobre diseño](../guides/index.md), incluidas como parte de la guía Cloud Adoption Framework.

## <a name="budget-overruns"></a>Rebasamientos del presupuesto

**Riesgo empresarial**: la implementación de autoservicio plantea un riesgo de exceso de gastos.

**Declaración de directiva**: todas las implementaciones en la nube deben asignarse a una unidad de facturación con un presupuesto aprobado y un mecanismo para establecer límites presupuestarios.

**Opciones de diseño**: en Azure, puede controlar el presupuesto con [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/manage-budgets).

## <a name="underutilization"></a>Infrautilización

**Riesgo empresarial**: la empresa ha realizado el prepago de servicios en la nube o ha asumido un compromiso anual de gasto de una cantidad específica. Existe el riesgo de que no se use la cantidad acordada, lo que supone una pérdida de la inversión.

**Declaración de directiva**: Cada unidad de facturación con un presupuesto asignado para la nube se reunirá cada año para determinar los presupuestos, cada trimestre para ajustarlos y todos los meses para asignar el tiempo para revisar el gasto previsto frente al real. Analice todas las desviaciones superiores al 20 % con el jefe de la unidad de facturación con carácter mensual. Para fines de seguimiento, asigne todos los recursos a una unidad de facturación.

**Opciones de diseño**:

- en Azure, el gasto previsto frente al real se puede administrar con [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/quick-acm-cost-analysis).
- Hay varias opciones para agrupar recursos por unidad de facturación. En Azure, es necesario elegir un [modelo de coherencia de recursos](../../decision-guides/resource-consistency/index.md) en colaboración con el equipo de gobernanza, que se deberá aplicar a todos los recursos.

## <a name="overprovisioned-assets"></a>Recursos sobreaprovisionados

**Riesgo empresarial**: en los centros de datos locales tradicionales, es una práctica común implementar los recursos con un planeamiento de capacidad adicional para abordar crecimientos en un futuro lejano. La nube puede escalar más rápido que el equipo tradicional. Los precios de los recursos en la nube también se fijan en función de la capacidad técnica. Existe el riesgo de que la antigua práctica local infle el gasto en la nube artificialmente.

**Declaración de directiva**: todos los recursos implementados en la nube deben inscribirse en un programa que pueda supervisar la utilización y notificar cualquier aumento de capacidad por encima del 50 % de utilización. Todos los recursos implementados en la nube deben agruparse o etiquetarse de forma lógica, para que los miembros del equipo de gobernanza puedan interactuar con el propietario de la carga de trabajo para abordar cualquier optimización de recursos sobreaprovisionados.

**Opciones de diseño**:

- en Azure, [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations) puede proporcionar recomendaciones de optimización.
- Hay varias opciones para agrupar recursos por unidad de facturación. En Azure, es necesario elegir un [modelo de coherencia de recursos](../../decision-guides/resource-consistency/index.md) en colaboración con el equipo de gobernanza, que se deberá aplicar a todos los recursos.

## <a name="overoptimization"></a>Sobreoptimización

**Riesgo empresarial**: una administración de costos eficaz puede plantear nuevos riesgos. La optimización del gasto es lo contrario al rendimiento del sistema. Al reducir los costos, existe el riesgo de restringir excesivamente el gasto y crear experiencia de usuario deficientes.

**Declaración de directiva**: todos los recursos que afecten a las experiencias de los clientes deben identificarse mediante agrupación o etiquetado. Antes de optimizar todos los recursos que afecten a la experiencia del cliente, el equipo de gobernanza de la nube debe ajustar la optimización basándose en las tendencias de utilización de 90 días como mínimo. Documente todos los picos temporales o basados en eventos que se han tenido en cuenta para optimizar los recursos.

**Opciones de diseño**:

- en Azure, las [características de información de Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-performance) pueden facilitar el análisis de la utilización del sistema.
- Hay varias opciones para agrupar y etiquetar los recursos en función de los roles. En Azure, debe elegir un [modelo de coherencia de recursos](../../decision-guides/resource-consistency/index.md) en colaboración con el equipo de gobernanza, que se deberá aplicar a todos los recursos.

## <a name="next-steps"></a>Pasos siguientes

Use los ejemplos mencionados en este artículo como punto de partida para desarrollar directivas que aborden los riesgos de negocio específicos que se alinean con los planes de adopción de la nube.

Para empezar a desarrollar sus propias declaraciones de directiva personalizadas relacionadas con la administración de costos, descargue la [plantilla de administración de costos](./template.md).

Para acelerar la adopción de esta materia, elija la [guía accionable de gobernanza](../guides/index.md) que más se ajuste a su entorno. Después, modifique el diseño para incorporar las decisiones de directiva específicas de su organización.

A partir de los riesgos y la tolerancia, establezca un proceso para gobernar y comunicar la adhesión a la directiva de administración de costos.

> [!div class="nextstepaction"]
> [Establecimiento de procesos para el cumplimiento de directivas](./compliance-processes.md)
