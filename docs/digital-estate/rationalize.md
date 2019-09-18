---
title: Racionalización del patrimonio digital
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Evalúe sus recursos digitales para determinar la mejor manera de hospedarlos en la nube.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: governance
ms.openlocfilehash: 7bb9eb697beb44aa5bf4e9eec736a5be4b575eb7
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70837786"
---
# <a name="rationalize-the-digital-estate"></a>Racionalización del patrimonio digital

La racionalización de la nube es el proceso de evaluación de los recursos para determinar el mejor enfoque para hospedarlos en la nube. Una vez que haya determinado el [enfoque](approach.md) y que haya agregado un [inventario](inventory.md), puede comenzar la racionalización de la nube. En [Racionalización de la nube](rationalize.md) se describen las opciones de racionalización más comunes.

## <a name="traditional-view-of-rationalization"></a>Vista tradicional de la racionalización

La racionalización es fácil de entender cuando el proceso tradicional de racionalización se visualiza como un árbol de decisión complejo. Cada recurso del patrimonio digital se introduce mediante un proceso que da como resultado una de las cinco respuestas (las 5 R). Para pequeños patrimonios, este proceso funciona bien. Para patrimonios mayores, no es eficaz y puede dar lugar a retrasos importantes. Vamos a examinar el proceso para comprender el motivo. Después, presentaremos un modelo más eficiente.

**Inventario.** Se requiere un inventario completo de los recursos, incluidas aplicaciones, software, hardware, sistemas operativos y métricas de rendimiento del sistema para completar una racionalización completa mediante modelos tradicionales.

**Análisis cuantitativo.** En el árbol de decisión, las preguntas cuantitativas conducen a la primera capa de decisiones. Estas son algunas de las preguntas más habituales: ¿Está el recurso en uso hoy en día? Si es así, ¿está optimizado y dimensionado correctamente? ¿Qué dependencias existen entre los recursos? Estas preguntas son fundamentales para la clasificación del inventario.

**Análisis cualitativo.** El siguiente conjunto de decisiones requiere inteligencia humana en forma de análisis cualitativo. A menudo, estas preguntas son exclusivas de la solución y solo las partes interesadas de la empresa y los usuarios avanzados pueden responderlas. Estas decisiones son las que generalmente retrasan el proceso y ralentizan todo considerablemente. Este análisis generalmente consume de 40 a 80 horas de empleados a tiempo completo por aplicación.

Para ver una guía sobre la elaboración de una lista de preguntas de análisis cualitativo, consulte [Enfoques de planeamiento del patrimonio digital](approach.md).

**Decisión de racionalización.** En manos de un equipo de racionalización experimentado, los datos cualitativos y cuantitativos crean decisiones claras. Desafortunadamente, los equipos con un alto grado de experiencia en racionalización son caros de contratar o tardan meses en entrenarse.

## <a name="rationalization-at-enterprise-scale"></a>Racionalización a escala empresarial

Si este esfuerzo consume mucho tiempo y es desalentador para un patrimonio digital de 50 máquinas virtuales, nos podemos imaginar el esfuerzo necesario para impulsar la transformación del negocio en un entorno con miles de máquinas virtuales y cientos de aplicaciones. El esfuerzo humano requerido puede fácilmente exceder las 1500 horas de empleados a tiempo completo y 9 meses de planeamiento.

Si bien la racionalización completa es el objetivo final y un gran camino a seguir, rara vez produce una elevada rentabilidad de la inversión con relación al tiempo y la energía requeridos.

Cuando la racionalización es esencial para las decisiones financieras, vale la pena considerar la posibilidad de usar una organización de servicios profesionales especializada en la racionalización de la nube para acelerar el proceso. Incluso así, la racionalización completa puede resultar un esfuerzo costoso y lento que retrase la transformación o los resultados del negocio.

En el resto de este artículo se describe un enfoque alternativo, conocido como racionalización incremental.

## <a name="incremental-rationalization"></a>Racionalización incremental

La racionalización completa de un gran patrimonio digital es propensa al riesgo y puede sufrir retrasos debido a su complejidad. El supuesto que subyace tras el enfoque incremental es que la demora en la toma de decisiones escalona la carga sobre el negocio y reduce el riesgo de obstáculos. Con el tiempo, este enfoque crea un modelo orgánico para desarrollar los procesos y la experiencia necesarios para tomar decisiones de racionalización cualificadas de manera más eficiente.

