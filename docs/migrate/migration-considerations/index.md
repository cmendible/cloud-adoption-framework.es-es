---
title: Modelo de migración de Cloud Adoption Framework
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Modelo de migración de Cloud Adoption Framework
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 99e5deee6551d7e4db3a0404c6dd0e81deffe35d
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224036"
---
# <a name="cloud-adoption-framework-migration-model"></a>Modelo de migración de Cloud Adoption Framework

En esta sección de Cloud Adoption Framework se explican los principios que subyacen en el modelo de migración. Siempre que sea posible, este contenido intenta mantener una posición neutral respecto a los proveedores mientras le guía por los procesos y actividades que se pueden aplicar a cualquier migración a la nube, independientemente del proveedor de nube elegido.

## <a name="understand-migration-motivations"></a>Descripción de las motivaciones de migración

La migración a la nube es un esfuerzo de administración de carteras, disfrazado de manera inteligente como una implementación técnica. Durante el proceso de migración, decidirá mover algunos recursos, invertir en otros y retirar recursos obsoletos o no utilizados. Algunos recursos se optimizarán, refactorizarán o se reemplazarán por completo como parte de este proceso. Cada una de estas decisiones debe alinearse con las motivaciones que subyacen a la migración a la nube. Las migraciones de más éxito también van un paso más allá y alinean estas decisiones con los resultados empresariales deseados.

El modelo de migración de Cloud Adoption Framework depende de que la organización haya completado un proceso de preparación empresarial para la adopción de la nube. Asegúrese de que ha revisado la guía de [planeación](../../strategy/index.md) y [preparación](../../ready/index.md) en Cloud Adoption Framework para determinar las motivaciones empresariales u otra justificación para una migración a la nube, así como cualquier planeamiento organizativo o aprendizaje necesario antes de ejecutar un proceso de migración a escala.

> [!NOTE]
> Mientras que el planeamiento empresarial es importante, una mentalidad de crecimiento es igualmente importante. Paralelamente a los esfuerzos de planeamiento empresarial más amplios del equipo de estrategia en la nube, se sugiere que el equipo de adopción de la nube comience a migrar una primera carga de trabajo como precursora de los esfuerzos de migración a mayor escala. Esta migración inicial permitirá que el equipo adquiera experiencia práctica con las cuestiones comerciales y técnicas que implica una migración.

## <a name="envision-an-end-state"></a>Previsión de un estado final

Es importante establecer una visión aproximada del estado final antes de iniciar los esfuerzos de migración. En el diagrama siguiente se muestra un punto inicial local de la infraestructura, las aplicaciones y los datos, que define su *patrimonio digital*. Durante el proceso de migración, esos recursos realizan la transición mediante una de las cinco estrategias de migración descritas en [Las cinco "R" de la racionalización](../../digital-estate/5-rs-of-rationalization.md).

![Infografía de las opciones de migración](../../_images/migrate/migration-options.png)

La migración y la modernización de las cargas de trabajo van desde simples migraciones de *rehospedaje* ("lift and shift") mediante las funcionalidades de infraestructura como servicio (IaaS) que no requieren cambios de código y aplicaciones, pasando por la *refactorización* con cambios mínimos, a *rediseño* para modificar y ampliar la funcionalidad de código y aplicaciones para aprovechar las tecnologías de la nube.

Las estrategias nativas de la nube y las estrategias de plataforma como servicio (PaaS) *recompilan* cargas de trabajo locales mediante ofertas de la plataforma Azure y servicios administrados. Las cargas de trabajo que tienen ofertas equivalentes de software como servicio (SaaS) totalmente administrado basadas en la nube pueden *reemplazarse* totalmente por estos servicios como parte del proceso de migración.

> [!NOTE]
> Durante la versión preliminar pública de Cloud Adoption Framework, en esta sección de la plataforma se hace hincapié en una estrategia de migración de rehospedaje. Aunque las soluciones PaaS y SaaS se tratan como alternativas cuando es apropiado, la migración de cargas de trabajo basadas en máquinas virtuales que utilizan funcionalidades IaaS es el objetivo principal.
>
> Otras secciones e iteraciones futuras de este contenido se ampliarán en otros enfoques. Para obtener una descripción de alto nivel sobre la ampliación del ámbito de la migración para incluir estrategias de migración más complicadas, consulte el artículo sobre cómo equilibrar la cartera.

## <a name="incremental-migration"></a>Migración incremental

El modelo de migración de Cloud Adoption Framework se basa en un proceso de transformación incremental en la nube. Asume que la organización comenzará con un esfuerzo inicial, de ámbito limitado, de migración a la nube, al que nos referimos comúnmente como la primera carga de trabajo. Este esfuerzo se ampliará de forma iterativa para incluir más cargas de trabajo a medida que los equipos de operaciones perfeccionen y mejoren sus procesos de migración.

Las herramientas de migración en nube como [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) pueden migrar centros de datos completos que consisten en decenas de miles de máquinas virtuales. Sin embargo, la empresa y las operaciones de TI existentes rara vez pueden controlar un ritmo de cambio tan alto. Como tales, muchas organizaciones dividen el esfuerzo de migración en varias iteraciones y, para ello, mueven una carga de trabajo (o una colección de cargas de trabajo) por iteración.

Los principios que subyacen en este modelo incremental se basan en la ejecución de procesos y requisitos previos a los que se hace referencia en la siguiente infografía.

![Modelo de migración de Cloud Adoption Framework](../../_images/operational-transformation-migrate.png)

La aplicación coherente de estos principios representa un objetivo final para sus procesos de migración a la nube y no debe considerarse como un punto inicial necesario. A medida que maduren los esfuerzos de migración, consulte la guía en esta sección para ayudar a definir el mejor proceso para apoyar sus necesidades organizacionales.

## <a name="next-steps"></a>Pasos siguientes

Para aprender sobre este modelo, [investigue los requisitos previos para la migración](./prerequisites/index.md).

> [!div class="nextstepaction"]
> [Requisitos previos para la migración](./prerequisites/index.md)
