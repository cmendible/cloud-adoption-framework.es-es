---
title: Creación de una organización con control de costos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Conozca los procedimientos recomendados para crear una organización con control de costos.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.openlocfilehash: 88944a786bb783d1a2e4bf651c142b8148b0dd2e
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031233"
---
# <a name="building-a-cost-conscious-organization"></a>Creación de una organización con control de costos

Tal como se señala en [Motivaciones: ¿por qué se realiza el traslado a la nube?](../strategy/motivations.md), hay muchas razones de peso para que una empresa adopte la nube. Si la reducción de costos es uno de los principales factores, es importante crear una organización con control de costos.

El control de costos no se garantiza en un solo día. Al igual que otros temas de adopción de la nube, es una actividad iterativa. En el diagrama siguiente se describe este proceso, centrado en tres actividades interdependientes: *visibilidad*, *responsabilidad* y *optimización*. Estos procesos se aplican en macro y microniveles, que se describen en detalle en este artículo.

![Proceso de control de costos](../_images/ready/cost-optimization-process.png)
*Figura 1: Esquema de la organización con control de costos*

## <a name="general-cost-conscious-processes"></a>Procesos generales de control de costos

- **Visibilidad**: para que una organización pueda controlar los costos, necesita verlos. La visibilidad en una organización con control de costos requiere informes coherentes para los equipos que adoptan la nube, los equipos de finanzas que administran los presupuestos y los equipos de administración responsables de los costos. Esta visibilidad se logra estableciendo:
  - El ámbito de informes adecuado.
  - La organización de recursos adecuada (grupos de administración, grupos de recursos, suscripciones).
  - Estrategias claras de etiquetado.
  - Controles de acceso (RBAC) adecuados.

- **Responsabilidad**: la responsabilidad es tan importante como la visibilidad. La responsabilidad comienza con unos presupuestos claros de los esfuerzos de adopción. Los presupuestos deben estar bien establecidos, comunicarse claramente y basarse en expectativas realistas. La responsabilidad requiere un proceso iterativo y una mentalidad de crecimiento para situarse en el nivel adecuado.

- **Optimización**: la optimización es la acción que crea las reducciones de costos. Durante la optimización, las asignaciones de recursos se modifican para reducir el costo de admitir diversas cargas de trabajo. Este proceso precisa iteración y experimentación. Cada reducción de costo reduce el rendimiento. Para encontrar el equilibrio adecuado entre el control de costos y las expectativas de rendimiento del usuario final se necesita información de varias partes.

En las secciones siguientes se describen los papeles que juegan el *equipo de estrategia de la nube*, el *equipo de adopción de la nube*, el *equipo de gobernanza de la nube* y el *Centro de excelencia en la nube* (CCoE) en el desarrollo de una organización con control de costos.

## <a name="cloud-strategy-team"></a>Equipo de estrategia de la nube

El desarrollo del control de costos en los trabajos de adopción de la nube comienza en el nivel de liderazgo. Para que sea efectivo a largo plazo, el [equipo de estrategia de la nube](./cloud-strategy.md) debe incluir un miembro del equipo de finanzas. Si la estructura financiera incluye administradores empresariales responsables de los costos de la solución, también se les debe invitar a unirse al equipo. Además de las actividades básicas que normalmente se asignan al equipo de estrategia de la nube, todos sus miembros deben ser responsables de los siguientes aspectos:

- **Visibilidad**: el equipo de estrategia de la nube y el [equipo de gobernanza de la nube](./cloud-governance.md) necesitan conocer los costos reales de los trabajos de adopción de la nube. Este equipo tiene una visión de nivel ejecutivo, por lo que debe tener acceso a varios ámbitos de costo para analizar las decisiones de gasto. Normalmente, un ejecutivo necesita ver el total de los costos en todo el "gasto" de la nube. Como miembro activo del equipo de estrategia de la nube, también debe poder ver los costos por unidad de negocio o por unidad de facturación, para validar la visualización de costos, los contracargos u otros [modelos de contabilidad de la nube](../strategy/cloud-accounting.md).

- **Responsabilidad**: los presupuestos se deben establecer entre los equipos de estrategia de la nube, [gobernanza de la nube](./cloud-governance.md) y [adopción de la nube](./cloud-adoption.md), en función de las actividades de adopción esperadas. Cuando se producen desviaciones respecto al presupuesto, los equipos de estrategia de la nube y gobernanza de la nube deben colaborar para determinar rápidamente el mejor curso de acción para corregirlas.

- **Optimización**: durante los trabajos de optimización, el equipo de estrategia de la nube puede representar la inversión y el valor devuelto de cargas de trabajo específicas. Si una carga de trabajo tiene un valor estratégico o un impacto financiero en el negocio, los trabajos de optimización de costos deben supervisarse muy de cerca. Si no hay ningún impacto estratégico en la organización y no hay ningún costo inherente para el bajo rendimiento de una carga de trabajo, el equipo de estrategia de la nube puede aprobar la sobreoptimización. Para adoptar estas decisiones, el equipo debe ser capaz de ver los costos en un ámbito por proyecto.

## <a name="cloud-adoption-team"></a>Equipo de adopción de la nube

El [equipo de adopción de la nube](./cloud-adoption.md) se sitúa en el centro de todas las actividades de adopción. Es, por lo tanto, la primera línea de defensa contra el exceso de gasto. Este equipo tiene un papel activo en las tres fases del control de costos.

