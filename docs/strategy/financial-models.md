---
title: Creación de un modelo financiero para la transformación en la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Cómo crear un modelo financiero para la transformación en la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: governance
ms.openlocfilehash: 75f19fcdc9f23066d5a6471cd79c0a6a00869554
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031627"
---
# <a name="create-a-financial-model-for-cloud-transformation"></a>Creación de un modelo financiero para la transformación en la nube

Crear un modelo financiero que represente con precisión el valor empresarial completo de cualquier transformación en la nube puede ser complicado. Los modelos financieros y las justificaciones empresariales tienden a variar entre distintas organizaciones. En este artículo se establecen algunas fórmulas y se señalan algunas cosas que normalmente faltan cuando los estrategas crean modelos financieros.

## <a name="return-on-investment"></a>Rentabilidad de la inversión

La rentabilidad de la inversión (ROI) suele ser un criterio importante para los ejecutivos de máximo rango o la junta. ROI se usa para comparar diferentes formas de invertir recursos limitados de capital. La fórmula de ROI es bastante sencilla. Sin embargo, los datos necesarios para crear cada entrada de la fórmula pueden no ser tan simples. Básicamente, ROI es la cantidad de rentabilidad generada por una inversión inicial. Normalmente se representa como un porcentaje:

![ROI es igual a (ganancia de la inversión menos costo de la inversión) dividido entre costo de la inversión](../_images/strategy/formula-roi.png)

En las secciones siguientes, se le guía por los datos necesarios para calcular la inversión inicial y la ganancia de la inversión (beneficios).

## <a name="calculating-initial-investment"></a>Cálculo de la inversión inicial

La inversión inicial es el gasto de capital y el gasto operativo necesarios para llevar a cabo una transformación. La clasificación de los costos puede variar según los modelos de contabilidad y las preferencias del CFO. En esta categoría se incluirían elementos como servicios profesionales para transformar, licencias de software que se usan únicamente durante la transformación, costo de los servicios en la nube durante la transformación y, posiblemente, el costo de los empleados asalariados durante la transformación.

Sume estos costos para crear una estimación de la inversión inicial.

## <a name="calculating-the-gain-from-investment"></a>Cálculo de la ganancia de la inversión

El cálculo de la ganancia de la inversión requiere con frecuencia una segunda fórmula, que es específica de los resultados empresariales y los cambios técnicos asociados. Calcular los beneficios es más difícil que calcular las reducciones de costos.

Para calcular los beneficios, se requieren dos variables:

![Ganancia de la inversión es igual a ingresos diferenciales más costos diferenciales](../_images/strategy/formula-gain-from-investment.png)

Estas variables se describen en las secciones siguientes.

## <a name="revenue-deltas"></a>Ingresos diferenciales

Los ingresos diferenciales se deben prever en colaboración con las partes interesadas de la empresa. Una vez que las partes interesadas acuerdan un impacto sobre los ingresos, se puede usar para mejorar la posición de los beneficios.

## <a name="cost-deltas"></a>Costos diferenciales

Los costos diferenciales son la cantidad de aumento o disminución que generará la transformación. Los costos diferenciales pueden verse afectados por variables independientes. Los beneficios se basan en gran medida en los costos directos como la reducción de gastos de capital, la prevención de costos, las reducciones de costos operativos y las reducciones de amortización. En las secciones siguientes se describen algunos costos diferenciales que se deben tener en cuenta.

### <a name="depreciation-reduction-or-acceleration"></a>Reducción o aceleración de la depreciación

Para más información sobre la depreciación, hable con el CFO o el equipo financiero. La siguiente información sirve de referencia general sobre al tema de la depreciación.

Cuando se invierte capital en la adquisición de un recurso, esa inversión podría usarse con fines fiscales o financieros para producir beneficios continuados durante la vida útil del recurso. Algunas compañías consideran que la depreciación es una ventaja fiscal positiva. Otras la consideran un gasto que se realiza constantemente, de forma parecida a otros gastos recurrentes atribuidos al presupuesto anual de TI.

Hable con la administración de hacienda para determinar si es posible eliminar la depreciación y si contribuiría de forma positiva a los costos diferenciales.

### <a name="physical-asset-recovery"></a>Recuperación de los recursos físicos

En algunos casos, se pueden vender recursos retirados como una fuente de ingresos. Estos ingresos se suelen agrupar dentro de la reducción de costos por motivos de simplicidad. Sin embargo, realmente es un aumento de los ingresos y puede tributarse como tal. Hable con la administración de hacienda para conocer la viabilidad de esta opción y cómo justificar los ingresos resultantes.

