---
title: Guías de gobernanza en la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Más información sobre las guías prácticas de gobernanza que se proporcionan en Cloud Adoption Framework.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
layout: LandingPage
ms.openlocfilehash: 60c3f092f8b9b88b3fd9f4002683e55e1435fcf0
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70905677"
---
# <a name="cloud-governance-guides"></a>Guías de gobernanza en la nube

En las guías prácticas de gobernanza de esta sección se explica el enfoque incremental del modelo de gobernanza de Cloud Adoption Framework, basado en la [metodología de gobernanza](../methodology.md) descrita anteriormente. Puede establecer un enfoque ágil con respecto a la gobernanza en la nube que crecerá para satisfacer las necesidades de cualquier escenario de gobernanza en la nube.

## <a name="review-and-adopt-cloud-governance-best-practices"></a>Revisar y adoptar los procedimientos recomendados de gobernanza en la nube

Para comenzar el proceso de adopción de la nube, elija una de las siguientes guías de gobernanza. Cada guía describe un conjunto de procedimientos recomendados, basados en un conjunto de experiencias ficticias de clientes. Para los lectores que no están familiarizados con el enfoque incremental del modelo de gobernanza de Cloud Adoption Framework, se recomienda revisar la introducción de nivel superior a la teoría de la gobernanza que aparece a continuación, antes de adoptar cualquier procedimiento recomendado.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsZ">
<li style="display: flex; flex-direction: column;">
    <a href="./standard-enterprise/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
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
    <a href="./complex-enterprise/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
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

## <a name="an-incremental-approach-to-cloud-governance"></a>Enfoque incremental para la gobernanza de la nube

## <a name="choosing-a-governance-guide"></a>Elección de una guía de gobernanza

Las guías muestran cómo implementar un MVP de gobernanza. A partir de ahí, cada guía muestra cómo el equipo de gobernanza en la nube puede trabajar por delante de los equipos de adopción de la nube, como asociado, para acelerar los esfuerzos de adopción. El modelo de gobernanza de Cloud Adoption Framework guía la aplicación de la gobernanza desde la base mediante mejoras y evoluciones posteriores.

Para iniciar un recorrido de gobernanza, elija una de las dos opciones siguientes. Las opciones se basan en experiencias sintetizadas de los clientes. Los títulos se basan en la complejidad de la empresa para facilitar la navegación. Sin embargo, la decisión del lector puede ser más compleja. En las tablas siguientes se indican las diferencias entre las dos opciones.

