---
title: 'Preparación para la complejidad técnica: administración de cambios ágil'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Preparación para la complejidad técnica: administración de cambios ágil'
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: ba799c8634fc6eeda70507ae85464506103e44ff
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025367"
---
# <a name="prepare-for-technical-complexity-agile-change-management"></a>Preparación para la complejidad técnica: administración de cambios ágil

Cuando se puede desaprovisionar y volver a crear un centro de datos entero con una sola línea de código, los procesos tradicionales luchan por estar a la altura. Las instrucciones de Cloud Adoption Framework se basan en prácticas como la Administración de servicios de TI (ITSM), el marco Open Group Architecture Framework (TOGAF), etc. Sin embargo, para garantizar la agilidad y la capacidad de respuesta al cambio empresarial, este marco de trabajo moldea esas prácticas para incorporar metodologías ágiles y enfoques de DevOps.

Al cambiar a un modelo ágil donde se resaltan la flexibilidad y la iteración, la complejidad técnica y la administración de cambios se tratan de forma diferente a como se hace en un modelo en cascada tradicional, que se centra en una serie lineal de pasos de migración. En este artículo se describe un enfoque general para la administración de cambios en un trabajo de migración basado en el método ágil. Al final del artículo, debería tener una idea general de los niveles de administración de cambios y de la documentación que conlleva un enfoque de migración incremental. Es necesario más aprendizaje y tomar más decisiones para seleccionar e implementar prácticas ágiles basadas en esta idea. La intención de este artículo es preparar a los arquitectos de la nube para una conversación facilitada con los directores de proyectos al objeto de explicar el concepto general de administración de cambios con este enfoque.

## <a name="addressing-technical-complexity"></a>Cómo solucionar la complejidad técnica

Cuando se cambia cualquier sistema técnico, la complejidad y la interdependencia suponen un riesgo en los planes del proyecto. Las migraciones a la nube no son una excepción. Cuando se mueven miles &mdash;o decenas de miles&mdash; de recursos a la nube, estos riesgos se multiplican. La detección y la asignación de todas las dependencias de un patrimonio digital podría tardar años. Pocas empresas pueden tolerar un ciclo de análisis tan largo. Con el fin de equilibrar la necesidad de análisis arquitectónico y aceleración empresarial, el marco Cloud Adoption Framework se centra en un modelo INVEST para la administración del trabajo pendiente de los productos. En las secciones siguientes se resume este tipo de modelo.

## <a name="invest-in-workloads"></a>INVEST en las cargas de trabajo

El término _carga de trabajo_ está presente en todo el marco Cloud Adoption Framework. Una carga de trabajo es una unidad de funcionalidad de una aplicación que se puede migrar a la nube. Podría ser una sola aplicación, una capa de una aplicación o una colección de una aplicación. La definición es flexible y puede variar en diferentes fases de la migración. El marco Cloud Adoption Framework utiliza el término _INVEST_ para definir una carga de trabajo.

INVEST es un acrónimo común en muchas metodologías ágiles para escribir casos de usuario o elementos de trabajo pendiente de productos. Ambos son unidades de salida en herramientas de administración de proyectos ágiles. La unidad de salida mensurable en una migración es una carga de trabajo migrada. El marco Cloud Adoption Framework modifica un poco el acrónimo inglés INVEST para crear una construcción que defina las cargas de trabajo:

