---
title: 'Redes definidas por software: Red híbrida'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Análisis sobre cómo las redes híbridas permiten a las redes virtuales en la nube conectarse a recursos locales.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 94e285f59442b6632209e1cd6a76c39cfccd337b
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70837858"
---
# <a name="software-defined-networking-hybrid-network"></a>Redes definidas por software: Red híbrida

La arquitectura de red en una nube híbrida permite a las redes virtuales acceder a los recursos y servicios locales y viceversa, mediante una conexión WAN dedicada como ExpressRoute o cualquier otro método de conexión que conecte directamente las redes.

![Red híbrida](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/images/expressroute.png)

Al crear en una arquitectura de red virtual nativa en la nube, la red virtual híbrida está aislada en el momento de su creación. El hecho de incorporar la conectividad al entorno local concede acceso a la red local y desde esta, aunque el resto del tráfico entrante con destino a recursos de la red virtual deberá permitirse explícitamente. Puede proteger la conexión mediante dispositivos de firewall y reglas de enrutamiento virtuales para restringir el acceso, o puede indicar a qué servicios se puede acceder específicamente entre las dos redes mediante características de enrutamiento nativas para la nube o la implementación de aplicaciones virtuales de red (NVA) que administren el tráfico.

Aunque la arquitectura de red híbrida es compatible con las conexiones VPN, se prefieren conexiones WAN dedicadas, como ExpressRoute, debido a un mayor rendimiento y a una seguridad mejorada.

## <a name="hybrid-assumptions"></a>Suposiciones sobre la red híbrida

La implementación de una red virtual híbrida incluye las siguientes suposiciones:

- El equipo de seguridad de TI se ha alineado con una directiva de seguridad de red local y otra basada en la nube que garantiza que las redes virtuales basadas en la nube sean de confianza para poder comunicarse directamente con sistemas locales.
- Sus cargas de trabajo basadas en la nube requieren acceso al almacenamiento, las aplicaciones y los servicios hospedados en sus redes locales o de terceros, o sus usuarios o aplicaciones del entorno local necesitan acceso a los recursos hospedados en la nube.
- Debe migrar las aplicaciones y servicios existentes que dependen de recursos locales, pero no desea gastar los recursos en un nuevo desarrollo para eliminar esas dependencias.
- La conexión de las redes locales a los recursos en la nube a través de VPN o WAN dedicada no se evita mediante directivas corporativas, requisitos de soberanía de datos ni otros temas de cumplimiento normativo.
- Las cargas de trabajo o no requieren varias suscripciones para omitir los límites de recursos de suscripción o incluyen varias suscripciones, pero no requieren una administración central de la conectividad ni los servicios compartidos usados por los recursos distribuidos entre varias suscripciones.

El equipo de adopción de la nube debe tener en cuenta los siguientes problemas al considerar la implementación de una arquitectura de red virtual híbrida:

- Conectar redes locales con redes en la nube aumenta la complejidad de los requisitos de seguridad. Ambas redes deben protegerse frente a vulnerabilidades externas y accesos no autorizados desde ambos lados del entorno híbrido.
- Escalar el número y el tamaño de las cargas de trabajo dentro de un entorno de nube híbrida puede agregar una complejidad significativa a la administración del enrutamiento y el tráfico.
- Deberá desarrollar directivas compatibles de administración y control de acceso para mantener una gobernanza coherente en toda la organización.

## <a name="learn-more"></a>Más información

Para obtener más información sobre las redes híbridas en Azure, vea:

- [Arquitectura de referencia de una red híbrida](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/expressroute). Las redes virtuales híbridas de Azure usan un circuito de ExpressRoute o una VPN de Azure para conectar la red virtual con los recursos de TI existentes de la organización no hospedados en Azure. En este artículo se describen las opciones para crear una red híbrida de Azure.