> [!WARNING]
> Es posible que se requiera un punto de partida de gobernanza más sólido. En estos casos, considere la posibilidad de usar el enfoque de [Centro de datos virtual de Azure](#azure-virtual-datacenter) que se describe brevemente [a continuación](#azure-virtual-datacenter). Este enfoque se suele recomendar durante los esfuerzos de adopción de escala empresarial y, especialmente, los esfuerzos que superan los 10 000 activos. También es la elección de facto para los escenarios complejos de gobernanza cuando no se necesita ninguno de los elementos siguientes: requisitos de cumplimiento normativo de terceros ampliados, conocimiento profundo de los dominios o paridad con los requisitos de cumplimiento normativo y las directivas de gobernanza de TI madurados.

> [!NOTE]
> No es probable que alguna de las guías se adapte completamente a su situación. Elija la guía más adecuada y úsela como punto de partida. A lo largo de la guía, se proporciona información adicional que le ayudará a personalizar las decisiones para que cumplan criterios específicos.

### <a name="business-characteristics"></a>Características empresariales

| Característica | Organización estándar                                                                              | Empresa compleja                                                                                               |
|--------------------------------------------|---------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| Geografía (país o región geopolítica) | Los clientes y el personal residen en gran medida en una geografía.                                                      | Los clientes y el personal residen en varias regiones geográficas o requieren nubes soberanas.                                                             |
| Unidades de negocio afectadas                    | Unidades de negocio que comparten una infraestructura de TI común                                                                                    | Varias unidades de negocio que no comparten ninguna infraestructura de TI común                                                                                        |
| Presupuesto de TI                                  | Presupuesto de TI único.                                                                                        | Presupuesto asignado a varias unidades de negocio y en varias divisas                                                                         |
| Inversiones en TI                             | Las inversiones determinadas por los gastos de capital se planean anualmente y, por lo general, cubren solo el mantenimiento básico. | Las inversiones orientadas a los gastos de capital se planean anualmente y a menudo incluyen el mantenimiento y un ciclo de actualización de 3 a 5 años. |

### <a name="current-state-before-adopting-cloud-governance"></a>Estado actual antes de adoptar la gobernanza de la nube

| State | Empresa estándar                                                                               | Empresa compleja                                                                                                          |
|---------------------------------------------|----------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| Proveedores de hospedaje de terceros o centro de datos | Menos de cinco centros de datos                                                                                  | Más de cinco centros de datos                                                                                                   |
| Redes                                  | Sin WAN o 1 &ndash; 2 proveedores de WAN                                                                             | Red compleja o WAN global                                                                                             |
| Identidad                                    | Un único bosque, un único dominio. | Varios bosques complejos, varios dominios.  |

### <a name="desired-future-state-after-incremental-improvement-of-cloud-governance"></a>Estado futuro deseado después de la mejora incremental de la gobernanza de la nube

| State | Organización estándar                                                                        | Empresa compleja                                                                                        |
|----------------------------------------------|---------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| Administración de costos: cuentas de nube           | Modelo showback. La facturación se centraliza a través de TI.                                                | Modelo chargeback. La facturación se puede distribuir a través de la contratación de TI.                                  |
| Línea de base de seguridad: datos protegidos           | Datos financieros de la compañía e IP. Datos limitados del cliente. Sin requisitos de cumplimiento de terceros.     | Varias colecciones de datos financieros y personales de los clientes. Es posible que deba considerar el cumplimiento de terceros. |

## <a name="azure-virtual-datacenter"></a>Centro de datos virtual de Azure

El centro de datos virtual de Azure permite sacar el máximo partido a las funcionalidades de la plataforma de nube de Azure al tiempo que respeta los requisitos de seguridad y de gobernanza de una empresa.

En comparación con los entornos locales tradicionales, Azure permite a los equipos de desarrollo de cargas de trabajo y a sus patrocinadores empresariales disfrutar de una mayor agilidad de implementación que otras ofertas de plataforma de nube. No obstante, a medida que sus esfuerzos de adopción de nube se amplían para incluir cargas de trabajo y datos críticos, esta agilidad puede entrar en conflicto con los requisitos de cumplimiento de directivas y seguridad corporativos que han establecido sus equipos de TI. Esto es especialmente cierto en el caso de grandes empresas que tienen requisitos normativos y de gobernanza complejos.

El enfoque del centro de datos virtual de Azure pretende abordar estas preocupaciones en una fase temprana del ciclo de vida de adopción mediante el suministro de modelos, arquitecturas de referencia, artefactos de automatización de ejemplo y orientación para ayudar a lograr el equilibrio entre los requisitos de gobernanza de los desarrolladores y los equipos de TI durante los esfuerzos de adopción de la nube empresarial. La esencia de este enfoque es el concepto de centro de datos virtual en sí: la implementación de límites de aislamiento en su infraestructura en la nube mediante la aplicación de controles de acceso y seguridad, directivas de red y supervisión del cumplimiento.

Un centro de datos virtual puede considerarse su propia nube aislada en la plataforma Azure, que integra los procesos de administración, los requisitos normativos y los procesos de seguridad que exigen sus directivas de gobernanza. Dentro de este límite virtual, el centro de datos virtual de Azure ofrece modelos de ejemplo para implementar cargas de trabajo y garantizar un cumplimiento constante, además de proporcionar instrucciones básicas sobre cómo implementar la separación de roles y responsabilidades de la organización en la nube.

### <a name="azure-virtual-datacenter-assumptions"></a>Supuestos sobre el centro de datos virtual de Azure

Aunque los equipos más pequeños pueden beneficiarse de los modelos y las recomendaciones que proporciona el centro de datos virtual de Azure, este enfoque está diseñado para guiar a los grupos de TI empresariales en la administración de grandes entornos de nube. Para aquellas organizaciones que cumplen los criterios siguientes, se recomienda considerar la posibilidad de consultar las instrucciones del centro de datos virtual de Azure al diseñar la infraestructura de nube basada en Azure:

- Su empresa está sujeta a los requisitos de cumplimiento normativo, que exigen funcionalidades de supervisión y auditoría centralizadas.
- Debe mantener el cumplimiento de las directivas comunes y de la gobernanza, y el control de TI central de los servicios principales.
- Su sector depende de una plataforma compleja que requiere controles complejos y un conocimiento profundo del dominio para controlar la plataforma. Esto es lo más habitual en grandes empresas del sector financiero, petrolífero y gasístico, o de fabricación.
- Las directivas de gobernanza de TI existentes requieren una paridad más ajustada con las características existentes, incluso durante la adopción en fases tempranas.

Para más información, visite la sección [Centro de datos virtual de Azure](/azure/architecture/vdc) de Cloud Adoption Framework.

## <a name="next-steps"></a>Pasos siguientes

Elija una de estas guías:

> [!div class="nextstepaction"]
> [Guía de gobernanza estándar](./standard-enterprise/index.md)
>
> [Guía de gobernanza para empresas complejas](./complex-enterprise/index.md)
