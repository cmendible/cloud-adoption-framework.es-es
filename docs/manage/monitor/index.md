---
title: Guía sobre la supervisión en la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introducción a Azure Monitor y System Center Operations Manager
author: MGoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: d2f699596d6464deba81690827de00bab4a33520
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71026025"
---
# <a name="cloud-monitoring-guide-introduction"></a>Guía sobre la supervisión en la nube: Introducción

La nube presenta un cambio fundamental en la forma en que las empresas adquieren y utilizan los recursos de tecnología. En el pasado, las empresas asumían la propiedad y responsabilidad en todos los niveles de tecnología desde la infraestructura al software. Ahora, la nube ofrece a las empresas la posibilidad de aprovisionar y consumir recursos según sea necesario.

Aunque la nube ofrece una flexibilidad prácticamente ilimitada en términos de opciones de diseño, las empresas buscan una metodología probada y coherente para la adopción de tecnologías en la nube. Cada empresa tiene objetivos y escalas de tiempo diferentes para la adopción de la nube, lo cual hace que sea casi imposible encontrar un único enfoque de adopción.

![Diagrama de estrategias de adopción de la nube](./media/monitoring-management-guidance-cloud-and-on-premises/introduction-cloud-adoption.png)

Esta transformación digital también permite una oportunidad de modernizar la infraestructura, las cargas de trabajo y las aplicaciones. Según la estrategia empresarial y los objetivos, la adopción de un modelo de nube híbrida forma, probablemente, parte del proceso de transición de la migración desde un entorno local al funcionamiento completo en la nube. Durante este proceso, los equipos de TI se enfrentan al desafío de adoptar y obtener un valor rápido de la nube. El personal de TI también debe saber cómo supervisar con eficacia la aplicación o el servicio que se van a migrar a Azure y seguir ofreciendo DevOps y operaciones de TI eficaces.

Las partes interesadas quieren usar herramientas de supervisión y administración de software como servicio (SaaS) basadas en la nube. Necesitan comprender lo que los servicios y las soluciones ofrecen para lograr una visibilidad de un extremo a otro, reducir costos y prestar una menor atención a la infraestructura y el mantenimiento de las herramientas operativas tradicionales de TI basadas en software.

Sin embargo, el equipo de TI suele preferir utilizar las herramientas en las que ya ha realizado una inversión importante. Esto permite que sus procesos de operaciones de servicio supervisen ambos modelos de nube, con el objetivo final de realizar la transición a una oferta basada en SaaS. Esto se debe no solo a que lleva bastante tiempo el planeamiento, los recursos y la financiación del cambio. También existe confusión sobre qué productos o servicios de Azure son apropiados o aplicables para conseguir la transición.

El objetivo de esta guía es proporcionar una referencia detallada para ayudar a los administradores empresariales de tecnologías de TI, a los responsables de toma de decisiones empresariales y a los arquitectos y desarrolladores de aplicaciones a comprender:

* Las plataformas de supervisión, con información general y una comparación de sus funcionalidades.
* La solución que mejor se adapta a la supervisión de cargas de trabajo híbridas, privadas y nativas de Azure.
* El enfoque de supervisión recomendado para la infraestructura y las aplicaciones como un conjunto, de un extremo a otro. Esto incluye soluciones que se pueden implementar para estas cargas de trabajo comunes que se van a migrar a Azure.

Esta no es una guía paso a paso de uso o configuración de servicios y soluciones individuales de Azure, pero hace referencia a esas fuentes si son aplicables o están disponibles. Después de leer esta guía, comprenderá cómo usar correctamente una carga de trabajo siguiendo unos procedimientos y patrones recomendados.

Si no está familiarizado con Azure monitor y System Center Operations Manager y desea descubrir qué es lo que los hace únicos y cómo compararlos entre sí antes de avanzar más, revise [Introducción a las plataformas de supervisión](./platform-overview.md).

## <a name="audience"></a>Público

Esta guía resulta especialmente útil para administradores de empresas, operaciones de TI, seguridad y cumplimiento de TI, arquitectos de aplicaciones, propietarios del desarrollo de cargas de trabajo y propietarios de operaciones con estas.

## <a name="how-this-guide-is-structured"></a>Cómo se estructura esta guía

Este artículo forma parte de una serie. Los siguientes artículos están diseñados para leerlos de forma conjunta y en orden:

* Introducción (este artículo)
* [Estrategia de supervisión para modelos de implementación en la nube](./cloud-models-monitor-overview.md)
* [Recopilación de los datos adecuados](./data-collection.md)
* [Alertas](./alerting.md)

## <a name="products-and-services"></a>Productos y servicios

Hay una selección de software y servicios disponible para supervisar y administrar diversos recursos hospedados en Azure, en la red corporativa o en otros proveedores de nube. Son las siguientes:

* System Center Operations Manager
* Azure Monitor, que ahora incluye Log Analytics y Application Insights
* Azure Policy y Azure Blueprints
* Azure Automation
* Azure Logic Apps
* Azure Event Hubs

En esta primera versión de la guía se describen nuestras plataformas de supervisión actuales: Azure Monitor y System Center Operations Manager, y se describe la estrategia recomendada para supervisar cada uno de los modelos de implementación en la nube. También se incluye el primer conjunto de recomendaciones de supervisión, comenzando por la recopilación de datos y las alertas.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Estrategia de supervisión para modelos de implementación en la nube](./cloud-models-monitor-overview.md)
