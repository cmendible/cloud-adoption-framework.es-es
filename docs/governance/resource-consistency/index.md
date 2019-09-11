---
title: Introducción a la materia de coherencia de recursos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introducción a la materia de coherencia de recursos
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: fa82b90981b5621ad3e82176c06bbb4506adfeed
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817373"
---
# <a name="resource-consistency-discipline-overview"></a>Introducción a la materia de coherencia de recursos

La coherencia de recursos es una de las [cinco materias de la gobernanza en la nube](../governance-disciplines.md) dentro del [modelo de gobernanza de Cloud Adoption Framework](../index.md). Esta materia se centra en las distintas formas de establecer directivas relacionadas con la administración operativa de un entorno, una aplicación o una carga de trabajo. Los equipos de operaciones de TI suelen proporcionar la supervisión de aplicaciones, la carga de trabajo y el rendimiento de recurso. También suelen ejecutar las tareas necesarias para satisfacer las demandas de escala, corregir las infracciones del Acuerdo de Nivel de Servicio (SLA) de rendimiento y evitar de forma proactiva las infracciones del SLA de rendimiento a través de la corrección automatizada. Dentro de las cinco materias de la gobernanza de la nube, la coherencia de recursos es una materia que garantiza la configuración coherente de los recursos de forma que las operaciones de TI puedan detectarlos, su inclusión en soluciones de recuperación y su incorporación en procesos de operaciones reiterativas.

> [!NOTE]
> La gobernanza de la coherencia de recursos no reemplaza los procedimientos, procesos y equipos de TI existentes que permiten a su organización administrar eficazmente recursos basados en la nube. El principal objetivo de esta materia es identificar posibles riesgos empresariales y proporcionar orientación en mitigación de riesgos al personal de TI responsable de la administración de sus recursos en la nube. A medida que desarrolla procesos y directivas de gobernanza, asegúrese de implicar a los equipos de TI pertinentes en sus procesos de revisión y planeación.

En esta sección de Cloud Adoption Framework se describe cómo desarrollar una materia de coherencia de recursos como parte de la estrategia de gobernanza en la nube. La principal audiencia a la que se dirigen estas instrucciones son los arquitectos de nube de su organización y otros miembros de su equipo de gobernanza en la nube. Sin embargo, las decisiones, las directivas y los procesos que emergen de esta materia deben implicar la involucración y discusiones con miembros pertinentes de los equipos de TI responsables de la implementación y administración de soluciones de coherencia de recursos de su organización.

Si su organización carece de conocimientos internos sobre estrategias de coherencia de recursos, considere la posibilidad de involucrar a consultores externos como parte de esta materia. Considere también la posibilidad de involucrar a [Servicios de consultoría de Microsoft](https://www.microsoft.com/enterprise/services), el servicio de adopción de la nube [Microsoft FastTrack](https://azure.microsoft.com/programs/azure-fasttrack) u otros expertos en adopción de la nube externos para determinar la mejor forma de organizar, optimizar y realizar un seguimiento de sus recursos basados en la nube.

## <a name="policy-statements"></a>Policy statements

Las declaraciones de la directiva accionable y los requisitos de arquitectura resultantes actúan como base de una materia de coherencia de recursos. Para ver ejemplos de declaraciones de la directiva, consulte el artículo sobre [declaraciones de la directiva de coherencia de recursos](./policy-statements.md). Estos ejemplos pueden actuar como punto de inicio para las directivas de gobernanza de su organización.

> [!CAUTION]
> Las directivas de ejemplo proceden de experiencias habituales de los clientes. Para alinear mejor estas directivas con necesidades de gobernanza en la nube específicas, ejecute los pasos siguientes para crear declaraciones de la directiva que satisfagan sus necesidades empresariales únicas.

## <a name="developing-resource-consistency-governance-policy-statements"></a>Desarrollo de declaraciones de la directiva de gobernanza de coherencia de recursos

Los seis pasos siguientes ofrecen ejemplos y posibles opciones que se deben tener en cuenta al desarrollar la gobernanza de coherencia de recursos. Use cada paso como punto de partida para análisis en el equipo de gobernanza en la nube y con los equipos de TI y empresariales afectados de toda la organización para establecer las directivas y procesos necesarios para administrar los riesgos de coherencia de recursos.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsE">
<li style="display: flex; flex-direction: column;">
    <a href="./template.md">
        <div class="cardSize">
            <div class="cardPadding" >
                <div class="card" >
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../../_images/governance/process-template.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Plantilla de la coherencia de recursos</h3>
                        <p class="x-hidden-focus">Descargue la plantilla para documentar una materia de coherencia de recursos</p>
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
                            <img src="../../_images/governance/process-risks.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Riesgos empresariales</h3>
                        <p class="x-hidden-focus">Conozca los motivos y riesgos asociados normalmente a la materia de coherencia de recursos.</p>
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
                            <img src="../../_images/governance/process-metrics.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Indicadores y métricas</h3>
                        <p class="x-hidden-focus">Indicadores para saber si es el momento adecuado para invertir en la materia de coherencia de recursos.</p>
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
                            <img src="../../_images/governance/process-enforce.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Procesos de adhesión a las directivas</h3>
                        <p class="x-hidden-focus">Procesos recomendados para admitir el cumplimiento de directiva en la materia de coherencia de recursos.</p>
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
                            <img src="../../_images/governance/process-maturity.png" class="x-hidden-focus"/>
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
                            <img src="../../_images/governance/process-toolchain.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText" style="padding-left:0px;">
                        <h3>Cadena de herramientas</h3>
                        <p class="x-hidden-focus">Servicios de Azure que se pueden implementar para admitir la materia de coherencia de recursos.</p>
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
