---
title: Funciones de TI centralizadas
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Más información sobre la formación de funciones de TI centralizadas.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 54e08a42a64d06005620b450b1458288316df74e
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224020"
---
# <a name="central-it-capabilities"></a>Funciones de TI centralizadas

A medida que se escala la adopción de la nube, puede que las funcionalidades de gobernanza de la nube no sean suficientes por sí solas para gobernar los esfuerzos de adopción. Si la adopción es gradual, los equipos tienden a desarrollar orgánicamente las aptitudes y los procesos necesarios para estar preparados para la nube con el tiempo.

Sin embargo, cuando un equipo de adopción de la nube aprovecha la nube para lograr un resultado empresarial de alto perfil, este rara vez es el caso. El éxito llama al éxito. Esto también es cierto en la adopción de la nube, pero se produce en la escala de la nube. Cuando la adopción de la nube se amplía de un equipo a varios equipos en un período de tiempo relativamente corto, se necesita soporte adicional por parte del personal de TI existente. Sin embargo, es posible que ese personal no tenga el entrenamiento y la experiencia necesarios para dar soporte técnico a la nube mediante herramientas de TI nativas en la nube. Esto a menudo conduce a la formación de un equipo de TI central que gobierna la nube.

> [!CAUTION]
> Aunque se trata de un paso habitual del proceso de consolidación, su adopción puede suponer un riesgo elevado y es posible que bloquee los esfuerzos de innovación y migración si no se administra correctamente. Consulte la sección sobre riesgos que aparece a continuación para aprender a mitigar el riesgo de que la centralización se convierta en un antipatrón cultural.

## <a name="possible-sources-for-central-it-expertise"></a>Posibles fuentes de conocimientos de TI centralizados

Las aptitudes necesarias para proporcionar funciones de TI centralizadas pueden proceder de:

- Un equipo de TI central ya existente
- Arquitectos empresariales
- Operaciones de TI
- Gobernanza de TI
- Infraestructura de TI
- Redes
- Identidad
- Virtualización
- Continuidad empresarial y recuperación ante desastres
- Propietarios de aplicaciones dentro de TI

> [!WARNING]
> Las funciones de TI centralizadas solo se deberían aplicar en la nube si el entorno local existente de trabajo se basa en un modelo de TI centralizado. Si el modelo local actual se basa en el control delegado, considere la posibilidad de emplear un enfoque con un centro de excelencia de la nube (CCoE) como una alternativa más adecuada.

## <a name="key-responsibilities"></a>Principales responsabilidades

Adapte los procedimientos de TI existentes para asegurarse de que los esfuerzos de adopción den como resultado entornos bien gobernados y bien administrados en la nube.

Las siguientes tareas se ejecutan normalmente con regularidad:

### <a name="strategic-tasks"></a>Tareas estratégicas

- Revisión:
  - [Resultados empresariales](../strategy/business-outcomes/index.md)
  - [Modelos financieros](../strategy/financial-models.md)
  - [Motivaciones para la adopción de la nube](../strategy/motivations.md)
  - [Riesgos empresariales](../govern/policy-compliance/risk-tolerance.md)
  - [Racionalización del patrimonio digital](../digital-estate/index.md)
- Supervisión de los planes de adopción y del progreso en comparación con los [trabajos pendientes de migración prioritarios](../migrate/migration-considerations/assess/release-iteration-backlog.md).
- Identificación y clasificación por orden de prioridad de los cambios necesarios para dar soporte a los trabajos pendientes de la migración.
- Actuar como un nivel intermedio o de traducción entre las necesidades de adopción de la nube y los equipos de TI existentes.
- Aprovechar los equipos de TI existentes para acelerar las funciones de la plataforma y permitir la adopción.

### <a name="technical-tasks"></a>Tareas técnicas

- Creación y mantenimiento de la plataforma en la nube que admita las soluciones.
- Definición e implementación de la arquitectura de la plataforma.
- Funcionamiento y administración de la plataforma en la nube.
- Mejora continua de la plataforma.
- Mantenerse al día de las innovaciones en la plataforma de nube.
- Proporcionar nuevas funciones de nube que promuevan la creación de valor empresarial.
- Sugerir soluciones de autoservicio.
- Asegurarse de que las soluciones cumplen los requisitos de gobernanza y cumplimiento existentes.
- Creación y validación de la implementación de la arquitectura de la plataforma.
- Revisión de los planes de lanzamiento para conocer el origen de los nuevos requisitos de la plataforma.

## <a name="meeting-cadence"></a>Cadencia de las reuniones

