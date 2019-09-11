---
title: Consideraciones sobre la zona de aterrizaje de Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Conozca cómo una zona de aterrizaje proporciona el bloque de creación básico de cualquier entorno de adopción de la nube.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/20/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: f9926fd59133303960338ac4e8b45cc9007dad51
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70816234"
---
# <a name="landing-zone-considerations"></a>Consideraciones sobre la zona de aterrizaje

Una zona de aterrizaje es el bloque de creación básico de cualquier entorno de adopción de la nube. El término *zona de aterrizaje* hace referencia a un entorno que se ha aprovisionado y preparado para hospedar cargas de trabajo en un entorno en la nube como Azure. Una zona de aterrizaje plenamente funcional es el resultado final de cualquier iteración de la metodología de preparación de Cloud Adoption Framework.

![Consideraciones sobre la zona de aterrizaje](../../_images/ready/landing-zone-considerations.png)

Esta imagen muestra las principales consideraciones para realizar cualquier implementación de la zona de aterrizaje. Las consideraciones se pueden dividir en tres categorías o tipos: hospedaje, aspectos básicos de Azure y gobernanza.

## <a name="hosting-considerations"></a>Consideraciones sobre hospedaje

Todas las zonas de aterrizaje proporcionan una estructura para las opciones de hospedaje. La estructura se crea explícitamente mediante controles de gobernanza u orgánicamente mediante la adopción de servicios dentro de la zona de aterrizaje. Los artículos siguientes pueden ayudarle a tomar decisiones que se reflejarán en el plano técnico o en otros scripts de automatización que crean la zona de aterrizaje:

- **[Decisiones de proceso](./compute-decisions.md)** . Para minimizar la complejidad operativa, adapte las opciones de proceso a la finalidad de la zona de aterrizaje. Esta decisión se puede llevar a la práctica mediante cadenas de herramientas de automatización, como las iniciativas de Azure Policy y los planos técnicos de la zona de aterrizaje.
- **[Decisiones sobre el almacenamiento](./storage-guidance.md)** . Seleccione la solución de Azure Storage adecuada que cumpla los requisitos de las cargas de trabajo.
- **[Decisiones respecto a las redes](./network-decisions.md)** . Elija los servicios, las herramientas y las arquitecturas de redes que satisfagan los requisitos de carga de trabajo, gobernanza y conectividad de la organización.
- **[Decisiones respecto a las bases de datos](./data-decisions.md)** . Determinar qué tecnología de base de datos es la más adecuada para sus requisitos de cargas de trabajo.

## <a name="azure-fundamentals"></a>Aspectos básicos de Azure

Cada zona de aterrizaje forma parte de una solución más amplia para organizar los recursos a través de un entorno en la nube. Los aspectos básicos de Azure constituyen los bloques de creación fundamentales para la organización.

- **[Conceptos básicos de Azure](./fundamental-concepts.md)** . Conozca los conceptos y términos fundamentales que se usan para organizar los recursos en Azure y cómo los conceptos se relacionan entre sí.
- **Guía para la toma de decisiones sobre la organización de recursos**. Una vez que comprenda cada uno de los aspectos básicos, la guía para la toma de decisiones sobre la organización de recursos puede ayudarle a tomar las decisiones que darán forma a la zona de aterrizaje.

## <a name="governance-considerations"></a>Consideraciones de gobernanza

Las metodologías de gobierno de Cloud Adoption Framework establecen un proceso que permite gobernar el entorno en su conjunto. Sin embargo, hay muchos casos de uso que pueden requerir que tome decisiones de gobernanza según la zona de aterrizaje. En muchos escenarios, las líneas de base de gobernanza se aplican por zona de aterrizaje, incluso aunque se hayan establecido holísticamente. Esto es aplicable a las primeras zonas de aterrizaje que una organización implementa.

Los artículos siguientes pueden ayudarle a tomar decisiones relacionadas con la gobernanza respecto a su zona de aterrizaje. Puede tener en cuenta cada decisión en las líneas de base de gobernanza.

- **Requisitos de costos**. Según la motivación de una organización en relación con los compromisos operativos y de adopción de la nube respecto a su entorno, es posible que sea necesario cambiar varias configuraciones de administración de costos para la zona de aterrizaje.
- **Decisiones sobre la supervisión**. En función de los requisitos operativos para una zona de aterrizaje, se pueden implementar varias herramientas de supervisión. El artículo sobre la toma de decisiones relacionadas con la supervisión le puede ayudar a determinar las herramientas más adecuadas que puede implementar.
- **Uso del control de acceso basado en rol**. El [control de acceso basado en rol (RBAC)](../azure-best-practices/roles.md) de Azure ofrece administración de acceso específico basado en grupos para recursos organizados en torno a roles de usuario.
- **Decisiones sobre directivas**. Los ejemplos de plano técnico de Azure proporcionan planos técnicos de cumplimiento previamente creados, cada uno con iniciativas de directivas predefinidas. Las decisiones sobre directivas le informan sobre una selección del mejor plano técnico o iniciativa de directiva según sus requisitos y restricciones.
- **[Creación de coherencia en la nube híbrida](../../infrastructure/misc/hybrid-consistency.md)** . Cree soluciones de nube híbrida que ofrezcan a su organización las ventajas de la innovación en la nube conservando muchas de las comodidades de la administración local.
