---
title: ¿Qué papel desempeñan la replicación y sincronización en el proceso de migración?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Un proceso de la migración a la nube que se centra en las tareas de migración de cargas de trabajo.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 3e65631f0adf2584bbf0ee24b10d20df73ece715
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70839066"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-role-does-replication-play-in-the-migration-process"></a>¿Qué papel desempeña la replicación en el proceso de migración?

Los centros de datos locales se rellenan con recursos físicos como servidores, dispositivos y dispositivos de red. Sin embargo, cada servidor es solo un shell físico. El valor real procede de los datos binarios que se ejecutan en el servidor. Las aplicaciones y los datos constituyen el objetivo del centro de datos. Esos son los datos binarios principales que se van a migrar. Detrás de estas aplicaciones y de los almacenes de datos se encuentran otros recursos digitales y fuentes de datos binarios, como sistemas operativos, rutas de red, archivos y protocolos de seguridad.

La replicación es el verdadero caballo de batalla de los trabajos de migración. Es el proceso que consiste en copiar una versión en un momento dado de varios datos binarios. Posteriormente, las instantáneas de los datos binarios se copian en una nueva plataforma y se implementan en un hardware nuevo, en un proceso denominado *propagación*. Cuando se ejecuta correctamente, la copia propagada de los datos binarios se debe comportar de forma idéntica a los datos binarios originales en el hardware antiguo. Sin embargo, esa instantánea de los datos binarios deja de estar actualizada y alineada con la fuente original inmediatamente. Para mantener alineados los nuevos datos binarios y los antiguos existe un proceso denominado *sincronización* que continuamente actualiza la copia almacenada en la nueva plataforma. La sincronización continúa hasta que se promociona el recurso según el modelo de promoción elegido. En ese momento, se interrumpe la sincronización.

## <a name="required-prerequisites-to-replication"></a>Requisitos previos necesarios para la replicación

Antes de la replicación, la *nueva plataforma* y el hardware deben estar preparados para recibir las copias de los datos binarios. En el artículo sobre [requisitos previos](../prerequisites/index.md) se describen los requisitos mínimos del entorno para ayudar a crear una plataforma segura, sólida y eficaz para recibir las réplicas de los datos binarios.

Los *datos binarios de origen* también deben estar preparados para la replicación y la sincronización. Los artículos sobre evaluación, arquitectura y corrección abordan cada uno las acciones necesarias para asegurarse de que los datos binarios de origen están listos para la replicación y la sincronización.

Se debe implementar una *cadena de herramientas* que se alinee con la nueva plataforma y con los datos binarios de origen para ejecutar y administrar los procesos de replicación y sincronización. En el artículo sobre [opciones de replicación](./replicate-options.md) se describen varias herramientas que pueden contribuir a una migración a Azure.

## <a name="replication-risks---physics-of-replication"></a>Riesgos de la replicación: física de la replicación

Al planear la replicación de cualquier fuente de datos binarios en un nuevo destino, hay algunas leyes fundamentales que se deben tener en cuenta durante la planeación y la ejecución.

- **Velocidad de la luz.** Para mover grandes volúmenes de datos, la fibra sigue siendo la opción más rápida. Lamentablemente, este tipo de cables solo puede trasladar datos a dos tercios de la velocidad de la luz. Esto significa que no hay ningún método para la replicación instantánea o ilimitada de datos.
- **Velocidad de la canalización WAN.** De mayor importancia que la velocidad del movimiento de datos es el ancho de banda del vínculo superior, que define el volumen de datos por segundo que se pueden trasladar a través de la WAN existente de la compañía al centro de datos de destino.
- **Velocidad de expansión de WAN.** Si el presupuesto lo permite, se puede agregar ancho de banda adicional a la solución WAN de la empresa. Sin embargo, puede tardar semanas o meses en adquirir, aprovisionar e integrar conexiones de fibra adicionales.
- **Velocidad de los discos.** Aunque los datos pudieran moverse más rápidamente y no hubiera limitación del ancho de banda entre los datos binarios de origen y el destino, aún existiría otra limitación física. Los datos solo se pueden replicar a la velocidad a la que se pueden leer desde los discos de origen. Leer cada uno o cada cero de todos los discos en movimiento de un centro de datos lleva tiempo.
- **Velocidad de los cálculos humanos.** Los discos y la luz son infinitamente más rápidos que los procesos humanos de toma de decisiones. Cuando se necesita que un grupo de personas colabore y tome decisiones de forma conjunta, los resultados serán incluso más lentos. La replicación nunca podrá solventar los retrasos relacionados con la inteligencia humana.

Cada una de estas leyes físicas conlleva los siguientes riesgos que pueden afectar normalmente a los planes de migración:

- **Tiempo de replicación.** Las herramientas de replicación avanzadas no pueden ignorar las limitaciones físicas básicas. La replicación requiere tiempo y ancho de banda. Los planes deben incluir escalas de tiempo realistas que reflejen la cantidad de tiempo que se tarda en replicar los datos binarios. El *ancho de banda total disponible para la migración* es la cantidad de ancho de banda ascendente, medida en megabits por segundo (Mbps) o gigabits por segundo (Gbps), que no consumen otras necesidades empresariales de mayor prioridad. El *almacenamiento total de migración* es el espacio total en disco, medido en gigabytes o terabytes, necesario para almacenar una instantánea de todos los recursos que se van a migrar. Se puede calcular una estimación del tiempo inicial dividiendo el *almacenamiento total de migración* por el *ancho de banda total disponible para la migración*. Observe la conversión de bits a bytes. Consulte la entrada siguiente, "Efectos acumulativos del desfase del disco", para obtener un cálculo de tiempo más preciso.
- **Efectos acumulativos del desfase del disco.** Desde el punto de replicación al de promoción de un recurso a producción, los datos binarios de origen y destino deben estar sincronizados. El *desfase* de los datos binarios consume ancho de banda adicional, ya que se deben replicar los datos binarios de forma periódica. Durante la sincronización, se debe incluir todo el desfase de los datos binarios en el cálculo del almacenamiento total de la migración. Cuanto más tiempo se tarde en promocionar un recurso a producción, se acumulará un mayor desfase. Cuanto mayor es el número de recursos que se sincronizan, mayor es el ancho de banda consumido. Con cada recurso que se mantiene en estado de sincronización, se pierde un poco más del ancho de banda total disponible para la migración.
- **Tiempo para el cambio empresarial.** Como se mencionó en la entrada anterior, "Efectos acumulativos del desfase del disco", el tiempo de sincronización tiene un efecto negativo acumulativo en la velocidad de la migración. La priorización del trabajo pendiente de la migración y la preparación avanzada del [plan de cambio empresarial](../optimize/business-change-plan.md) es fundamental para la velocidad de la migración. La prueba más significativa de la alineación técnica y empresarial durante un esfuerzo de migración es el ritmo de promoción. Cuanto más rápido se pueda promocionar un recurso a producción, menor será el impacto del desfase de disco en el ancho de banda y mayor será el ancho de banda y el tiempo que se puedan asignar a la replicación de la siguiente carga de trabajo.

## <a name="next-steps"></a>Pasos siguientes

Una vez completada la replicación, pueden comenzar las [actividades de ensayo](./stage.md).

> [!div class="nextstepaction"]
> [Actividades de ensayo durante una migración](./stage.md)
