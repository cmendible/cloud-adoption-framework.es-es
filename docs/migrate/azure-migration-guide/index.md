---
title: Introducción a la guía de migración a Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Aprenda cómo migrar eficazmente los servicios de la organización a Azure con una guía paso a paso.
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: 9b77b8fbbe6479b716d9b9f91d6e0154db8c0db7
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022793"
---
::: zone target="chromeless"

# <a name="before-you-start"></a>Antes de comenzar

::: zone-end

::: zone target="docs"

# <a name="introduction-to-the-azure-migration-guide"></a>Introducción a la guía de migración a Azure

::: zone-end

Antes de migrar recursos a Azure, debe elegir el método de migración y las funciones que utilizará para gobernar y proteger su entorno. Esta guía le guía por este proceso de decisión.

::: zone target="docs"

> [!TIP]
> Para una experiencia interactiva, consulte esta guía en Azure Portal. Vaya al [Centro de inicio rápido de Azure](https://portal.azure.com/?feature.quickstart=true#blade/Microsoft_Azure_Resources/QuickstartCenterBlade) en Azure Portal y seleccione **Migrate your environment to Azure** (Migrar su entorno a Azure).

::: zone-end

# <a name="overviewtaboverview"></a>[Información general](#tab/Overview)

En esta guía se describen los conceptos básicos de la migración de aplicaciones y recursos desde el entorno local a Azure. Está diseñado para ámbitos de migración con una complejidad mínima. Para determinar la idoneidad de esta guía para la migración, consulte la pestaña **Cuándo utilizar esta guía**.

Cuando migra a Azure, puede migrar sus aplicaciones tal y como están mediante soluciones de máquinas virtuales basadas en IaaS (conocidas como migración de "rehospedaje" o "lift and shift"), o puede tener la flexibilidad de utilizar servicios administrados y otras características de la nube para modernizar las aplicaciones. Consulte la pestaña **Opciones de migración** para más información sobre estas opciones. A medida que desarrolle su estrategia de migración, podría considerar lo siguiente:

- ¿Funcionarán mis aplicaciones de migración en la nube?
- ¿Cuál es la mejor estrategia (en cuanto a tecnología, herramientas y migraciones) para mi aplicación? Para más información, consulte la guía [Migration Tool Decision Guide](../../decision-guides/migrate-decision-guide/index.md) (Guía de toma de decisiones sobre herramientas de migración) de Microsoft Cloud Adoption Framework.
- ¿Cómo puedo minimizar el tiempo de inactividad durante la migración?
- ¿Cómo puedo controlar los costos?
- ¿Cómo puedo realizar un seguimiento de los costos de los recursos y facturarlos de forma precisa?
- ¿Cómo puedo asegurarme de que seguimos cumpliendo con las regulaciones?
- ¿Cómo puedo cumplir los requisitos legales de soberanía de datos en determinados países?

Esta guía le ayuda a responder a estas preguntas. Sugiere las tareas y características que hay que tener en cuenta mientras se prepara para implementar recursos en Azure, incluyendo:

> [!div class="checklist"]
>
> - **Configuración de los requisitos previos.** Planee y prepárese para la migración.
> - **Evaluación de la adecuación técnica.** Valide la preparación técnica y la idoneidad para la migración.
> - **Administración de costos y facturación.** Examine los costos de los recursos.
> - **Migración de los servicios.** Realice la migración real.
> - **Organización de los recursos.** Bloquee los recursos críticos para el sistema y etiquete los recursos para realizar un seguimiento de los mismos.
> - **Optimización y transformación.** Aproveche la oportunidad posterior a la migración para revisar los recursos.
> - **Protección y administración.** Asegúrese de que el entorno sea seguro y esté bien supervisado.
> - **Obtención de ayuda.** Obtenga ayuda y soporte técnico durante las actividades de migración o posteriores a ella.

::: zone target="docs"

Para más información sobre la organización y estructuración de las suscripciones, la administración de los recursos implementados y el cumplimiento de los requisitos de la directiva corporativa, consulte [Administración de Azure: gobernanza](https://docs.microsoft.com/azure/security/governance-in-azure).

::: zone-end

# <a name="when-to-use-this-guidetabwhentousethisguide"></a>[Cuándo utilizar esta guía](#tab/WhenToUseThisGuide)

Si bien las herramientas analizadas en esta guía son compatibles con una amplia variedad de escenarios de migración, esta guía se centrará en esfuerzos de ámbito limitado con _complejidad mínima_. Para determinar si esta guía de migración es adecuada para el proyecto, considere si las siguientes condiciones se pueden aplicar a su caso:

- Está migrando a un entorno homogéneo.
- Solo unas pocas unidades de negocio necesitan alinearse para completar la migración.
- No tiene previsto automatizar la migración completa.
- Está migrando un pequeño número de servidores.
- La asignación de dependencias de los componentes que se van a migrar es fácil de definir.
- Su sector tiene requisitos normativos mínimos relevantes para esta migración.

Si alguna de estas condiciones _no_ se aplican a su situación, debería considerar la [guía del ámbito ampliado](../expanded-scope/index.md). También le recomendamos que solicite la asistencia de uno de nuestros equipos o asociados de Microsoft para realizar migraciones que requieran la guía del ámbito ampliado. Los clientes que se relacionan con Microsoft o con asociados certificados tienen más éxito en estos escenarios. Para más información sobre cómo solicitar asistencia, consulte esta guía.

<!-- markdownlint-enable MD033 -->

::: zone target="docs"

Para más información, consulte:

- [Guía del ámbito ampliado](../expanded-scope/index.md)

::: zone-end

# <a name="migration-optionstabmigrationoptions"></a>[Opciones de migración](#tab/MigrationOptions)

Puede realizar una migración a la nube de varias maneras. Algunas se adaptan mejor a diferentes escenarios que otras. Al determinar cómo migrar su entorno, tenga en cuenta las siguientes opciones a la hora de decidir sobre una estrategia de migración:

- **Rehospedaje:** También conocido como "lift and shift", un esfuerzo de rehospedaje mueve el estado actual a Azure, con un cambio mínimo en la arquitectura general.
- **Refactorización:** Las opciones de plataforma como servicio (PaaS) pueden reducir los costos operativos asociados a muchas aplicaciones. Puede ser prudente refactorizar ligeramente una aplicación para ajustarla a un modelo de PaaS. Esto también hace referencia al proceso de desarrollo de aplicaciones de refactorización del código para permitir que una aplicación satisfaga nuevas oportunidades de negocio.
- **Rediseño:** Algunas aplicaciones antiguas no son compatibles con los proveedores de nube debido a las decisiones de arquitectura que se tomaron cuando se creó la aplicación. En estos casos, puede ser necesario rediseñar la aplicación antes de la transformación.
- **Recompilación:** En algunos escenarios, los cambios necesarios para migrar una aplicación pueden ser demasiado grandes para justificar una mayor inversión, y la solución debe recompilarse.
- **Reemplazo:** Las soluciones se implementan normalmente con la mejor tecnología y técnicas disponibles en ese momento. En algunos casos, las aplicaciones modernas de software como servicio (SaaS) pueden satisfacer toda la funcionalidad proporcionada por la aplicación hospedada. En estos escenarios, se podría programar una carga de trabajo para su sustitución en el futuro, con lo que se dejaría de considerar como parte de la migración.

::: zone target="chromeless"

Estos métodos no se excluyen mutuamente &mdash;por ejemplo, aunque la migración inicial podría utilizar un modelo de **rehospedaje**, puede optar por implementar el **rehospedaje** o el **rediseño** como parte de la fase de optimización posterior a la migración. Esto se revisa en la sección **Optimización y transformación** de esta guía.

::: zone-end

::: zone target="docs"

Estos métodos no se excluyen mutuamente &mdash;por ejemplo, aunque la migración inicial podría utilizar un modelo de **rehospedaje**, puede optar por implementar el **rehospedaje** o el **rediseño** como parte de la fase de optimización posterior a la migración. Esto se revisa en la sección [Optimización y transformación](./optimize-and-transform.md) de esta guía.

::: zone-end

![Infografía de las opciones de migración](../../_images/migrate/migration-options.png)
