---
title: Requisitos previos para la migración a Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Requisitos previos para la migración a Azure
author: matticusau
ms.author: mlavery
ms.date: 04/04/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: de42ed98f4b7101b2de10240988e9964f57cd415
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818921"
---
::: zone target="chromeless"

# <a name="prerequisites"></a>Requisitos previos

::: zone-end

::: zone target="docs"

# <a name="prerequisites-for-migrating-to-azure"></a>Requisitos previos para la migración a Azure

::: zone-end

Los recursos que aparecen en esta sección lo ayudarán a preparar el entorno actual para la migración a Azure.

# <a name="overviewtaboverview"></a>[Información general](#tab/Overview)

Entre los motivos para migrar a Azure se incluyen la eliminación de los riesgos asociados con el hardware heredado, la reducción de los gastos de capital, la liberación de espacio en el centro de datos y una rentabilidad de la inversión (ROI) rápida.

- **Eliminar el hardware heredado**: puede que tenga aplicaciones hospedadas en una infraestructura que esté llegando a la finalización del ciclo de vida o del soporte técnico, ya sea en el entorno local o en un proveedor de hospedaje. La migración a la nube ofrece una solución atractiva al desafío, puesto que la capacidad de migrar "tal cual" permite que el equipo resuelva rápidamente el desafío del ciclo de vida de la infraestructura actual y, luego, centre su atención en la planificación a largo plazo del ciclo de vida de la aplicación y su optimización en la nube.
- **Abordar la finalización del soporte técnico**: puede tener aplicaciones que dependen de otro software o sistemas operativos que están llegando a la finalización del soporte técnico. Migrar a Azure puede proporcionar opciones de soporte técnico extendido para estas dependencias u otras opciones de migración que minimizan los requisitos de refactorización para dar soporte técnico a las aplicaciones de aquí en adelante. Por ejemplo, consulte las [opciones de soporte técnico extendido para Windows Server 2008 y SQL Server2008](https://azure.microsoft.com/blog/announcing-new-options-for-sql-server-2008-and-windows-server-2008-end-of-support).
- **Reducir los gastos de capital**: hospedar su propia infraestructura de servidor requiere una gran inversión en hardware, software, electricidad y personal. La migración a una solución en la nube puede proporcionar reducciones importantes en términos de gastos de capital. Para alcanzar la mejor reducción de los gastos de capital, es posible que sea necesario rediseñar la solución. Sin embargo, una migración "tal cual" es un excelente primer paso.
- **Liberar espacio en el centro de datos**: puede elegir Azure para expandir la capacidad del centro de datos. Una forma de hacerlo es usar la nube como una extensión de las funcionalidades locales.
- **Obtener una rentabilidad de la inversión rápida**: obtener una devolución de la inversión (ROI) es mucho más fácil con las soluciones en la nube, puesto que el modelo de pago en la nube proporciona una gran información sobre el uso y promueve una referencia cultural para obtener la rentabilidad de la inversión.

Cada uno de los escenarios anteriores puede ser un punto de entrada para ampliar la superficie de la nube mediante otra metodología (rehospedar, refactorizar, rediseñar, recompilar o reemplazar).

## <a name="migration-characteristics"></a>Características de la migración

En esta guía se da por supuesto que antes de esta migración, el patrimonio digital se compone principalmente de la infraestructura hospedada en el entorno local y puede incluir aplicaciones hospedadas críticas para la empresa. Después de realizar una migración correcta, el patrimonio de datos puede ser muy parecido al que tenía en el entorno local, pero con la infraestructura hospedada en los recursos en la nube. Como alternativa, el patrimonio de datos ideal es una variación del patrimonio de datos actual, ya que tiene aspectos de la infraestructura local con componentes que se han refactorizado para optimizar y aprovechar las ventajas de la plataforma de nube.

El objetivo de este recorrido de migración es lograr:

- La corrección del término de la vida útil de hardware heredado.
- La reducción de los gastos de capital.
- La rentabilidad de la inversión.

> [!NOTE]
> Una ventaja adicional de este recorrido de migración es el modelo de soporte técnico de software adicional para Windows 2008, Windows 2008 R2 y SQL Server 2008 y SQL Server 2008 R2. Para más información, consulte:
>
> - [Windows Server 2008 y Windows Server 2008 R2](https://www.microsoft.com/cloud-platform/windows-server-2008).
> - [SQL Server 2008 y SQL Server 2008 R2](https://www.microsoft.com/sql-server/sql-server-2008).

# <a name="understand-migration-approachestabapproach"></a>[Descripción de los enfoques de migración](#tab/Approach)

La estrategia y las herramientas que usa para migrar una aplicación en Azure dependerán considerablemente de sus motivaciones empresariales, los requisitos tecnológicos y las escalas de tiempo, así como de tener un profundo conocimiento de la carga de trabajo y los recursos reales (infraestructura, aplicaciones y datos) que se van a migrar.

Antes de determinar la estrategia de migración a la nube, analice las aplicaciones candidatas para identificar su compatibilidad con las tecnologías de hospedaje en la nube. Use la [Guía para la toma de decisiones de las herramientas de migración](../../decision-guides/migrate-decision-guide/index.md) de la Plataforma de adopción de la nube para que lo ayude a empezar a trabajar con este proceso.

Una migración centrada en IaaS, donde los servidores (junto con sus aplicaciones y datos asociados) se rehospedan en la nube mediante máquinas virtuales (VM), suele ser el enfoque más sencillo para trasladar cargas de trabajo a la nube. Sin embargo, tenga en cuenta que la configuración, la protección y el mantenimiento correctos de las máquinas virtuales pueden requerir más tiempo y conocimientos de TI en comparación con el uso de servicios de PaaS en Azure. Si está considerando la opción de Azure Virtual Machines, tenga en cuenta el esfuerzo constante de mantenimiento requerido para aplicar revisiones al entorno de la máquina virtual, así como para actualizarlo y administrarlo.

Al evaluar las cargas de trabajo para la migración, identifique las aplicaciones que no requieren una modificación sustancial para ejecutarse mediante tecnologías de PaaS, como Azure App Service u orquestadores como Azure Kubernetes Service. Estas aplicaciones deben ser las primeras candidatas para la modernización y optimización de la nube.

## <a name="learn-more"></a>Más información

- [Guía para la toma de decisiones de las herramientas de migración de la Plataforma de adopción de la nube](../../decision-guides/migrate-decision-guide/index.md).
- [Las 5 "R" de la racionalización](../../digital-estate/5-rs-of-rationalization.md).

# <a name="planning-checklisttabchecklist"></a>[Lista de comprobación de planeamiento](#tab/Checklist)

Antes de iniciar una migración, debe completar algunos requisitos previos. Los detalles exactos de estas actividades varían en función del entorno que se está migrando. Por lo general, se aplica la lista de comprobación siguiente:

> [!div class="checklist"]
>
> - **Identificar a las partes interesadas:** identifique a las personas clave que juegan un rol o que tienen interés en el resultado de la migración.
> - **Identificar los hitos clave:** para planear de manera eficaz las escalas de tiempo de migración, identifique los hitos clave que se deben cumplir.
> - **Identificar la estrategia de migración:** determine cuál de las 5 "R" de la racionalización va a utilizar.
> - **Evaluar la adecuación técnica:** valide la disponibilidad técnica y la idoneidad para la migración y determine qué nivel de asistencia puede necesitar de parte de asociados externos o del Soporte técnico de Azure.
> - **Planear la migración:** realice la evaluación y el planeamiento detallados que se necesitan para preparar los recursos (infraestructura, aplicaciones y datos), así como la infraestructura de Azure para la migración.
> - **Probar la migración:** valide el plan de migración realizando una migración de prueba de ámbito limitado.
> - **Migrar los servicios:** Realice la migración real.
> - **Después de la migración:** conozca lo que es necesario hacer después de migrar el entorno a Azure.

Supongamos que elige un enfoque de rehospedaje para la migración, en cuyo caso las actividades siguientes también serán importantes:

> [!div class="checklist"]
>
> - **Alineación de gobernanza:** ¿se logró algún consenso con respecto a la alineación de gobernanza con Migration Foundation?
> - **Red:** una estrategia de red debe estar seleccionada y alineada con los requisitos de seguridad de TI.
> - **Identidad:** una estrategia de identidad híbrida debe estar alineada para ajustarse al plan de adopción de la nube y la administración de identidades.

::: zone target="docs"

<!-- markdownlint-disable MD024 -->

## <a name="learn-more"></a>Más información

- [Las 5 "R" de la racionalización](../../digital-estate/5-rs-of-rationalization.md).
- [Guía para la toma de decisiones de las herramientas de migración](../../decision-guides/migrate-decision-guide/index.md).
- [Lista de comprobación del planeamiento de la Plataforma de adopción de la nube](../migration-considerations/prerequisites/planning-checklist.md).

::: zone-end
