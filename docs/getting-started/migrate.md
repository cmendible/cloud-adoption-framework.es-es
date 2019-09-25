---
title: Introducción al recorrido de migración a la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introducción al recorrido de migración a la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.openlocfilehash: ab637312535f1497b8f506cb9636025460a7905b
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223061"
---
# <a name="getting-started-with-a-cloud-migration-journey"></a>Introducción al recorrido de migración a la nube

Aprenda a usar Microsoft Cloud Adoption Framework para Azure y comience el recorrido de migración a la nube. Este marco proporciona una guía completa para la transición de las cargas de trabajo de aplicaciones heredadas mediante innovadoras tecnologías basadas en la nube.

## <a name="executive-summary"></a>Resumen ejecutivo

Cloud Adoption Framework ayuda a los clientes a simplificar su recorrido hacia la adopción de la nube. Este marco contiene información detallada que incluye un recorrido de adopción de la nube de un extremo a otro, que comienza con resultados empresariales fijados y la alineación de la preparación para la nube y las evaluaciones con objetivos empresariales claramente definidos. Esos resultados se logran mediante una ruta definida para la adopción de la nube. Con la adopción basada en la migración, la ruta definida se centra en gran medida en realizar una migración de las cargas de trabajo locales a la nube. En ocasiones, este recorrido incluye la modernización de las cargas de trabajo para aumentar la rentabilidad de la inversión del trabajo de migración.

Este marco está diseñado principalmente para los arquitectos de la nube y los equipos de estrategia de la nube que lideran los trabajos de adopción. Sin embargo, muchos temas de este marco son de interés para otros roles de la empresa y de TI. Los arquitectos de la nube suelen servir como facilitadores de la interacción con cada uno de los roles pertinentes. Este resumen Ejecutivo está diseñado para preparar a los distintos roles antes de facilitar las conversaciones.

> [!NOTE]
> Esta guía es actualmente una versión preliminar pública. Durante esta fase, la terminología, los enfoques y las instrucciones se están probando minuciosamente con clientes, asociados y equipos de Microsoft. Por tanto, el índice y las instrucciones pueden cambiar ligeramente con el tiempo.

## <a name="motivations"></a>Motivaciones

Las migraciones a la nube pueden ayudar a las empresas a lograr sus resultados empresariales deseados. La comunicación clara de las motivaciones, los factores empresariales y las medidas del éxito son bases importantes para tomar decisiones acertadas a lo largo de los trabajos de migración a la nube. En la tabla siguiente se clasifican las motivaciones para facilitar esta conversación. Se supone que la mayoría de las empresas tendrán motivaciones en cada clasificación. La finalidad de esta tabla no es limitar los resultados, sino más bien facilitar la clasificación en orden de prioridad de los objetivos y las motivaciones generales:

<!-- markdownlint-disable MD033 -->

|Eventos empresariales críticos | Motivaciones de migración | Motivaciones de innovación |
|---------|---------|---------|
| Salida del centro de datos<br/><br/>Fusiones, adquisiciones o desinversiones<br/><br/>Reducciones en gastos de capital<br/><br/>Finalización del soporte técnico de tecnologías críticas<br/><br/>Respuesta a los cambios de cumplimiento normativo<br/><br/>Satisfacer los requisitos de soberanía de los datos<br/><br/>Reducir las interrupciones y mejorar la estabilidad de TI|Ahorros en costos<br/><br/>Reducción de la complejidad técnica o de proveedores<br/><br/>Optimización de las operaciones internas<br/><br/>Aumento de la agilidad comercial<br/><br/>Prepararse de cara a las nuevas funcionalidades técnicas<br/><br/>Escalar para satisfacer las demandas del mercado<br/><br/>Escalar para satisfacer las demandas geográficas|Prepararse de cara a las nuevas funcionalidades técnicas<br/><br/>Crear funcionalidades técnicas<br/><br/>Escalar para satisfacer las demandas del mercado<br/><br/>Escalar para satisfacer las demandas geográficas<br/><br/>Mejorar las experiencias e interacciones de los clientes<br/><br/>Transformar productos o servicios<br/><br/>Sorprender al mercado con nuevos productos o servicios|

