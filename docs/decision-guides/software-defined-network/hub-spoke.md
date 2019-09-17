---
title: 'Redes definidas por software: En estrella tipo hub-and-spoke'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Descripción de los servicios de redes virtuales nativas para la nube.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: f47bf0256e00eafe37ebf71ed2da9b64f0b07484
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70837874"
---
# <a name="software-defined-networking-hub-and-spoke"></a>Redes definidas por software: En estrella tipo hub-and-spoke

El modelo de redes en estrella tipo hub-and-spoke organiza la infraestructura de la red en la nube basada en Azure en varias redes virtuales conectadas. Este modelo le permite administrar los requisitos comunes de comunicación o seguridad de manera más eficaz, así como gestionar las posibles limitaciones de suscripción.

En el modelo en estrella tipo hub-and-spoke, el _centro de conectividad_ es una red virtual que actúa como ubicación central para administrar la conectividad externa y los servicios de hospedaje que las diversas cargas de trabajo utilizan. Los _radios_ son redes virtuales que hospedan las cargas de trabajo y se conectan al centro de conectividad central a través del [emparejamiento de redes virtuales](/azure/virtual-network/virtual-network-peering-overview).

Todo el tráfico que pasa hacia dentro o fuera de las redes radiales de carga de trabajo se enruta a través de la red del centro de conectividad donde se puede enrutar, inspeccionar o administrar mediante reglas o procesos de TI administrados centralmente.

Este modelo pretende abordar cada uno de los siguientes aspectos:

- **Ahorro en costos y eficiencia de la administración**. La centralización de los servicios que se pueden compartir entre varias cargas de trabajo, como las aplicaciones virtuales de red (NVA) y los servidores DNS, en una única ubicación permite que TI minimice los recursos redundantes y el esfuerzo de administración en varias cargas de trabajo.
- **Superación de los límites de las suscripciones**. Las cargas de trabajo grandes basadas en la nube pueden requerir el uso de más recursos que los permitidos en una sola suscripción de Azure (consulte [límites de suscripción](/azure/azure-subscription-service-limits)). El emparejamiento de redes virtuales de carga de trabajo de distintas suscripciones con un centro de conectividad central puede superar estos límites.
- **Separación de intereses**. La capacidad de implementar cargas de trabajo individuales entre los equipos de TI centrales y los equipos de las cargas de trabajo.

En el diagrama siguiente se muestra un ejemplo de arquitectura en estrella tipo hub-and-spoke, incluida la conectividad híbrida administrada centralmente.

![Arquitectura de red en estrella tipo hub-and-spoke](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/images/hub-spoke.png)

La arquitectura en estrella tipo hub-and-spoke se usa a menudo junto con la arquitectura de red híbrida, lo que proporciona una conexión administrada centralmente para el entorno local compartido entre varias cargas de trabajo. En este escenario, todo el tráfico realizado entre las cargas de trabajo y el entorno local pasa a través del centro de conectividad, donde puede administrarse y protegerse.

## <a name="hub-and-spoke-assumptions"></a>Suposiciones de redes en estrella tipo hub-and-spoke

En la implementación de una arquitectura de red virtual en estrella tipo hub-and-spoke, se da por supuesto lo siguiente:

- Las implementaciones en la nube implicarán cargas de trabajo hospedadas en entornos de trabajo independientes, como desarrollo, prueba y producción, y todos ellos se basan en un conjunto de servicios comunes, como DNS o servicios de directorio.
- Las cargas de trabajo no necesitan comunicarse entre sí, pero tienen requisitos comunes de comunicaciones externas y servicios compartidos.
- Las cargas de trabajo requieren más recursos de los que están disponibles en una sola suscripción de Azure.
- Deberá proporcionar a los equipos de carga de trabajo derechos de administración delegada sobre sus propios recursos mientras conservan el control de seguridad central sobre la conectividad externa.

## <a name="global-hub-and-spoke"></a>Redes en estrella tipo hub-and-spoke

Las arquitecturas en estrella tipo hub-and-spoke normalmente se implementan con redes virtuales implementadas en la misma región de Azure para minimizar la latencia entre las redes. Sin embargo, puede que las grandes organizaciones con alcance global necesiten implementar cargas de trabajo en varias regiones para la disponibilidad, la recuperación ante desastres o los requisitos normativos. El modelo de hub-and-spoke puede usar el [emparejamiento global de redes virtuales](/azure/virtual-network/virtual-network-peering-overview) de Azure para extender la administración centralizada y los servicios compartidos entre regiones y admitir cargas de trabajo distribuidas en todo el mundo.

## <a name="learn-more"></a>Más información

Para ver cómo implementar las redes en estrella tipo hub-and-spoke en Azure, consulte los ejemplos siguientes en el sitio de arquitecturas de referencia de Azure:

- [Implementación de una topología de red en estrella tipo hub-and-spoke en Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)
- [Implementación de una topología de red en estrella tipo hub-and-spoke con servicios compartidos en Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services)