### <a name="inventory-reduce-discovery-data-points"></a>Inventario: Reducción de los puntos de datos de detección

Pocas organizaciones invierten el tiempo, la energía y los gastos necesarios para mantener un inventario preciso y en tiempo real de todo el patrimonio digital. La pérdida, el robo, los ciclos de actualización y la incorporación de empleados a menudo justifican el seguimiento detallado de los recursos de los dispositivos de los usuarios finales. Sin embargo, la rentabilidad de la inversión que supone mantener un inventario preciso de los servidores y las aplicaciones en un centro de datos local tradicional suele ser baja. La mayoría de las organizaciones de TI tienen otros problemas más urgentes que resolver que el seguimiento del uso de los recursos en un centro de datos.

En una transformación a la nube, el inventario está directamente relacionado con los costos operativos. Se requieren datos de inventario precisos para un planeamiento adecuado. Lamentablemente, las opciones actuales de análisis del entorno pueden retrasar las decisiones durante semanas o meses. Afortunadamente, hay algunos trucos que pueden acelerar la recopilación de los datos.

El análisis basado en agente es el retraso citado con más frecuencia. Los datos sólidos que se requieren para una racionalización tradicional a menudo solo pueden recopilarse con un agente que se ejecuta en cada recurso. Esta dependencia de los agentes ralentiza el progreso porque puede requerir comentarios de las funciones de seguridad, operaciones y administración.

En un proceso de racionalización incremental, se podría utilizar una solución sin agentes para una detección inicial a fin de acelerar las decisiones tempranas. En función del nivel de complejidad del entorno, es posible que siga siendo necesaria una solución basada en agente. Sin embargo, se puede quitar de la ruta crítica para el cambio empresarial.

### <a name="quantitative-analysis-streamline-decisions"></a>Análisis cuantitativo: Optimización de las decisiones

Con independencia del enfoque de la detección de inventario, el análisis cuantitativo puede conducir a una serie de decisiones y supuestos iniciales. Esto es especialmente cierto cuando se trata de identificar la primera carga de trabajo o cuando el objetivo de la racionalización es una comparación de costos de alto nivel. En un proceso de racionalización incremental, los equipos de adopción y estrategia de la nube limitan las [5 R de la racionalización](5-rs-of-rationalization.md) a dos decisiones concisas y solo aplican esos factores cuantitativos. Esto simplifica el análisis y reduce la cantidad de datos iniciales necesarios para impulsar el cambio.

Por ejemplo, si una organización se encuentra en medio de una migración de IaaS a la nube, se puede suponer que la mayoría de las cargas de trabajo se retirarán o se volverán a hospedar.

### <a name="qualitative-analysis-temporary-assumptions"></a>Análisis cualitativo: Supuestos temporales

Al reducir el número de resultados potenciales, es más fácil tomar una decisión inicial sobre el estado futuro de un recurso. Cuando se reducen las opciones, también se reduce el número de preguntas que se formulan a la empresa en esta fase inicial.

Por ejemplo, si las opciones se limitan a rehospedar o retirar, la empresa solo debe responder a una pregunta durante la racionalización inicial, que es si se va a retirar el recurso.

"El análisis sugiere que ningún usuario está utilizando activamente este recurso. ¿Es eso correcto o se nos ha pasado algo por alto?" Una pregunta binaria de este tipo es generalmente mucho más fácil de ejecutar mediante un análisis cualitativo.

Este enfoque simplificado produce líneas de base, planes financieros, estrategia y dirección. En actividades posteriores, cada recurso pasa por una mayor racionalización y un análisis cualitativo para evaluar otras opciones. Todas las suposiciones que realice en esta racionalización inicial se prueban antes.

## <a name="challenge-assumptions"></a>Supuestos desafiantes

El resultado de la sección anterior es una racionalización aproximada cargada de supuestos. A continuación, es hora de cuestionar algunos de estos supuestos.

### <a name="retire-assets"></a>Retirar recursos