- **Independent** (independiente): una carga de trabajo no debe tener ninguna dependencia inaccesible. Para que una carga de trabajo se considere migrada, todas las dependencias deben ser accesibles y estar incluidas en el trabajo de migración.
- **Negotiable** (negociable): a medida que se realiza una nueva detección, la definición de una carga de trabajo cambia. Los arquitectos que planean la migración podrían negociar factores con respecto a las dependencias. Algunos ejemplos de puntos de negociación podrían ser la versión preliminar de características, el acceso a las características a través de una red híbrida o el empaquetado de todas las dependencias en una única versión.
- **Valuable** (valiosa): el valor de una carga de trabajo se mide por la capacidad de proporcionar a los usuarios acceso a una carga de trabajo de producción.
- **Estimable** (calculable): las dependencias, los recursos, el tiempo de migración, el rendimiento y los costos de la nube deben poderse calcular y deben calcularse antes de la migración.
- **Small** (pequeña): el objetivo es empaquetar las cargas de trabajo en un solo sprint. Sin embargo, puede que esto no sea posible siempre. Por eso se recomienda que los equipos planeen los sprints y las versiones para minimizar el tiempo necesario para mover una carga de trabajo a producción.
- **Testable** (comprobable): Siempre debe haber un medio definido para probar o validar la finalización de la migración de una carga de trabajo.

Este acrónimo no pretende ser una base que haya que adoptar de forma estricta, pero debería servir de guía para definir el término _carga de trabajo_.

## <a name="migration-backlog-aligning-business-priorities-and-timing"></a>Trabajo pendiente de migración: alineación de las prioridades empresariales y los plazos

El trabajo pendiente de migración permite realizar un seguimiento de la cartera general de cargas de trabajo que se pueden migrar. Se recomienda que, antes de la migración, los equipos de estrategia en la nube y de adopción de la nube revisen el [patrimonio digital](../../../digital-estate/index.md) actual y acuerden una lista de las cargas de trabajo que deben migrarse por orden de prioridad. Esta lista constituye la base del trabajo pendiente de migración inicial.

Al principio, es poco probable que las cargas de trabajo pendientes de migración cumplan los criterios INVEST que se han descrito en la sección anterior. Más bien sirven como agrupación lógica de recursos de un inventario inicial que se usará como marcador de posición para el trabajo futuro. Puede que esos marcadores de posición no sean exactos desde un punto de vista técnico, pero sirven como base para la coordinación con la empresa.

![Relación entre los trabajos pendientes de migración, versión e iteración que se usan durante el proceso de migración](../../../_images/migrate/backlog-relationships.png)

*Los trabajos pendientes de migración, versión e iteración realizan un seguimiento de los distintos niveles de actividad durante los procesos de migración.*

En cualquier trabajo pendiente de una migración, el equipo de administración de cambios debe procurar obtener la siguiente información para cualquier carga de trabajo del plan. Como mínimo, deben estar disponibles estos datos para cualquier carga de trabajo prioritaria para la migración en las dos o tres versiones siguientes.

### <a name="migration-backlog-data-points"></a>Puntos de datos del trabajo pendiente de migración

- **Impacto de negocio.** Comprensión del impacto que tendría en el negocio si no se cumple la escala de tiempo prevista o si se reduce la funcionalidad durante los períodos de inmovilización.
- **Prioridad empresarial relativa.** Lista de cargas de trabajo clasificada por prioridad empresarial.
- **Propietario empresarial.** Documente la persona responsable de tomar decisiones empresariales en relación con esta carga de trabajo.
- **Propietario técnico.** Documente la persona responsable de tomar decisiones técnicas en relación con esta carga de trabajo.
- **Escalas de tiempo previstas.** Fecha de finalización programada para la migración.
- **Inmovilizaciones de la carga de trabajo.** Períodos en los que no se puede cambiar la carga de trabajo.
- **Nombre de la carga de trabajo.**
- **Inventario inicial.** Recursos necesarios para proporcionar la funcionalidad de la carga de trabajo, como las máquinas virtuales, los dispositivos de TI, los datos, las aplicaciones, las canalizaciones de implementación, etc. Es probable que esta información no sea precisa.

## <a name="release-backlog-aligning-business-change-and-technical-coordination"></a>Trabajo pendiente de versión: alineación del cambio empresarial y la coordinación técnica

