---
title: ¿En qué consiste la contabilidad en la nube?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Explicación del concepto de contabilidad de la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 834beb021b394e2d6ffe58723caced7519923b59
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031509"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-cloud-accounting"></a>¿En qué consiste la contabilidad en la nube?

La nube cambia el modo en que TI justifica los costos, como se describe en [Creación de un modelo financiero para la transformación a la nube](./financial-models.md). Es mucho más fácil admitir varios modelos de contabilidad de TI debido al modo en que la nube asigna los costos. Por lo tanto, es importante comprender cómo justificar los costos de la nube antes de comenzar el recorrido de transformación hacia esta nueva plataforma. En este artículo se describen los modelos de contabilidad de la nube más comunes para TI.

## <a name="traditional-it-accounting-cost-center-model"></a>Contabilidad de TI tradicional (modelo de centro de costos)

A menudo es preciso considerar la TI un centro de costos. En el modelo tradicional de contabilidad de TI, el departamento de TI consolida la capacidad adquisitiva para todos los activos de TI. Como se señaló en el artículo de [modelos financieros](./financial-models.md), dicha consolidación de la capacidad adquisitiva puede incluir licencias de software, cargos periódicos de licencias de CRM, compra de equipos de escritorio para los empleados y otros costos de gran envergadura.

Cuando la TI funciona como centro de costos, su valor percibido se ve en gran medida a través de un objetivo de administración de adquisiciones. Esta percepción dificulta que la Junta u otros ejecutivos comprendan el verdadero valor que proporciona la TI. Los costos de adquisición tienden a sesgar la visión de la TI al sopesar cualquier otro valor agregado por la organización. Esta consideración explica por qué la TI se suele agrupar en las responsabilidades del director financiero (CFO) o del director de información (COO). Esta percepción de la TI es limitada y puede llevar a un planteamiento corto de miras.

## <a name="central-it-accounting-profit-center-model"></a>Contabilidad de TI central (modelo de centro de beneficios)

Para superar la visión de la TI como un centro de costos, algunos CIO han optado por un modelo de contabilidad de TI central. En este tipo de modelo, la TI se trata como una unidad de negocio competitiva que se encuentra al mismo nivel que las unidades de negocio de generación de ingresos. En algunos casos, este modelo puede ser completamente lógico. Por ejemplo, algunas organizaciones disponen de una división profesional de servicios de TI que genera un flujo de ingresos. Con frecuencia, los modelos de TI centrales no generan ingresos significativos, lo que dificulta la justificación del modelo.

Con independencia del modelo de ingresos, los modelos de contabilidad de TI centrales son únicos debido a la manera en que la unidad de TI justifica los costos. En un modelo de TI tradicional, el equipo de TI registra los costos y paga esos costos de los fondos compartidos, como operaciones y mantenimiento (O&M) o una cuenta de pérdidas y ganancias (P&G) dedicada.

En un modelo de contabilidad de TI central, el equipo de TI incrementa el precio de los servicios proporcionados para justificar los gastos generales, de administración y de otro tipo estimados. Luego, se facturan a las unidades de negocio competidoras los servicios de precio incrementado. En este modelo, se espera que el CIO administre las ganancias y pérdidas asociadas con la venta de esos servicios. Esta situación puede llevar a inflar los costos de TI y a la discordia entre TI central y las unidades de negocio, en especial cuando es necesario reducir los costos de TI o no se están cumpliendo los Acuerdos de Nivel de Servicio acordados. Durante los períodos de cambios tecnológicos o del mercado, cualquier tecnología nueva provocará una interrupción en el balance de ingresos de TI central, lo que dificultará la transformación.

## <a name="chargeback"></a>Contracargo

