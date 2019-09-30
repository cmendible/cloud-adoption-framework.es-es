---
title: Instrucciones de directiva de ejemplo de coherencia de recursos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Instrucciones de directiva de ejemplo de coherencia de recursos
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: f2e15ad1640bec4e289c49a1f9dcf83de7c04ec3
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221974"
---
# <a name="resource-consistency-sample-policy-statements"></a>Instrucciones de directiva de ejemplo de coherencia de recursos

Las instrucciones individuales de directiva de nube son directrices para abordar los riesgos específicos identificados durante el proceso de evaluación de riesgos. Estas declaraciones deben proporcionar un breve resumen de los riesgos y los planes para resolverlos. La definición de cada declaración debe incluir estos fragmentos de información:

- **Riesgo técnico**: Un resumen del riesgo que esta directiva abordará.
- **Declaración de directiva**: Una explicación clara que resuma los requisitos de la directiva.
- **Opciones de diseño**: Recomendaciones que requieren acción, especificaciones u otras instrucciones que los equipos de TI y los desarrolladores pueden usar al implementar la directiva.

Las siguientes declaraciones de directiva de ejemplo abordan riesgos empresariales comunes relacionados con la coherencia de recursos. Estas declaraciones son ejemplos a los que se puede hacer referencia al elaborar el borrador de declaraciones de directiva para satisfacer las necesidades de su organización. Estos ejemplos no pretenden ser excluyentes y hay varias opciones posibles de directiva para solucionar cada riesgo concreto identificado. Trabaje estrechamente con los equipos de TI y negocio para identificar las mejores directivas para su conjunto de riesgos en particular.

## <a name="tagging"></a>Etiquetado

**Riesgo técnico:** Sin el etiquetado correcto de metadatos asociado con los recursos implementados, las operaciones de TI no pueden dar prioridad al soporte técnico o la optimización de recursos en función del SLA necesario, la importancia de las operaciones empresariales o los costos operativos. Esto puede provocar una asignación errónea de recursos de TI y posibles retrasos en la resolución de incidentes.

**Declaración de directiva**: se implementarán las siguientes directivas:

- Los recursos implementados se deben etiquetar con los valores siguientes:
  - Coste
  - Importancia crítica
  - Contrato de nivel de servicio
  - Entorno
- Las herramientas de gobernanza deben validar el etiquetado relacionado con el costo, la importancia, el SLA, la aplicación y el entorno. Todos los valores deben alinearse con valores predefinidos, administrados por el equipo de gobernanza.

**Opciones de diseño posibles:** En Azure, se admiten las [etiquetas de metadatos estándar de nombre y valor](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) en la mayoría de los tipos de recursos. [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) se usa para exigir etiquetas específicas como parte de la creación de recursos.

## <a name="ungoverned-subscriptions"></a>Suscripciones sin gobierno

**Riesgo técnico:** La creación arbitraria de suscripciones y grupos de administración puede dar lugar a secciones aisladas del entorno de nube que no estén correctamente sujetas a las directivas de gobernanza.

**Declaración de directiva**: La creación de suscripciones o grupos de administración para las aplicaciones críticas o datos protegidos requerirá una revisión del equipo de gobernanza en la nube. Los cambios aprobados se integrarán en una asignación de plano técnico adecuada.

