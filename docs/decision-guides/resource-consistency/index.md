---
title: Guía de decisiones de la coherencia de recursos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información acerca de la coherencia de recursos al planear una migración de Azure.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 2fc051e232fde095ca511bad3f4035198488b5f4
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817594"
---
# <a name="resource-consistency-decision-guide"></a>Guía de decisiones de la coherencia de recursos

El [diseño de suscripciones](../subscriptions/index.md) de Azure define cómo organizar los recursos en la nube en relación con la estructura de la organización, las prácticas contables y los requisitos de las cargas de trabajo. Además de este nivel de estructura, abordar los requisitos de directivas de gobernanza organizativa en todo el entorno en la nube requiere la capacidad de organizar, implementar y administrar los recursos dentro de una suscripción de forma coherente.

![Trazado de opciones de coherencia de recursos de menos a más complejas, alineadas con vínculos](../../_images/discovery-guides/discovery-guide-resource-consistency.png)

Vaya a: [Agrupación básica](#basic-grouping) | [Coherencia de implementación](#deployment-consistency) | [Coherencia de directivas](#policy-consistency) | [Coherencia jerárquica](#hierarchical-consistency)  |  [Coherencia automatizada](#automated-consistency)

Las decisiones relativas al nivel de los requisitos de coherencia de los recursos del entorno en la nube se rigen principalmente por estos factores: el tamaño del patrimonio digital posterior a la migración, los requisitos del entorno o del negocio que no encajan claramente dentro de los enfoques de diseño de suscripción existentes o la necesidad de aplicar gobernanza a lo largo del tiempo una vez implementados los recursos.

Con el aumento de la importancia de estos factores, las ventajas de garantizar la implementación, agrupación y administración de los recursos basados en la nube de forma coherente se vuelve más importante. Lograr niveles de coherencia de los recursos más avanzados para satisfacer las crecientes necesidades requiere más esfuerzo invertido en automatización, herramientas y la aplicación de la coherencia y esto da como resultado más tiempo invertido en la administración y el seguimiento de cambios.

## <a name="basic-grouping"></a>Agrupación básica

En Azure, los [grupos de recursos](/azure/azure-resource-manager/resource-group-overview#resource-groups) son un mecanismo principal de organización de recursos para agrupar lógicamente los recursos dentro de una suscripción.

Los grupos de recursos actúan como contenedores para los recursos con un ciclo de vida común o restricciones de administración compartidas, como la directiva o los requisitos de control de acceso basado en rol (RBAC). Los grupos de recursos no pueden anidarse, y los recursos solo pueden pertenecer a un solo grupo de recursos. Algunas acciones pueden aplicarse a todos los recursos de un grupo de recursos. Por ejemplo, al eliminar un grupo de recursos, se quitan todos los recursos de ese grupo. Los patrones habituales para crear grupos de recursos normalmente se dividen en dos categorías:

- **Cargas de trabajo de TI tradicionales:** se suelen agrupar por elementos dentro del mismo ciclo de vida, como una aplicación. Si se agrupan las aplicaciones, se podrán administrar las aplicaciones de forma individual.
- **Cargas de trabajo de TI ágiles:** se centran en las aplicaciones en la nube orientadas a los clientes externos. Estos grupos de recursos suelen reflejar las capas funcionales de implementación (por ejemplo, el nivel web y el de aplicaciones) y administración.

## <a name="deployment-consistency"></a>Coherencia de implementación

Creadas sobre el mecanismo de agrupación de recursos base, la plataforma de Azure proporciona un sistema para usar plantillas para implementar los recursos en el entorno en la nube. Puede usar plantillas para crear convenciones de nomenclatura y organización coherentes al implementar cargas de trabajo, reforzando esos aspectos del diseño de la implementación y la administración de recursos.

Las [plantillas de Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview#template-deployment) permiten implementar repetidamente los recursos en un estado coherente mediante una estructura de grupos de recursos y una configuración predeterminada. Las plantillas de Resource Manager ayudan a definir un conjunto de estándares como punto de partida para las implementaciones.

Por ejemplo, puede tener una plantilla estándar para la implementación de una carga de trabajo de servidor web que contiene dos máquinas virtuales como servidores web combinadas con un equilibrador de carga para distribuir el tráfico entre los servidores. A continuación, puede volver a usar esta plantilla para crear un conjunto de máquinas virtuales y un equilibrador de carga estructuralmente idénticos cada vez que se necesita este tipo de carga de trabajo, solo cambiando el nombre de la implementación y las direcciones IP implicadas.

También puede implementar estas plantillas mediante programación e integrarlas con los sistemas de CI/CD.

## <a name="policy-consistency"></a>Coherencia de directivas

Para asegurarse de que se aplican las directivas de gobernanza cuando se crean recursos, parte del diseño de agrupación de recursos implica el uso de una configuración común al implementar recursos.

Mediante la combinación de grupos de recursos y plantillas de Resource Manager estandarizadas, puede aplicar estándares para los parámetros que son necesarios en una implementación y las reglas de [Azure Policy](/azure/governance/policy/overview) que se aplican a cada grupo de recursos o recurso.

Por ejemplo, puede existir el requisito de que todas las máquinas virtuales implementadas dentro de su suscripción se conecten a una subred común administrada por el equipo de TI central. Puede crear una plantilla estándar para implementar máquinas virtuales de carga de trabajo para crear un grupo de recursos independiente para la carga de trabajo e implementar allí las máquinas virtuales necesarias. Este grupo de recursos tendría una regla de directiva para permitir solo que las interfaces de red dentro del grupo de recursos se unan a la subred compartida.

Para obtener una explicación más detallada de la aplicación de las decisiones de directiva dentro de una implementación en la nube, consulte [Aplicación de directivas](../policy-enforcement/index.md).

## <a name="hierarchical-consistency"></a>Coherencia jerárquica

Los grupos de recursos permiten niveles adicionales de jerarquía dentro de la organización y suscripción, aplicando reglas de Azure Policy y controles de acceso en un nivel de grupo de recursos. No obstante, a medida que crece el tamaño del entorno en la nube, es posible que deba admitir requisitos de gobernanza en varias suscripciones más complicados que pueden admitirse mediante la jerarquía de empresa, departamento, cuenta y suscripción del contrato Enterprise de Azure.

Los [grupos de administración de Azure](/azure/governance/management-groups) le permiten organizar las suscripciones en estructuras organizativas más sofisticadas mediante la agrupación de suscripciones en una jerarquía distinta de la jerarquía del contrato Enterprise. Esta jerarquía alternativa le permite aplicar mecanismos de control de acceso y cumplimiento de directivas en varias suscripciones y los recursos que contienen. Las jerarquías de grupos de administración se pueden utilizar para hacer coincidir las suscripciones del entorno en la nube con los requisitos de gobernanza del negocio o las operaciones. Para más información, consulte la [Guía de decisiones de suscripción](../subscriptions/index.md).

## <a name="automated-consistency"></a>Coherencia automatizada

Para las implementaciones de nube de gran tamaño, la gobernanza global pasa a ser más importante y más complejo. Es fundamental aplicar y exigir automáticamente los requisitos de gobernanza al implementar recursos, así como satisfacer requisitos actualizados para las implementaciones existentes.

[Azure Blueprints](/azure/governance/blueprints/overview) permiten a las organizaciones admitir la gobernanza global de entornos de nube de gran tamaño en Azure. Los planos técnicos van más allá de las capacidades proporcionadas por las plantillas estándar de Azure Resource Manager para crear orquestaciones de implementación completa capaz de implementar los recursos y aplicar reglas de directiva. Los planos técnicos son compatibles con el control de versiones, la capacidad de actualizar todas las suscripciones en las que se usó el plano técnico y la capacidad de bloquear las suscripciones implementadas para evitar la creación y la modificación no autorizadas de recursos.

Estos paquetes de implementación permiten que los equipos de TI y de desarrollo implementen rápidamente nuevas cargas de trabajo y recursos de red que cumplan con los requisitos cambiantes de la directiva organizativa. Los planos técnicos también se pueden integrar en canalizaciones CI/CD para aplicar los estándares de gobernanza revisados a las implementaciones cuando se actualizan.

## <a name="next-steps"></a>Pasos siguientes

La coherencia de recursos es solo uno de los principales componentes de infraestructura que requieren decisiones de arquitectura durante un proceso de adopción de la nube. Visite la [introducción a las guías de decisión](../index.md) para obtener información sobre los patrones o los modelos alternativos que se usan al tomar decisiones de diseño para otros tipos de infraestructura.

> [!div class="nextstepaction"]
> [Guías de decisiones sobre arquitectura](../index.md)
