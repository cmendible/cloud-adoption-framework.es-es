---
title: Migración a la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introducción al contenido de migración a la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 1bf9497684c1043d23eec48b1ab5d5f1f12ef752
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70838002"
---
# <a name="cloud-migration-in-the-microsoft-cloud-adoption-framework-for-azure"></a>Migración a la nube en Microsoft Cloud Adoption Framework para Azure

La migración a la nube es el proceso de mover los recursos digitales existentes a una plataforma en la nube. Con este enfoque, los recursos existentes se replican en la nube con modificaciones mínimas. Cuando una aplicación o carga de trabajo se vuelve operativa en la nube, los usuarios pasan de la solución existente a la solución en la nube. La migración a la nube es una forma de equilibrar de forma eficaz una cartera en la nube. Este es a menudo el enfoque más rápido y ágil a corto plazo. Por el contrario, es posible que algunas de las ventajas de la nube no se puedan conseguir en este enfoque sin una modificación adicional en el futuro. Las empresas y los clientes del mercado medio utilizan este enfoque para acelerar el ritmo del cambio, evitar los gastos de capital planeado y reducir los costos operativos en curso.

## <a name="cloud-migration-guidance"></a>Guía de migración a la nube

La guía de esta sección de Cloud Adoption Framework está diseñada para dos fines:

- Proporcione guías prácticas de migración que representen experiencias comunes que los clientes encuentran a menudo. Cada guía resume el proceso y las herramientas necesarias para que el esfuerzo de migración a la nube se realice correctamente. Por necesidad, la guía de diseño es específica de Azure. El resto de las recomendaciones de estas guías puede aplicarse como parte de un enfoque independiente de la nube o de un enfoque de nube múltiple.
- Ayude a los lectores a crear planes de migración personalizados que puedan satisfacer diversas necesidades empresariales, incluido la migración a varias nubes públicas, mediante una guía detallada sobre el desarrollo de procesos, roles y responsabilidades, y los controles de administración de cambios.

Este contenido está diseñado para el equipo de adopción de la nube. También es adecuado para los arquitectos de nube que necesitan desarrollar una base sólida en la migración a la nube.

## <a name="intended-audience"></a>Audiencia objetivo

Las instrucciones de Cloud Adoption Framework afectan al negocio, a la tecnología y a la cultura de las empresas. Esta sección afecta significativamente a los propietarios de aplicaciones, al personal de administración de cambios (como PMO y el personal de administración ágil) y a los directivos de las líneas de negocio, y al equipo de adopción de la nube. Existen varias dependencias entre estas personas que requerirán facilitación por parte de los arquitectos de la nube que usen esta guía. La facilitación con estos equipos puede ser un esfuerzo puntual, pero en algunos casos, dará como resultado interacciones recurrentes con estas otras personas.

El arquitecto de la nube sirve como líder de pensamiento y facilitador para reunir a estas audiencias. El contenido de esta colección de guías está diseñado para ayudar al arquitecto de nube a facilitar la conversación correcta, con la audiencia adecuada, para tomar las decisiones necesarias. La transformación del negocio potenciada por la nube depende del rol del arquitecto de la nube para ayudar a guiar las decisiones en todo el negocio y en TI.

**Especialización de arquitecto de nube en esta sección:** Cada una de las secciones de Cloud Adoption Framework representa una especialización o variante diferentes del rol de arquitecto de la nube. Esta sección está diseñada para arquitectos de la nube con conocimientos sobre el entorno local existente y cómo esto afecta a las opciones de migración.

**Separación de obligaciones:** En muchas empresas, la separación de obligaciones existe para limitar el acceso a los sistemas de producción o a determinados segmentos del entorno corporativo. En tal caso, el proceso de migración se vuelve más complejo. En algunos casos, esos roles y responsabilidades pueden requerir que varios arquitectos de la nube abarquen todo el proceso de migración.

**Opciones de asociación**. En cada uno de estos procesos, los equipos aprenderán nuevas habilidades y enfoques para la ejecución técnica. La expansión de las aptitudes técnicas entre los miembros del equipo existente es una opción durante la ejecución. La contratación de personal adicional es otra opción. A menudo, la asociación con terceros puede proporcionar una aceleración significativa y reducir los riesgos. Las [opciones de asociación](./migration-considerations/assess/partnership-options.md) pueden ayudarle a tomar decisiones para elegir la mejor opción de asociación.

## <a name="next-steps"></a>Pasos siguientes

Para aquellos lectores que deseen seguir esta guía de principio a fin, este contenido ayudará a desarrollar una sólida estrategia de migración a la nube. Estas instrucciones guían al lector mediante la teoría y la implementación de dicha estrategia.

Como primer paso, se recomienda que los lectores repasen la [guía sobre la migración a Azure](./azure-migration-guide/index.md) para conocer el conjunto de herramientas y los enfoques estándar necesarios para la migración en un caso de uso habitual. Posteriormente, las instrucciones básicas se pueden ampliar para ajustarse a las necesidades de los lectores con contenido adicional sobre [escenarios de migración complejos](./expanded-scope/index.md), [procedimientos recomendados de migración](./azure-best-practices/index.md) y [consideraciones sobre la migración](./migration-considerations/index.md).

> [!div class="nextstepaction"]
> [Guía de migración a Azure](./azure-migration-guide/index.md)
