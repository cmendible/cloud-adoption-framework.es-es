---
title: Motivaciones para la coherencia de recursos y riesgos empresariales
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Motivaciones para la coherencia de recursos y riesgos empresariales
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 42510f62cb3f673698832403126901789b05e978
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031446"
---
# <a name="resource-consistency-motivations-and-business-risks"></a>Motivaciones para la coherencia de recursos y riesgos empresariales

En este artículo se describen las razones por las que los clientes normalmente adoptan una materia de coherencia de recursos dentro de una estrategia de gobernanza en la nube. También se proporcionan algunos ejemplos de posibles riesgos empresariales que pueden impulsar las declaraciones de directivas.

<!-- markdownlint-disable MD026 -->

## <a name="is-resource-consistency-relevant"></a>¿Es pertinente la coherencia de recursos?

Cuando se trata de implementar recursos y cargas de trabajo, la nube ofrece una mayor agilidad y flexibilidad con respecto a la mayoría de los centros de datos locales tradicionales. Sin embargo, estas posibles ventajas basadas en la nube también vienen acompañadas de posibles inconvenientes de administración que pueden poner en grave peligro el éxito de su adopción de la nube. ¿Qué recursos ha implementado? ¿Qué equipos poseen qué recursos? ¿Tiene suficientes recursos para admitir una carga de trabajo? ¿Cómo sabe si las cargas de trabajo están funcionando correctamente?

La coherencia de los recursos es crucial para garantizar que los recursos se implementen, actualicen y configuren de manera coherente y repetitiva, y que las interrupciones del servicio se minimicen y solucionen en el menor tiempo posible.

La materia de coherencia de recursos se ocupa de identificar y mitigar los riesgos empresariales relacionados con los aspectos operativos de su implementación en la nube. La coherencia de recursos incluye la supervisión de aplicaciones, cargas de trabajo y rendimiento de los recursos. También incluye las tareas necesarias para satisfacer las demandas de escalado, corregir las infracciones del Acuerdo de Nivel de Servicio (SLA) de rendimiento y evitar de forma activa las infracciones del SLA de rendimiento mediante una corrección automatizada.

Es posible que las implementaciones iniciales de prueba no requieran mucho más que la adopción de algunos estándares de nomenclatura y etiquetado para satisfacer sus necesidades de coherencia de recursos. A medida que su adopción de la nube madure e implemente recursos más complicados y críticos, la necesidad de invertir en la materia de coherencia de recursos aumentará rápidamente.

## <a name="business-risk"></a>Riesgo empresarial

La materia de coherencia de recursos intenta abordar los principales riesgos empresariales operativos. Trabaje con su empresa y los equipos de TI para identificar estos riesgos y supervise cada uno de ellos para determinar su pertinencia a medida que planifique e implemente sus implementaciones en la nube.

Los riesgos variarán según la organización, pero los siguientes sirven como riesgos comunes que puede usar como punto de partida para debatir en el seno de su equipo de gobernanza de la nube:

- **Costos operativos innecesarios.** Los recursos obsoletos o no utilizados, o los recursos que se sobreaprovisionan en épocas de baja demanda, agregan costos operativos innecesarios.
- **Recursos infraaprovisionados.** Los recursos que experimentan una demanda mayor a la prevista pueden dar lugar a una interrupción del negocio, ya que los recursos de la nube se ven desbordados por la demanda.
- **Ineficiencias de administración.** La falta de metadatos de nomenclatura y etiquetado coherentes asociados con los recursos puede hacer que el personal de TI tenga dificultades para encontrar recursos para las tareas de administración o para determinar la propiedad y la información de cuentas relacionada con los recursos. Esto se traduce en ineficiencias de administración que pueden aumentar los costos y retardar la capacidad de respuesta de la TI ante la interrupción del servicio u otros problemas operativos.
- **Interrupción del negocio.** Las interrupciones del servicio que resultan en infracciones de los Acuerdos de Nivel de Servicio (SLA) establecidos por su organización pueden dar lugar a la pérdida de negocios o a repercusiones financieras negativas para la empresa.

## <a name="next-steps"></a>Pasos siguientes

Utilice la [plantilla de administración de la nube](./template.md) para documentar los riesgos empresariales que probablemente se presentarán en el plan de adopción de la nube actual.

Una vez que se consigue una comprensión realista de los riesgos empresariales, el siguiente paso es documentar la tolerancia al riesgo de la empresa y los indicadores y métricas clave para supervisar esa tolerancia.

> [!div class="nextstepaction"]
> [Descripción de indicadores, métricas y tolerancia al riesgo](./metrics-tolerance.md)
