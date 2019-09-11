---
title: Requisitos previos para la migración
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Requisitos previos para la migración
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 96ab62dc2adf17890989160c0af4fb80636b31b9
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818172"
---
# <a name="prerequisites-for-migration"></a>Requisitos previos para la migración

Antes de comenzar cualquier migración, se debe preparar el _entorno_ de destino de la migración para los cambios que se van a producir. En este caso, el entorno hace referencia a la base técnica en la nube. El entorno también significa el entorno empresarial y la mentalidad que promueven la migración. Del mismo modo, el entorno incluye la referencia cultural de los equipos que llevan a cabo los cambios y de los que se ven afectados por estos. La falta de preparación para estos cambios es el motivo más habitual para los errores en las migraciones. Esta serie de artículos le guiará a través de los requisitos previos recomendados para preparar el entorno.

## <a name="objective"></a>Objetivo

Garantice la preparación empresarial, cultural y técnica antes de comenzar un plan de migración iterativo.

## <a name="review-business-drivers"></a>Revisión de los impulsores de negocios

Antes de comenzar cualquier migración a la nube, revise las guías [Planeamiento](../../../business-strategy/index.md) y [Preparación](../../../ready/index.md) de Cloud Adoption Framework para asegurarse de que la organización está preparada para los procesos de adopción de la nube y de migración. En concreto, revise los requisitos empresariales y los resultados esperados que impulsan la migración:

- [Introducción: Migración](../../../getting-started/migrate.md)
- [¿Por qué queremos realizar el traslado a la nube?](../../../business-strategy/motivations-why-are-we-moving-to-the-cloud.md)

## <a name="definition-of-done"></a>Definición de *Listo*

Los requisitos previos están completos cuando se cumple lo siguiente:

- **Preparación empresarial.** El equipo de estrategia en la nube ha definido y clasificado por orden de prioridad un trabajo pendiente de migración de alto nivel que representa la parte del patrimonio digital que se va a migrar en las próximas dos o tres etapas. Los equipos de estrategia en la nube y de adopción de esta han acordado una estrategia inicial para administrar los cambios.
- **Preparación cultural.** Se han acordado las funciones, responsabilidades y expectativas del equipo de adopción de la nube, el equipo de estrategia en la nube y los usuarios afectados en relación con las cargas de trabajo que se van a migrar en las próximas dos o tres etapas.
- **Preparación técnica.** La zona de aterrizaje (o espacio asignado de hospedaje en la nube) que recibirá los recursos migrados cumple unos requisitos mínimos para hospedar la primera carga de trabajo migrada.

> [!CAUTION]
> La preparación es clave para el éxito de una migración. Sin embargo, demasiada preparación puede conducir a una *parálisis del análisis* en la que el exceso de tiempo invertido en la planeación puede retrasar seriamente un esfuerzo de migración. Los procesos y requisitos previos que se definen en esta sección están diseñados para ayudarle a tomar decisiones, pero no les permita que supongan un impedimento para lograr un progreso significativo.
>
> Elija una carga de trabajo relativamente sencilla para la migración inicial. Use los procesos descritos en esta sección cuando planee e implemente esta primera migración. Este primer esfuerzo de migración permitirá mostrar rápidamente los principios de la nube a su equipo y obligarlos a obtener información acerca del funcionamiento de la nube. A medida que el equipo gana en experiencia, integre los elementos aprendidos en migraciones de mayor calado y complejidad.

## <a name="accountability-during-prerequisites"></a>Responsabilidad durante la fase de los requisitos previos

Dos equipos son responsables de la preparación durante la fase de requisitos previos:

- **Equipo de estrategia en la nube:** Este equipo es responsable de identificar y clasificar por orden de prioridad la dos o tres primeras cargas de trabajo que actuarán como candidatas a la migración.
- **Equipo de adopción de la nube:** Este equipo es responsable de validar la preparación del entorno técnico y la viabilidad de migrar las cargas de trabajo propuestas.

Se debe identificar un único miembro de cada equipo como responsable de cada una de las tres definiciones de preparación que se indicaban en la sección anterior.

## <a name="responsibilities-during-prerequisites"></a>Responsabilidades durante la fase de los requisitos previos

Además de la responsabilidad de alto nivel, hay acciones de las que un individuo o grupo se deben hacer responsables directamente. Estas son algunas de las responsabilidades que afectan a estas actividades:

- **Prioridades empresariales.** Tome decisiones empresariales en relación a las cargas de trabajo que se desean migrar y a las restricciones temporales generales. Para más información, consulte [Cloud migration business motivations](../../../business-strategy/motivations-why-are-we-moving-to-the-cloud.md) (Motivaciones empresariales para la migración a la nube).
- **Preparación para la administración de cambios.** Establezca y comunique el plan para realizar el seguimiento de los cambios técnicos durante la migración. Habrá más información disponible sobre este tema en el tercer trimestre de 2019.
- **Alineación del usuario empresarial.** Establezca un plan de preparación de la comunidad de usuarios empresariales para la ejecución de la migración. Habrá más información disponible sobre este tema en el tercer trimestre de 2019.
- **Inventario y análisis del patrimonio digital.** Ejecución de las herramientas necesarias para catalogar y analizar el patrimonio digital. Consulte el análisis de Cloud Adoption Framework del [patrimonio digital](../../../digital-estate/index.md) para más información.
- **Preparación de la nube.** Evalúe el entorno de implementación de destino para asegurarse de que cumple con los requisitos de las primeras cargas de trabajo candidatas a la migración. Consulte la [Guía de preparación para Azure](../../../ready/azure-readiness-guide/index.md) para más información.

Los artículos restantes de esta serie ayudan con la ejecución de cada uno de los pasos.

## <a name="next-steps"></a>Pasos siguientes

Con un reconocimiento general de los requisitos previos, estará listo para adoptar las primeras [decisiones iniciales de la migración](./decisions.md) sobre los requisitos previos.

> [!div class="nextstepaction"]
> [Decisiones iniciales de la migración](./decisions.md)
