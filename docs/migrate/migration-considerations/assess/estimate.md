---
title: Estimación del costo de la nube antes de la migración
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Explicación del proceso de estimación del costo de la nube antes de la migración.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 09492fea252ac9b07372c2def75d61df62e727ec
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70834782"
---
# <a name="estimate-cloud-costs"></a>Estimación del costo de la nube

Durante la migración, hay varios factores que pueden afectar a las decisiones y las actividades de ejecución. Para ayudar a entender cuáles son las opciones más adecuadas para las distintas situaciones, en este artículo se describen varias opciones para estimar el costo de la nube.

## <a name="digital-estate-size"></a>Tamaño del patrimonio digital

El tamaño del patrimonio digital afecta directamente a las decisiones de migración. Las migraciones que impliquen menos de 250 máquinas virtuales se pueden calcular mucho más fácilmente que una migración que implique más de 10 000 máquinas virtuales. Se recomienda encarecidamente que seleccione una carga de trabajo más pequeña para su primera migración. Esto le brinda al equipo una oportunidad para aprender a calcular los costos de un esfuerzo de migración sencillo antes de intentar calcular migraciones de cargas de trabajo más grandes y complejas.

Sin embargo, tenga en cuenta que las migraciones más pequeñas, de una sola carga de trabajo, de todos modos pueden implicar una cantidad muy variable de recursos complementarios. Si la migración implica menos de 1000 máquinas virtuales, una herramienta como [Azure Migrate](/azure/migrate/migrate-overview) probablemente sea suficiente para recopilar datos sobre el inventario y realizar una previsión de los costos. Las opciones de herramientas de cálculos de costos adicionales se describen en el artículo sobre los [cálculos de costos del patrimonio digital](../../../digital-estate/calculate.md).

Si hablamos de patrimonios digitales con más de 1000 unidades, todavía es posible desglosar una estimación en cuatro o cinco iteraciones accionables, lo que permite que el proceso de estimación sea manejable. En el caso de patrimonios más grandes o cuando se requiere un mayor grado de precisión para la previsión, es posible que se requiera un enfoque más integral, como el que se describe en la sección "[Patrimonio digital](../../../digital-estate/index.md)" de la Plataforma de adopción de la nube.

## <a name="accounting-models"></a>Modelos de contabilidad

Modelos de contabilidad

Si está familiarizado con los procesos de adquisición de TI tradicionales, es posible que la estimación en la nube parezca externa. Cuando se adoptan tecnologías de nube, la adquisición pasa de un modelo rígido y estructurado de gastos de capital a un modelo de gastos operativos fluidos. En el modelo de gastos de capital tradicional, el equipo de TI intentaría consolidar el poder adquisitivo de varias cargas de trabajo en varios programas con el fin de centralizar un grupo de recursos de TI compartidos que podrían admitir cada una de esas soluciones. En el modelo de gastos operativos en la nube, los costos se pueden atribuir directamente a las necesidades de compatibilidad de cargas de trabajo individuales, equipos o unidades de negocio. Este enfoque permite una atribución más directa de los costos al cliente interno compatible. Al estimar los costos, es importante comprender primero qué parte de esta nueva funcionalidad de contabilidad usará el equipo de TI.

Para quienes deseen replicar el enfoque de gastos de capital heredado para la contabilidad, use las salidas de cualquiera de los enfoques sugeridos en la sección "[Tamaño del patrimonio digital](#digital-estate-size)" más arriba para obtener una base de costos anual. A continuación, multiplique ese costo anual por el ciclo de actualización de hardware típico de la empresa. El ciclo de actualización de hardware se refiere la velocidad con la que una empresa reemplaza el hardware antiguo y que, por lo general, se mide en años. La velocidad de ejecución anual multiplicada por el ciclo de actualización de hardware crea una estructura de costos similar a un patrón de inversión de gastos de capital.

## <a name="next-steps"></a>Pasos siguientes

Después de estimar los costos, puede comenzar la migración. Sin embargo, sería aconsejable revisar las [opciones de colaboración y soporte técnico](./partnership-options.md) antes de comenzar cualquier migración.

> [!div class="nextstepaction"]
> [Descripción de las opciones de colaboración](./partnership-options.md)
