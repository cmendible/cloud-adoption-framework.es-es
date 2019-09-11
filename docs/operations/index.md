---
title: Introducción a la administración operativa
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Descripción de la administración operativa dentro de Cloud Adoption Framework.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/19/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.custom: manage
ms.openlocfilehash: ed8afc403f217475cb69d4f0bf6742fe64443ae3
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818444"
---
# <a name="establishing-operational-management-practices-in-the-cloud"></a>Establecimiento de los procedimientos de administración operativa en la nube

La adopción de la nube actúa como catalizador para impulsar el valor empresarial. Sin embargo, el valor empresarial real se obtiene mediante el funcionamiento constante y estable de los recursos tecnológicos implementados en la nube. En esta sección de Cloud Adoption Framework, se guía al lector por diversas transiciones hasta la administración operativa de la nube.

## <a name="actionable-best-practices"></a>Procedimientos recomendados viables

Las soluciones actuales de administración operativa crean una vista de varias nubes de las operaciones. Los recursos administrados mediante los siguientes procedimientos recomendados pueden residir en la nube, en un centro de datos existente o incluso en un proveedor de nube de la competencia. Actualmente, la plataforma incluye dos procedimientos recomendados de referencia para lograr la madurez de la administración de las operaciones en la nube:

* [Azure Server Management](./azure-server-management/index.md): Guía de incorporación para agregar las herramientas y servicios nativos de la nube necesarios para administrar las operaciones.
* [Supervisión híbrida](./monitor/index.md): Muchos clientes ya han realizado una inversión sustancial en System Center Operations Manager. Para esos clientes, esta guía sobre la supervisión híbrida les ayudará a comparar y contrastar las herramientas de notificación nativas de la nube con las herramientas de Operations Manager. Con esta comparación le resultará más fácil decidir qué herramientas utilizar para la administración operativa.

## <a name="cloud-operations"></a>Operaciones en la nube

Ambos procedimientos recomendados conducen hacia una metodología de estado futuro para la administración de operaciones.

![Metodología de administración de Cloud Adoption Framework](../_images/operate/caf-manage.png)

**Alineación de negocios:** En la metodología de administración todas las cargas de trabajo se clasifican por nivel de importancia y por valor empresarial. Posteriormente, esa clasificación se puede medir mediante un análisis de impacto, que calcula el valor perdido asociado con una degradación del rendimiento o con interrupciones en su negocio. Con ese impacto tangible de los ingresos, los equipos de operaciones en la nube pueden trabajar con la empresa para establecer un compromiso que equilibre el costo y el rendimiento.

**Materias de operaciones en la nube:** Una vez alineado el negocio, es mucho más fácil realizar un seguimiento e informar sobre las materias adecuadas de las operaciones en la nube para cada carga de trabajo. La toma de decisiones en cada materia se puede convertir posteriormente en términos de compromiso fácilmente comprensibles por parte de la empresa. Este enfoque de colaboración hace que las partes interesadas de la empresa se conviertan en asociados a la hora de encontrar el equilibrio adecuado entre costo y rendimiento.

* Inventario y visibilidad: Como mínimo, la administración de operaciones necesita un medio para realizar un inventario de los recursos y visibilidad sobre el estado de ejecución de cada recurso.
* Cumplimiento operativo: La administración regular de la configuración, tamaño, costo y rendimiento de los recursos es clave para mantener las expectativas de rendimiento.
* Protección y recuperación: Minimizar las interrupciones operativas y agilizar la recuperación ayuda a evitar pérdidas de rendimiento e impactos en los ingresos. Detección y recuperación son aspectos esenciales de esta materia.
* Operaciones de la plataforma: Todos los entornos de TI contienen un conjunto de plataformas que se emplean habitualmente. Estas plataformas pueden incluir almacenes de datos como SQL Server o HDInsight. Otras plataformas comunes pueden incluir soluciones de contenedores como Kubernetes o AKS. Con independencia de las plataformas, la madurez de las operaciones de estas se centra en personalizar las operaciones en función de cómo se implementan, configuran y utilizan estas plataformas habituales.
* Operaciones con cargas de trabajo: En el nivel más alto de madurez operativa, los equipos de operaciones en la nube pueden optimizar las operaciones para las cargas de trabajo que son cruciales para el éxito del negocio. Para esas cargas de trabajo de gran importancia, los datos disponibles pueden ayudar a automatizar la corrección, el ajuste de tamaño o la protección de las cargas de trabajo según su uso.

Instrucciones adicionales como las contenidas en [Diseño de la plataforma de revisión (Nombre en clave: Principios de diseño en la nube)](/azure/architecture/reliability) pueden ayudar a tomar decisiones de arquitectura detalladas en relación con cada carga de trabajo de las materias anteriores.

Esta sección de Cloud Adoption Framework se creará sobre cada uno de estos temas para hacer madurar las operaciones en la nube dentro de la organización.
