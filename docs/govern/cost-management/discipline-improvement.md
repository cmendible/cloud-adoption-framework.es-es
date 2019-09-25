---
title: Mejora de la materia de Cost Management
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Mejora de la materia de Cost Management
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 2bb94c18833ccfd8594088da29b63f8006b6fa94
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222697"
---
# <a name="cost-management-discipline-improvement"></a>Mejora de la materia de Cost Management

La materia de Cost Management intenta abordar los principales riesgos empresariales relacionados con los gastos que se derivan de hospedar cargas de trabajo basadas en la nube. Dentro de las cinco materias de gobernanza de la nube, la materia Administración de costos está involucrada en el control de costos y el uso de los recursos en la nube con el objetivo de crear y mantener un ciclo de costos planificado.

En este artículo se describen las tareas potenciales que su empresa realiza para desarrollar y desarrollar la disciplina de Cost Management. Estas tareas se dividen en las fases de planeamiento, compilación, adopción y funcionamiento de la implementación de una solución de nube que, posteriormente, se iteran para permitir el desarrollo de un [enfoque incremental a la gobernanza de la nube](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Cuatro fases de adopción](../../_images/govern/adoption-phases.png)

*Figura 1: Fases de adopción del enfoque incremental para la gobernanza de la nube.*

Ningún documento único puede dar cuenta de los requisitos de todas las empresas. Por lo tanto, en este artículo se detallan ejemplos de actividades mínimas y potenciales sugeridas para cada fase del proceso de desarrollo de la gobernanza. El objetivo inicial de estas actividades es ayudarle a crear un [producto viable mínimo de directiva](../guides/index.md#an-incremental-approach-to-cloud-governance) y establecer un marco para la mejora incremental de las directivas. El equipo de gobernanza de la nube deberá decidir cuánto invertir en estas actividades para mejorar las funcionalidades de gobernanza de la administración de costos.

> [!CAUTION]
> Ni las actividades mínimas ni las posibles que se describen en este artículo están en línea con directivas corporativas específicas ni con requisitos de cumplimiento de terceros. Esta guía está diseñada como ayuda para facilitar las conversaciones que darán lugar a la alineación de los requisitos con un modelo de gobernanza de la nube.

## <a name="planning-and-readiness"></a>Planeamiento y preparación

Esta fase del desarrollo de la gobernanza permite salvar las diferencias entre los resultados empresariales y unas estrategias accionables. Durante este proceso, el equipo directivo define métricas específicas, las asigna al patrimonio digital y empieza a planear el esfuerzo global de migración.

**Actividades mínimas sugeridas:**

- Evalúe las opciones de la [cadena de herramientas de Cost Management](./toolchain.md).
- Desarrolle un borrador con las directrices de arquitectura y distribúyalo a las partes interesadas clave.
- Eduque e implique a las personas y equipos que se vean afectados por el desarrollo de las directrices de arquitectura.

**Actividades potenciales:**

- Asegúrese de tomar decisiones presupuestarias que respalden la justificación comercial de su estrategia en la nube.
- Valide las métricas de aprendizaje que usa para informar sobre la asignación exitosa de fondos.
- Comprenda el modelo de contabilidad en la nube seleccionado y que afecta al modo de contabilizar los costos de la nube.
- Familiarícese con el plan de patrimonio digital y valide las expectativas de costos exactos.
- Evalúe las opciones de compra para determinar si es mejor "pagar sobre la marcha" o realizar un compromiso previo mediante la compra de un Contrato Enterprise.
- Alinee los objetivos comerciales con los presupuestos planificados y ajuste los planes presupuestarios según sea necesario.
- Desarrolle un mecanismo de notificación de objetivos y presupuestos para enviar una notificación a las partes técnicas y comerciales interesadas al final de cada ciclo de costos.

## <a name="build-and-predeployment"></a>Compilación y fase anterior a la implementación

Se necesitan varios requisitos técnicos y no técnicos para migrar correctamente un entorno. Este proceso se centra en las decisiones, la preparación y la infraestructura principal que precede a una migración.

**Actividades mínimas sugeridas:**

- Para implementar su [cadena de herramientas de administración de costos](./toolchain.md), agréguela en una fase anterior a la implementación.
- Actualice el documento de directrices de arquitectura y distribúyalo a las principales partes interesadas.
- Desarrolle materiales y documentación educativos, comunicaciones de reconocimiento, incentivos y otros programas para ayudar a impulsar la adopción del usuario.
- Determine si sus requisitos de compra se alinean con sus presupuestos y objetivos.

**Actividades potenciales:**

- Alinee sus planes presupuestarios con la [Estrategia de suscripción](../../decision-guides/subscriptions/index.md) que defina su modelo de propiedad principal.
- Use la [estrategia de coherencia de los recursos](../../decision-guides/resource-consistency/index.md) para aplicar las instrucciones de arquitectura y costos con el tiempo.
- Determine si existen anomalías en los costos que afecten a sus planes de adopción y migración.

## <a name="adopt-and-migrate"></a>Adopción y migración

La migración es un proceso incremental que se centra en el traslado, las pruebas y la adopción de las aplicaciones o cargas de trabajo de un patrimonio digital existente.

**Actividades mínimas sugeridas:**

- Migre su [cadena de herramientas de administración de costos](./toolchain.md) de la fase anterior a la implementación a la fase de producción.
- Actualice el documento de directrices de arquitectura y distribúyalo a las principales partes interesadas.
- Desarrolle materiales y documentación educativos, comunicaciones de reconocimiento, incentivos y otros programas para ayudar a impulsar la adopción del usuario.

**Posible actividades:**

- Implemente su modelo de contabilidad en la nube.
- Asegúrese de que sus presupuestos reflejen los gastos reales durante cada lanzamiento y ajústelos según sea necesario.
- Supervise los cambios en los planes presupuestarios y confirme con las partes interesadas si es necesario realizar aprobaciones adicionales.
- Actualice los cambios en el documento de las directrices de arquitectura para reflejar los costos reales.

## <a name="operate-and-post-implementation"></a>Funcionamiento y fase posterior a la implementación

Una vez completada la transformación, la gobernanza y las operaciones deben estar disponibles durante el ciclo de vida natural de una aplicación o carga de trabajo. Esta fase de desarrollo de la gobernanza se centra en las actividades que surgen habitualmente cuando la solución ya está implementada y el ciclo de transformación comienza a estabilizarse.

**Actividades mínimas sugeridas:**

- Personalice su [cadena de herramientas de Cost Management](./toolchain.md) según los cambios en las necesidades de administración de costos de la organización.
- Considere la posibilidad de automatizar cualquier notificación e informe para reflejar el gasto real.
- Refina las directrices de arquitectura para guiar los procesos de adopción futuros.
- Ofrezca cursos a los equipos afectados de forma periódica para garantizar que se cumplan las directrices de arquitectura.

**Actividades potenciales:**

- Ejecute una revisión trimestral del negocio en la nube para saber el valor entregado al negocio y los costos asociados.
- Ajuste los planes trimestralmente para reflejar los cambios en los gastos reales.
- Determine la alineación financiera con los P&L para las suscripciones de las unidades de negocio.
- Analice mensualmente el valor y los métodos de notificación de costos con las partes interesadas.
- Compruebe los recursos infrautilizados y determine si merece la pena continuar con ellos.
- Detecte desajustes y anomalías entre los gastos planeados y los reales.
- Ayude a los equipos de adopción y estrategia de la nube a conocer y resolver estas anomalías.

## <a name="next-steps"></a>Pasos siguientes

Ahora que conoce el concepto de gobernanza de identidades en la nube, examine la [cadena de herramientas de Cost Management](./toolchain.md) para identificar las herramientas y características de Azure que necesitará al desarrollar la materia de gobernanza de Cost Management en la plataforma de Azure.

> [!div class="nextstepaction"]
> [Cadena de herramientas de Cost Management de Azure](./toolchain.md)