- **Visibilidad**:

  - **Reconocimiento**: es importante que el equipo de adopción de la nube conozca los objetivos de ahorro de costos del trabajo. La simple indicación de que el trabajo de adopción de la nube ayudará a reducir los costos da pie al error. La *visibilidad* específica es importante. Por ejemplo, si el objetivo es reducir el TCO del centro de datos en un 3 por ciento o los gastos operativos anuales en un 7 por ciento, esta información debe divulgarse pronto y de forma clara.
  - **Telemetría**: este equipo necesita ver el impacto de sus decisiones. Durante las actividades de migración o innovación, sus decisiones tienen un efecto directo en los costos y el rendimiento. El equipo debe equilibrar estos dos factores opuestos. La supervisión del rendimiento y de los costos limitada al ámbito de los proyectos activos del equipo es importante para contar con la visibilidad necesaria.

- **Responsabilidad**: el equipo de adopción de la nube debe tener en cuenta los presupuestos preestablecidos asociados a sus trabajos de adopción. Cuando los costos reales no se corresponden con el presupuesto, la responsabilidad entra en juego. La responsabilidad no equivale a penalizar al equipo de adopción por superar el presupuesto, ya que este exceso puede ser resultado de decisiones de rendimiento necesarias. En su lugar, la responsabilidad supone educar al equipo sobre los objetivos y cómo sus decisiones afectan a estos objetivos. Además, incluye establecer un diálogo que permita al equipo explicar las decisiones que han provocado el exceso de gasto. Si esas decisiones no se ajustan a los objetivos del proyecto, esta labor ofrece una buena oportunidad de colaborar con el equipo de estrategia de la nube para adoptar mejores decisiones.

- **Optimización**: este trabajo es una labor de equilibrio, ya que la optimización de los recursos puede reducir el rendimiento de las cargas de trabajo que admiten. A veces, no se materializan los ahorros previstos o presupuestados para una carga de trabajo porque esta no funciona correctamente con los recursos presupuestados. En estos casos, el equipo de adopción de la nube tiene que tomar decisiones razonables e informar de los cambios a los equipos de estrategia de la nube y gobernanza de la nube, para que se puedan corregir los presupuestos o las decisiones de optimización.

## <a name="cloud-governance-team"></a>Equipo de gobernanza de la nube

Por lo general, el equipo de [gobernanza de la nube](./cloud-governance.md) es responsable de la administración de los costos en todo el trabajo de adopción de la nube. Como se describe en el tema sobre la [materia de administración de costos](../govern/cost-management/index.md) de la metodología de gobernanza de Cloud Adoption Framework, la administración de costos es la primera de las cinco materias de gobernanza de la nube. En esos artículos se describen una serie de responsabilidades más detalladas para el equipo de gobernanza de la nube.

Este trabajo se centra en las siguientes actividades relacionadas con el desarrollo de una organización con control de costos:

- **Visibilidad**: el equipo de gobernanza de la nube funciona en el mismo nivel y en colaboración con el equipo de estrategia de la nube a la hora de planear presupuestos de adopción de la nube. Estos dos equipos también trabajan juntos para revisar periódicamente los gastos reales. El equipo de gobernanza de la nube es responsable de garantizar unos informes de costos coherentes y confiables, así como una telemetría del rendimiento.

- **Responsabilidad**: cuando se producen desviaciones de presupuesto, el equipo de estrategia de la nube y el equipo de gobernanza de la nube deben colaborar para determinar rápidamente el mejor curso de acción para corregir las desviaciones. Por lo general, el equipo de gobernanza de la nube actuará a partir de las decisiones adoptadas. A veces, la acción puede ser sencillamente una nueva formación del [equipo de adopción de la nube](./cloud-adoption.md) afectado. El equipo de gobernanza de la nube también puede ayudar a optimizar los recursos implementados, a cambiar las opciones de descuento o incluso a implementar opciones de control de costos automatizadas, como el bloqueo de la implementación de recursos no planeados.

- **Optimización**: después de migrar recursos a la nube o crearlos en ella, se pueden emplear herramientas de supervisión para evaluar el rendimiento y el uso de esos recursos. Unos datos de rendimiento y supervisión adecuados pueden identificar los recursos que deben optimizarse. El equipo de gobernanza de la nube es responsable de garantizar que las herramientas de supervisión y generación de informes de costos se implementan de forma coherente. También pueden ayudar a los equipos de adopción a identificar oportunidades de optimización en función de la telemetría de costos y rendimiento.

## <a name="cloud-center-of-excellence"></a>Centro de excelencia de la nube

Aunque no suele ser responsable de la administración de costos, el equipo de CCoE puede tener un impacto significativo en las organizaciones con control de costos. Muchas decisiones fundamentales de TI afectan a los costos a escala. Cuando el equipo de CCoE realiza su labor, se pueden reducir los costos de varios trabajos de adopción de la nube.

- **Visibilidad**: el equipo de CCoE debe ver cualquier grupo de administración o grupo de recursos que aloje recursos básicos de TI. El equipo puede utilizar estos datos para buscar oportunidades que optimizar.

- **Responsabilidad**: aunque no suele ser responsable del costo, el equipo de CCoE puede responsabilizarse de crear soluciones repetibles que minimicen el costo y maximicen el rendimiento.

- **Optimización**: dada la visibilidad con la que cuenta el equipo de CCoE sobre varias implementaciones, se encuentra en una posición idónea para ofrecer sugerencias de optimización y ayudar a los equipos de adopción a optimizar los recursos.

## <a name="next-steps"></a>Pasos siguientes

La práctica de estas responsabilidades en cada nivel del negocio ayuda a conseguir una organización con control de costos. Para comenzar a actuar sobre esta guía, revise la [Introducción a la preparación de la organización](./index.md) como ayuda para identificar las estructuras de equipo adecuadas.

> [!div class="nextstepaction"]
> [Identificación de las estructuras de equipo correctas](./index.md)