**Opciones de diseño posibles:** Bloquear el acceso administrativo a los [grupos de administración de Azure](https://docs.microsoft.com/azure/governance/management-groups) de la organización y solo permitirlo a los miembros aprobados del equipo de gobernanza que controlarán la creación de suscripciones y el proceso de control de acceso.

## <a name="manage-updates-to-virtual-machines"></a>Administrar las actualizaciones de las máquinas virtuales

**Riesgo técnico:** Las máquinas virtuales (VM) que no estén actualizadas con las actualizaciones y revisiones de software más recientes son vulnerables a problemas de seguridad o rendimiento, que pueden dar lugar a interrupciones del servicio.

**Declaración de directiva**: Las herramientas de gobernanza deben exigir que las actualizaciones automáticas estén habilitadas en todas las máquinas virtuales implementadas. Las infracciones deben revisarse con los equipos de administración de operaciones y corregirse de acuerdo con las directivas de operaciones. Los recursos que no se actualicen automáticamente deben incluirse en procesos que sean propiedad del departamento de operaciones de TI.

**Opciones de diseño posibles:** Para las máquinas virtuales hospedadas en Azure, puede proporcionar la administración de actualizaciones coherentes mediante la [solución Update Management en Azure Automation](https://docs.microsoft.com/azure/automation/automation-update-management).

## <a name="deployment-compliance"></a>Cumplimiento de la implementación

**Riesgo técnico:** Los scripts y las herramientas de automatización de la implementación que el equipo de gobernanza en la nube no haya aprobado completamente pueden dar lugar a implementaciones de recursos que infrinjan la directiva.

**Declaración de directiva**: se implementarán las siguientes directivas:

- El equipo de gobernanza en la nube debe aprobar las herramientas de implementación para garantizar la gobernanza en curso de los recursos implementados.
- Los scripts de implementación deben conservarse en el repositorio central accesible para el equipo de gobernanza en la nube para su revisión y auditoría periódicas.

**Opciones de diseño posibles:** Un uso coherente de [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints) para administrar implementaciones automatizadas permite implementaciones coherentes de los recursos de Azure que cumplan con los estándares de gobernanza y las directivas de la organización.

## <a name="monitoring"></a>Supervisión

**Riesgo técnico:** Si la supervisión se implementa incorrectamente o se instrumenta de forma incoherente puede impedir la detección de problemas de mantenimiento de la carga de trabajo u otras infracciones de cumplimiento de directivas.

**Declaración de directiva**: se implementarán las siguientes directivas:

- Las herramientas de gobernanza deben validar que todos los recursos se incluyen en la supervisión de la disminución, seguridad, cumplimiento y optimización de los recursos.
- Las herramientas de gobernanza deben validar que se recopila el nivel adecuado de datos de registro para todas las aplicaciones y datos.

**Opciones de diseño posibles:** [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) es el servicio de supervisión predeterminado de Azure y puede aplicarse supervisión coherente a través de [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints) al implementar recursos.

## <a name="disaster-recovery"></a>Recuperación ante desastres

**Riesgo técnico:** Los errores, las eliminaciones o los daños de los recursos pueden producir una interrupción de las aplicaciones críticas o de los servicios y la pérdida de datos confidenciales.

**Declaración de directiva**: Todas las aplicaciones críticas y los datos protegidos deben tener implementadas soluciones de copia de seguridad y recuperación para minimizar el impacto en el negocio de las interrupciones o errores del sistema.

**Opciones de diseño posibles:** El servicio [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) proporciona funcionalidades de copia de seguridad, recuperación y replicación que minimizan la duración de la interrupción en escenarios de recuperación ante desastres y continuidad del negocio (BCDR).

## <a name="next-steps"></a>Pasos siguientes

Use los ejemplos mencionados en este artículo como punto de partida para desarrollar directivas que aborden los riesgos de negocio específicos que se alinean con los planes de adopción de la nube.

Para comenzar a desarrollar sus propias instrucciones de directivas personalizadas relacionadas con la coherencia de recursos, descargue la [plantilla de coherencia recursos](./template.md).

Para acelerar la adopción de esta disciplina, elija la [guía práctica de gobernanza](../guides/index.md) que más se ajuste a su entorno. Después, modifique el diseño para incorporar las decisiones de directiva específicas de su organización.

A partir de los riesgos y la tolerancia, establezca un proceso para gobernar y comunicar la adhesión a la directiva de coherencia de los recursos.

> [!div class="nextstepaction"]
> [Establecimiento de procesos para el cumplimiento de directivas](./compliance-processes.md)