En el contexto de una migración, una _versión_ es una actividad que implementa una o varias cargas de trabajo en producción. Generalmente, una versión abarca varias iteraciones o trabajo técnico. Sin embargo, representa una sola iteración del cambio empresarial. Una vez que se han preparado una o más cargas de trabajo para pasarlas a producción, se produce una versión. La decisión de empaquetar una versión se realiza cuando las cargas de trabajo migradas representan un valor empresarial suficiente para justificar la inserción del cambio en un entorno empresarial. Las versiones se ejecutan junto con [un plan de cambio empresarial](../optimize/business-change-plan.md), después de haber realizado [pruebas empresariales](../optimize/business-test.md). El equipo de estrategia en la nube es responsable de planear y supervisar la ejecución de una versión para asegurarse de que se publica el cambio empresarial deseado.

Un *trabajo pendiente de versión* es el plan de estado futuro que define una versión próxima. El trabajo pendiente de versión es el punto de inflexión entre la administración de cambios empresariales (*trabajo pendiente de migración*) y la administración de cambios técnicos (*trabajo pendiente de sprint*). Un trabajo pendiente de versión consiste en una lista de cargas de trabajo del trabajo pendiente de migración que están alineadas con la realización de un subconjunto específico de resultados empresariales. La definición y el envío de un trabajo pendiente de versión al equipo de adopción de la nube sirven como desencadenador para un análisis más profundo y el planeamiento de la migración. Una vez que el equipo de adopción de la nube ha comprobado los detalles técnicos asociados a una versión, puede optar por confirmar la versión y establecer una escala de tiempo basada en el conocimiento actual.

Dado el grado de análisis necesario para validar una versión, el equipo de estrategia en la nube debe mantener una lista activa de las dos a cuatro versiones siguientes. El equipo también debe intentar validar la información siguiente en la medida de lo posible, antes de definir y enviar una versión. Un equipo de estrategia en la nube disciplinado capaz de mantener las cuatro versiones siguientes puede aumentar considerablemente la coherencia y la precisión de los cálculos de escala de tiempo para las versiones.

### <a name="release-backlog-data-points"></a>Puntos de datos del trabajo pendiente de versión

Los equipos de estrategia en la nube y de adopción de la nube deben colaborar para agregar los siguientes puntos de datos para cualquier carga de trabajo en el trabajo pendiente de versión:

- **Inventario refinado.** Validación de los recursos necesarios que se van a migrar. A menudo se validan con datos de registro o de supervisión a nivel de host, de la red o del sistema operativo para asegurar un conocimiento preciso de las dependencias de red y de hardware de cada recurso con una carga estándar.
- **Patrones de uso.** Comprensión de los patrones de uso de los usuarios finales. Estos patrones suelen incluir un análisis de la distribución geográfica de los usuarios finales, las rutas de red, los picos de uso temporales, los picos de uso por día y hora, y la composición de los usuarios finales (internos o externos).
- **Expectativas de rendimiento.** Análisis de los datos de registro disponibles que capturan el rendimiento, las vistas de páginas, las rutas de red y otros datos de rendimiento necesarios para replicar la experiencia del usuario final.
- **Dependencias.** Análisis del tráfico de red y de los patrones de uso de las aplicaciones para identificar otras dependencias posibles de las cargas de trabajo, que deben factorizarse en una secuenciación y en la preparación del entorno. No incluya una carga de trabajo en una versión hasta que se cumpla alguno de los siguientes criterios:
  - Todas las cargas de trabajo dependientes se han migrado.
  - Las configuraciones de red y de seguridad se han implementado para permitir que la carga de trabajo tenga acceso a todas las dependencias en línea con las expectativas de rendimiento actuales.
