---
title: Guía de decisiones sobre redes definidas por software
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información sobre las redes definidas por software como un servicio principal en las migraciones de Azure.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: ac8d65ab897ddeac94305c9d2c365281808b36c3
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817968"
---
# <a name="software-defined-networking-decision-guide"></a>Guía de decisiones sobre redes definidas por software

Redes definidas por software (SDN) es una arquitectura de red diseñada para permitir la funcionalidad de redes virtualizadas que se pueden administrar, configurar y modificar a través de software. SDN permite la creación de redes basadas en la nube con los equivalentes virtualizados de enrutadores físicos, firewalls y otros dispositivos de red que se usan en redes locales. SDN es fundamental para crear redes virtuales seguras en plataformas en la nube pública como Azure.

## <a name="networking-decision-guide"></a>Guía de decisiones sobre redes

![Esquema de las opciones de red, de las menos a las más complejas, con sus hipervínculos](../../_images/discovery-guides/discovery-guide-sdn.png)

Vaya a: [Solo PaaS](paas-only.md) | [Nativa de la nube](cloud-native.md) | [Red perimetral en la nube](cloud-dmz.md) [Híbrida](hybrid.md) | [Modelo en estrella tipo hub-and-spoke](hub-spoke.md) | [Más información](#learn-more)

SDN proporciona varias opciones con diversos grados de complejidad y precios. La guía de detección anterior proporciona una referencia para personalizar rápidamente dichas opciones, con el fin de ajustarlas lo mejor posible a estrategias empresariales y tecnológicas concretas.

El punto de inflexión de esta guía depende de varias decisiones clave que ha tomado el equipo de estrategia en la nube antes de tomar decisiones acerca de la arquitectura de red. Las más importantes de estas decisiones son aquellas en las que están implicados la [definición de patrimonio digital](../../digital-estate/index.md) y el [diseño de suscripciones](../subscriptions/index.md) (que también pueden requerir datos de decisiones relacionadas con la contabilidad en la nube y estrategias de los mercados globales).

A las implementaciones pequeñas, que se realizan en una sola región, de menos de 1 000 máquinas virtuales es menos probable que les afecte de manera considerable este punto de inflexión. Por el contrario, a los trabajos de adopciones de gran tamaño, con más de 1000 máquinas virtuales, varias unidades de negocio o varios mercados geopolíticos, podrían verse afectados considerablemente tanto por la decisión de SDN como por este punto de inflexión clave.

## <a name="choosing-the-right-virtual-networking-architectures"></a>Elección de las arquitecturas de red virtual adecuadas

Esta sección amplía la guía para la toma de decisiones, con el fin de ayudarle a elegir las arquitecturas de red virtual adecuadas.

Hay muchas maneras de implementar tecnologías de SDN para crear redes virtuales en la nube. Tanto la forma en que se estructuren las redes virtuales que se usen en la migración cómo la forma en que dichas redes interactúan con la infraestructura de TI existente dependerán de una combinación de requisitos de las cargas de trabajo y requisitos de gobernanza.

Al planear la arquitectura de red virtual o la combinación de arquitecturas que hay que tomar en consideración al planear una migración a la nube, tenga en cuenta las siguientes preguntas, ya que ello le ayudará a determinar lo que es más apropiado para su organización:

| Pregunta | solo PaaS | Nativas de la nube | Red perimetral en la nube | Híbrido | En estrella tipo hub-and-spoke |
|-----|-----|-----|-----|-----|-----|
| ¿Va a usar la carga de trabajo solo los servicios de PaaS y no va a requerir funcionalidades de red que vayan más allá de las proporcionados por los propios servicios? | Sí | No | No | No | Sin |
| ¿Requiere la carga de trabajo integración con las aplicaciones locales? | Sin | No | Sí | Sí | Sí |
| ¿Se han establecido directivas de seguridad maduras y una conectividad segura entre las redes local y en la nube? | Sin | No | No | Sí | Sí |
| ¿Requiere la carga de trabajo servicios de autenticación que no se admite a través de servicios de identidad en la nube o se necesita acceso directo a controladores de dominio locales? | Sin | No | No | Sí | Sí |
| ¿Va a ser preciso implementar y administrar un gran número de máquinas virtuales y cargas de trabajo? | Sin | No | No | No | Sí |
| ¿Se va a necesitar proporcionar administración centralizada y conectividad local al delegar el control sobre los recursos a los equipos de las cargas de trabajo individuales? | Sin | No | No | No | Sí |

## <a name="virtual-networking-architectures"></a>Arquitecturas de red virtual

Más información acerca de las arquitecturas de red principales definidas por el software:

- **[Solo PaaS](paas-only.md):** la mayoría de los productos de plataforma como servicio (PaaS) admiten un conjunto limitado de características de redes integradas y es posible que no necesiten una red definida por software explícitamente para cumplir los requisitos de las cargas de trabajo.
- **[Nativas de la nube](cloud-native.md):** una arquitectura nativa de la nube admite cargas de trabajo basadas en la nube con redes virtuales basadas en funcionalidades de redes definidas por software predeterminadas de la plataforma en la nube, sin necesidad de depender de recursos locales o externos.
- **[Red perimetral en la nube](cloud-dmz.md):** admite una conectividad limitada entre la red local y en la nube que se protege mediante la implementación de una red perimetral que controla estrechamente el tráfico entre los dos entornos.
- **[Híbrida](hybrid.md):** la arquitectura de red en la nube híbrida permite a las redes virtuales de entornos en la nube de confianza acceder a los recursos locales y viceversa.
- **[En estrella tipo hub-and-spoke](hub-spoke.md):** La arquitectura en estrella tipo hub-and-spoke permite administrar centralmente la conectividad externa y los servicios compartidos, aislar cargas de trabajo individuales y superar los límites de suscripciones posibles.

## <a name="learn-more"></a>Más información

Para más información acerca de las redes definidas por software en Azure, consulte:

- [Azure Virtual Network](/azure/virtual-network/virtual-networks-overview). En Azure, Azure Virtual Network proporciona la funcionalidad de SDN principal, que actúa como un análogo en la nube a las redes locales físicas. Las redes virtuales también actúan como límite de aislamiento predeterminado entre los recursos de la plataforma.
- [Procedimientos recomendados de seguridad de la red de Azure](/azure/security/azure-security-network-security-best-practices). Recomendaciones del equipo de seguridad de Azure para configurar las redes virtuales para minimizar las vulnerabilidades de seguridad.

## <a name="next-steps"></a>Pasos siguientes

Las redes definidas por software son solo uno de los principales componentes de infraestructura que requieren decisiones de arquitectura durante un proceso de adopción de la nube. Visite la [introducción a las guías de decisión](../index.md) para obtener información sobre los patrones o los modelos alternativos que se usan al tomar decisiones de diseño para otros tipos de infraestructura.

> [!div class="nextstepaction"]
> [Guías de decisiones sobre arquitectura](../index.md)
