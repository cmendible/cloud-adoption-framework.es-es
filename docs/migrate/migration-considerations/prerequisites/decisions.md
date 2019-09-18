---
title: Decisiones que afectan a las migraciones
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Decisiones importantes que se deben tomar con respecto al proceso de migración
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 4bc84ad8bd2d0a0521399c1762585db6f9a5a6ab
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025414"
---
# <a name="decisions-that-affect-migrations"></a>Decisiones que afectan a las migraciones

Durante la migración, hay varios factores que afectan a las decisiones y las actividades de ejecución. En este artículo se explica el tema central de esas decisiones y se exploran algunas de las cuestiones que conducen los análisis de los principios de la migración en esta sección de la guía del marco de adopción de la nube.

## <a name="business-outcomes"></a>Resultados empresariales

El objetivo o meta de cualquier esfuerzo de adopción puede tener un efecto importante sobre el enfoque que se ha sugerido ejecutar.

- **Migración.** Los impulsores de negocio urgentes, la velocidad de adopción o el ahorro de costos son ejemplos de resultados operativos. Estos resultados son fundamentales para los esfuerzos que generan valor empresarial por los cambios transitivos en los modelos de TI o de operaciones. La sección de migración del marco de adopción de la nube se centra en gran medida en los resultados empresariales basados en la migración.
- **Innovación de las aplicaciones.** La mejora de la experiencia del cliente y el crecimiento de la cuota de mercado son ejemplos de resultados incrementales. Los resultados proceden de una colección de cambios incrementales centrados en las necesidades y los deseos de los clientes actuales.
- **Innovación basada en los datos.** . Los nuevos productos o servicios, especialmente los que proceden del poder de los datos, son ejemplos de resultados perjudiciales. Estos resultados son el producto de la experimentación y las predicciones que usan datos para alterar el status quo en el mercado.

Ninguna empresa perseguirá solamente uno de estos resultados. Sin operaciones, no hay clientes y viceversa. La adopción de la nube no es diferente. Normalmente, las empresas trabajan para lograr cada uno de estos resultados, pero tratar de centrarse en todos ellos a la vez puede hacer que se abarque demasiado y que se ralentice el progreso del trabajo que podría beneficiar más a las necesidades de su empresa.

Este requisito previo no es una exigencia para que elija uno de estos tres objetivos, sino que puede ayudar a los equipos de estrategia y adopción de la nube a establecer un conjunto de prioridades operativas que guíen la ejecución durante el próximo período de tres a seis meses. Estas prioridades se establecen mediante la clasificación de cada una de las tres opciones detalladas de *más importante* a *menos importante*, ya que se relacionan con los esfuerzos con los que puede contribuir este equipo en los próximos uno o dos trimestres.

### <a name="acting-on-migration-outcomes"></a>Actuación sobre los resultados de la migración

Si los resultados operativos obtienen la clasificación más alta de la lista, esta sección del marco de adopción de la nube funcionará bien para su equipo. En esta sección, se supone que debe priorizar la velocidad y el ahorro en los costos como indicadores clave de rendimiento (KPI) principales, en cuyo caso un modelo de migración a la adopción se alineará bien con los resultados. Un modelo centrado en la migración se basa en gran medida en la migración mediante "lift and shift" de los recursos de infraestructura como servicio (IaaS) para consumir un centro de datos y producir ahorros en los costos. En este modelo, puede producirse alguna modernización, pero es un enfoque secundario hasta que se realice la misión principal de la migración.

### <a name="acting-on-application-innovations"></a>Actuación sobre las innovaciones de las aplicaciones

Si la cuota de mercado y la experiencia del cliente son los impulsores principales, es posible que esta no sea la mejor sección del marco de adopción de la nube para guiar los esfuerzos de los equipos. La innovación de las aplicaciones requiere un plan que se centre en la modernización y la transición de las cargas de trabajo, sin importar la infraestructura subyacente. En tal caso, las instrucciones de esta sección pueden ser informativas, pero es posible que no sea el mejor enfoque para guiar las decisiones básicas.

### <a name="acting-on-data-innovations"></a>Actuación sobre las innovaciones de los datos

Si los datos, la experimentación, la investigación y el desarrollo (I+D) o los nuevos productos son su prioridad durante los próximos seis meses, es posible que esta no sea la mejor sección del marco de adopción de la nube para guiar los esfuerzos de los equipos. Cualquier esfuerzo de innovación de los datos podría beneficiarse de las instrucciones relativas a la migración de los datos de origen existentes. Sin embargo, el enfoque más amplio de ese esfuerzo estaría sobre la entrada y la integración de orígenes de datos adicionales. La ampliación de estas instrucciones con predicciones y nuevas experiencias es mucho más importante que la migración de recursos de IaaS.

## <a name="balancing-the-portfolio"></a>Equilibrio de la cartera

En esta sección del marco de adopción de la nube se establece la teoría para ayudar a los lectores a comprender distintos enfoques para abordar el cambio dentro de una cartera equilibrada. El artículo sobre el [equilibrio de la cartera](../../expanded-scope/balance-the-portfolio.md) es un ejemplo de un ámbito ampliado, diseñado para ayudarlo a actuar sobre esta teoría.

## <a name="effort"></a>Esfuerzo

