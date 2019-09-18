---
title: Establecimiento de una revisión de adecuación operativa
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Orientación sobre los fundamentos operacionales
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/20/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 04afedc133d001405c5042b309a45c9b41f3268e
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032547"
---
# <a name="establish-an-operational-fitness-review"></a>Establecimiento de una revisión de adecuación operativa

Una vez que la empresa comienza a trabajar con cargas de trabajo en Azure, el siguiente paso es establecer un proceso de *revisión de la adecuación operativa*. Este proceso enumera, implementa y revisa de forma iterativa los *requisitos no funcionales* de estas cargas de trabajo. Los requisitos no funcionales están relacionados con el comportamiento operativo esperado del servicio.

Hay cinco categorías esenciales de requisitos no funcionales, que se denominan los [pilares de la calidad del software](https://docs.microsoft.com/azure/architecture/guide/pillars):

- Escalabilidad
- Disponibilidad
- Resistencia, que incluye la continuidad empresarial y recuperación ante desastres
- Administración
- Seguridad

El proceso de revisión de la adecuación operativa garantiza que sus cargas de trabajo críticas cumplen las expectativas de la empresa con respecto a los fundamentos de calidad.

Su empresa debe llevar a cabo un proceso de revisión de la adecuación operativa para entender los problemas derivados de ejecutar cargas de trabajo en un entorno de producción, determinar cómo solucionar los problemas y resolverlos. En este artículo se describe un proceso general de revisión de la adecuación operativa que puede usar su empresa para conseguir este objetivo.

## <a name="operational-fitness-at-microsoft"></a>Adecuación operativa en Microsoft

Desde el principio, el desarrollo de la plataforma Azure ha sido un proyecto de integración y desarrollo continuos acometido por diversos equipos en Microsoft. Es difícil garantizar la calidad y la coherencia de un proyecto de tal tamaño y complejidad. Se necesita un proceso sólido para enumerar e implementar los requisitos fundamentales no funcionales de forma periódica.

Los procesos que Microsoft sigue constituyen la base de los procesos que se describen en este artículo.

## <a name="understand-the-problem"></a>Comprender el problema

Como aprendió en la [Introducción](../getting-started/migrate.md), el primer paso en la transformación digital de una empresa es identificar los problemas empresariales que se van a resolver con la adopción de Azure. El siguiente paso es determinar una solución general para el problema, como la migración de una carga de trabajo a la nube o la adaptación de un servicio local existente para incluir funcionalidad de nube. Finalmente, la solución está diseñada e implementada.

Durante este proceso, el foco suelen ser las características del servicio: el conjunto de requisitos _funcionales_ que desea que el servicio realice. Por ejemplo, un servicio de entrega de productos requiere características para determinar las ubicaciones de origen y destino del producto, realizar el seguimiento del producto durante la entrega, enviar notificaciones al cliente, etc.

En cambio, los requisitos _no funcionales_ se relacionan con propiedades como la [disponibilidad](https://docs.microsoft.com/azure/architecture/checklist/availability), la [resistencia](https://docs.microsoft.com/azure/architecture/resiliency) y la [escalabilidad](https://docs.microsoft.com/azure/architecture/checklist/scalability) del servicio. Estas propiedades se diferencian de los requisitos funcionales en que no influyen directamente sobre la función final de ninguna característica en particular del servicio. Sin embargo, los requisitos no funcionales están relacionados con el rendimiento y la continuidad del servicio.

Algunos requisitos no funcionales se pueden especificar en los términos de un Acuerdo de Nivel de Servicio (SLA). Por ejemplo, en el caso de la continuidad del servicio, un requisito de disponibilidad del servicio se puede expresar como un porcentaje: "Disponible el 99,99 % del tiempo". Otros requisitos no funcionales pueden ser más difíciles de definir y pueden cambiar a medida que cambian las necesidades de producción. Por ejemplo, un servicio orientado al consumidor podría comenzar a toparse con requisitos de rendimiento no anticipados tras un aumento repentino de popularidad.

> [!NOTE]
> Los requisitos de resistencia se exploran con más detalle en [Diseño de aplicaciones de Azure confiables](https://docs.microsoft.com/azure/architecture/reliability#define-requirements). Este artículo incluye explicaciones de conceptos como el objetivo de punto de recuperación (RPO), el objetivo de tiempo de recuperación (RTO), Acuerdo de Nivel de Servicio y otros.

## <a name="process-for-operational-fitness-review"></a>Proceso de revisión de la adecuación operativa

La clave para mantener el rendimiento y la continuidad de los servicios de una empresa es implementar un proceso de revisión de la adecuación operativa.

![Introducción al proceso de revisión de la adecuación operativa](../_images/manage/ofr-flow.png)

En un nivel alto, el proceso tiene dos fases. En la *fase de requisitos previos*, se establecen los requisitos y se asignan a los servicios correspondientes. Esta fase se produce con poca frecuencia; quizás cada año o cuando se introducen nuevas operaciones. El resultado de la fase de requisitos previos se usa en la *fase de flujo*. La fase de flujo se produce con más frecuencia; se recomienda una vez al mes.

### <a name="prerequisites-phase"></a>Fase de requisitos previos

En los pasos descritos en esta fase se capturan los requisitos para llevar a cabo una revisión periódica de los servicios importantes.

1. **Identificar las operaciones empresariales críticas**. Identifique las operaciones empresariales críticas de la empresa. Las operaciones empresariales son independientes de cualquier funcionalidad de servicio complementaria. En otras palabras, las operaciones empresariales representan las actividades reales que el negocio debe realizar y están respaldadas por un conjunto de servicios de TI.

    El término *crítico* (o *crítico para el negocio*), refleja un impacto grave en la empresa si se impide la operación. Por ejemplo, un minorista en línea puede tener una operación empresarial del tipo "permitir que un cliente agregue un artículo al carro de la compra" o "procesar un pago con tarjeta de crédito". Si alguna de estas operaciones genera un error, el cliente no puede realizar la transacción y la empresa no puede realizar ventas.

1. **Asignar operaciones a servicios**. Asigne las operaciones empresariales críticas a los servicios correspondientes. En el ejemplo del carro de la compra, pueden intervenir varios servicios: un servicio de administración del stock de inventario, un servicio de carro de la compra y otros. Para procesar un pago con tarjeta de crédito, un servicio de pago local podría interactuar con un servicio de procesamiento de pagos de terceros.

1. **Analizar las dependencias de los servicios**. La mayoría de las operaciones empresariales requiere la orquestación de varios servicios. Es importante comprender las dependencias entre los servicios y el flujo de transacciones críticas a través de estos servicios.

    Considere también las dependencias entre los servicios locales y los servicios de Azure. En el ejemplo de carro de la compra, el servicio de administración de existencias de inventario podría estar hospedado en el entorno local e ingerir los datos introducidos por los empleados desde un almacén físico. Sin embargo, podría almacenar los datos fuera del entorno local en un servicio de Azure, como [Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-introduction), o en una base de datos, como [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).

Una salida de estas actividades es un conjunto de *métricas del cuadro de mandos* de las operaciones de servicio. Las métricas se clasifican en términos de criterios no funcionales, como disponibilidad, escalabilidad y recuperación ante desastres. Las métricas del cuadro de mandos expresan los criterios operativos que se espera que cumpla el servicio. Estas métricas se pueden expresar con cualquier nivel de detalle que sea necesario para la operación del servicio.

El cuadro de mandos debe expresarse en términos sencillos para facilitar la comunicación significativa entre los propietarios de empresa y los ingenieros. Por ejemplo, una métrica del cuadro de mandos de escalabilidad se puede expresar como verde para indicar que se cumplen los criterios deseados, amarillo para indicar que no se cumplen los criterios deseados, pero se está en proceso de implantar un plan de corrección, y rojo para indicar que no se cumplen los criterios deseados con ningún plan o acción.

Es importante destacar que estas métricas deben reflejar directamente las necesidades empresariales.

### <a name="service-review-phase"></a>Fase de revisión de los servicios

La fase de revisión de los servicios es el núcleo del proceso de revisión de la adecuación operativa. Implica estos pasos:

1. **Medir las métricas de los servicios**. Use las métricas del cuadro de mandos para supervisar los servicios con el fin de garantizar que cumplen las expectativas empresariales. En otras palabras, la supervisión de los servicios es fundamental. Si no puede supervisar un conjunto de servicios con respecto a los requisitos no funcionales, las métricas del cuadro de mando correspondientes se deben considerar en rojo. En este caso, el primer paso para solucionarlo es implementar la supervisión de los servicios adecuada. Por ejemplo, si la empresa espera que un servicio funcione con una disponibilidad del 99,99 %, pero no dispone de datos de telemetría de producción para medir la disponibilidad, dé por hecho que no satisface el requisito.

2. **Planear las acciones correctivas**. Para cada operación de servicio con métricas que se encuentren por debajo de un umbral aceptable, determine el costo de corregir el servicio para llevar la operación a un nivel aceptable. Si el costo de la corrección del servicio es mayor que ingresos esperados del servicio, pase a considerar los costos no tangibles como la experiencia del cliente. Por ejemplo, si los clientes tienen dificultad para realizar pedidos correctamente con el servicio, podrían elegir en su lugar a la competencia.

3. **Implementar el plan correctivo**. En cuanto los propietarios del negocio y los ingenieros acuerden un plan, impleméntelo. Informe del estado de la implementación cada vez que revise las métricas del cuadro de mandos de revisión.

Este proceso es iterativo y lo ideal es que la empresa tenga un equipo destinado a él. Este equipo debe reunirse periódicamente para revisar los proyectos de corrección existentes, poner en marcha la revisión de aspectos básicos de nuevas cargas de trabajo y realizar un seguimiento del cuadro de mandos general de la empresa. El equipo debe tener la autoridad necesaria para hacer responsables a los equipos de corrección si se retrasan o no cumplen las métricas.

## <a name="structure-of-the-review-team"></a>Estructura del equipo de revisión

El equipo de revisión de la adecuación operativa se compone de los siguientes roles:

- **Propietario de la empresa**: proporciona los conocimientos del negocio para identificar y clasificar por orden de prioridad cada operación empresarial crítica. Este rol también compara el costo de la solución con la repercusión para el negocio y conduce la decisión final sobre la corrección.

- **Defensor del negocio.** Divide las operaciones empresariales en diferentes partes y las asigna a los servicios y la infraestructura, ya sea en el entorno local o en la nube. El rol requiere un conocimiento profundo de la tecnología asociada con cada operación empresarial.

- **Propietario de ingeniería.** Implementa los servicios asociados al funcionamiento del negocio. Estas personas pueden participar en el diseño y la implementación de posibles soluciones para resolver los problemas de requisitos no funcionales detectados por el equipo de revisión.

- **Propietario del servicio**. Se encarga del funcionamiento de las aplicaciones y los servicios de la empresa. Estos individuos recopilan datos de registro y uso de estas aplicaciones y servicios. Estos datos se usan para identificar problemas y para comprobar las correcciones una vez que se han implementado.

## <a name="review-meeting"></a>Reuniones de revisión

Es recomendable que el equipo de revisión se reúna periódicamente. Por ejemplo, podría reunirse todos los meses e informar del estado y las métricas al equipo de dirección trimestralmente.

Adapte los detalles del proceso y las reuniones a sus necesidades específicas. Como punto de partida, se recomiendan las siguientes tareas:

1. El propietario y el defensor del negocio enumeran y determinan los requisitos no funcionales de cada operación empresarial, con la aportación de los propietarios de la ingeniería y los servicios. En el caso de las operaciones empresariales que se han identificado previamente, se revisa y se comprueba la prioridad. En el caso de las nuevas operaciones comerciales, se asigna una prioridad en la lista existente.

2. Los propietarios de la ingeniería y los servicios asignan el estado actual de las operaciones empresariales a los servicios en la nube y locales correspondientes. La asignación es una lista de los componentes de cada servicio en forma de árbol de dependencias. Una vez que se generan la lista y el árbol de dependencias, se determinan las rutas críticas a través del árbol.

3. Los propietarios de ingeniería y del servicio revisan el estado actual del registro y la supervisión operativos de los servicios enumerados en el paso anterior. Para identificar los componentes del servicio que contribuyen al incumplimiento de los requisitos no funcionales, son esenciales procedimientos de registro y supervisión de gran solidez. Si no se disponen de suficientes procedimientos de registro y supervisión, se debe crear e implementar un plan para implantarlos.

4. Se crean métricas del cuadro de mandos para las nuevas operaciones empresariales. El cuadro de mandos consta de la lista de componentes que forman cada uno de los servicios identificados en el paso 2. Está en línea con los requisitos no funcionales e incluye una medida del grado en que cada componente cumple los requisitos.

5. Para los componentes constituyentes que no cumplen los requisitos no funcionales, se diseña una solución general y se asigna un propietario de ingeniería. En este momento, el propietario y el defensor del negocio establecen un presupuesto para el trabajo de corrección, en función de los ingresos previstos de la operación empresarial.

6. Por último, se lleva a cabo una revisión del trabajo de corrección en curso. Cada una de las métricas del cuadro de mandos de trabajo en curso se revisa comparándola con los criterios previstos. En el caso de los componentes constituyentes que cumplen los criterios, el propietario de los servicios presenta los datos de registro y supervisión para confirmar que se cumplen los criterios. En cuanto a los componentes constituyentes que no cumplen los criterios de las métricas, cada propietario de ingeniería explica los problemas que impiden que se alcancen las métricas y nuevas formas posibles de corregir el problema.

## <a name="recommended-resources"></a>Recursos recomendados

- [Fundamentos de calidad del software](https://docs.microsoft.com/azure/architecture/guide/pillars).
    En esta sección de la guía de arquitectura de aplicaciones de Azure se describen los cinco fundamentos de la calidad del software: escalabilidad, disponibilidad, resistencia, administración y seguridad.
- [Diez principios de diseño para las aplicaciones de Azure](https://docs.microsoft.com/azure/architecture/guide/design-principles).
    En esta sección de la guía de arquitectura de aplicaciones de Azure se analiza un conjunto de principios de diseño para que la aplicación sea más escalable, resistente y fácil de administrar.
- [Diseño de aplicaciones resistentes de Azure](https://docs.microsoft.com/azure/architecture/resiliency).
    Esta guía comienza con una definición del término _resistencia_ y los conceptos relacionados. Después, se describe un proceso para lograr resistencia, mediante un enfoque estructurado durante la vigencia de una aplicación, desde el diseño y la puesta en marcha hasta la implementación y operaciones.
- [Patrones de diseño en la nube](https://docs.microsoft.com/azure/architecture/patterns).
    Estos patrones de diseño son útiles para los equipos de ingeniería al compilar aplicaciones sobre los fundamentos de calidad del software.
