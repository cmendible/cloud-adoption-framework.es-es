---
title: Equilibrio de la cartera
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Equilibrio de la cartera
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 1227b798972ce7e139181c9267a1a1e860390029
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70836710"
---
# <a name="balance-the-portfolio"></a>Conciliar la cartera

La adopción de la nube es un esfuerzo de administración de carteras, disfrazado de manera inteligente como una implementación técnica. Al igual que cualquier ejercicio de administración de carteras, el equilibrio de una cartera es un elemento crítico para alcanzar el éxito. En un nivel estratégico, esto significa equilibrar la migración, innovación y experimentación para aprovechar la nube al máximo. Cuando el esfuerzo de adopción de la nube se inclina demasiado en una dirección o en la otra, la complejidad se abre camino en el esfuerzo de migración. En este artículo se le guiará al lector a través de los enfoques para alcanzar el equilibrio de la cartera.

## <a name="general-scope-expansion"></a>Expansión del ámbito general

Este tema es estratégico por naturaleza. De ese modo, el enfoque que se lleva a cabo en este artículo es igualmente estratégico. Para basar la estrategia en decisiones impulsadas por los datos, en este artículo se presupone que el lector ha evaluado el [patrimonio digital](../../digital-estate/index.md) existente (o que está en proceso de hacerlo). El objetivo de este enfoque es ayudar a evaluar las cargas de trabajo para garantizar un equilibrio adecuado en toda la cartera a través de preguntas cualitativas y el perfeccionamiento de la cartera.

### <a name="documenting-business-outcomes"></a>Documentación de los resultados empresariales

Antes de equilibrar la cartera, es importante documentar y compartir los resultados empresariales que impulsan el esfuerzo de migración a la nube. Para ver algunos ejemplos de los resultados empresariales generales relativos a las migraciones a la nube, consulte el [resumen ejecutivo de la migración a la nube](../../getting-started/migrate.md).

La tabla siguiente puede ayudar a documentar y compartir los resultados empresariales deseados. Es importante tener en cuenta que la mayoría de las empresas buscan obtener varios resultados a la vez. La importancia de este ejercicio es aclarar los resultados que están relacionados de manera más directa con el esfuerzo de migración a la nube:

|Resultado  |Medido por  |Objetivo  |Período de tiempo  |Prioridad de este esfuerzo  |
|---------|---------|---------|---------|---------|
|Reducción de los costos de TI     |Presupuesto del centro de datos         |Reducción en USD 2 millones         |12 meses         |N.° 1         |
|Salida del centro de datos     |Salida de los centros de datos         |2 centros de datos         |6 meses         |N.° 2         |
|Aumento de la agilidad comercial     |Mejor tiempo de comercialización  |Disminuir el tiempo de implementación en seis meses         |2 años         |N.° 3        |
|Mejor experiencia del cliente     |Satisfacción del cliente (CSAT)         |10 % de mejora         |12 meses         |N.° 4         |

> [!IMPORTANT]
> La tabla anterior es un ejemplo ficticio y no se debe usar para establecer las prioridades. En muchos casos, esta tabla se podría considerar como un antipatrón si los ahorros de costos se ponen por sobre las experiencias de los usuarios.

La tabla anterior podría representar de manera precisa las prioridades de los equipos de estrategia en la nube y de adopción de la nube que supervisan una migración a la nube. Debido a restricciones a corto plazo, este equipo pone un mayor énfasis en la reducción de costos de TI y en establecer la prioridad de una salida de datos como medio para lograr las reducciones de costos de TI deseadas. Sin embargo, al documentar las prioridades contrapuestas en esta tabla, el equipo de adopción de la nube está capacitado para ayudar al equipo de estrategia en la nube a identificar oportunidades para alinear mejor la implementación de la estrategia de cartera general.

### <a name="move-fast-while-maintaining-balance"></a>Traslado rápido mientras se mantiene el equilibrio