El esfuerzo de migración puede variar considerablemente en función del tamaño y las complejidades de las cargas de trabajo implicadas. Una migración de cargas de trabajo más pequeña en la que solo intervengan unos cientos de máquinas virtuales (VM) es un proceso táctico, que puede implementarse mediante herramientas automatizadas como [Azure Migrate](https://docs.microsoft.com/azure/migrate/migrate-overview). Por el contrario, una gran migración empresarial de decenas de miles de cargas de trabajo requiere un proceso muy estratégico y puede implicar una extensa refactorización, recompilación y reemplazo de las aplicaciones existentes que integran las funcionalidades de plataforma como servicio (PaaS) y software como servicio (SaaS). [Es fundamental identificar y equilibrar el ámbito](../../expanded-scope/balance-the-portfolio.md) de las migraciones planeadas.

Antes de tomar decisiones que pudieran tener un efecto a largo plazo sobre el programa de migración actual, es fundamental crear un consenso sobre las siguientes decisiones.

### <a name="effort-type"></a>Tipo de esfuerzo

En cualquier migración de escala considerable (más de 250 máquinas virtuales), los recursos se migran mediante una variedad de opciones de transición, que se describen en las cinco R de la racionalización: *Rehospedaje*, *Refactorización*, *Rediseño*, *Recompilación* y *Reemplazo*.

Algunas cargas de trabajo se modernizan mediante un proceso de *recompilación* o *rediseño*, lo que crea aplicaciones más modernas con nuevas características y funcionalidades técnicas. Otros recursos pasan por un proceso de *refactorización*, por ejemplo, se mueven a contenedores u otros enfoques más modernos de funcionamiento y hospedaje que no afectan necesariamente al código base de las soluciones. Normalmente, las máquinas virtuales y otros recursos que están más establecidos pasan por un proceso de *rehospedaje*, con una transición de esos recursos del centro de datos a la nube. Es posible que algunas cargas de trabajo se puedan migrar a la nube, pero que en cambio se deban *reemplazar* mediante servicios en la nube basados en servicios (basados en SaaS) que satisfagan la misma necesidad empresarial; por ejemplo, usar con Office 365 como alternativa a la migración de instancias de Exchange Server.

En la mayoría de los escenarios, algunos eventos empresariales crean una función impulsora que hace que un alto porcentaje de recursos se migren temporalmente mediante el proceso de *rehospedaje*, seguido de una transición secundaria más significativa por medio de una de las otras estrategias de migración después de que están en la nube. Este proceso se conoce normalmente como *transición a la nube*.

Durante el proceso de [racionalización del patrimonio digital](../../../digital-estate/calculate.md), estos tipos de decisiones se aplican a cada recurso que se va a migrar. Sin embargo, el requisito previo necesario en este momento es realizar una suposición de línea base. De las cinco estrategias de migración, ¿cuál concuerda más con los objetivos empresariales o los resultados empresariales que impulsan este esfuerzo de migración? Esta decisión sirve como supuesto guía en todo el esfuerzo de migración.

### <a name="effort-scale"></a>Escala del esfuerzo

La escala de la migración es la siguiente decisión importante que constituye un requisito previo. Los procesos necesarios para migrar 1000 recursos serán diferentes de los procesos necesarios para mover 10 000. Antes de comenzar cualquier esfuerzo de migración, es importante responder a las siguientes preguntas:

- **¿Cuántos recursos admiten las cargas de trabajo de migración hoy en día?** Los recursos incluirán estructuras de datos, aplicaciones, máquinas virtuales y los dispositivos de TI necesarios. Se recomienda que elija una carga de trabajo relativamente pequeña para su primer candidato a la migración.
- **De esos recursos, ¿cuántos están planeados para la migración?** Es habitual que durante un proceso de migración se termine un porcentaje de recursos, debido a la falta de dependencia sostenida del usuario final.
- **¿Cuáles son las estimaciones descendentes de la escala de recursos que se pueden migrar?** En el caso de las cargas de trabajo que se incluyen en la migración, calcule el número de recursos auxiliares, como aplicaciones, máquinas virtuales, orígenes de datos y dispositivos de TI. Consulte la sección sobre el [patrimonio digital](../../../digital-estate/index.md) del marco de adopción de la nube para obtener instrucciones sobre cómo identificar recursos importantes.

### <a name="effort-timing"></a>Tiempo del esfuerzo

A menudo, las migraciones están impulsadas por un evento empresarial apremiante que depende del tiempo. Por ejemplo, un impulsor común es la terminación o la renovación de un contrato de hospedaje de terceros. Aunque hay muchos posibles eventos empresariales que requieren una migración, todos tienen algo en común: una fecha de finalización. Es importante comprender la temporalidad de cualquier evento empresarial inminente, de forma que sea posible planear y validar correctamente las actividades y la velocidad.

## <a name="recap"></a>Resumen

Antes de continuar, documente los siguientes supuestos y compártalos con los equipos de estrategia en la nube y adopción de la nube:

- Resultados empresariales
- Roles Este supuesto se documentará y perfeccionará para los procesos de migración *Evaluación*, *Migración*, *Optimización* y *Protección y administración*.
- Definición de finalizado. Este supuesto se documentará y perfeccionará por separado para los procesos de migración *Evaluación*, *Migración*, *Optimización* y *Protección y administración*.
- Tipo de esfuerzo
- Escala del esfuerzo
- Tiempo del esfuerzo

## <a name="next-steps"></a>Pasos siguientes

Una vez entendido el proceso en el equipo, es el momento de revisar los requisitos previos técnicos. La [lista de comprobación de planeamiento del entorno de migración](./planning-checklist.md) ayuda a garantizar que los cimientos técnicos están listos para la migración.

Una vez que el proceso se entienda en el equipo, es hora de revisar los requisitos previos técnicos; la [Lista de comprobación del planeamiento de la migración] ayudará a garantizar que los cimientos técnicos están listos para la migración.

> [!div class="nextstepaction"]
> [Revisión de la lista de comprobación del planeamiento de la migración](./planning-checklist.md)