Uno de los primeros pasos habituales que hay que seguir para cambiar la reputación de la TI como centro de costos es implementar un modelo de contabilidad de contracargo. Este modelo es especialmente común en empresas más pequeñas o en organizaciones de TI con una elevada eficiencia. En el modelo de contracargo, los costos de TI asociados a una unidad de negocio específica se tratan como gastos operativos en el presupuesto de esa unidad de negocio. Esta práctica reduce los efectos de costos acumulados sobre la TI, lo que permite que los valores empresariales se muestren con mayor claridad.

En un modelo local heredado, el contracargo es difícil de lograr porque todavía alguien tiene que arrastrar los grandes gastos de capital y la amortización. La conversión continua de gastos de capital en gastos operativos asociados al uso es un ejercicio de contabilidad difícil. Esta dificultad es una de las razones principales para la creación del modelo de contabilidad de TI tradicional y el modelo de contabilidad de TI central. El modelo de gastos operativos de contabilidad de costos de la nube es casi obligatorio si quiere proporcionar eficazmente un modelo de contracargo.

Pero no debe implementar este modelo sin considerar las implicaciones. Estas son algunas de las consecuencias que son específicas de un modelo de contracargo:

- El contracargo produce una reducción masiva del presupuesto general de TI. En el caso de organizaciones de TI que no son eficaces o que requieren extensas habilidades técnicas complejas en operaciones o mantenimiento, este modelo puede exponer esos gastos de forma poco saludable.
- Una de las consecuencias comunes es la pérdida de control. En entornos con un gran componente político, el contracargo puede dar lugar a la pérdida de control y a la reasignación de personal a la empresa. Esta situación podría crear importantes ineficiencias y reducir la capacidad de TI para cumplir sistemáticamente los Acuerdos de Nivel de Servicio o los requisitos del proyecto.
- Otra consecuencia común es la dificultad para justificar los servicios compartidos. Si la organización ha crecido mediante adquisiciones y, como resultado, arrastra la deuda técnica, es probable que se deba mantener un alto porcentaje de servicios compartidos para que todos los sistemas funcionen juntos de manera efectiva.

Las transformaciones hacia la nube incluyen soluciones a estas y otras consecuencias asociadas a un modelo de contracargo. Pero cada una de esas soluciones incluye gastos operativos y de implementación. El CIO y el director financiero (CFO) deben sopesar detenidamente las ventajas y desventajas de un modelo de contracargo antes de considerar uno.

## <a name="showback-or-awareness-back"></a>Visualización de costos o reconocimiento de costos

En el caso de empresas más grandes, un modelo de visualización de costos o reconocimiento de costos es un primer paso más seguro en la transición desde el centro de costos hasta el centro de valores. Este modelo no afecta a la contabilidad financiera. De hecho, las pérdidas y ganancias de cada organización no cambian. El mayor cambio está en la mentalidad y el reconocimiento. En un modelo de visualización de costos o reconocimiento de costos, TI administra la capacidad adquisitiva consolidada centralizada como un agente para la empresa. En la presentación de informes a la empresa, el departamento de TI atribuye los costos directos a la unidad de negocio correspondiente, lo que reduce el presupuesto percibido que consume directamente la TI. El departamento de TI también planea los presupuestos en función de las necesidades de las unidades de negocio asociadas, lo que le permite justificar con mayor precisión los costos asociados a las iniciativas exclusivamente de TI.

Este modelo proporciona un equilibrio entre un modelo verdaderamente de contracargo y modelos de contabilidad de TI más tradicionales.

## <a name="impact-of-cloud-accounting-models"></a>Efecto de los modelos de contabilidad de la nube

La elección de los modelos de contabilidad es fundamental en el diseño del sistema. Puede afectar a las estrategias de suscripción, los estándares de nomenclatura, los estándares de etiquetado y los diseños de directivas y planos técnicos.

Después de haber trabajado con la empresa para tomar decisiones sobre un modelo de contabilidad de la nube y los [mercados globales](./global-markets.md), dispone de suficiente información para [desarrollar una base de Azure](../ready/index.md).

> [!div class="nextstepaction"]
> [Desarrollo de una base de Azure](../ready/index.md)