Las instrucciones relacionadas con la [racionalización incremental del patrimonio digital](../../digital-estate/index.md) sugieren un enfoque en el que la racionalización comienza con una posición no equilibrada. El equipo de estrategia en la nube debe evaluar cada carga de trabajo para ver si es compatible con un enfoque de rehospedaje. Se sugiere este tipo de enfoque porque permite realizar una evaluación rápida de un patrimonio digital complejo en función de datos cuantitativos. Una suposición inicial así permite que el equipo de adopción de la nube participe rápidamente, con lo que disminuirá el tiempo para obtener resultados empresariales. Sin embargo, tal como se indica en este artículo, las preguntas cualitativas proporcionarán el equilibrio necesario en la cartera. En este artículo se documenta el proceso de creación del equilibrio prometido.

### <a name="importance-of-sunset-and-retire-decisions"></a>Importancia de las decisiones sobre expiración y retirada

En la tabla que aparece en la sección de [documentación de los resultados empresariales](#documenting-business-outcomes) falta un resultado clave que podría permitir el objetivo número uno de reducir los costos de TI. Cuando las reducciones de los costos de TI están en cualquier parte de la lista de resultados empresariales, resulta importante considerar el potencial para expirar o retirar cargas de trabajo. En algunos escenarios, el ahorro de costos puede provenir de NO migrar las cargas de trabajo que no garantizan una inversión a corto plazo. Algunos clientes han informado ahorros de costos superiores al 20 % de las reducciones de costos totales al retirar las cargas de trabajo infrautilizadas.

Para equilibrar la cartera, lo que refleja mejor las decisiones sobre expiración y retirada, se recomienda que los equipos de estrategia en la nube y de adopción de la nube hagan las preguntas siguientes sobre cada carga de trabajo dentro de los procesos de evaluación y migración:

- ¿Los usuarios finales han usado la carga de trabajo en los últimos seis meses?
- ¿El tráfico de usuario final es coherente o va en aumento?
- ¿La empresa necesitará esta carga de trabajo en 12 meses más?

Si la respuesta a cualquiera de estas preguntas es "No", la carga de trabajo podría ser candidata a la retirada. Si se confirma el potencial de retirada con el propietario de la aplicación, puede que migrar la carga de trabajo no tenga sentido. Esto implica algunas preguntas de calificación:

- ¿Se puede establecer un plan de retirada o un plan de expiración para esta carga de trabajo?
- ¿Esta carga de trabajo se puede retirar antes de la salida del centro de datos?

Si la respuesta a ambas preguntas es "Sí", sería recomendable _no_ migrar la carga de trabajo. Este enfoque ayudaría a cumplir los objetivos de disminuir costos y salir del centro de datos.

Si al respuesta a cualquier pregunta es "No", podría ser aconsejable establecer un plan para hospedar la carga de trabajo hasta que se pueda retirar. Este plan podría incluir el traslado de los recursos a un centro datos de menor costo o a uno alternativo, lo que también lograría los objetivos de reducir los costos y salir de un centro de datos.

## <a name="suggested-prerequisites"></a>Requisitos previos sugeridos

Los requisitos previos especificados en la guía de línea base deben seguir siendo suficientes para abordar este tema de la complejidad. Sin embargo, el inventario de recursos y el patrimonio digital se deben resaltar y enfatizar entre estos requisitos previos, ya que los datos controlarán las actividades siguientes.

## <a name="assess-process-changes"></a>Evaluación de los cambios en el proceso

El equilibrio de la cartera requiere un análisis cualitativo adicional durante el proceso de evaluación, que ayudará a impulsar una racionalización de cartera sencilla.

### <a name="suggested-action-during-the-assess-process"></a>Acción sugerida durante el proceso de evaluación

En función de los datos de la tabla que aparece en la sección [Documentación de los resultados empresariales](#documenting-business-outcomes) anterior, hay un riesgo probable de que la cartera se incline demasiado hacia un modelo de ejecución centrado en la migración. Si la experiencia del cliente fuese una prioridad principal, sería más probable una cartera inclinada a la innovación. Ninguno de estos enfoques es correcto ni equivocado, pero inclinarse demasiado en una sola dirección habitualmente generá una disminución en las devoluciones, agrega complejidad innecesaria y aumenta el tiempo de ejecución relacionado con los esfuerzos de adopción de la nube.

Para disminuir la complejidad, se recomienda que el lector siga un enfoque tradicional con respecto a la racionalización de la cartera, pero en un modelo iterativo. Los pasos siguientes describen un modelo cualitativo para dicho tipo de enfoque:

- El equipo de estrategia en la nube mantiene un trabajo pendiente priorizados de las cargas de trabajo que se van a migrar.
- Los equipos de estrategia en la nube y de adopción de la nube realizan una reunión de planeamiento de liberación antes de completar cada liberación.
- En la reunión de planeamiento de liberación, los equipos llegan a un acuerdo sobre las principales 5 a 10 cargas de trabajo en el trabajo pendiente con prioridad.
- Fuera de la reunión de planeamiento de liberación, el equipo de adopción de la nube formular estas preguntas a los propietarios de la aplicación y a los expertos en la materia:
  - ¿Esta aplicación se podría reemplazar por un equivalente de plataforma como servicio (PaaS)?
  - ¿Es una aplicación de terceros?
  - ¿Se aprobó presupuesto para invertir en el desarrollo en curso de la aplicación durante los próximos 12 meses?
  - ¿El desarrollo adicional de esta aplicación mejoraría la experiencia del cliente? ¿Crearía un diferenciador competitivo? ¿Generaría ingresos adicionales para la empresa?
  - ¿Los datos dentro de esta carga de trabajo contribuirán a una innovación de nivel inferior relacionada con BI, Machine Learning, IoT o tecnologías relacionadas?
  - ¿La carga de trabajo es compatible con plataformas de aplicaciones modernas como Azure App Service?
- Las respuestas a las preguntas anteriores y cualquier otro análisis cualitativo necesarios podrían influir en los ajustes en el trabajo pendiente con prioridad. Estos ajustes pueden incluir:
  - Si una carga de trabajo se pudiera reemplazar por una solución de PaaS, se puede quitar totalmente del trabajo pendiente de migración. Como mínimo, la diligencia requerida adicional para decidir entre rehospedaje y reemplazo se podría agregar como tarea, lo que reduciría de manera temporal la prioridad de esa carga de trabajo del trabajo pendiente de migración.
  - Si una carga de trabajo está en proceso de desarrollo (o debería estarlo), es posible que se ajuste mejor a un modelo de refactorización/rediseño/recompilación. Como la innovación y la migración requieren aptitudes técnicas distintas, a menudo se recomienda que las aplicaciones, que se alinean con un enfoque de refactorización/rediseño/recompilación, se administren a través de un trabajo pendiente de innovación, en lugar de un trabajo pendiente de migración.
  - Si una carga de trabajo forma parte de una innovación de nivel inferior, es posible que tenga sentido refactorizar la plataforma de datos, pero dejar los niveles de aplicación como candidatos a rehospedaje. A menudo, la refactorización secundaria de la plataforma de datos de una carga de trabajo se puede abordar en un trabajo pendiente de innovación o migración. Este resultado de la racionalización puede generar elementos de trabajo más detallados en el trabajo pendiente, pero ningún otro cambio en las prioridades.
  - Si una carga de trabajo no es estratégica pero es compatible con plataformas de hospedaje de aplicaciones modernas basadas en la nube, puede ser aconsejable realizar una refactorización secundaria en la aplicación para implementarla como una aplicación moderna. Esto puede contribuir al ahorro general al disminuir los requisitos de licencias del SO y de IaaS generales de la migración a la nube.
  - Si una carga de trabajo es una aplicación de terceros y no hay planes de usar los datos de esa carga de trabajo en una innovación de nivel inferior, puede ser mejor dejarla como una opción de rehospedaje en el trabajo pendiente.

Estas preguntas no deben ser la extensión del análisis cualitativo que se completa para cada carga de trabajo, sino que están diseñadas para guiar una conversación que ayude a abordar la complejidad de una cartera no equilibrada.

## <a name="migrate-process-changes"></a>Cambios en el proceso de migración

Durante la migración, las actividades de equilibrio de cartera pueden tener un impacto negativo en la velocidad de migración (la velocidad a la que se migran los recursos). Las instrucciones siguientes expandirán el motivo y la manera de alinear el trabajo para impedir que se produzcan interrupciones en el esfuerzo de migración.

### <a name="suggested-action-during-the-migrate-process"></a>Acción sugerida durante el proceso de migración

La racionalización de la cartera requiere diversos esfuerzos técnicos. Para los equipos de adopción en la nube, es tentador hacer coincidir esa diversidad de la cartera dentro de los esfuerzos de migración. Las partes interesadas de la empresa piden que un solo equipo de adopción de la nube aborde todo el trabajo pendiente de la migración. Este rara vez es un enfoque aconsejable y, en muchos casos, puede ser contraproducente.

Se recomienda que estos distintos esfuerzos se segmentan entre dos o más equipos de adopción de la nube. Cuando se usa un modelo de dos equipos como modo de ejecución de ejemplo, el Equipo 1 es el equipo de migración y el Equipo 2, el de innovación. En el caso de esfuerzos de mayor tamaño, estos equipos se podrían segmentar aún más para abordar otros enfoques como los esfuerzos de Reemplazo/PaaS o Refactorización secundaria. A continuación, se describen las aptitudes y los roles que se necesitan para Rehospedaje, Refactorización o Refactorización secundaria:

**Rehospedaje:** el rehospedaje requiere que los miembros del equipo implementen cambios centrados en la infraestructura. Por lo general, se usa una herramienta como Azure Site Recovery para migrar máquinas virtuales u otros recursos a Azure. Este trabajo se alinea correctamente con los implementadores de TI o los administradores de centros de datos. El equipo de migración a la nube está bien estructurado para entregar este trabajo a gran escala. Este es el enfoque más rápido para migrar los recursos existentes en la mayoría de los escenarios.

**Refactorización:** la refactorización requiere que los miembros del equipo modifiquen el código fuente, cambien la arquitectura de una aplicación o adopten servicios en la nube nuevos. Por lo general, este esfuerzo usaría herramientas de desarrollo, como Visual Studio, y herramientas de canalización de implementación, como Azure DevOps, para volver a implementar aplicaciones modernizadas en Azure. Este trabajo se alinea correctamente con los roles de desarrollo de aplicaciones o con los roles de desarrollo de canalizaciones de DevOps. El equipo de innovación en la nube está mejor estructurado para brindar este trabajo. Este enfoque podría tardar más en reemplazar los recursos existentes por los recursos en la nube, pero las aplicaciones pueden aprovechar las características nativas de la nube.

**Refactorización secundaria:** algunas aplicaciones se pueden modernizar con la refactorización secundaria en el nivel de datos o el de aplicación. Este trabajo requiere que los miembros del equipo implementen datos en las plataformas de datos basadas en la nube o hagan cambios de configuración menores en la aplicación. Esto puede requerir un respaldo limitado de los expertos en el desarrollo de aplicaciones o datos. Sin embargo, este trabajo es similar al que realizan los implementadores de TI al implementar aplicaciones de terceros. Este trabajo se puede alinear fácilmente con el equipo de migración a la nube o con el de estrategia en la nube. Si bien este esfuerzo no es tan rápido como una migración de rehospedaje, demora menos en ejecutarse que los esfuerzos de refactorización.

Durante la migración, se recomienda segmentar esos esfuerzos de las tres maneras ya mencionadas y que esos esfuerzos los ejecute el equipo adecuado en la iteración correspondiente. Si bien se aconseja que la cartera esté diversificada, también se aconseja que los esfuerzos se mantengna muy centrados y segregados.

## <a name="optimize-and-promote-process-changes"></a>Optimización y promoción de los cambios del proceso

No se requiere ningún cambio adicional durante los procesos de seguridad y administración dentro del esfuerzo de migración.

## <a name="secure-and-manage-process-changes"></a>Cambios en el proceso de protección y administración

No se requiere ningún cambio adicional durante los procesos de protección y administración dentro del esfuerzo de migración.

## <a name="next-steps"></a>Pasos siguientes

Vuelva a la [lista de comprobación del ámbito ampliado](./index.md) para asegurarse de que el método de migración está totalmente alineado.

> [!div class="nextstepaction"]
> [Lista de comprobación del ámbito ampliado](./index.md)
