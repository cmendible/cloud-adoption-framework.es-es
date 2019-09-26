---
title: Información general sobre la materia de base de referencia de identidad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Explicación del concepto de base de referencia de identidad en relación con la gobernanza de la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 7b670f2159784fdb948c95ea45b70adfd6a5fe2d
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222249"
---
# <a name="identity-baseline-discipline-overview"></a>Información general sobre la materia de base de referencia de identidad

La base de referencia de identidad es una de las [cinco materias de la gobernanza en la nube](../governance-disciplines.md) dentro del [modelo de gobernanza de Cloud Adoption Framework](../index.md). La identidad se considera cada vez más como el perímetro de seguridad principal en la nube, lo que supone un avance respecto del enfoque tradicional de seguridad de red. Los servicios de identidad proporcionan los mecanismos principales que respaldan el control de acceso y la organización en entornos de TI, y la materia de la base de referencia de identidad complementa a la [materia de la base de referencia de seguridad](../security-baseline/index.md) mediante la aplicación coherente de requisitos de autenticación y autorización en el trabajo de adopción de la nube.

> [!NOTE]
> La gobernanza de base de referencia de identidad no reemplaza los procedimientos, procesos y equipos de TI existentes que permiten a su organización administrar y proteger los servicios de identidad. El propósito principal de esta materia es identificar los posibles riesgos empresariales relacionados con la identidad y proporcionar orientación sobre la mitigación de riesgos al personal de TI responsable de la implementación, el mantenimiento y el funcionamiento de la infraestructura de administración de identidad. A medida que desarrolla procesos y directivas de gobernanza, asegúrese de implicar a los equipos de TI pertinentes en sus procesos de revisión y planeación.

En esta sección de Cloud Adoption Framework se describe el enfoque de desarrollo de una materia de base de referencia de identidad como parte de la estrategia de gobernanza en la nube. La principal audiencia a la que se dirigen estas instrucciones son los arquitectos de nube de su organización y otros miembros de su equipo de gobernanza en la nube. Sin embargo, las decisiones, las directivas y los procesos que emergen de esta materia deben implicar la involucración y discusiones con miembros pertinentes de los equipos de TI responsables de la implementación y administración de soluciones de administración de identidad de su organización.

Si su organización carece de conocimientos internos sobre la base de referencia de identidad y seguridad, considere la posibilidad de involucrar a consultores externos como parte de esta materia. Considere también la posibilidad de involucrar a [Servicios de consultoría de Microsoft](https://www.microsoft.com/enterprise/services), el servicio de adopción de la nube [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) u otros asociados externos de adopción de la nube para determinar los problemas relacionados con esta materia.

## <a name="policy-statements"></a>Policy statements

Las declaraciones de la directiva accionable y los requisitos de arquitectura resultantes actúan como base de una materia de base de referencia de identidad. Para ver ejemplos de declaraciones de la directiva, consulte el artículo sobre [declaraciones de la directiva de base de referencia de identidad](./policy-statements.md). Estos ejemplos pueden actuar como punto de inicio para las directivas de gobernanza de su organización.

> [!CAUTION]
> Las directivas de ejemplo proceden de experiencias habituales de los clientes. Para alinear mejor estas directivas con necesidades de gobernanza en la nube específicas, ejecute los pasos siguientes para crear declaraciones de la directiva que satisfagan sus necesidades empresariales únicas.

## <a name="developing-identity-baseline-governance-policy-statements"></a>Desarrollo de declaraciones de directivas de gobernanza de base de referencia de identidad

Los seis pasos siguientes ofrecen ejemplos y posibles opciones que se deben tener en cuenta al desarrollar la gobernanza de base de referencia de identidad. Use cada paso como punto de partida para análisis en el equipo de gobernanza en la nube y con los equipos de TI y empresariales afectados de toda la organización para establecer las directivas y los procesos necesarios para administrar los riesgos relacionados con la identidad.

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
                        <h3>Plantilla de base de referencia de identidad</h3>
                        <p class="x-hidden-focus">Descargue la plantilla para documentar una materia de base de referencia de identidad.</p>
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
                        <p class="x-hidden-focus">Conozca los motivos y riesgos asociados normalmente a la materia de base de referencia de identidad.</p>
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
                        <p class="x-hidden-focus">Indicadores para saber si es el momento adecuado para invertir en la materia de base de referencia de identidad.</p>
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
                        <p class="x-hidden-focus">Procesos recomendados para admitir el cumplimiento de directiva en la materia de base de referencia de identidad.</p>
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
                        <p class="x-hidden-focus">Servicios de Azure que se pueden implementar para apoyar la materia de base de referencia de identidad.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Pasos siguientes

Empiece evaluando los [riesgos empresariales](./business-risks.md) en un entorno específico.

> [!div class="nextstepaction"]
> [Descripción de los riesgos empresariales](./business-risks.md)
