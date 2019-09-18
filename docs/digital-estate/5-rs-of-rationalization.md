---
title: Racionalización de la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Revise las opciones disponibles para racionalizar un patrimonio digital.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: governance
ms.openlocfilehash: 40962b8c658c40e4a27e3c025bc42b3aa5acd0f3
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71023613"
---
# <a name="cloud-rationalization"></a>Racionalización de la nube

La racionalización de la nube es el proceso de evaluar los recursos para determinar la mejor manera de migrar o modernizar cada activo en la nube. Para más información sobre el proceso de racionalización, vea [¿Qué es un patrimonio digital?](./index.md).

## <a name="rationalization-context"></a>Contexto de racionalización

Las cinco "R" de la racionalización que se mencionan en este artículo son una excelente manera de etiquetar un posible estado futuro para cualquier carga de trabajo que se esté considerando como candidato para la nube. Pero este proceso de etiquetado debe colocarse en el contexto correcto antes de intentar racionalizar un entorno. Eche un vistazo a estos mitos para proporcionar ese contexto:

- **Mito: Es fácil tomar decisiones de racionalización en las primeras etapas del proceso**. Para que la racionalización sea precisa, se necesitan amplios conocimientos de la carga de trabajo y los recursos asociados (aplicaciones, máquinas virtuales y datos). Lo más importante es que las decisiones de racionalización precisas tardan tiempo. Se recomienda usar un [proceso de racionalización incremental](./rationalize.md#incremental-rationalization).

- **Mito: La adopción de la nube tiene que esperar a que se racionalicen todas las cargas de trabajo**. La racionalización de una cartera de TI completa o incluso un único centro de datos puede retrasar la realización del valor empresarial en meses o incluso años. La racionalización completa debe evitarse siempre que sea posible. Es preferible usar el enfoque de [la eficacia de 10 para el planeamiento de la liberación](./rationalize.md#release-planning), para tomar decisiones acertadas sobre las 10 próximas cargas de trabajo que están programadas para la adopción en la nube.

- **Mito: La justificación empresarial tiene que esperar a que se racionalicen todas las cargas de trabajo**. Para desarrollar una justificación comercial para un esfuerzo de adopción en la nube, realice algunas suposiciones básicas en el nivel de cartera. Cuando las motivaciones están en la misma línea que la innovación, habrá que repetir la arquitectura. Cuando las motivaciones están en la misma línea que la migración, habrá que realizar un rehospedaje. Estas suposiciones pueden acelerar el proceso de justificación empresarial. Después, se cuestionan las suposiciones y se refinan los presupuestos durante la fase de evaluación de los ciclos de adopción de cada carga de trabajo.

Ahora eche un vistazo a las cinco "R" de la racionalización para familiarizarse con el proceso a largo plazo. Al desarrollar el plan de adopción de la nube, elija la opción que mejor se adapte a sus motivaciones, resultados empresariales y el entorno de estado actual. El objetivo de la racionalización del patrimonio digital es establecer una base de referencia, en lugar de racionalizar cada carga de trabajo.

## <a name="the-five-rs-of-rationalization"></a>Las cinco "R" de la racionalización

Las cinco "R" de la racionalización que se enumeran aquí describen las opciones más comunes para la racionalización.

## <a name="rehost"></a>Rehospedaje

También conocido como una migración "lift and shift", el rehospedaje cambia la ubicación del recurso de estado actual al proveedor de nube elegido, con un cambio mínimo en la arquitectura general.

Estos son los principales motivos para hacer un rehospedaje:

- Reducir los gastos de capital
- Liberar espacio en el centro de datos
- Conseguir una rápida rentabilidad de la inversión en la nube

Factores de análisis cuantitativo:

- Tamaño de máquina virtual (CPU, memoria, almacenamiento)
- Dependencias (tráfico de red)
- Compatibilidad de recursos

Factores de análisis cualitativo:

- Tolerancia al cambio
- Prioridades empresariales
- Eventos empresariales críticos
- Dependencias de procesos

## <a name="refactor"></a>Refactorización

Las opciones de plataforma como servicio (PaaS) pueden reducir los costos operativos asociados a muchas aplicaciones. Se aconseja refactorizar ligeramente una aplicación para ajustarla a un modelo basado en PaaS.

"Refactorizar" también hace referencia al proceso de desarrollo de aplicaciones de refactorizar el código para permitir que una aplicación satisfaga nuevas oportunidades de negocio.

Estos son los principales motivos para hacer un rehospedaje:

- Actualizaciones más rápidas y cortas
- Portabilidad del código
- Mayor eficiencia en la nube (recursos, velocidad, costo)

Factores de análisis cuantitativo:

- Tamaño de los recursos de la aplicación (CPU, memoria, almacenamiento)
- Dependencias (tráfico de red)
- Tráfico de usuarios (vistas de página, tiempo en la página, tiempo de carga)
- Plataforma de desarrollo (idiomas, plataforma de datos, servicios de nivel intermedio)

Factores de análisis cualitativo:

- Inversiones empresariales continuadas
- Ampliación de opciones y plazos
- Dependencias de procesos de negocio

## <a name="rearchitect"></a>Rediseño

Algunas aplicaciones antiguas no son compatibles con los proveedores de nube debido a las decisiones de arquitectura que se tomaron cuando se creó la aplicación. En estos casos, puede ser necesario rediseñar la aplicación antes de la transformación.

En otros casos, las aplicaciones que son compatibles con la nube, pero que no son nativas de la nube, podrían ser eficientes en cuanto a costos y operaciones si se rediseñara la solución para convertirla en una aplicación nativa de nube.

Estos son los principales motivos para hacer un rehospedaje:

- Agilidad y escalabilidad de la aplicación
- Adopción más fácil de nuevas funcionalidades de nube
- Mezcla de pilas de tecnología

Factores de análisis cuantitativo:

- Tamaño de los recursos de la aplicación (CPU, memoria, almacenamiento)
- Dependencias (tráfico de red)
- Tráfico de usuarios (vistas de página, tiempo en la página, tiempo de carga)
- Plataforma de desarrollo (idiomas, plataforma de datos, servicios de nivel intermedio)

Factores de análisis cualitativo:

- Crecientes inversiones empresariales
- Costos operativos
- Posibles bucles de comentarios e inversiones en DevOps.

## <a name="rebuild"></a>Recompilación

En algunos casos, los obstáculos que deben salvarse para llevar adelante una aplicación pueden ser demasiado grandes como para justificar la inversión. Esto ocurre especialmente en el caso de las aplicaciones que antes eran útiles para una empresa, pero que ya no son compatibles o no están en línea con los procesos empresariales actuales. En este caso, se crea una nueva base de código para alinearla con un enfoque [nativo de nube](https://azure.microsoft.com/overview/cloudnative).

Estos son los principales motivos para hacer un rehospedaje:

- Acelerar la innovación
- Crear aplicaciones más rápidas
- Reducir los costos operativos

Factores de análisis cuantitativo:

- Tamaño de los recursos de la aplicación (CPU, memoria, almacenamiento)
- Dependencias (tráfico de red)
- Tráfico de usuarios (vistas de página, tiempo en la página, tiempo de carga)
- Plataforma de desarrollo (idiomas, plataforma de datos, servicios de nivel intermedio)

Factores de análisis cualitativo:

- Rechazar la satisfacción del usuario final
- Procesos de negocio limitados por funcionalidad
- Posibles ganancias de costo, experiencia o ingresos

## <a name="replace"></a>Replace

Las soluciones suelen implementarse usando la mejor tecnología y el enfoque que haya disponible en ese momento. A veces, las aplicaciones de software como servicio (SaaS) pueden proporcionar todas las funciones necesarias para la aplicación hospedada. En estos casos, se puede programar una carga de trabajo para reemplazarla en el futuro y eliminarla de manera eficaz del esfuerzo de transformación.

Estos son los principales motivos para hacer un rehospedaje:

- Estandarizar en torno a procedimientos recomendados del sector
- Acelerar la adopción de enfoques basados en procesos de negocio
- Reasignar inversiones en el desarrollo de aplicaciones que crean diferenciación o ventaja competitivas

Factores de análisis cuantitativo:

- Reducciones generales de costos operativos
- Tamaño de máquina virtual (CPU, memoria, almacenamiento)
- Dependencias (tráfico de red)
- Activos que se van a retirar

Factores de análisis cualitativo:

- Análisis de costo/beneficio de la arquitectura actual frente a la solución SaaS
- Asignaciones de procesos de negocio
- Esquemas de datos
- Procesos automatizados o personalizados

## <a name="next-steps"></a>Pasos siguientes

En conjunto, puede aplicar estos cinco puntos esenciales de la racionalización a un patrimonio digital para que sea más fácil tomar decisiones de racionalización sobre el estado futuro de cada aplicación.

> [!div class="nextstepaction"]
> [¿Qué es un patrimonio digital?](./index.md)