- **Estrategia de migración deseada.** En el nivel de trabajo pendiente de migración, el trabajo de migración supuesto es la única consideración que se usa en el análisis. Por ejemplo, si el resultado empresarial es la salida de un centro de datos actual, se supone que todas las migraciones son un escenario de rehospedaje en el trabajo pendiente de migración. En el trabajo pendiente de versión, los equipos de estrategia en la nube y de adopción de la nube deben evaluar el valor a largo plazo de características adicionales, la modernización y las inversiones continuas en desarrollo para evaluar si debe utilizarse un enfoque más moderno.
- **Criterios para pruebas empresariales.** Una vez agregada una carga de trabajo al trabajo pendiente de migración, deben acordarse los criterios de prueba. En algunos casos, los criterios de prueba se pueden limitar a una prueba de rendimiento con un grupo de usuarios avanzados definido. Sin embargo, para la validación estadística, es preferible una prueba de rendimiento automatizada y debe incluirse. A menudo, la instancia actual de la aplicación no tiene ninguna funcionalidad de pruebas automatizadas. En estos casos, no es raro que los arquitectos de la nube trabajen con usuarios avanzados para crear una prueba de carga de referencia para la solución actual con el fin de establecer un banco de pruebas que se usará durante la migración.

### <a name="release-backlog-cadence"></a>Cadencia del trabajo pendiente de versión

En migraciones consolidadas, las versiones tienen una cadencia periódica. La velocidad del equipo de adopción de la nube a menudo se normaliza y se produce una versión cada dos a cuatro iteraciones (aproximadamente cada uno o dos meses). Sin embargo, debe ser un resultado natural. La creación de cadencias de versión artificiales puede afectar negativamente a la capacidad del equipo de adopción de la nube de lograr un rendimiento constante.

Para estabilizar el impacto de negocio, el equipo de estrategia en la nube debe establecer un proceso de versión mensual con la empresa para mantener un diálogo regular, pero también debe crear la expectativa de que serán necesarios varios meses para que se pueda predecir una cadencia de versión periódica.

## <a name="sprint-or-iteration-backlog-aligning-technical-change-and-effort"></a>Trabajo pendiente de sprint o iteración: alineación del cambio técnico y el trabajo

Un *sprint*, o *iteración*, es una unidad de trabajo coherente con un plazo determinado. En el proceso de migración, suele medirse en incrementos de dos semanas. Sin embargo, no es raro que se tengan iteraciones de una semana o de cuatro semanas. La creación de iteraciones con un plazo determinado obliga a tener intervalos de finalización del trabajo coherentes y permite ajustarse a los planes con más frecuencia, en función de los nuevos conocimientos. Durante un sprint determinado, suele haber tareas para la evaluación, la migración y la optimización de las cargas de trabajo definidas en el trabajo pendiente de migración. Debe realizarse un seguimiento de estas unidades de trabajo y deben administrarse con la misma herramienta de administración de proyectos que la migración y el trabajo pendiente de versión, con el fin de favorecer la coherencia en cada nivel de la administración de cambios.

Un *trabajo pendiente de sprint*, o *trabajo pendiente de iteración*, consiste en el trabajo técnico que debe realizarse en un único sprint (o iteración), abordando la migración de recursos individuales. Ese trabajo debe derivarse de la lista de cargas de trabajo que se van a migrar. Cuando se usan herramientas como Azure DevOps (antes conocido como Visual Studio Online) para la administración de proyectos, los elementos de trabajo de un sprint serían elementos secundarios de los elementos de trabajo pendiente del producto en un trabajo pendiente de versión y las epopeyas en un trabajo pendiente de migración. Esta relación principal-secundario aporta claridad en todos los niveles de la administración de cambios.

Dentro de un solo sprint o una iteración, el equipo de adopción de la nube trabajaría para ofrecer la cantidad de trabajo técnico confirmada, con el fin de migrar una carga de trabajo definida. Este es el resultado final de la estrategia de administración de cambios. Una vez finalizado este trabajo, se puede probar validando la preparación para producción de una carga de trabajo almacenada provisionalmente en la nube.

### <a name="large-or-complex-sprint-structures"></a>Estructuras de sprint grandes o complejas

Para una migración pequeña con un equipo de migración independiente, un solo sprint podría incluir las cuatro fases de la migración para una sola carga de trabajo (*evaluación*, *migración*, *optimización* y *protección y administración*). Normalmente, cada uno de estos procesos se comparte entre varios equipos en elementos de trabajo diferentes en varios sprints. En función del tipo de trabajo, la escala de trabajo y los roles, estos sprints pueden tener formas diferentes.

