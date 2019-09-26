---
title: Introducción a la materia de aceleración de la implementación
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Explicación de la aceleración de la implementación con respecto a la gobernanza de la nube.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: f96ada5b1c43694d0ea1af10524f3c344db62356
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222713"
---
# <a name="deployment-acceleration-discipline-overview"></a>Introducción a la materia de aceleración de la implementación

La aceleración de la implementación es una de las [cinco materias de la gobernanza en la nube](../governance-disciplines.md) dentro del [modelo de gobernanza de Cloud Adoption Framework](../index.md). Esta materia se centra en las distintas maneras de establecer directivas para gobernar la configuración o implementación de recursos. Dentro de las cinco materias de la gobernanza en la nube, la aceleración de la implementación incluye la implementación, la alineación de la configuración y la reutilización de scripts. Esto se puede realizar a través de actividades manuales o de actividades de DevOps completamente automatizadas. En cualquier caso, las directivas seguirían siendo en gran medida las mismas. A medida que madura esta materia, el equipo de gobernanza en la nube puede actuar como asociado en las estrategias de DevOps y de implementación al acelerar las implementaciones y eliminar los obstáculos para la adopción de la nube, mediante la aplicación de recursos reutilizables.

En este artículo se describe el proceso de aceleración de la implementación que una empresa experimenta durante las fases de planeamiento, compilación, adopción y operación de implementación de una solución en la nube. Es imposible que ningún documento recopile todos los requisitos para ninguna empresa. Por lo tanto, cada sección de este artículo describe actividades posibles y mínimas sugeridas. El objetivo inicial de estas actividades es ayudarle a crear un [MVP de directivas](../policy-compliance/index.md#minimum-viable-product-mvp-for-policy), pero establecer un marco para la mejora de [directivas incrementales](../policy-compliance/index.md#incremental-policy-growth). El equipo de gobernanza en la nube debe decidir cuánto invertir en estas actividades para mejorar la posición de la aceleración de la implementación.

> [!NOTE]
> La materia de aceleración de la implementación no reemplaza los procedimientos, procesos y equipos de TI existentes que permiten a su organización implementar y configurar de manera eficaz los recursos basados en la nube. El principal objetivo de esta materia es identificar posibles riesgos empresariales y proporcionar orientación en mitigación de riesgos al personal de TI responsable de la administración de sus recursos en la nube. A medida que desarrolla procesos y directivas de gobernanza, asegúrese de implicar a los equipos de TI pertinentes en sus procesos de revisión y planeación.

La principal audiencia a la que se dirigen estas instrucciones son los arquitectos de nube de su organización y otros miembros de su equipo de gobernanza en la nube. Sin embargo, las decisiones, las directivas y los procesos que emergen de esta materia deben implicar la involucración y discusiones con miembros pertinentes de los equipos de TI y la empresa, especialmente aquellos directores responsables de la implementación y configuración de cargas de trabajo basadas en la nube.

## <a name="policy-statements"></a>Policy statements

Las instrucciones accionables de las directivas y los requisitos de arquitectura resultantes actúan como base de una materia de aceleración de la implementación. Para ver ejemplos de declaraciones de la directiva, consulte el artículo sobre [declaraciones de la directiva de aceleración de la implementación](./policy-statements.md). Estos ejemplos pueden actuar como punto de inicio para las directivas de gobernanza de su organización.

> [!CAUTION]
> Las directivas de ejemplo proceden de experiencias habituales de los clientes. Para alinear mejor estas directivas con necesidades de gobernanza en la nube específicas, ejecute los pasos siguientes para crear declaraciones de la directiva que satisfagan sus necesidades empresariales únicas.

## <a name="developing-deployment-acceleration-governance-policy-statements"></a>Desarrollo de las instrucciones de directiva de gobernanza de aceleración de la implementación

Los seis pasos siguientes le ayudarán a definir las directivas de gobernanza para controlar la implementación y configuración de recursos en el entorno de nube.

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
                        <h3>Plantilla de aceleración de la implementación</h3>
                        <p class="x-hidden-focus">Descargue la plantilla para documentar una materia de aceleración de la implementación.</p>
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
                        <p class="x-hidden-focus">Conozca los motivos y riesgos asociados normalmente a la materia de aceleración de la implementación.</p>
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
                        <p class="x-hidden-focus">Indicadores para saber si es el momento adecuado para invertir en la materia de aceleración de la implementación.</p>
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
                        <p class="x-hidden-focus">Procesos recomendados para admitir el cumplimiento de directiva en la materia de aceleración de la implementación.</p>
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
                        <p class="x-hidden-focus">Servicios de Azure que se pueden implementar para admitir la materia de aceleración de la implementación.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

## <a name="next-steps"></a>Pasos siguientes

Empiece evaluando los [riesgos empresariales](./business-risks.md) en un entorno específico.

> [!div class="nextstepaction"]
> [Descripción de los riesgos empresariales](./business-risks.md)

<!-- markdownlint-enable MD033 -->