Normalmente, los conocimientos de TI centralizados proceden de un equipo de trabajo. Se espera que los participantes se comprometan a emplear gran parte de sus programaciones diarias en los esfuerzos de alineación. Las contribuciones no se limitan a reuniones y ciclos de comentarios.

## <a name="central-it-risks"></a>Riesgos de las funciones de TI centralizadas

Cada una de las funcionalidades de la nube y las fases de madurez de la organización van acompañadas de la palabra "nube". Las funciones de TI centralizadas son la única excepción. Las funciones de TI centralizadas son las más frecuentes cuando todos los recursos de TI se pueden hospedar en varias ubicaciones y un número reducido de equipos puede administrarlas y controlarlas mediante una única plataforma de administración de operaciones. Los procedimientos empresariales globales y la economía digital han reducido en gran medida las instancias de tales entornos de administración centralizados.

Desde el punto de vista más actual de TI, los recursos se distribuyen globalmente. Las responsabilidades se delegan. La administración de las operaciones se proporciona gracias a una combinación de personal interno, proveedores de servicios administrados y proveedores de servicios en la nube. En cuanto a la economía digital, los procedimientos de administración de TI están evolucionando a un modelo de control delegado y de autoservicio con claras directrices de seguridad para aplicar la gobernanza. Un equipo de TI centralizado puede resultar un gran colaborador para la adopción de la nube si se convierte en agente y asociado de la nube para impulsar la innovación y la agilidad empresarial.

Un equipo de TI centralizado se encuentra en una buena posición para recabar conocimientos y procedimientos valiosos a partir de los modelos locales existentes y aplicar esos procedimientos para la implementación de la nube. No obstante, este proceso necesita cambios. Se necesitan nuevos procesos, nuevas aptitudes y nuevas herramientas para promover la adopción de la nube a escala. Cuando se adapta el equipo de TI centralizado, se convierte en un asociado importante para los esfuerzos de adopción de la nube. Sin embargo, si el equipo de TI centralizado no se adapta a la nube, o si intenta usar esta como un catalizador para imponer unos controles más estrictos, este equipo se convierte rápidamente en un elemento de bloqueo para los trabajos de adopción, innovación y migración.

Los valores para medir este riesgo son la velocidad y la flexibilidad. La nube simplifica la adopción de nuevas tecnologías rápidamente. Cuando hay nuevas funcionalidades de la nube que se pueden implementar en cuestión de minutos, pero las revisiones del equipo de TI centralizado agregan semanas o meses al proceso de implementación, estos procesos centralizados se convierten en un obstáculo importante para el éxito empresarial. Si se encuentra este indicador, considere la posibilidad de usar estrategias alternativas a la entrega de TI.

### <a name="exceptions"></a>Excepciones

Muchos sectores requieren una estricta adhesión a requisitos de cumplimiento de terceros. Algunos requisitos de cumplimiento siguen demandando un control de TI centralizado. Proporcionar estas medidas de cumplimiento puede agregar tiempo a los procesos de implementación, especialmente en el caso de nuevas tecnologías que no se han usado ampliamente. En estos casos, espere retrasos en la implementación durante las primeras fases de la adopción. Pueden existir situaciones similares para las empresas que trabajan con información confidencial de los clientes, pero que no están gobernadas por un requisito de cumplimiento de terceros.

### <a name="operating-within-the-exceptions"></a>Funcionamiento en las excepciones

Si se requieren procesos de TI centralizados y esos procesos crean puntos de control apropiados en la adopción de nuevas tecnologías, estos puntos de control de la innovación se pueden abordar con rapidez. Los requisitos de gobernanza y cumplimiento están diseñados para proteger la información confidencial, no para proteger todo tipo de información. La nube proporciona mecanismos sencillos para adquirir e implementar recursos aislados manteniendo barreras de seguridad adecuadas.

Un equipo de TI centralizado maduro mantiene las protecciones necesarias, pero negocia procedimientos que siguen permitiendo la innovación. La demostración de este nivel de madurez depende de una adecuada clasificación y aislamiento de los recursos.

### <a name="example-narrative-of-operating-within-exceptions-to-empower-adoption"></a>Ejemplo de narrativa de funcionamiento en las excepciones para habilitar la adopción

Este ejemplo de narrativa sirve para ilustrar el enfoque adoptado por un equipo de TI centralizado maduro para habilitar la adopción.

Contoso LLC ha adoptado un modelo de TI centralizado para dar soporte a los recursos en la nube de la empresa. Para proporcionar este modelo, han implementado controles estrictos para varios servicios compartidos, como las conexiones de red de entrada. Esta medida prudente ha reducido la exposición de su entorno en la nube y ha proporcionado un único dispositivo de "emergencia" para bloquear todo el tráfico en caso de que se produzca una infracción. Sus directivas de base de referencia de la seguridad establecen que todo el tráfico de entrada debe pasar por un dispositivo compartido que administra el equipo de TI centralizado.

