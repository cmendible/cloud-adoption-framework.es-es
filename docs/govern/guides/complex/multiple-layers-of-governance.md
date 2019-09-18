---
title: 'Guía de gobernanza para empresas complejas: Varias capas de gobernanza'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Guía de gobernanza para empresas complejas: Varias capas de gobernanza'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: a0a2674a91b963154d757eb35290b8aeead5c503
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032216"
---
# <a name="governance-guide-for-complex-enterprises-multiple-layers-of-governance"></a>Guía de gobernanza para empresas complejas: Varias capas de gobernanza

Si las grandes empresas requieren varios niveles de gobernanza, existen mayores niveles de complejidad que deben tenerse en cuenta en el producto viable mínimo de gobernanza y las posteriores mejoras de gobernanza.

Entre algunos ejemplos comunes de esas complejidades se incluyen:

- Funciones de gobernanza distribuido.
- Grupo de TI corporativo que asiste a organizaciones de TI de unidades de negocio.
- Grupo de TI corporativo que asiste a organizaciones de TI distribuidas geográficamente.

En este artículo se exploran algunas maneras de atravesar este tipo de complejidad.

## <a name="large-enterprise-governance-is-a-team-sport"></a>La gobernanza para grandes empresas es un deporte en equipo

A menudo, las grandes empresas establecidas tienen equipos o empleados que se centran en las materias mencionadas en esta guía. En esta guía se muestra un enfoque para hacer que la gobernanza sea un deporte en equipo.

En muchas grandes empresas, las cinco materias de gobernanza de la nube pueden ser obstáculos para la adopción. Generar experiencia de nube en identidad, seguridad, operaciones, implementaciones y configuración en toda una empresa lleva tiempo. La implementación holística de una directiva de gobernanza de TI y de la seguridad de TI puede ralentizar la innovación durante meses o incluso años. Equilibrar la necesidad empresarial de innovar y la necesidad de gobernanza para proteger los recursos existentes es un aspecto delicado.

Las funcionalidades intrínsecas de la nube pueden eliminar los bloqueadores de la innovación, pero aumentan los riesgos. En esta guía de gobernanza, hemos mostrado cómo la empresa de ejemplo crea barreras de seguridad para controlar los riesgos. En lugar de abordar cada una de las materias necesarias para proteger el entorno, el equipo de gobernanza de la nube pone en práctica un enfoque basado en riesgos para controlar lo que se podría implementar, mientras que los demás equipos generarían los niveles de madurez necesarios de la nube. Lo que es más importante, a medida que cada equipo alcanza el nivel de madurez de la nube, la gobernanza aplica sus soluciones de manera holística. A medida que cada equipo madura y se suma a la solución general, el equipo de gobernanza de la nube puede abrirse a nuevas etapas, lo que permite que prosperen nuevas innovaciones y adopciones.

Este modelo ilustra el crecimiento de una asociación entre el equipo de gobernanza de la nube y los equipos empresariales existentes (Seguridad, Gobernanza de TI, Redes, Identidad,etc.). La guía empieza por el producto viable mínimo de gobernanza y evoluciona hacia un estado final holístico a través de las evoluciones de gobernanza.

## <a name="requirements-to-supporting-such-a-team-sport"></a>Requisitos para admitir este tipo de deporte en equipo

El primer requisito de un modelo de gobernanza de varias capas es entender la jerarquía de gobernanza. Responder a las preguntas siguientes le ayudará a comprender la jerarquía general de gobernanza:

- ¿Cómo se asignan las cuentas de nube (la facturación de servicios en la nube) a las unidades de negocio?
- ¿Cómo se asignan las responsabilidades de gobernanza entre el grupo de TI corporativo y cada unidad de negocio?
- ¿Qué tipos de entorno administra cada una de estas unidades de TI?

## <a name="central-governance-of-a-distributed-governance-hierarchy"></a>Gobernanza central de una jerarquía de gobernanza distribuido

Las herramientas como los grupos de administración permiten al grupo de TI corporativo crear una estructura jerárquica que coincida con la jerarquía de gobernanza. Herramientas como Azure Blueprints pueden aplicar recursos a diferentes capas de esa jerarquía. Azure Blueprints puede tener varias versiones, y se pueden aplicar varias versiones a grupos de administración, suscripciones o grupos de recursos. Cada uno de estos conceptos se describe con más detalle en el MVP de gobernanza.

El aspecto importante de cada una de estas herramientas es la capacidad para aplicar varios planos técnicos a una jerarquía. Esto permite que la gobernanza sea un proceso en capas. El siguiente es un ejemplo de esta aplicación jerárquica de gobernanza:

- **Grupo de TI corporativo:** El grupo de TI corporativo crea un conjunto de estándares y directivas que se aplican a toda la adopción de la nube. Esto se materializa en un plano técnico de "base de referencia". El grupo de TI corporativo es propietario de la jerarquía de grupos de administración, lo que garantiza que una versión de la base de referencia se aplique a todas las suscripciones de la jerarquía.
- **Grupo de TI regional o unidad de negocio:** Varios equipos de TI pueden aplicar una capa adicional de gobernanza al crear su propio plano técnico. Esos planos técnicos crearían estándares y directivas adicionales. Una vez desarrollado, el grupo de TI corporativo podría aplicar esos planos técnicos a los nodos correspondientes dentro de la jerarquía de grupos de administración.
- **Equipos de adopción de la nube:** Cada equipo de adopción de la nube puede tomar decisiones detalladas sobre la implementación de aplicaciones o cargas de trabajo, en el contexto de los requisitos de gobernanza. A veces, el equipo también puede solicitar plantillas adicionales de coherencia de recursos de Azure para acelerar los esfuerzos de adopción.

Los detalles relativos a la implementación de gobernanza en cada nivel requerirán la coordinación entre cada equipo. El producto viable mínimo de gobernanza y las mejoras de gobernanza que se describen en esta guía pueden ayudar a alinear esta coordinación.

