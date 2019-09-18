---
title: 'Red definida por software: Red perimetral en la nube'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Esta arquitectura de red permite un acceso limitado entre la red local y las redes basadas en la nube.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 6dfee69d20afac27c735f2ff77abbadc2816ca26
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70837506"
---
# <a name="software-defined-networking-cloud-dmz"></a>Red definida por software: Red perimetral en la nube

La arquitectura de red permite un acceso limitado entre la red local y la basada en la nube, y utiliza una red privada virtual (VPN) para conectar las redes. Aunque los modelos de red perimetral se usan normalmente cuando se desea proteger el acceso externo a una red, la arquitectura de red perimetral en la nube que se describe aquí está pensada específicamente para proteger el acceso a la red local desde los recursos basados en la nube y viceversa.

![Arquitectura de red híbrida segura](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/images/dmz-private.png)

Esta arquitectura está diseñada para admitir escenarios en los que su organización desea comenzar a integrar cargas de trabajo basadas en la nube con cargas de trabajo locales pero puede que no tenga directivas de seguridad en la nube completamente maduras o no haya adquirido una conexión WAN dedicada segura entre los dos entornos. Como resultado, las redes en la nube deben tratarse como una zona desmilitarizada para garantizar que los servicios locales sean seguros.

La red perimetral implementa aplicaciones virtuales de red (NVA) para aplicar la funcionalidad de seguridad, como firewalls e inspección de paquetes. El tráfico que circula entre aplicaciones o servicios locales y basados en la nube debe pasar a través de la red perimetral, donde se puede auditar. Las conexiones de VPN y las reglas que determinan qué tráfico se permite a través de la perimetral están estrictamente controladas por los equipos de seguridad de TI.

## <a name="cloud-dmz-assumptions"></a>Suposiciones de la red perimetral en la nube

En la implementación de una red perimetral en la nube se da por hecho lo siguiente:

- Sus equipos de seguridad no han alineado completamente las directivas y los requisitos de seguridad locales y basados en la nube.
- Sus cargas de trabajo basadas en la nube requieren acceso a un subconjunto limitado de servicios hospedados en sus redes locales o de terceros, o los usuarios o aplicaciones del entorno local necesitan acceso limitado a los recursos hospedados en la nube.
- La implementación de una conexión VPN entre las redes locales y el proveedor de servicios en la nube no se ve impedida por la directiva corporativa, los requisitos normativos o los problemas de compatibilidad técnica.
- Sus cargas de trabajo no requieren múltiples suscripciones para omitir los límites de recursos de suscripción, o implican múltiples suscripciones pero no requieren una administración central de la conectividad o los servicios compartidos utilizados por los recursos distribuidos entre varias suscripciones.

El equipo de adopción de la nube debe considerar los siguientes problemas al considerar la implementación de una arquitectura de red virtual perimetral en la nube:

- Conectar redes locales con redes en la nube aumenta la complejidad de los requisitos de seguridad. Aunque se proteja la conexión entre las redes en la nube y el entorno local, deberá cerciorarse de que los recursos en la nube están seguros. Todas las direcciones IP públicas creadas para acceder a las cargas de trabajo basadas en la nube deben protegerse correctamente mediante una [red perimetral de acceso público](/azure/architecture/reference-architectures/dmz/secure-vnet-dmz) o [Azure Firewall](/azure/firewall).
- La arquitectura de la red perimetral en la nube se usa comúnmente como punto de partida, mientras que la conectividad se protege aún más y la directiva de seguridad se alinea entre las redes locales y en la nube, lo que permite una adopción más amplia de una arquitectura de red híbrida a gran escala. Sin embargo, también puede aplicarse a implementaciones aisladas con necesidades específicas de seguridad, identidad y conectividad que el enfoque de la red perimetral en la nube satisface.

## <a name="learn-more"></a>Más información

Para más información acerca de cómo implementar una red perimetral en la nube en Azure, consulte:

- [Implementación de una zona DMZ entre Azure y el centro de datos local](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) Este artículo aborda el proceso para implementar una arquitectura de red híbrida segura en Azure.