### <a name="operational-cost-reductions"></a>Reducciones de costos operativos

Los gastos recurrentes necesarios para operar un negocio a menudo se denominan gastos operativos. Esta es una categoría amplia. En la mayoría de los modelos de contabilidad, incluye:

- Licencias de software.
- Gastos de hospedaje.
- Facturas de electricidad.
- Alquileres de bienes inmuebles.
- Gastos de refrigeración.
- Personal temporal necesario para las operaciones.
- Alquiler de equipos.
- Piezas de recambio.
- Contratos de mantenimiento.
- Servicios de reparación.
- Servicios de continuidad del negocio y recuperación ante desastres (BC/DR).
- Otros gastos que no requieren la aprobación de gastos de capital.

Esta categoría proporciona uno de los costos diferenciales más elevados. Si está considerando la posibilidad de realizar una migración a la nube, el tiempo invertido en la creación de esta lista estará bien empleado. Formule preguntas al CIO y al equipo financiero para asegurarse de que se justifican todos los costos operativos.

### <a name="cost-avoidance"></a>Prevención de costos

Cuando se espera un gasto operativo, pero no se encuentra aún en un presupuesto aprobado, no se puede incluir en una categoría de reducción de costos. Por ejemplo, si las licencias de Microsoft y VMware se deben volver a negociar y pagarse el próximo año, no son aún costos completos. Las reducciones en esos costos esperados se tratan como costos operativos solo para el cálculo de los costos diferenciales. Sin embargo, de manera informal, se deben considerar "prevención de costos" hasta que finalice la negociación y aprobación del presupuesto.

### <a name="soft-cost-reductions"></a>Reducciones de costos indirectos

En algunas compañías también se podrían incluir los costos indirectos, como las reducciones en la complejidad operativa o la reducción del personal a jornada completa para operar un centro de datos, en los costos diferenciales. No obstante, incluir costos indirectos puede no ser una buena idea. Al incluir reducciones de costos indirectos, se introduce un supuesto sin documentar de que la reducción creará un ahorro de costos tangible. Los proyectos de tecnología rara vez dan lugar a una recuperación real de los costos indirectos.

### <a name="headcount-reductions"></a>Reducciones de plantilla

Los ahorros de tiempo para el personal se incluyen a menudo en la reducción de costos indirectos. Cuando esos ahorros de tiempo se asignan a la reducción real de salario o personal de TI, se podrían calcular por separado como una reducción de plantilla.

Dicho esto, las aptitudes necesarias en el entorno local se asignan generalmente a un conjunto de aptitudes parecidas (o de nivel superior) necesarias en la nube. Esto significa que, por lo general, no se despide a la gente tras una migración a la nube.

Ocurre una excepción cuando un tercero o un proveedor de servicios administrados (MSP) proporcionan capacidad operativa. Si los sistemas de TI están administrados por un tercero, los costos operativos podrían reemplazarse por una solución o un MSP nativos de la nube. Es probable que un MSP nativo de la nube trabaje de manera más eficiente y posiblemente a un menor costo. Si es así, las reducciones de costos operativos pertenecen a los cálculos de costos directos.

### <a name="capital-expense-reductions-or-avoidance"></a>Reducción o prevención de gasto de capital

Los gastos de capital son ligeramente diferentes a los gastos operativos. Por lo general, esta categoría está controlada por los ciclos de actualización o la expansión del centro de datos. Un ejemplo de una expansión del centro de datos sería un nuevo clúster de alto rendimiento para hospedar una solución de macrodatos o almacenamiento de datos. Esto normalmente se incluiría en una categoría de gastos de capital. Más comunes son los ciclos de actualización básicos. Algunas compañías tienen ciclos de actualización de hardware rígidos, lo que significa que los recursos se retiran y se sustituyen en ciclos regulares (normalmente cada 3, 5 u 8 años). A menudo, estos ciclos coinciden con los ciclos de concesión de recursos o la duración prevista de los equipos. Cuando se alcanza un ciclo de actualización, TI extrae el gasto de capital para adquirir nuevos equipos.

Si se aprueba y se presupuesta un ciclo de actualización, la transformación a la nube podría ayudar a eliminar ese costo. Si un ciclo de actualización está planeado, pero aún no se ha aprobado, la transformación a la nube podría prevenir un gasto de capital. Ambas reducciones se agregarían al costo diferencial.

## <a name="next-steps"></a>Pasos siguientes

Más información sobre los modelos de [contabilidad en la nube](./cloud-accounting.md).

> [!div class="nextstepaction"]
> [Contabilidad en la nube](./cloud-accounting.md)
