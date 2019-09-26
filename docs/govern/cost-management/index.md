---
title: Información general sobre la materia de administración de costos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Explicación de la administración de costos en relación con la gobernanza de la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: b95d3ccf3a7248c38da9936a55fc169adcf2f2a2
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221164"
---
# <a name="cost-management-discipline-overview"></a>Información general sobre la materia de administración de costos

La administración de costos es una de las [cinco materias de la gobernanza en la nube](../governance-disciplines.md) dentro del [modelo de gobernanza de Cloud Adoption Framework](../index.md). Para muchos clientes, controlar los costos es una preocupación importante al adoptar tecnologías de nube. Equilibrar las demandas de rendimiento, el ritmo de adopción y los costos de los servicios en la nube puede suponer todo un desafío. Esto es especialmente pertinente durante las transformaciones de negocios importantes que implementan tecnologías de nube. En esta sección se describe el enfoque de desarrollo de una materia de administración de costos como parte de una estrategia de gobernanza en la nube.

> [!NOTE]
> La gobernanza de la administración de costos no reemplaza los equipos de negocios, las prácticas contables y los procedimientos existentes que intervienen en la administración financiera de la organización de los costos relacionados con la TI. El objetivo principal de esta materia es determinar los posibles riesgos relativos a la nube relacionados con el gasto en TI y proporcionar una guía de mitigación de riesgos para la empresa y los equipos de TI responsables de la implementación y la administración de los recursos en la nube.

La principal audiencia a la que se dirigen estas instrucciones son los arquitectos de nube de su organización y otros miembros de su equipo de gobernanza en la nube. Sin embargo, las decisiones, las directivas y los procesos que surgen de esta materia deben implicar la participación y los debates con miembros pertinentes de los equipos de TI y la empresa, especialmente aquellos directores responsables de la posesión, la administración y el pago de cargas de trabajo basadas en la nube.

## <a name="policy-statements"></a>Policy statements

Las declaraciones de la directiva que requieren acción y los requisitos de arquitectura resultantes actúan como base de una materia de administración de costos. Para ver ejemplos de declaraciones de la directiva, consulte el artículo sobre [declaraciones de la directiva de administración de costos](./policy-statements.md). Estos ejemplos pueden actuar como punto de inicio para las directivas de gobernanza de su organización.

> [!CAUTION]
> Las directivas de ejemplo proceden de experiencias habituales de los clientes. Para alinear mejor estas directivas con necesidades de gobernanza en la nube específicas, ejecute los pasos siguientes para crear declaraciones de la directiva que satisfagan sus necesidades empresariales únicas.

## <a name="developing-cost-management-governance-policy-statements"></a>Desarrollo de las declaraciones de directiva de gobernanza de administración de costos

Los seis pasos siguientes le ayudarán a definir directivas de gobernanza para controlar los costos en su entorno.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsE">
<li style="display: flex; flex-direction: column;">
    <a href="./template.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-template.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Plantilla de administración de costos</h3>
                        <p class="x-hidden-focus">Descargue la plantilla para documentar una materia de administración de costos.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li><li style="display: flex; flex-direction: column;">
    <a href="./business-risks.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-risks.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Riesgos empresariales</h3>
                        <p class="x-hidden-focus">Conozca los motivos y riesgos asociados normalmente a la materia de administración de costos.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./metrics-tolerance.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-metrics.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Indicadores y métricas</h3>
                        <p class="x-hidden-focus">Indicadores para saber si es el momento adecuado para invertir en la materia de administración de costos.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./compliance-processes.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-enforce.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Procesos de adhesión a las directivas</h3>
                        <p class="x-hidden-focus">Procesos recomendados para admitir el cumplimiento de directiva en la materia de administración de costos.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./discipline-improvement.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-maturity.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Madurez</h3>
                        <p class="x-hidden-focus">Alineación de la madurez de la administración en la nube con fases de adopción de la nube.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./toolchain.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/govern/process-toolchain.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Cadena de herramientas</h3>
                        <p class="x-hidden-focus">Servicios de Azure que se pueden implementar para admitir la materia de administración de costos.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

## <a name="next-steps"></a>Pasos siguientes

Empiece evaluando riesgos empresariales en un entorno específico.

> [!div class="nextstepaction"]
> [Descripción de los riesgos empresariales](./business-risks.md)

<!-- markdownlint-enable MD033 -->
