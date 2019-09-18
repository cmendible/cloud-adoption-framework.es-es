---
title: Establecimiento de una base de gobernanza de la nube inicial
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Empiece a trabajar con la gobernanza de la nube mediante el establecimiento de una base inicial.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 3e1f2c1b54a55a740376ba1d1c45c13dc9e7e26d
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031449"
---
# <a name="establish-an-initial-cloud-governance-foundation"></a>Establecimiento de una base de gobernanza de la nube inicial

El establecimiento de la gobernanza de la nube es un esfuerzo iterativo amplio. Es difícil lograr un equilibrio efectivo entre velocidad y control, especialmente durante las primeras fases de la adopción de la nube. La guía de gobernanza de Cloud Adoption Framework ayuda a proporcionar ese equilibrio mediante un enfoque ágil de adopción.

En este artículo se proporcionan dos opciones para establecer una base inicial de gobernanza. Cualquiera de las opciones garantiza que las restricciones de gobernanza se pueden escalar y expandir a medida que se implementa el plan de adopción y se definen más claramente los requisitos. De forma predeterminada, la base inicial presupone una posición de aislamiento y control. También se centra más en la organización de los recursos que en la gobernanza de estos. Este punto de partida inicial se denomina _producto viable mínimo_ para la gobernanza. El objetivo del producto viable mínimo es reducir las barreras en el establecimiento de una posición de gobernanza inicial y, a continuación, permitir la rápida maduración de la solución para dar respuesta a diversos riesgos tangibles.

## <a name="already-using-the-cloud-adoption-framework"></a>Ya usa Cloud Adoption Framework

Si ya ha leído la información sobre Cloud Adoption Framework, puede que ya haya implementado un producto viable mínimo de gobernanza. La guía es un aspecto fundamental de cualquier modelo operativo. Está presente durante todas las fases del ciclo de adopción de la nube. Por tanto, [Cloud Adoption Framework](../index.md) proporciona una guía que incluye gobernanza en las actividades relacionadas con la implementación del [plan de adopción de la nube](../plan/index.md). Un ejemplo de esta integración de la gobernanza es el uso de planos técnicos para implementar una o varias zonas de aterrizaje presentes en la guía de [preparación](../ready/index.md). Otro ejemplo es una guía para el [escalado horizontal de suscripciones](../ready/considerations/scaling-subscriptions.md). Si ha seguido alguna de esas recomendaciones, las siguientes secciones del producto viable mínimo son simplemente una revisión de las decisiones de implementación ya existentes. Después de una revisión rápida, vaya directamente a [Maduración de la solución de gobernanza inicial y aplicación de controles recomendados](./foundation-improvements.md).

## <a name="establish-an-initial-governance-foundation"></a>Establecimiento de una base de gobernanza inicial

A continuación se muestran dos ejemplos diferentes de bases de gobernanza iniciales (también denominados productos mínimos viables de gobernanza) para aplicar una base sólida para la gobernanza de las implementaciones nuevas o ya existentes. Elija el producto viable mínimo que mejor se adapte a sus necesidades empresariales para empezar:

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsZ">
<li style="display: flex; flex-direction: column;">
    <a href="./guides/standard/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Guía de gobernanza estándar</h3>
                        <p>Una guía útil para la mayoría de las organizaciones basada en el modelo recomendado de dos suscripciones, diseñada para implementaciones en varias regiones, pero que no abarca nubes públicas ni soberanas.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./guides/complex/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Guía de gobernanza para empresas complejas</h3>
                        <p>Una guía para empresas administradas por varias unidades de negocio de TI independientes o que incluyen nubes públicas y soberanas o gubernamentales.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>
<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Pasos siguientes

Una vez que se implementa una base de gobernanza, aplique las recomendaciones adecuadas para mejorar la solución y protegerse frente a riesgos tangibles.

> [!div class="nextstepaction"]
> [Mejora de la base de gobernanza inicial](./foundation-improvements.md)
