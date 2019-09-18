---
title: Las cinco disciplinas de la gobernanza de la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información sobre las cinco materias de gobernanza de la nube del Marco de adopción de la nube.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: e162dd4aad284d7de430a2483ccda04b99e21dd3
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032352"
---
# <a name="the-five-disciplines-of-cloud-governance"></a>Las cinco disciplinas de la gobernanza de la nube

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsI">
    <li style="display: flex; flex-direction: column;">
        <div class="cardSize">
            <div class="cardPadding" style="padding-bottom:10px;">
                <div class="card" style="padding-bottom:10px;">
                    <div class="cardText" style="padding-left:0px;">
Cualquier cambio en los procesos de negocio o en las plataformas tecnológicas presenta riesgos. Los equipos de gobernanza de la nube, cuyos miembros se conocen a veces como custodios de la nube, tienen la tarea de mitigar estos riesgos y de garantizar una interrupción mínima en los esfuerzos de adopción o innovación.<br/><br/>El modelo de gobernanza del Marco de adopción de la nube guía estas decisiones (independientemente de la plataforma de nube elegida) al centrarse en el <a href="./corporate-policy.md">desarrollo de directivas corporativas</a> y en las <a href="#disciplines-of-cloud-governance">cinco materias de gobernanza de la nube</a>. Las <a href="./guides/index.md">guías de diseño accionables</a> demuestran este modelo utilizando los servicios de Azure. Obtenga información sobre las materias del modelo de gobernanza del Marco de adopción de la nube a continuación.
                    </div>
                </div>
            </div>
        </div>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="../_images/operational-transformation-govern-highres.png" style="display: flex; flex-direction: column; flex: 1 0 auto;">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardText" style="padding-left:0px;">
    <img src="../_images/operational-transformation-govern-highres.png" alt="Diagram of the Cloud Adoption Framework governance model: Corporate policy and governance disciplines">
    <br>
    <i>Figura 1: diagrama de directivas corporativas y las cinco materias de gobernanza de la nube.</i>
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>

<!-- markdownlint-enable MD033 -->

## <a name="disciplines-of-cloud-governance"></a>Materias de gobernanza de la nube

Con cualquier plataforma en la nube, existen materias de gobernanza comunes que ayudan a informar las directivas y a alinear cadenas de herramientas. Estas materias guían las decisiones relativas al nivel adecuado de automatización y aplicación de las directivas corporativas en las plataformas en la nube.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsA">
<li style="display: flex; flex-direction: column;">
    <a href="./cost-management/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/cost-management.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Administración de costos</h3>
                        <p>El costo es una de las principales preocupaciones de los usuarios de la nube. Desarrolle directivas de control de los costos para todas las plataformas de nube.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./security-baseline/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/security-baseline.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Línea de base de seguridad</h3>
                        <p>La seguridad es un tema complejo, único para cada empresa. Una vez establecidos los requisitos de seguridad, las directivas de cumplimiento y gobernanza de la nube aplican esos requisitos en las configuraciones de red, datos y recursos.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./identity-baseline/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/identity-baseline.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Línea de base de identidad</h3>
                        <p>Las incoherencias en la aplicación de los requisitos de identidad pueden aumentar el riesgo de infracciones. La materia de línea de base de identidad se centra en garantizar que la identidad se aplique de manera coherente en los esfuerzos de adopción de la nube.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./resource-consistency/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/resource-consistency.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Coherencia de recursos</h3>
                        <p>Las operaciones en la nube dependen de una configuración de los recursos coherente. Con las herramientas de gobernanza, los recursos se pueden configurar de forma coherente a fin de administrar los riesgos relativos a la incorporación, el desfase, la capacidad de detección y la recuperación.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./deployment-acceleration/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../_images/govern/deployment-acceleration.png" class="x-hidden-focus"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Aceleración de la implementación</h3>
                        <p>La centralización, la normalización y la coherencia en los enfoques de implementación y configuración mejoran los procedimientos de gobernanza. Si se proporcionan mediante herramientas de gobernanza basadas en la nube, crean un factor de nube que puede acelerar las actividades de implementación.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->
