---
title: Guías de decisiones sobre arquitectura
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información acerca de las guías de decisiones sobre arquitectura de Cloud Adoption Framework.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 1ddb65153cde9fac7426c8ef9b10f58a60918b82
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223879"
---
# <a name="architectural-decision-guides"></a>Guías de decisiones sobre arquitectura

Las guías de decisiones sobre arquitectura de Cloud Adoption Framework describen patrones y modelos que ayudan a crear la guía de diseño de la gobernanza de la nube. Cada una de estas guías se centra en un componente principal de la infraestructura de las implementaciones en la nube y enumera los patrones y modelos que pueden admitir escenarios concretos de implementación en la nube.

Al empezar a establecer la gobernanza de la nube en una organización, los procesos de gobernanza que requieren acciones ofrecen una hoja de ruta de la base de referencia. Sin embargo, estos recorridos realizan suposiciones acerca de los requisitos y prioridades que puede que no reflejen los de su organización.

Estas guías de decisiones complementan los recorridos de gobernanza de ejemplo, ya que proporcionan patrones y modelos alternativos que le ayudan a alinear las opciones de diseño de arquitectura realizadas en la guía de diseño de ejemplo con sus propios requisitos.

## <a name="decision-guidance-categories"></a>Categorías de guía en la toma de decisiones

Cada una de las categorías siguientes representa una tecnología fundamental de todas las implementaciones en la nube. Los procesos de gobernanza de ejemplo toman decisiones de diseño relacionadas con estas tecnologías según en las necesidades de los negocios del ejemplo y es posible que algunas de estas decisiones no coincida con las necesidades de su propia organización. En las secciones siguientes se describen opciones alternativas para cada una de estas categorías, lo que le permite elegir el patrón o modelo que mejor se adapte a sus necesidades.

[Suscripciones](./subscriptions/index.md): planee la estructura de cuentas y el diseño de la suscripción de la implementación en la nube para ajustarlos a la propiedad, facturación y funcionalidades de administración de su organización.

[Identidad](./identity/index.md): integre los servicios de identidad basados en la nube en los recursos de identidad existentes para poder usar la autorización y el control de acceso en su entorno de TI.

[Aplicación de directivas](./policy-enforcement/index.md): defina y aplique las reglas de la directiva de la organización para los recursos implementados en la nube y las cargas de trabajo que se alinean con los requisitos de gobernanza.

[Coherencia de recursos](./resource-consistency/index.md): asegúrese de que se alinean la implementación y la organización de los recursos basados en la nube para exigir los requisitos de directiva y administración de recursos.

[Etiquetado de recursos](./resource-tagging/index.md): organice los recursos basados en la nube para que admitan los modelos de facturación, los enfoques de contabilidad en la nube y la administración, y para la utilización de recursos y su costo. El etiquetado de recursos requiere un esquema de metadatos y de nomenclatura coherente y bien organizado.

[Red definida por software](./software-defined-network/index.md): implemente cargas de trabajo seguras en la nube mediante una implementación rápida y la modificación de las funcionalidades de redes virtuales. Las redes definidas por software (SDN) pueden admitir flujos de trabajo ágiles, aislar los recursos e integrar sistemas en la nube con la infraestructura de TI existente.

[Cifrado](./encryption/index.md): proteja la información confidencial para adecuarse a los requisitos de la directiva de seguridad y cumplimiento de su organización.

[Registro e informes](./logging-and-reporting/index.md): supervise los datos de registro generados por los recursos en la nube. El análisis de los datos, proporciona información relacionada con el estado de las operaciones, el mantenimiento y el estado de cumplimiento de las cargas de trabajo.

[Orientación sobre las regiones](./regions/index.md): Un análisis de los criterios de decisión adecuados para la colocación regional de los recursos dentro de la plataforma Azure.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo tanto las suscripciones como las sirven como base de una implementación en la nube.

> [!div class="nextstepaction"]
> [Diseño de suscripciones](./subscriptions/index.md)
