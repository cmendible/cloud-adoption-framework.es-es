---
title: Gobernanza en Microsoft Cloud Adoption Framework para Azure
description: Más información sobre la gobernanza en Microsoft Cloud Adoption Framework para Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: adaf4358cb3d3781b892c8a614ecaba6177c6d5a
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817526"
---
# <a name="governance-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Gobernanza en Microsoft Cloud Adoption Framework para Azure

La nube crea nuevos paradigmas para las tecnologías que respaldan el negocio. Estos nuevos paradigmas también cambian la forma en que se adoptan, administran y gobiernan esas tecnologías. Si es posible destruir y volver a crear centros de datos enteros con una sola línea de código ejecutada desde un proceso desatendido, es preciso volver a considerar los enfoques tradicionales. Esto es especialmente cierto en el caso de la gobernanza.

## <a name="get-started-with-cloud-governance"></a>Introducción a la gobernanza de la nube

La gobernanza de la nube es un proceso iterativo. Para las organizaciones con directivas existentes que gobiernan los entornos de TI locales, la gobernanza de la nube debe complementar esas directivas. Sin embargo, el nivel de integración de las directivas corporativas entre el entorno local y la nube varía en función de la madurez de la gobernanza de la nube y del patrimonio digital en la nube. A medida que el patrimonio de la nube cambia con el tiempo, también lo hacen los procesos y las directivas de gobernanza de la nube. Los ejercicios siguientes le ayudarán a empezar a crear su base de gobernanza inicial.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsF">
    <li style="display: flex; flex-direction: column;">
        <a href="./methodology.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/1.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Metodología</h3>
Establezca un reconocimiento básico de la metodología que promueve la gobernanza en la nube dentro de Cloud Adoption Framework para empezar a pensar en la solución de estado final.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./benchmark.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/2.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Prueba comparativa</h3>
Evaluación del estado actual y futuro para establecer una visión a la hora de aplicar la plataforma.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./getting-started.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/3.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Base de gobernanza inicial</h3>
Comience su recorrido por la gobernanza con un pequeño conjunto de herramientas de gobernanza de fácil implementación. Esta base de gobernanza inicial se denomina producto viable mínimo (MVP).
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./best-practices.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/4.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Mejora de la base de gobernanza inicial</h3>
Durante la implementación del plan de adopción de la nube, agregue de manera iterativa los controles de gobernanza para afrontar riesgos tangibles a medida que avanza hacia el estado final.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="objective-of-this-content"></a>Objetivo de este contenido

La guía de esta sección de Cloud Adoption Framework sirve para dos fines:

- Proporcionar ejemplos de guías prácticas de gobernanza que representan experiencias comunes que los clientes encuentran a menudo. Cada ejemplo encapsula los riesgos empresariales, las directivas corporativas para la mitigación de riesgos y la guía de diseño para la implementación de soluciones técnicas. Por necesidad, la guía de diseño es específica de Azure. El contenido restante de estas guías puede aplicarse en un enfoque independiente de la nube o en un enfoque de nube múltiple.
- Ayudar a crear soluciones de gobernanza personalizadas que satisfagan diferentes necesidades empresariales. Estas necesidades incluyen la gobernanza de varias nubes públicas con una guía detallada sobre el desarrollo de las herramientas, los procesos y las directivas corporativas.

Este contenido está diseñado para su uso por parte del equipo de gobernanza de la nube. También es relevante para los arquitectos de nube que necesitan desarrollar una base sólida en la gobernanza de la nube.

## <a name="intended-audience"></a>Destinatarios

El contenido de Cloud Adoption Framework afecta al negocio, a la tecnología y a la cultura de las empresas. Esta sección de Cloud Adoption Framework interactúa considerablemente con los equipos de seguridad de TI, gobernanza de TI, finanzas, responsables de línea de negocio, redes, identidad y adopción de la nube. Varias dependencias de estos roles requieren un enfoque facilitador por parte de los arquitectos de la nube que usan esta guía. La facilitación de estos equipos puede ser una tarea única. En algunos casos, las interacciones con estos otros usuarios serán continuas.

El arquitecto de la nube sirve como líder de pensamiento y facilitador para reunir a estas audiencias. El contenido de esta colección de guías está diseñado para ayudar al arquitecto de la nube a facilitar la conversación correcta, con la audiencia adecuada, para tomar las decisiones necesarias. La transformación empresarial que potencia la nube depende de que el arquitecto de la nube sirva de guía en las decisiones tanto de TI como de toda la empresa.

**Especialización de arquitecto de la nube en esta sección**: Cada una de las secciones de Cloud Adoption Framework representa una especialización o variante diferentes del rol de arquitecto de la nube. Esta sección de Cloud Adoption Framework está diseñada para arquitectos de la nube con pasión por la reducción de riesgos técnicos. Algunos proveedores de servicios en la nube se refieren a estos especialistas como *administradores de la nube*, pero nosotros preferimos llamarles *protectores de la nube* o, colectivamente, *equipo de gobernanza de la nube*. En cada guía práctica de gobernanza, los artículos muestran cómo la composición y el rol del equipo de gobernanza de la nube pueden cambiar con el tiempo.

## <a name="use-this-guide"></a>Uso de esta guía

Si desea seguir esta guía de principio a fin, este contenido ayuda a desarrollar una sólida estrategia de gobernanza en la nube en paralelo con la implementación de la nube. Estas instrucciones le guían mediante la teoría y la implementación de dicha estrategia.

Para un curso intensivo sobre la teoría y el acceso rápido a la implementación de Azure, comience con la [introducción a las guías de gobernanza](./journeys/index.md). Mediante esta guía, puede empezar con poco y mejorar iterativamente sus necesidades de gobernanza en paralelo con los esfuerzos de adopción de la nube.

## <a name="next-steps"></a>Pasos siguientes

Establezca un reconocimiento básico de la metodología que promueve la gobernanza en la nube dentro de Cloud Adoption Framework.

> [!div class="nextstepaction"]
> [Descripción de la metodología](./methodology.md)