En un entorno local tradicional, hospedar recursos pequeños no utilizados rara vez tiene un impacto significativo en los costos anuales. Con algunas excepciones, el ahorro de costos derivado de la limpieza y retirada de estos recursos se compensa por el tiempo de empleados a tiempo completo requerido para analizar y retirar el recurso.

Sin embargo, cuando se pasa a un modelo de contabilidad en la nube, la retirada de recursos puede producir ahorros significativos en los costos operativos anuales y en los esfuerzos iniciales de migración.

No es raro que las organizaciones retiren el 20 % o más de su patrimonio digital después de completar un análisis cuantitativo. Es recomendable realizar un análisis cualitativo adicional antes de decidir sobre dicha acción. Una vez confirmada, la retirada de esos recursos puede producir la primera victoria de la migración a la nube en cuanto a la rentabilidad de la inversión. En muchos casos, este es uno de los mayores factores de ahorro de costos. Como tal, es recomendable que el equipo de estrategia de la nube supervise la validación y la retirada de los recursos, en paralelo a la fase de creación del proceso de migración, para permitir una ganancia financiera temprana.

### <a name="program-adjustments"></a>Ajustes del programa

Una empresa rara vez se embarca en un único viaje de transformación. La elección entre reducción de costos, crecimiento del mercado y nuevas fuentes de ingresos rara vez es una decisión binaria. Por lo tanto, es recomendable que el equipo de estrategia de la nube trabaje con el departamento de TI para identificar los recursos que haya en esfuerzos de transformación paralelos y que estén fuera del alcance del recorrido de transformación principal.

En el ejemplo de migración de IaaS que se utiliza en este artículo:

- Pida al equipo de DevOps que identifique los recursos que ya forman parte de una automatización de la implementación y los quite del plan de migración principal.

- Pida a los equipos de datos e I+D que identifiquen los recursos que impulsan nuevas fuentes de ingresos y que los quiten del plan de migración principal.

Este análisis cualitativo enfocado en el programa se puede ejecutar rápidamente y producirá la alineación de los diferentes trabajos pendientes de migración.

Tal vez tenga que considerar algunos recursos para rehospedaje durante un tiempo. Puede realizar una racionalización posterior después de la migración inicial.

## <a name="select-the-first-workload"></a>Seleccionar la primera carga de trabajo

Implementar la primera carga de trabajo es clave para realizar pruebas y aprender. Es la primera oportunidad para demostrar y crear una mentalidad de crecimiento.

### <a name="business-criteria"></a>Criterios de negocio

Para garantizar la transparencia del negocio, identifique una carga de trabajo admitida por un miembro de la unidad de negocio del equipo de estrategia de la nube. Preferiblemente, elija una en la que el equipo tenga un interés personal y una fuerte motivación para pasarla a la nube.

### <a name="technical-criteria"></a>Criterios técnicos

Seleccione una carga de trabajo que tenga dependencias mínimas y que se pueda desplazar como un pequeño grupo de recursos. Se recomienda seleccionar una carga de trabajo con una ruta de pruebas definida para facilitar la validación.

La primera carga de trabajo se implementa a menudo en un entorno experimental sin capacidad operativa ni de gobernanza. Es muy importante seleccionar una carga de trabajo que no interactúe con datos seguros.

### <a name="qualitative-analysis"></a>Análisis cualitativo

Los equipos de adopción y estrategia de la nube pueden trabajar juntos para analizar esta pequeña carga de trabajo. Esta colaboración ofrece una oportunidad controlada de crear y probar criterios de análisis cualitativo. La población más pequeña ofrece la oportunidad de encuestar a los usuarios afectados para realizar un análisis cualitativo detallado en una semana o menos. Para conocer los factores comunes de análisis cualitativo, consulte el objetivo de racionalización específico en el documento [Las 5 R de la racionalización](5-rs-of-rationalization.md).

### <a name="migration"></a>Migración

Paralelamente a la racionalización continua, el equipo de adopción de la nube puede comenzar a migrar la pequeña carga de trabajo para ampliar el aprendizaje en las siguientes áreas clave:

- Reforzar las habilidades con la plataforma del proveedor de nube.
- Definir los servicios básicos (y estándar de Azure) necesarios para ajustarse a la visión a largo plazo.
- Comprender mejor cómo las operaciones pueden necesitar cambiar más adelante en la transformación.
- Comprender los riesgos inherentes al negocio y la tolerancia del negocio a dichos riesgos.
- Establecer un producto mínimamente viable (MVP) o de referencia para la gobernanza basado en la tolerancia al riesgo del negocio.

## <a name="release-planning"></a>Planeamiento de la versión

Mientras el equipo de adopción de la nube ejecuta la migración o implementación de la primera carga de trabajo, el equipo de estrategia de la nube puede empezar a priorizar las aplicaciones o cargas de trabajo restantes.

### <a name="power-of-10"></a>La potencia de 10

En el enfoque tradicional de la racionalización, se intentan abordar todas las necesidades previsibles. Afortunadamente, a menudo no se requiere un plan para cada aplicación para iniciar un viaje de transformación. En un modelo incremental, la potencia de 10 proporciona un buen punto de partida. En este modelo, el equipo de estrategia de la nube selecciona las primeras diez aplicaciones que se van a migrar. Esas diez cargas de trabajo deben contener una mezcla de cargas de trabajo simples y complejas.

### <a name="build-the-first-backlogs"></a>Creación de los primeros trabajos pendientes

Los equipos de adopción y estrategia de la nube pueden trabajar juntos en el análisis cualitativo de las diez primeras cargas de trabajo. Este esfuerzo crea el primer trabajo pendiente de migración con prioridad y el primer trabajo pendiente de versión con prioridad. Este enfoque permite a los equipos iterar sobre el enfoque y proporciona tiempo suficiente para crear un proceso adecuado para el análisis cualitativo.

### <a name="mature-the-process"></a>Maduración del proceso

Cuando los dos equipos se ponen de acuerdo sobre los criterios de análisis cualitativo, la evaluación puede convertirse en una tarea dentro de cada iteración. Alcanzar el consenso sobre los criterios de evaluación suele requerir dos o tres versiones.

Una vez que la evaluación se traslada a los procesos de ejecución incremental de la migración, el equipo de adopción de la nube puede iterar más rápidamente en la evaluación y arquitectura. En esta etapa, el equipo de estrategia de la nube también se abstrae, lo que reduce el consumo de su tiempo. Esto también permite que el equipo de estrategia de la nube se centre en priorizar las aplicaciones que aún no tienen una versión específica, lo que asegura una alineación ajustada con las condiciones cambiantes del mercado.

No todas las aplicaciones con prioridad estarán listas para la migración. Es probable que la secuencia cambie, ya que el equipo realiza un análisis cualitativo más profundo y descubre eventos y dependencias que podrían dar lugar a una nueva priorización de los trabajos pendientes. Algunas versiones pueden agrupar un pequeño número de cargas de trabajo. Otras podrían contener una única carga de trabajo.

Es probable que el equipo de adopción de la nube ejecute iteraciones que no produzcan una migración completa de la carga de trabajo. Cuanto menor sea la carga de trabajo y menor sea el número de dependencias, mayor será la probabilidad de que una carga de trabajo se adapte a un solo sprint o iteración. Por este motivo, es recomendable que las primeras aplicaciones de la lista de trabajos pendientes sean pequeñas y contengan pocas dependencias externas.

## <a name="end-state"></a>Finalización del estado

Con el tiempo, la combinación de los equipos de adopción y estrategia de la nube realizarán una racionalización completa del inventario. Sin embargo, este enfoque incremental permite a los equipos ser más ágiles en el proceso de racionalización. También permite que el recorrido de transformación produzca resultados de negocio tangibles antes, sin un esfuerzo de análisis inicial tan grande.

En algunos casos, el modelo financiero puede ser demasiado estricto para tomar una decisión sin una racionalización adicional. En estos casos, quizás sea necesario un enfoque más tradicional de la racionalización.

## <a name="next-steps"></a>Pasos siguientes

El resultado de un esfuerzo de racionalización es un trabajo pendiente priorizado de todos los recursos afectados por la transformación elegida. Este trabajo pendiente ya está listo para servir de base para los modelos de cálculo de costos de los servicios en la nube.

> [!div class="nextstepaction"]
> [Alineación de los modelos de costos con el patrimonio digital](calculate.md)