Sin embargo, uno de sus equipos de adopción de la nube necesita ahora un entorno con una conexión de red de entrada dedicada y configurada especialmente para aprovechar una tecnología en la nube concreta. Un equipo de TI centralizado inmaduro simplemente rechazaría la solicitud y daría prioridad a los procesos existentes en lugar de a las necesidades de adopción. El equipo de TI centralizado de Contoso es diferente. Han identificado rápidamente una solución sencilla de cuatro partes a este dilema: Clasificación, negociación, aislamiento y automatización.

**Clasificación:** Dado que el equipo de adopción de la nube se encontraba en las primeras fases de la creación de una nueva solución y no tenía ninguna información confidencial ni necesidades de soporte técnico críticas, los recursos del entorno se clasificaron como de bajo riesgo y no críticos. Una clasificación efectiva es un signo de madurez del equipo de TI centralizado. La clasificación de todos los recursos y entornos permite directivas más claras.

**Negociación:** Solo la clasificación no es suficiente. Se implementaron servicios compartidos para trabajar de forma coherente con recursos confidenciales y críticos. El cambio de las reglas pondría en peligro las directivas de cumplimiento y gobernanza diseñadas para los recursos que necesitan más protección. No se puede habilitar la adopción a costa de poner en peligro la estabilidad, seguridad o gobernanza. Esto condujo a una negociación con el equipo de adopción para dar respuesta a preguntas específicas. ¿Podría un equipo de desarrollo y operaciones dirigido por la empresa proporcionar administración de operaciones para este entorno? ¿Requeriría esta solución acceso directo a otros recursos internos? Si el equipo de adopción de la nube acepta estos inconvenientes, puede que el tráfico de entrada sea posible.

**Aislamiento:** Como la empresa puede proporcionar su propia administración de las operaciones en curso y dado que la solución no depende del tráfico directo a otros recursos internos, esta se puede aislar en una nueva suscripción. Esa suscripción también se agrega a un nodo independiente de la nueva jerarquía del grupo de administración.

**Automation:** Otro signo de madurez de este equipo son sus principios de automatización. El equipo usa Azure Policy para automatizar la aplicación de directivas. También usan Azure Blueprints para automatizar la implementación de los componentes habituales de la plataforma y aplicar la adhesión a la base de referencia de la identidad definida. Para esta suscripción y cualquier otra del nuevo grupo de administración, las directivas y plantillas son ligeramente diferentes. Se han suprimido las directivas que bloqueaban el ancho de banda de entrada. Se han sustituido por requisitos para enrutar el tráfico a través de la suscripción de los servicios compartidos, como cualquier tráfico de entrada, para aplicar el aislamiento del tráfico. Dado que las herramientas de administración de operaciones del entorno local no pueden acceder a esta suscripción, los agentes de esa herramienta ya no son necesarios. Las demás barreras de seguridad de la gobernanza que requieren otras suscripciones de la jerarquía del grupo de administración se siguen aplicando, lo que garantiza que haya suficientes barreras de seguridad.

El enfoque creativo maduro del equipo de TI centralizado de Contoso ofreció una solución que no ponía en peligro ni la gobernanza ni el cumplimiento, y que fomentaba la adopción. Este enfoque de intermediación en lugar de los enfoques de propiedad nativos en la nube para conseguir un equipo de TI centralizado es el primer paso hacia la creación de un verdadero centro de excelencia de la nube (CCoE). La adopción de este enfoque para desarrollar rápidamente las directivas existentes le permitirá tener un control centralizado si es necesario y barreras de seguridad de gobernanza cuando una mayor flexibilidad sea aceptable. El equilibrio entre estos dos aspectos mitiga los riesgos asociados a un equipo de TI centralizado en la nube.

## <a name="next-steps"></a>Pasos siguientes

A medida que va madurando el equipo de TI centralizado, el siguiente paso de madurez es normalmente el acoplamiento débil de las [operaciones en la nube](./cloud-operations.md). La disponibilidad de herramientas de administración de operaciones nativas en la nube y unos costos operativos más bajos de las soluciones basadas en PaaS, a menudo conducen a los equipos empresariales (o, más concretamente, a los equipos de desarrollo y operaciones de la empresa) a asumir la responsabilidad de las operaciones en la nube.

> [!div class="nextstepaction"]
> [Funcionalidades de operaciones en la nube](./cloud-operations.md)
