---
title: Guía de decisiones sobre el cumplimiento de directivas
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga más información sobre las suscripciones de cumplimiento de directivas como prioridad de diseño principal en las migraciones de Azure.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 383f2d6a2443c70c8e082183f601b8186fc98870
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71023708"
---
# <a name="policy-enforcement-decision-guide"></a>Guía de decisiones sobre el cumplimiento de directivas

La definición de una directiva de la organización no será eficaz a menos que se pueda aplicar en la organización. Un aspecto clave a la hora de planear cualquier migración a la nube consiste en determinar la mejor manera de combinar las herramientas que ofrece la plataforma de nube con los procesos de TI ya existentes para maximizar el cumplimiento de la directiva en todo el patrimonio de la nube.

![Esquema de las opciones de cumplimiento de directivas, de las menos a las más complejas, con sus hipervínculos](../../_images/decision-guides/decision-guide-policy-enforcement.png)

Vaya a: [Procedimientos recomendados de la base de referencia](#baseline-recommended-practices) | [Supervisión del cumplimiento de la directiva](#policy-compliance-monitoring) | [Cumplimiento de la directiva](#policy-enforcement) | [Directiva para toda la organización](#cross-organization-policy) | [Cumplimiento automatizado](#automated-enforcement)

A medida que crece el entorno en la nube, se tendrá que enfrentar con la correspondiente necesidad de mantener y aplicar las directivas en una amplia matriz de recursos y suscripciones. A medida que el entorno se amplía y aumentan los requisitos de directivas de la organización, el ámbito de los procesos de cumplimiento de directivas se debe expandir para garantizar un cumplimiento coherente de la directivas y una detección de infracciones rápida.

Los mecanismos de cumplimiento de directivas que proporciona la plataforma en el nivel de recurso o en el de suscripción normalmente son suficientes para entornos en la nube menores. Las implementaciones más grandes justifican un ámbito de cumplimiento mayor y podrían necesitar aprovechar las ventajas de mecanismos de cumplimiento más sofisticados que implican estándares de implementación, agrupación de recursos y organización y la integración del cumplimiento de directivas con los sistemas de registro e informes.

Los principales factores para determinar el ámbito de los procesos de cumplimiento de directivas son los [requisitos de gobernanza en la nube](../../govern/index.md) de la organización, el tamaño y la naturaleza del entorno en la nube y cómo se refleja la organización en el [diseño de suscripciones](../subscriptions/index.md). Un aumento de tamaño del entorno o una mayor necesidad de administrar de forma centralizada la aplicación de directivas pueden justificar un aumento en el ámbito del cumplimiento.

## <a name="baseline-recommended-practices"></a>Procedimientos recomendados sobre la base de referencia

Para una sola suscripción e implementaciones sencillas en la nube, se pueden aplicar muchas directivas corporativas mediante características que son nativas a los recursos y las suscripciones de Azure. El uso coherente de los patrones descritos en las [guías de decisión](../index.md) de Cloud Adoption Framework puede ayudar a establecer un nivel de línea de base de cumplimiento de directivas sin inversión específica en cumplimiento de directivas. Estas características son:

- Las [plantillas de implementación](../resource-consistency/index.md) pueden aprovisionar recursos con una estructura y una configuración estándar.
- [El etiquetado y las normas estándar de nomenclatura](../resource-tagging/index.md) pueden ayudar a organizar las operaciones y a respaldar los requisitos empresariales y de contabilidad.
- La administración del tráfico y las restricciones de las redes se pueden implementar mediante [redes definidas por software](../software-defined-network/index.md).
- El [control de acceso basado en rol](../identity/index.md) puede proteger y aislar los recursos de la nube.

Inicie la planeación del cumplimiento de la directiva de la nube mediante el análisis de cómo la aplicación de los patrones estándar descritos en estas guías puede ayudarle a cumplir con los requisitos organizativos.

## <a name="policy-compliance-monitoring"></a>Supervisión del cumplimiento de la directiva

Un primer paso más allá de la simple confianza en los mecanismos de cumplimiento de directivas proporcionados por la plataforma de Azure es garantizar la posibilidad de comprobar que las aplicaciones y servicios basados en la nube cumplen con la directiva organizativa. Esto incluye la implementación de funcionalidades de notificación para alertar a las partes responsables si un recurso no logra el cumplimiento. El [registro y notificación](../logging-and-reporting/index.md) eficaz del estado de cumplimiento de las cargas de trabajo de la nube es una parte fundamental de una estrategia de cumplimiento de la directiva corporativa.

A medida que crece el patrimonio de la nube, hay herramientas adicionales como [Azure Security Center](https://docs.microsoft.com/azure/security-center) que ofrecen seguridad y detección de amenazas integrada, y que ayuda a aplicar una administración centralizada de la directiva y a enviar alertas sobre el estado de los recursos locales y en la nube.

## <a name="policy-enforcement"></a>Aplicación de directivas

En Azure, también puede aplicar opciones de configuración y reglas de creación de recursos en el nivel de grupo de administración, suscripción o grupo de recursos para ayudar a garantizar la alineación con las directivas.

[Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) es un servicio de Azure para crear, asignar y administrar directivas. Dichas directivas aplican distintas reglas y efectos a los recursos, con el fin de que estos sigan siendo compatibles con los estándares corporativos y los acuerdos de nivel de servicio. Azure Policy evalúa los recursos que incumplen las directivas asignadas. Por ejemplo, puede que desee limitar el tamaño de SKU de las máquinas virtuales del entorno. Una vez que se implementa la directiva correspondiente, se evalúa el cumplimiento de los recursos nuevos y existentes. Con la directiva correcta, se puede conseguir el cumplimiento de los recursos existentes.

## <a name="cross-organization-policy"></a>Directiva para toda la organización

A medida que crece su entorno en la nube y este abarca muchas suscripciones que requieren cumplimiento, deberá centrarse en una estrategia de cumplimiento que abarque a todo el entorno para garantizar la coherencia de las directivas.

El [diseño de las suscripciones](../subscriptions/index.md) deberá tener en cuenta la directiva en lo referente a la estructura organizativa. Además de ayudar a admitir una organización compleja dentro del diseño de suscripciones, los [grupos de administración de Azure](../../ready/considerations/scaling-subscriptions.md#managing-multiple-subscriptions) se pueden usar para asignar reglas de Azure Policy en varias suscripciones.

## <a name="automated-enforcement"></a>Cumplimiento automatizado

Aunque las plantillas de implementación estándar son eficaces a una escala menor, [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview) permite un aprovisionamiento estándar a gran escala y la orquestación de la implementación de las soluciones de Azure. Las cargas de trabajo de varias suscripciones se pueden implementar con valores de directiva coherentes en cualquier recurso que se cree.

En entornos de TI que integran recursos locales y en la nube, puede que necesite usar sistemas de registro y notificación que ofrezcan funcionalidades de supervisión híbridas. Los sistemas de supervisión operativa personalizados o de terceros pueden ofrecer otras funcionalidades adicionales de cumplimiento de directivas. Para entornos en la nube mayores o más maduros, analice cómo integrar mejor estos sistemas con los recursos en la nube.

## <a name="next-steps"></a>Pasos siguientes

El cumplimiento de directivas es solo uno de los principales componentes de infraestructura que requieren decisiones de arquitectura durante un proceso de adopción de la nube. Visite la [introducción a las guías de decisión](../index.md) para obtener información sobre los patrones o los modelos alternativos que se usan al tomar decisiones de diseño para otros tipos de infraestructura.

> [!div class="nextstepaction"]
> [Guías de decisiones sobre arquitectura](../index.md)
