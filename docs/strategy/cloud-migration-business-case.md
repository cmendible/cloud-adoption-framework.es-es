---
title: Compilación de una justificación comercial para la migración a la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Consideraciones para crear una justificación empresarial para la migración a la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: governance
ms.openlocfilehash: d545b977a4c98692ba8503d5512b8cb0d0b7dd0d
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224197"
---
# <a name="build-a-business-justification-for-cloud-migration"></a>Compilación de una justificación comercial para la migración a la nube

Las migraciones a la nube pueden generar una rápida rentabilidad de la inversión (ROI) por los esfuerzos de transformación en la nube. Sin embargo, desarrollar una justificación empresarial clara con costos y rendimientos pertinentes y tangibles puede ser un proceso complejo. Este artículo le ayudará a pensar en qué datos son necesarios para crear un modelo financiero que se alinee con los resultados de la migración a la nube. En primer lugar, vamos a destruir unos cuantos mitos sobre la migración a la nube, de forma que su organización pueda evitar cometer algunos errores comunes.

## <a name="dispelling-cloud-migration-myths"></a>Acabar con los mitos de la migración a la nube

**Mito: la nube es siempre más barata.** Es una creencia común que tener un centro de datos en la nube es más barato que operarlo en el entorno local. Aunque generalmente esta suposición puede ser cierta, no siempre es el caso. A veces, los costos operativos en la nube son superiores. Estos costos más altos suelen deberse a un deficiente control de los costos, a arquitecturas de sistema desajustadas, a la duplicación de procesos, a configuraciones de sistema atípicas o a costos de personal más elevados. Afortunadamente, puede mitigar muchos de estos problemas para crear una rentabilidad de la inversión temprana. Siga las instrucciones que se indican en [Creación de la justificación empresarial](#building-the-business-justification), que le ayudarán a detectar y evitar estos desajustes. También puede ayudarle la información que aquí se describe sobre cómo acabar con los otros mitos.

**Mito: todo debe introducirse en la nube.** De hecho, es posible que algunos impulsores del negocio le lleven a elegir una solución híbrida. Antes de finalizar un modelo de negocio, es aconsejable realizar una primera ronda de análisis cuantitativo, como se describe en los [artículos sobre el patrimonio digital](../digital-estate/5-rs-of-rationalization.md). Para más información sobre los factores cuantitativos individuales implicados en la racionalización, consulte [Las 5 R de la racionalización](../digital-estate/5-rs-of-rationalization.md). En cualquiera de los enfoques se usarán datos de inventario obtenidos fácilmente y un breve análisis cuantitativo para identificar cargas de trabajo o aplicaciones que podrían dar lugar a costos más elevados en la nube. Estos enfoques podrían identificar también dependencias o patrones de tráfico que necesitarían una solución híbrida.

**Mito: crear un reflejo de mi entorno local me ayuda a ahorrar dinero en la nube.** Durante el planeamiento del patrimonio digital, no es algo insólito que los clientes detecten capacidad sin usar por encima del 50 % del entorno aprovisionado. Si se aprovisionan recursos en la nube para que coincidan con el aprovisionamiento actual, será difícil que haya ahorros en los costos. Considere la posibilidad de reducir el tamaño de los recursos implementados para que se alineen con los patrones de uso, en lugar de con los patrones de aprovisionamiento.

**Mito: en la migración a la nube, los costos del servidor controlan los casos empresariales.** A veces, esta suposición es verdadera. Para algunas compañías, es importante reducir los gastos de capital constantes relacionados con los servidores. Sin embargo, esto depende de varios factores. No es probable que las compañías con un ciclo de actualización de hardware de entre cinco y ocho años encuentren rendimientos rápidos en su migración a la nube. Las compañías con ciclos de actualización estandarizados o impuestos pueden puedan llegar a un umbral de rentabilidad rápidamente. En cualquier caso, otros gastos pueden ser los desencadenadores financieros que justifiquen la migración. Aquí se incluyen algunos ejemplos de los costos que normalmente se pasan por alto cuando las compañías adoptan una visión de los costos basada únicamente en el servidor o en la máquina virtual:

- Los costos de software de virtualización, servidores y middleware pueden ser amplios. Los proveedores de nube eliminan algunos de estos costos. Dos ejemplos de un proveedor de nube que reduce los costos de virtualización son los programas [Ventaja híbrida de Azure](https://azure.microsoft.com/pricing/hybrid-benefit/#services) y [Reservas de Azure](https://azure.microsoft.com/reservations).
- Las pérdidas empresariales debidas a interrupciones pueden superar rápidamente los costos de hardware o software. Si su centro de datos actual es inestable, trabaje con la empresa para cuantificar el impacto de las interrupciones en términos de costos de oportunidad o costos empresariales reales.
- Los costos del entorno también pueden ser considerables. Para una familia estadounidense media, su casa es la inversión más grande y el costo más alto en su presupuesto. Con frecuencia, lo mismo puede decirse de los centros de datos. Los costos de bienes inmuebles, instalaciones y servicios públicos representan una buena parte de los costos locales. Cuando se retiran los centros de datos, se pueden reutilizar esas instalaciones, o la empresa podría quedar liberada de los costos completamente.

**Mito: el modelo de gastos operativos es mejor que el modelo de gastos de capital.** Como se explica en el artículo sobre los [resultados fiscales](./business-outcomes/fiscal-outcomes.md), el modelo de gastos operativos puede ser una buena opción. No obstante, algunos sectores ven los gastos operativos de forma negativa. Los siguientes son algunos ejemplos que desencadenarían una integración más fuerte con las unidades de contabilidad y negocio respecto al debate de gastos operativos:

- Cuando una empresa considera los activos fijos como un factor para la valoración del negocio, las reducciones de gastos de capital podrían ser un resultado negativo. Aunque no es un estándar universal, esta opinión se observa con más frecuencia en los sectores del comercio minorista, fabricación y construcción.
- Las empresas propiedad de capital privado o que buscan una afluencia de capitales podrían considerar los aumentos de gastos operativos como un resultado negativo.
- Si una empresa se centra principalmente en mejorar los márgenes de ventas o reducir el costo de bienes vendidos (COGS), los gastos operativos podrían ser un resultado negativo.

Es más probable que las empresas consideren los gastos operativos como más favorables que los gastos de capital. Por ejemplo, este enfoque pueden adoptarlo también las empresas que intentan mejorar el flujo de efectivo, reducir las inversiones de capital o disminuir las tenencias de activos.

Antes de proporcionar una justificación empresarial centrada en una conversión de gastos de capital a gastos operativos, sepa qué es lo mejor para su empresa. Contabilidad y compras pueden con frecuencia ayudar a alinear el mensaje con los objetivos financieros.

**Mito: pasar a la nube es como darle a un botón.** Las migraciones son una transformación técnica manualmente intensa. Al desarrollar una justificación empresarial, en especial justificaciones que dependen del tiempo, tenga en cuenta los siguientes aspectos que podrían aumentar el tiempo necesario para migrar los recursos:

- **Limitaciones de ancho de banda:** la cantidad de ancho de banda entre el centro de datos actual y el proveedor de nube determinará las escalas de tiempo durante la migración.
- **Plazos de pruebas:** probar las aplicaciones con la empresa para garantizar la preparación y el rendimiento puede llevar mucho tiempo. Es fundamental alinear los usuarios avanzados y los procesos de prueba.
- **Plazos de migración:** la cantidad de tiempo y esfuerzo necesarios para implementar la migración puede aumentar los costos y provocar retrasos. La asignación de empleados o partes contratantes también puede retrasar el proceso. El plan debe tener en cuenta estas asignaciones.

Impedimentos técnicos y culturales pueden ralentizar la adopción de la nube. Cuando el tiempo es un aspecto importante de la justificación empresarial, la mejor solución de mitigación es el planeamiento adecuado. Durante el planeamiento, dos enfoques pueden ayudar a mitigar los riesgos para los plazos:

- Invierta tiempo y energía en comprender las restricciones de la adopción técnica. Aunque la presión para realizar la transición rápidamente puede ser alta, es importante considerar plazos realistas.
- Si surgen impedimentos culturales o relacionados con las personas, su efecto será más grave que las restricciones técnicas. La adopción de la nube crea cambios, que producen la transformación deseada. Por desgracia, a veces las personas temen el cambio y pueden necesitar apoyo adicional para alinearse con el plan. Identifique las personas claves del equipo que se oponen al cambio y consiga su adhesión desde el principio.

Para aumentar la buena disposición y reducir los riesgos para los plazos, prepare a las partes interesadas para conseguir una fuerte alineación del valor y los resultados empresariales. Ayude a esas partes interesadas a comprender los cambios que acompañan a la transformación. Sea claro y establezca expectativas realistas desde el principio. Cuando las personas o las tecnologías ralenticen el proceso, será más fácil conseguir el apoyo ejecutivo.

## <a name="building-the-business-justification"></a>Creación de la justificación empresarial

El proceso siguiente define un enfoque para desarrollar la justificación empresarial para las migraciones a la nube. Para más información sobre los cálculos y los términos financieros, consulte el artículo sobre [modelos financieros](./financial-models.md).

En términos generales, la fórmula de justificación empresarial es sencilla. Sin embargo, los puntos de datos sutiles necesarios para rellenar la fórmula pueden ser difíciles de alinear. En general, la justificación empresarial se centra en la rentabilidad de la inversión (ROI) asociada con el cambio técnico propuesto. La fórmula genérica de la ROI es:

![ROI es igual a (ganancia de la inversión menos costo de la inversión) dividido entre costo de la inversión](../_images/strategy/formula-roi.png)

Podemos desempaquetar esta ecuación para obtener una vista de las fórmulas específica de la migración para las variables de entrada por el lado adecuado de esta ecuación. En el resto de las secciones de este artículo se ofrecen algunos aspectos que se deben tener en cuenta.

## <a name="migration-specific-initial-investment"></a>Inversión inicial específica de la migración

- Los proveedores de nube como Azure ofrecen calculadoras para estimar las inversiones en la nube. La [calculadora de precios de Azure](https://azure.microsoft.com/pricing) es un ejemplo.
- Algunos proveedores de nube también proporcionan calculadoras de costo diferencial. La [Calculadora de costo total de propiedad (TCO) de Azure](https://azure.com/tco) es un ejemplo.
- Para estructuras de costo más refinadas, considere un ejercicio de [planeamiento del patrimonio digital](../digital-estate/index.md).
- Estime el costo de la migración.
- Estime el costo de las oportunidades de aprendizaje esperadas. [Microsoft Learn](/learn) puede ayudarle a reducir esos costos.
- En algunas compañías, puede ser necesario incluir en los costos iniciales el tiempo invertido por los miembros del personal existentes. Para más información, consulte con la administración de hacienda.
- Valide con ellos los costos adicionales o costos de cargas.

## <a name="migration-specific-revenue-deltas"></a>Ingresos diferenciales específicos de la migración

Con frecuencia, los estrategas pasan este aspecto por alto al crear una justificación empresarial para la migración. En algunas áreas, la nube puede reducir los costos. Sin embargo, el objetivo final de cualquier transformación es producir mejores resultados con el tiempo. Para comprender las mejoras de los ingresos a largo plazo, considere los efectos de bajada. ¿Qué tecnologías nuevas estarán disponibles para la empresa tras la migración que no se puedan utilizar actualmente? ¿Qué proyectos u objetivos de negocio están bloqueados por las dependencias de tecnologías heredadas? ¿Qué programas están en espera, pendientes de gastos de capital elevados en tecnología?

Después de considerar las oportunidades que crea la nube, trabaje con la empresa para calcular el aumento de los ingresos que podría provenir de esas oportunidades.

## <a name="migration-specific-cost-deltas"></a>Costos diferenciales específicos de la migración

Calcule los cambios en los costos como resultado de la migración propuesta. Consulte el artículo sobre [modelos financieros](./financial-models.md) para más información sobre los tipos de costos diferenciales. Los proveedores de nube con frecuencia proporcionan herramientas para el cálculo de los costos diferenciales. La [Calculadora de costo total de propiedad (TCO) de Azure](https://azure.com/tco) es un ejemplo.

Otros ejemplos de costos que pueden reducirse con una migración a la nube:

- Terminación o reducción del centro de datos (costos de entorno)
- Reducción en la energía consumida (costos de entorno)
- Terminación del bastidor (recuperación de recursos físicos)
- Prevención de actualizaciones de hardware (prevención de costos)
- Prevención de renovación de software (reducción de costos operativos o prevención de costos)
- Consolidación del proveedor (reducción de costos operativos y posible reducción de costos indirectos)

## <a name="when-roi-results-are-surprising"></a>Cuando los resultados de la ROI son sorprendentes

Si la ROI de una migración a la nube no está en consonancia con las expectativas, puede ser útil revisar los mitos comunes enumerados al principio de este artículo.

Sin embargo, es importante entender que un ahorro en los costos no siempre es posible. Hay aplicaciones que cuesta más tener en la nube que en el entorno local. Estas aplicaciones pueden sesgar considerablemente los resultados en un análisis.

Cuando el ROI sea inferior al 20 %, podría realizar un ejercicio de [planeamiento del patrimonio digital](../digital-estate/index.md), con una atención específica a la [racionalización](../digital-estate/rationalize.md). Durante el análisis cuantitativo, revise cada aplicación para encontrar las cargas de trabajo que sesgan los resultados. Podría ser aconsejable quitar esas cargas de trabajo del plan. Si existen datos de uso, considere la posibilidad de reducir el tamaño de las máquinas virtuales para que coincidan con el uso.

Si aún no está alineado el ROI, solicite la ayuda de un representante de ventas de Microsoft o [hable con un asociado experimentado](https://azure.microsoft.com/migration/support).

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Creación de un modelo financiero para la transformación en la nube](./financial-models.md)
