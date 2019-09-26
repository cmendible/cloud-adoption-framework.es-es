---
title: Información general sobre la materia de base de referencia de seguridad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Información general sobre la materia de base de referencia de seguridad
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 1338fb14ed39915dc9e55c855dd5bbf00ba7a6eb
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221753"
---
# <a name="security-baseline-discipline-overview"></a>Información general sobre la materia de base de referencia de seguridad

La coherencia de recursos es una de las [cinco materias de la gobernanza en la nube](../governance-disciplines.md) dentro del [modelo de gobernanza de Cloud Adoption Framework](../index.md). La seguridad es un componente de cualquier implementación de TI y la nube presenta problemas de seguridad únicos. Muchas empresas están sujetas a requisitos reglamentarios que convierten la protección de datos confidenciales en una prioridad importante de la organización al considerar una transformación de la nube. La identificación de posibles amenazas de seguridad al entorno en la nube y el establecimiento de procesos y procedimientos de tratamiento de estas amenazas deben ser prioritarios para cualquier equipo de seguridad cibernética o seguridad de TI. La materia de base de referencia de seguridad garantiza la aplicación coherente de requisitos técnicos y restricciones de seguridad a entornos en la nube, a medida que esos requisitos se desarrollan.

> [!NOTE]
> La gobernanza de base de referencia de seguridad no reemplaza los procedimientos, procesos y equipos de TI existentes que usa su organización para proteger los recursos implementados por la nube. El principal objetivo de esta materia es identificar riesgos empresariales relacionados con la seguridad y proporcionar orientación en mitigación de riesgos al personal de TI responsable de la infraestructura de seguridad. A medida que desarrolla procesos y directivas de gobernanza, asegúrese de implicar a los equipos de TI pertinentes en sus procesos de revisión y planeación.

En este artículo se describe el enfoque de desarrollo de una materia de base de referencia de seguridad como parte de su estrategia de gobernanza en la nube. La principal audiencia a la que se dirigen estas instrucciones son los arquitectos de nube de su organización y otros miembros de su equipo de gobernanza en la nube. Sin embargo, las decisiones, las directivas y los procesos que emergen de esta materia deben implicar la involucración y discusiones con miembros pertinentes de los equipos de seguridad y TI, especialmente aquellos líderes técnicos responsables de la implementación de servicios de identidad, cifrado y redes.

Tomar las decisiones de seguridad correctas es fundamental para el éxito de sus implementaciones en la nube y un mayor éxito empresarial. Si su organización carece de conocimientos internos sobre seguridad cibernética, considere la posibilidad de involucrar a consultores de seguridad externos como componente de esta materia. Considere también la posibilidad de involucrar a [Servicios de consultoría de Microsoft](https://www.microsoft.com/enterprise/services), el servicio de adopción de la nube [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) u otros expertos en adopción de la nube externos para determinar los problemas relacionados con esta materia.

## <a name="policy-statements"></a>Policy statements

Las declaraciones de la directiva accionable y los requisitos de arquitectura resultantes actúan como base de una materia de base de referencia de seguridad. Para ver ejemplos de declaraciones de la directiva, consulte el artículo sobre [declaraciones de la directiva de base de referencia de seguridad](./policy-statements.md). Estos ejemplos pueden actuar como punto de inicio para las directivas de gobernanza de su organización.

> [!CAUTION]
> Las directivas de ejemplo proceden de experiencias habituales de los clientes. Para alinear mejor estas directivas con necesidades de gobernanza en la nube específicas, ejecute los pasos siguientes para crear declaraciones de la directiva que satisfagan sus necesidades empresariales únicas.

## <a name="developing-security-baseline-governance-policy-statements"></a>Desarrollo de declaraciones de directivas de gobernanza de base de referencia de seguridad

Los seis pasos siguientes ofrecen ejemplos y posibles opciones que se deben tener en cuenta al desarrollar la gobernanza de base de referencia de seguridad. Use cada paso como punto de partida de análisis en el equipo de gobernanza en la nube y con los equipos de seguridad, TI y empresariales afectados de toda la organización para establecer las directivas y procesos necesarios para administrar los riesgos relacionados con la seguridad.

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
                        <h3>Plantilla de base de referencia de seguridad</h3>
                        <p class="x-hidden-focus">Descargue la plantilla para documentar una materia de base de referencia de seguridad.</p>
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
                        <p class="x-hidden-focus">Conozca los motivos y riesgos asociados normalmente a la materia de base de referencia de seguridad.</p>
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
                        <p class="x-hidden-focus">Indicadores para saber si es el momento adecuado para invertir en la materia de base de referencia de seguridad.</p>
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
                        <p class="x-hidden-focus">Procesos recomendados para admitir el cumplimiento de directiva en la materia de base de referencia de seguridad.</p>
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
                        <p class="x-hidden-focus">Servicios de Azure que se pueden implementar para admitir la materia de base de referencia de seguridad.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="next-steps"></a>Pasos siguientes

Empiece evaluando riesgos empresariales en un entorno específico.

> [!div class="nextstepaction"]
> [Descripción de los riesgos empresariales](./business-risks.md)
