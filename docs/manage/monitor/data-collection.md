---
title: 'Guía de supervisión de la nube: recopilación de los datos correctos'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Decida cuándo usar Azure Monitor o System Center Operations Manager en Microsoft Azure.
author: MGoedtel
ms.author: magoedte
ms.date: 06/26/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 8b0aebe00d987ac49ba965fc1982c1615372ba92
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032093"
---
# <a name="cloud-monitoring-guide-collecting-the-right-data"></a>Guía sobre la supervisión en la nube: Recopilación de los datos adecuados

En este artículo se describen algunas consideraciones para recopilar datos de supervisión en una aplicación de la nube.

Para observar el estado y la disponibilidad de la solución en la nube, debe configurar las herramientas de supervisión para recopilar un nivel de señales que se basen en estados de error predecibles. Estas señales son los síntomas del error, no la causa. Las herramientas de supervisión usan métricas y, en caso de diagnósticos avanzados y el análisis de la causa principal, también usan registros.

Planee cuidadosamente la supervisión y la migración. Para empezar, incluya al propietario del servicio de supervisión, al administrador de las operaciones y a otro personal relacionado durante la fase de planeamiento y continúe contando con ellos en todo el ciclo de desarrollo y lanzamiento. Su enfoque será desarrollar una configuración de supervisión basada en los criterios siguientes:

- ¿Cuál es la composición del servicio y son esas las dependencias supervisadas hoy? Si es así, ¿hay varias herramientas implicadas? ¿Hay alguna oportunidad de consolidarla, sin introducir riesgos?
- ¿Cuál es el Acuerdo de Nivel de Servicio y cómo se mide y se notifica?
- ¿Qué aspecto debería tener el panel de servicio cuando se produce un incidente? ¿Qué aspecto debería tener el panel para el propietario del servicio y el equipo que respalda el servicio?
- ¿Qué métricas genera el recurso que se debe supervisar?  
- ¿Cómo realizarán búsquedas los registros el propietario del servicio, los equipos de soporte técnico y otro personal?

El modo en que se responda a esas preguntas, y los criterios de alerta, determinarán cómo se usará la plataforma de supervisión. Si va a migrar desde una plataforma de supervisión o un conjunto de herramientas de supervisión existentes, use la migración como una oportunidad para volver a evaluar las señales que recopile. Esto es especialmente cierto ahora que hay varios factores de costo que se deben tener en cuenta al migrar o integrar con una plataforma de supervisión basada en la nube como Azure Monitor. Recuerde que los datos de supervisión deben ser procesables. Es necesario haber recopilado datos optimizados para tener una buena visión general del estado del servicio. La instrumentación definida para identificar incidentes reales debe ser tan sencilla, predecible y confiable como sea posible.

## <a name="develop-a-monitoring-configuration"></a>Desarrollo de una configuración de supervisión

El equipo y el propietario del servicio de supervisión normalmente siguen un conjunto común de actividades para desarrollar una configuración de supervisión. Estas actividades se inician en las fases de planeación iniciales, continúan con las pruebas y se validan en un entorno que no es de producción; posteriormente, se amplían para implementarse en producción. Las configuraciones de supervisión se derivan de modos de error conocidos, de resultados de pruebas de errores simulados y de la experiencia de varias personas de la organización (el departamento de servicios, las operaciones, los ingenieros y los desarrolladores). En tales configuraciones se supone que el servicio ya existe, se está migrando a la nube y no se ha rediseñado.

Supervise el estado y la disponibilidad de estos servicios al principio del proceso de desarrollo, a fin de obtener los resultados de calidad del nivel de servicio. Si supervisa el diseño de ese servicio o aplicación como una ocurrencia tardía, los resultados no serán tan buenos.

Para impulsar una resolución más rápida del incidente, tenga en cuenta las siguientes recomendaciones:

- Defina un panel para cada componente de servicio.
- Use métricas que ayuden a guiar un diagnóstico posterior, a fin de identificar una solución definitiva o temporal del problema en caso de que no se pueda descubrir la causa principal.
- Use las funcionalidades de exploración en profundidad del panel o respalde la personalización de la vista para mejorarla.
- Si necesita registros detallados, las métricas deberían haber ayudado a identificar los criterios de búsqueda. Si no es así, mejore las métricas para el próximo incidente.

La adopción de este conjunto de principios guía le proporciona información casi en tiempo real, así como una mejor administración del servicio.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Estrategia de alertas](./alerting.md)