- **Factoría de migración.** A veces, las migraciones a gran escala requieren un enfoque similar al de una fábrica en el modelo de ejecución. En este modelo, se asignan varios equipos a la ejecución de un proceso (o subconjunto del proceso) de migración específico. Una vez finalizado, la salida del sprint de un equipo rellena el trabajo pendiente del equipo siguiente. Este enfoque es eficaz para migraciones de rehospedaje a gran escala de muchas cargas de trabajo posibles que implican miles de máquinas virtuales pasando por las fases de evaluación, arquitectura, corrección y migración. Sin embargo, para que este enfoque funcione, es imprescindible un entorno homogéneo con procesos optimizados de aprobación y administración de cambios.
- **Oleadas de migración.** Otro enfoque que funciona bien para migraciones de gran envergadura es un modelo por oleadas. En este modelo, la división del trabajo no está tan clara. Los equipos se dedican a ejecutar procesos de migración de cargas de trabajo individuales. Sin embargo, la naturaleza de cada sprint cambia. En un sprint, el equipo puede completar el trabajo de evaluación y de arquitectura. En otro sprint, puede completar el trabajo de migración. En otro sprint, la atención estaría en la optimización y en la versión para producción. Este enfoque permite que un equipo central permanezca alineado con las cargas de trabajo y las vea a lo largo del proceso en su totalidad. Cuando se usa este enfoque, la diversidad de conocimientos y el cambio de contexto puede reducir la velocidad potencial del equipo y ralentizar así el trabajo de migración. Además, los obstáculos durante los ciclos de aprobación pueden dar lugar a retrasos considerables. Con este modelo, es importante mantener opciones en el trabajo pendiente de versión para que el equipo no se quede parado durante los períodos de bloqueo. También es importante el aprendizaje cruzado de los miembros del equipo y asegurarse de que los conocimientos sean los adecuados para el tema de cada sprint.

### <a name="sprint-backlog-data-points"></a>Puntos de datos del trabajo pendiente de sprint

El resultado de un sprint captura y documenta los cambios realizados en una carga de trabajo, con lo que se cierra el bucle de administración de cambios. Una vez finalizado, debe documentarse, como mínimo, lo siguiente. A lo largo de la ejecución de un sprint, esta documentación debe completarse junto con los elementos de trabajo técnico.

- **Recursos implementados.** Todos los recursos implementados en la nube para hospedar la carga de trabajo.
- **Corrección.** Cambios realizados en los recursos con el fin de prepararlos para la migración a la nube.
- **Configuración.** Configuración elegida de los recursos implementados, incluidas las referencias a los scripts de configuración.
- **Modelo de implementación.** Enfoque usado para implementar el recurso en la nube, incluidas las referencias a cualquier script o herramienta de implementación.
- **Arquitectura.** Documentación de la arquitectura implementada en la nube.
- **Métricas de rendimiento.** Salida de pruebas automatizadas o pruebas empresariales realizadas para validar el rendimiento en el momento de la implementación.
- **Configuración o requisitos únicos.** Cualquier aspecto único de la implementación, la configuración o los requisitos técnicos necesarios para el funcionamiento de la carga de trabajo.
- **Aprobación operativa.** Aprobación que valida la preparación operativa que proporcionan el propietario de la aplicación y el personal de operaciones de TI responsable de administrar la carga de trabajo después de la implementación.
- **Aprobación de la arquitectura.** Aprobación del propietario de la carga de trabajo y del equipo de adopción de la nube que valida los cambios de arquitectura necesarios para hospedar cada recurso.

## <a name="next-steps"></a>Pasos siguientes

Una vez establecidos los enfoques de administración de cambios, es el momento de abordar el último requisito previo, la [revisión del trabajo pendiente de migración](./migration-backlog-review.md)

> [!div class="nextstepaction"]
> [Revisión del trabajo pendiente de migración](./migration-backlog-review.md)