<!-- markdownlint-enable MD033 -->

Cuando la prioridad más alta es dar respuesta a eventos empresariales críticos, es importante llevar a cabo la [implementación en la nube](#cloud-implementation) pronto, a menudo en paralelo con los trabajos de estrategia y planeamiento. La adopción de este enfoque requiere una mentalidad de crecimiento y una disposición para mejorar los procesos de forma iterativa, en función de las lecciones directas aprendidas.

Cuando las motivaciones de migración son una prioridad, la [estrategia y el planeamiento](#cloud-strategy-and-planning) desempeñarán un papel fundamental en los inicios del proceso. Sin embargo, es muy recomendable que la [implementación](#cloud-implementation) de la primera carga de trabajo se lleve a cabo en paralelo con el planeamiento, a fin de ayudar al equipo a comprender y planear las curvas de aprendizaje asociadas a la nube.

Cuando las motivaciones de innovación son la máxima prioridad, la estrategia y el planeamiento necesitarán inversiones adicionales al principio del proceso para garantizar el equilibrio en la cartera y la alineación acertada de la inversión realizada durante la nube. Para más información sobre cómo comprender las motivaciones de innovación, consulte [El recorrido hacia la innovación](./innovate.md).

Preparar a todos los que van a participar en el trabajo de migración de forma que comprendan las motivaciones garantizará la toma de decisiones acertadas. La siguiente metodología de migración describe el modo en que Microsoft sugiere a los clientes que guíen esas decisiones en una metodología coherente.

## <a name="migration-approach"></a>Enfoque de migración

Cloud Adoption Framework establece una construcción general de planeamiento, preparación y adopción para agrupar los tipos de trabajos necesarios en cualquier adopción de la nube. Este resumen ejecutivo se basa en ese flujo general para establecer procesos iterativos que puedan consolidar los trabajos de lift-and-shift y optimización, **así como** las labores de modernización, en un único enfoque para todas las actividades de migración a la nube.

Este enfoque se compone de dos metodologías o áreas de enfoque: estrategia y planeamiento de la nube e implementación en la nube. La [motivación](#motivations) o el resultado empresarial deseado para una migración a la nube a menudo determina cuánto debe invertir un equipo en [estrategia y planeamiento](#cloud-strategy-and-planning) y cuánto en [implementación](#cloud-implementation). Estas motivaciones también pueden influir en las decisiones para ejecutar cada fase secuencialmente o en paralelo.

## <a name="cloud-implementation"></a>Implementación en la nube

La implementación en la nube es un proceso iterativo para migrar y modernizar la información digital en consonancia con los resultados empresariales fijados y los controles de administración de cambios. Durante cada iteración, las cargas de trabajo se migran o modernizan en consonancia con la estrategia y el plan. Las decisiones relacionadas con las aplicaciones IaaS, PaaS o híbridas se realizan durante la fase de evaluación para optimizar el control y la ejecución. Estas decisiones determinarán las herramientas usadas durante la fase de migración. Este modelo se puede usar con unas dosis mínimas de estrategia y planeamiento. Sin embargo, para garantizar la máxima rentabilidad empresarial, es muy recomendable que tanto el departamento de TI como la empresa se vinculen a una estrategia y un plan claros que guíen las actividades de implementación.

![Metodología de implementación en la nube de Cloud Adoption Framework](../_images/operational-transformation-migrate.png)

El objetivo de este trabajo es la migración o la modernización de las cargas de trabajo. Una carga de trabajo es una colección de infraestructura, aplicaciones y datos que respaldan colectivamente un objetivo empresarial común o la ejecución de un proceso de negocio común. Algunos ejemplos de cargas de trabajo podrían incluir cosas como una aplicación de línea de negocio, una solución de nómina de RR. HH. una solución CRM, un flujo de trabajo de aprobación de documentos financieros o una solución de inteligencia empresarial. Las cargas de trabajo también pueden incluir recursos técnicos compartidos, como un almacenamiento de datos que admite otras diversas soluciones. En algunos casos, una carga de trabajo se puede representar mediante un único recurso, como un servidor, una aplicación o una plataforma de datos independientes.

Las migraciones a la nube a menudo se consideran un solo proyecto dentro de un programa más amplio para simplificar las operaciones, los costos o la complejidad de TI. La metodología de implementación en la nube ayuda a alinear los trabajos técnicos de una serie de migraciones de cargas de trabajo con valores empresariales más generales descritos en la estrategia y el planeamiento para la nube.

**Introducción:** para empezar a trabajar con una implementación en la nube, en la [guía de migración de Azure](../migrate/azure-migration-guide/index.md) y en la [guía de preparación de Azure](../ready/azure-readiness-guide/index.md) se describen las herramientas y los procesos generales necesarios para realizar correctamente una implementación en la nube. La migración de la primera carga de trabajo mediante esas guías ayudará al equipo a superar las curvas de aprendizaje iniciales en el proceso de planeamiento. Posteriormente, es necesario tener en cuenta además la [lista de comprobación de ámbito expandida](../migrate/expanded-scope/index.md), los [procedimientos recomendados de migración](../migrate/azure-best-practices/index.md) y las [consideraciones sobre la migración](../migrate/migration-considerations/index.md), a fin de alinear las orientaciones básicas con las restricciones, los procesos, las estructuras de equipo y los objetivos particulares de su trabajo.

## <a name="cloud-strategy-and-planning"></a>Estrategia y planeamiento de la nube

La estrategia y el planeamiento de la nube es una metodología que se centra en alinear los resultados, las prioridades y las restricciones empresariales a fin de establecer unos pasos claros de estrategia y planeamiento. El plan resultante (o trabajo pendiente de migración) describe el enfoque sobre la migración y la modernización en toda la cartera de TI, que puede abarcar centros de datos completos, varias cargas de trabajo o colecciones variadas de infraestructura, aplicaciones y datos. La administración adecuada de la cartera de TI mediante los trabajos de implementación en la nube le ayudará a determinar los resultados de negocio deseados.

![Introducción a Cloud Adoption Framework](../_images/caf-overview.png)

**Introducción:** en el resto de este artículo se prepara al lector para la correcta aplicación de la metodología de estrategia y planeamiento de Cloud Adoption Framework. También se describen recursos y vínculos adicionales que pueden ayudar al lector a adoptar este enfoque para guiar los trabajos de implementación en la nube.

### <a name="methodology-explained"></a>Metodología explicada

La metodología de estrategia y planeamiento de la nube de Cloud Adoption Framework se basa en un enfoque incremental sobre la implementación en la nube que se alinea con estrategias tecnológicas ágiles, la madurez cultural basada en enfoques de mentalidad del crecimiento y estrategias impulsadas por los resultados empresariales. Esta metodología consta de los siguientes componentes generales que guían la implementación de cada estrategia.

Como se ilustra en la imagen de arriba, este marco alinea las decisiones estratégicas con un pequeño número de procesos contenidos, que operan dentro de un modelo iterativo. Aunque se describen en un documento lineal, se espera que cada uno de los siguientes procesos se desarrolle en paralelo con las iteraciones de la implementación en la nube. Los vínculos de cada proceso ayudarán a definir el estado final deseado y los medios para llegar a él:

- **[Planeamiento](../strategy/index.md):** cuando la implementación técnica está vinculada con objetivos empresariales claros, es mucho más fácil medir y alinear el éxito de varios trabajos de implementación en la nube, con independencia de las decisiones técnicas.
- **[Listo](../ready/index.md):** preparar la empresa, la cultura, la gente y el entorno para los cambios venideros conduce al éxito de cada trabajo y acelera los proyectos de implementación y cambio.
- **Adopción:** garantizar la correcta implementación de los cambios deseados, en los procesos empresariales y de TI, para lograr los resultados empresariales.
  - **[Migración](../migrate/index.md):** ejecución iterativa de la [metodología de implementación en la nube](#cloud-implementation) que se adhiere al proceso probado de evaluar, migrar, optimizar, proteger y administrar a fin de crear un proceso repetible para la migración de las cargas de trabajo.
- **[Operaciones](../operate/index.md):** defina un modelo operativo administrable para guiar las actividades durante y después de la adopción.
  - **[Organizar](../organize/index.md):** alinear a personas y equipos para que las operaciones y la adopción de la nube se lleven a cabo de manera adecuada.
  - **[Control](../govern/index.md):** alinear las directivas corporativas con los riesgos tangibles, que se pueden mitigar mediante directivas, procesos y herramientas de gobernanza basadas en la nube.
  - **[Administrar](../manage/index.md):** expandir las operaciones de TI para garantizar que las soluciones basadas en la nube pueden funcionar mediante procesos seguros y rentables por medio de modernas herramientas de operaciones que tienen como prioridad la nube.

A lo largo de esta experiencia de migración, este marco se usará para abordar la ambigüedad, administrar el cambio y guiar a los equipos multifuncionales hasta la consecución de los resultados empresariales.

### <a name="common-cultural-changes-resulting-from-adherence-to-this-methodology"></a>Cambios culturales comunes derivados de la adhesión a esta metodología

El trabajo para alcanzar los resultados empresariales deseados puede desencadenar pequeños cambios en la cultura de TI y, hasta cierto punto, en la cultura de la empresa. A continuación se muestran algunos cambios culturales comunes que se han detectado en este proceso:

- Es probable que el equipo de TI adopte nuevas aptitudes para admitir las cargas de trabajo en la nube.
- La ejecución de una migración a la nube promueve enfoques iterativos o ágiles.
- La inclusión de la gobernanza de la nube también tiende a inspirar enfoques de DevOps.
- La creación de un equipo de estrategia de la nube puede conducir a una mayor integración entre los responsables empresariales y de TI.
- En conjunto, estos cambios suelen llevar a la agilidad de la empresa y de TI.

El cambio cultural no es un objetivo de la migración a la nube o de Cloud Adoption Framework, pero es un resultado que se experimenta normalmente.
No hay una guía que dicte los cambios culturales, sino que los cambios sutiles en la cultural se van insertando en las mejoras de procesos y los enfoques sugeridos a lo largo del camino.

### <a name="common-technical-efforts-associated-with-this-methodology"></a>Trabajos técnicos comunes asociados a esta metodología

Durante la implementación de la estrategia y el planeamiento de la nube, el equipo de TI centrará un gran porcentaje de su tiempo en la migración de los activos digitales existentes a la nube. Durante este proceso, se esperan cambios mínimos en el código, pero a menudo pueden estar limitados a cambios de configuración. En muchos casos, puede haber una sólida justificación empresarial para la modernización como parte de la migración a la nube.

### <a name="common-workload-examples"></a>Ejemplos comunes de cargas de trabajo

La estrategia y el planeamiento de la nube están con frecuencia dirigidos a una amplia colección de cargas de trabajo y aplicaciones. Dentro de la cartera, normalmente se migran aplicaciones o tipos de carga de trabajo comunes. Estos son algunos ejemplos:

- Aplicaciones de línea de negocio
- Aplicaciones orientadas al cliente
- Aplicaciones de terceros
- Plataformas de análisis de datos
- Soluciones distribuidas globalmente
- Soluciones de gran escalabilidad

### <a name="common-technologies-migrated"></a>Tecnologías comunes migradas

Las tecnologías migradas a la nube se expanden constantemente a medida que los proveedores de nube agregan nuevas funcionalidades. A continuación se muestran algunos ejemplos de las tecnologías que se suelen ver en un trabajo de migración:

- Windows y SQL Server
- Bases de datos Linux y de código abierto (OSS)
- Bases de datos no estructuradas/NoSQL
- SAP en Azure
- Analytics (Data Warehouse, Data Lake)

## <a name="next-steps-lifecycle-solution"></a>Pasos siguientes: Solución de ciclo de vida

Cloud Adoption Framework es una solución de ciclo de vida. Está diseñada para ayudar a los lectores que acaban de empezar su recorrido, pero también a aquellos que quieren profundizar en su migración. Como tal, el contenido es muy específico del contexto y del público. Los pasos siguientes se alinean mejor con el proceso general que al lector le gustaría mejorar a continuación.

> [!div class="nextstepaction"]
> [Plan](../plan/index.md)
>
> [Listo](../ready/index.md)
>
> [Migrar](../migrate/index.md)
>
> [Administración](../manage/index.md)
>
> [Gobernanza](../govern/index.md):
