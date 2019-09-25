---
title: Procesos de cumplimiento de directivas de Cost Management
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Procesos de cumplimiento de directivas de Cost Management
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6345a8cae51a6b26b7fad174113a40e9dc0dae3e
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71220974"
---
# <a name="cost-management-policy-compliance-processes"></a>Procesos de cumplimiento de directivas de Cost Management

En este artículo se explica un enfoque de creación de procesos que admiten una materia de gobernanza de [Cost Management](./index.md). Una gobernanza eficaz de los costos de la nube empieza con procesos manuales periódicos diseñados para admitir el cumplimiento de directivas. Esto requiere la participación regular del equipo de gobernanza de la nube y las partes interesadas de la empresa para revisar y actualizar la directiva y garantizar el cumplimiento de las directivas. Además, muchos procesos de aplicación y supervisión en curso se pueden automatizar o complementar con herramientas para reducir la sobrecarga de la gobernanza y permitir una respuesta más rápida a la desviación de directivas.

## <a name="planning-review-and-reporting-processes"></a>Procesos de planeación, revisión y creación de informes

Las mejores herramientas de Cost Management en la nube son solo tan buenas como los procesos y directivas que admiten. A continuación se muestra un conjunto de procesos de ejemplo habitualmente implicados en la materia de Cost Management. Use estos ejemplos como punto de partida al planear los procesos que le permitirán continuar actualizando la directiva de costos según los cambios del negocio y los comentarios de los equipos empresariales sujetos a la guía de gobernanza de costos.

**Planeamiento y evaluación inicial de los riesgos:** como parte de su adopción inicial de la materia de Cost Management, identifique sus principales riesgos empresariales y tolerancias relacionadas con los costos de la nube. Use esta información para debatir sobre el presupuesto y los riesgos relacionados con los costos con los miembros de sus equipos empresariales y desarrollar un conjunto de base de referencia de directivas para mitigar estos riesgos a fin de establecer su estrategia de gobernanza inicial.

**Planeación de la implementación:** antes de implementar cualquier recurso, establezca un presupuesto previsto en función de la asignación en la nube esperada. Asegúrese de que se documenta la información de propiedad y contabilidad para la implementación.

**Planeación anual:** realice un análisis de acumulación de todos los recursos implementados y aquellos que se van a implementar de forma anual. Alinee los presupuestos por unidades de negocio, departamentos, equipos y otras divisiones adecuadas para impulsar la adopción de autoservicio. Asegúrese de que el líder de cada unidad de facturación tenga conocimiento del presupuesto y de cómo realizar un seguimiento de los gastos.

Este es el momento de hacer una preasignación o adquisición previa para maximizar los descuentos. Es prudente alinear presupuestos anuales con el año fiscal del proveedor de nube para aprovechar más las opciones de descuento de fin de año.

**Planeación trimestral:** revise los presupuestos de forma trimestral con cada líder de la unidad de facturación para alinear la previsión y los gastos reales. Si hay cambios en el plan o patrones de gastos inesperados, alinee y reasigne el presupuesto.

Este proceso de planeamiento trimestral también es un buen momento para evaluar si el equipo de gobernanza de la nube actual está abordando las carencias de conocimientos relacionadas con los planes de negocios actuales o futuros. Invite al personal pertinente y los propietarios de la carga de trabajo a participar en las revisiones y la planeación como asesores temporales o miembros permanentes del equipo.

**Educación y aprendizaje:** ofrezca sesiones de aprendizaje bimensuales para asegurarse de que el personal de TI y la dirección está al día de los últimos requisitos de la directiva de administración de costos. Como parte de este proceso, revise y actualice cualquier documentación, guía u otros recursos de aprendizaje para asegurarse de que estén sincronizados con las declaraciones de directiva corporativa más recientes.

**Informes mensuales:** de forma mensual, notifique los gastos reales frente a la previsión. Informe a los líderes de facturación de cualquier desviación inesperada.

Estos procesos básicos ayudarán a alinear los gastos y establecer una base de la materia de Cost Management.

## <a name="ongoing-monitoring-processes"></a>Procesos de supervisión en curso

Una estrategia de gobernanza de Cost Management correcta depende de la visibilidad de los gastos relacionados con la nube pasados, actuales y futuros planeados. Sin la capacidad para analizar las métricas pertinentes y los datos de sus costos existentes, no se pueden identificar cambios en los riesgos o detectar infracciones de las tolerancias al riesgo. Los procesos de gobernanza en curso explicados anteriormente requieren datos de calidad para asegurarse de que se puede modificar la directiva para proteger mejor la infraestructura contra requisitos empresariales en constante cambio y el uso de la nube.

Asegúrese de que sus equipos de TI han implementado sistemas automatizados para supervisar sus gastos en la nube y el uso de desviaciones no planeadas de los costos esperados. Establezca sistemas de informes y alertas para garantizar la detección rápida y la mitigación de posibles infracciones de la directiva.

## <a name="compliance-violation-triggers-and-enforcement-actions"></a>Desencadenadores de infracción de cumplimiento y acciones de cumplimiento

Al detectarse las infracciones, debe tomar medidas de cumplimiento para la nueva alineación con la directiva. Puede automatizar la mayoría de los desencadenadores de infracción con las herramientas descritas en la [cadena de herramientas de Cost Management de Azure](./toolchain.md).

A continuación, se muestran ejemplos de desencadenadores:

- **Desviaciones de presupuesto mensuales.** debata toda desviación en los gastos mensuales que supere el 20 % de la proporción del gasto previsto frente al real con el líder de la unidad de facturación. Resoluciones de registro y cambios en la previsión.
- **Ritmo de adopción.** toda desviación en un nivel de suscripción que supere el 20 % desencadenará una revisión con el líder de la unidad de facturación. Resoluciones de registro y cambios en la previsión.

## <a name="next-steps"></a>Pasos siguientes

Mediante la [plantilla de Cloud Management](./template.md), documente los procesos y desencadenadores que se alineen con el plan de adopción de la nube actual.

Para obtener instrucciones sobre cómo ejecutar directivas de administración en la nube de conformidad con los planes de adopción, consulte el artículo sobre la mejora de la materia de Cost Management.

> [!div class="nextstepaction"]
> [Mejora de la materia de Cost Management](./discipline-improvement.md)
