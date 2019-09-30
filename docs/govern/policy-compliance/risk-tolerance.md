---
title: Evaluación de la tolerancia al riesgo
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Explicación de los riesgos empresariales asociados con una transformación a la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 2b8bc595377b2748bd00f306659a46196115e91d
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223547"
---
# <a name="evaluate-risk-tolerance"></a>Evaluación de la tolerancia al riesgo

Cada decisión empresarial genera nuevos riesgos. Hacer una inversión en cualquier cosa genera un riesgo de pérdida. Los nuevos productos o servicios generan riesgos de fracaso en el mercado. Los cambios realizados en los productos o servicios actuales podrían reducir la cuota de mercado. La transformación a la nube no ofrece una solución mágica a los riesgos empresariales cotidianos. Al contrario, las soluciones conectadas (en la nube o locales) presentan nuevos riesgos. Implementar recursos en cualquier instalación de red conectada también expande el perfil de amenazas potenciales al exponer las vulnerabilidades de seguridad a una comunidad global mucho más amplia. Afortunadamente, los proveedores de servicios en la nube son conscientes de los cambios, del aumento y de la suma de los riesgos. Hacen grandes inversiones para administrar y mitigar esos riesgos en nombre de sus clientes.

Este artículo no se centra en los riesgos en la nube. En su lugar, describe los riesgos empresariales asociados con las diversas formas de transformación a la nube. Más adelante en este artículo, el debate cambia el foco para describir las formas de entender la tolerancia al riesgo por parte de las empresas.

<!-- markdownlint-disable MD026 -->

## <a name="what-business-risks-are-associated-with-a-cloud-transformation"></a>¿Qué riesgos empresariales están asociados con una transformación a la nube?

Los verdaderos riesgos empresariales se basan en los detalles de las transformaciones específicas. Varios riesgos comunes ofrecen un punto de partida para comprender los riesgos específicos de la empresa.

> [!IMPORTANT]
> Antes de leer lo siguiente, tenga en cuenta que cada uno de estos riesgos se puede administrar. El objetivo de este artículo es informar y preparar a los lectores para mantener conversaciones más productivas sobre la administración de los riesgos.

- **Vulneración de los datos.** El riesgo número uno asociado con cualquier transformación, es la protección de los datos. Las fugas de datos pueden provocar daños importantes en la empresa y, como consecuencia, provocar la pérdida de clientes, disminución del negocio o incluso responsabilidades legales. Los cambios en cómo se almacenan, procesan o usan los datos crea un riesgo. Las transformaciones a la nube suponen un gran cambio con respecto a la administración de los datos, por lo que el riesgo no debe tomarse a la ligera. [Base de referencia de la seguridad](../security-baseline/index.md), [Clasificación de los datos](./data-classification.md) y [Racionalización incremental](../../digital-estate/rationalize.md#incremental-rationalization) pueden ayudar a administrar este riesgo.

- **Interrupción del servicio.** Las operaciones empresariales y las experiencias de los clientes dependen en gran medida de las operaciones técnicas. Las transformaciones a la nube generarán cambios en las operaciones de TI. En algunas organizaciones, el cambio es pequeño y se ajusta fácilmente. En otras organizaciones, estos cambios podrían requerir nuevas herramientas, nuevos conocimientos o nuevos enfoques para admitir las operaciones en la nube. Cuanto mayor sea el cambio, mayor será el impacto potencial en las operaciones empresariales y en las experiencias de los clientes. Administrar este riesgo requerirá la participación de la empresa en el planeamiento de la transformación. El planeamiento de la versión y la selección de la primera carga de trabajo que se describen en el artículo de [racionalización incremental](../../digital-estate/rationalize.md#incremental-rationalization) describen maneras de elegir las cargas de trabajo para los proyectos de transformación. El rol de la empresa en esa actividad es comunicar el riesgo para las operaciones empresariales de cambiar las cargas de trabajo prioritarias. Ayudar al departamento de TI a elegir cargas de trabajo con un menor impacto en las operaciones reducirá el riesgo general.

- **Control del presupuesto.** Los modelos de costos cambian en la nube. Este cambio puede generar riesgos asociados con sobrecostos o aumentos en el costo de los bienes vendidos (COGS), en especial directamente atribuidos a los gastos operativos. Cuando la empresa trabaja en estrecha colaboración con TI, es posible crear la transparencia relativa a los costos y los servicios usados por varias unidades de negocio, programas o proyectos. En [Administración de costos](../cost-management/index.md) se proporcionan ejemplos de cómo pueden asociarse las empresas y los departamentos de TI en este tema.

Los anteriores son algunos de los riesgos más comunes que han mencionado los clientes. El equipo de gobernanza de la nube y los equipos de adopción de la nube pueden empezar a desarrollar un perfil de riesgo, a medida que las cargas de trabajo se migren y estén listas para pasar a producción. Prepárese para mantener conversaciones para definir, refinar y administrar los riesgos según los resultados de negocio deseados y el esfuerzo de transformación.

## <a name="understanding-risk-tolerance"></a>Conceptos sobre la tolerancia al riesgo

La identificación de riesgos es un proceso bastante directo. Los riesgos relacionados con TI suelen ser estándar en todos los sectores. Sin embargo, la tolerancia a estos riesgos es específica de cada organización. Este es el punto donde las conversaciones entre la empresa y TI tienden a estancarse. Básicamente, cada lado habla un idioma diferente. Las comparaciones y las preguntas siguientes están diseñadas para dar pie a conversaciones que ayuden a cada parte a comprender y calcular la tolerancia al riesgo.

## <a name="simple-use-case-for-comparison"></a>Caso de uso sencillo para comparación

Para ayudarle a entender la tolerancia al riesgo, vamos a examinar los datos del cliente. Si una empresa de cualquier sector publica datos de clientes en un servidor no seguro, el riesgo técnico de que los datos estén en peligro o los roben es prácticamente el mismo. Sin embargo, la tolerancia de una empresa a este riesgo variará en función de la naturaleza y el valor potencial de los datos.

- Las empresas de atención sanitaria y servicios financieros en Estados Unidos se rigen por rígidos requisitos de cumplimiento de terceros. Se da por hecho que la información de identificación personal o los datos de salud son extremadamente confidenciales. Si estas empresas se ven involucradas en los escenarios de riesgo anteriores, pueden sufrir graves consecuencias. Su tolerancia será extremadamente baja. Los datos de clientes publicados dentro o fuera de la red deberán regirse por esas directivas de cumplimiento de terceros.
- Una empresa de juegos cuyos datos de cliente se limitan a un nombre de usuario, tiempos de juego y puntuaciones más altas no es propensa a sufrir consecuencias negativas significativas más allá de una pérdida de reputación si reproduce los comportamientos de riesgo anteriores. Aunque todos los datos no protegidos están en riesgo, el impacto de ese riesgo es pequeño. Por lo tanto, la tolerancia al riesgo en este caso es alta.
- Una empresa mediana que presta servicios de limpieza de alfombras a miles de clientes estaría entre estos dos extremos de tolerancia. Los datos de los clientes pueden más sólidos, por ejemplo, contener detalles como el número de teléfono o la dirección. Ambos se podrían considerar datos de identificación personal y deben protegerse. Sin embargo, puede no haber ningún requisito específico de gobernanza que indique que los datos deben protegerse. Desde una perspectiva de TI, la respuesta es sencilla, proteger los datos. Desde una perspectiva empresarial, puede que no sea tan sencilla. La empresa necesitará más detalles antes de poder decidir un nivel de tolerancia para este riesgo.

En la siguiente sección se indican algunas preguntas de ejemplo que podrían ayudar a las empresas a decidir el nivel de tolerancia al riesgo.

## <a name="risk-tolerance-questions"></a>Preguntas de tolerancia de riesgo

En esta sección se enumeran las preguntas que dan lugar a conversaciones en tres categorías: impacto en las pérdidas, probabilidad de pérdida y costos de remediación. Cuando la empresa y el departamento de TI se asocian para abordar cada una de estas áreas, se puede llegar fácilmente a la decisión sobre la administración de los riesgos y la tolerancia general a un riesgo en particular.

**Impacto de la pérdida.** Preguntas para determinar el impacto de un riesgo. Estas preguntas son de difícil respuesta. Cuantificar el impacto es lo mejor, pero a veces la conversación por sí sola alcanza para comprender la tolerancia. También son aceptables los rangos, en particular si incluyen supuestos que determinan esos rangos.

- ¿Podría infringir este riesgo los requisitos de cumplimiento de terceros?
- ¿Podría infringir este riesgo las directivas corporativas internas?
- ¿Podría este riesgo provocar la pérdida de vidas humanas, heridas graves o daños en la propiedad?
- ¿Podría este riesgo generar un costo para los clientes o para la cuota de mercado? Si es así, ¿se puede cuantificar este costo?
- ¿Podría este riesgo crear experiencias de cliente negativas? ¿Es probable que estas experiencias afecten a las ventas o a los ingresos?
- ¿Puede este riesgo crear una nueva responsabilidad jurídica? Si es así, ¿hay algún antecedente de sentencias por daños y perjuicios en estos tipos de casos?
- ¿Podría este riesgo detener de operaciones empresariales? Si es así, ¿cuánto tiempo se interrumpirían las operaciones?
- ¿Podría este riesgo ralentizar las operaciones empresariales? Si es así, ¿cuánto tiempo y en qué medida?
- En esta fase de la transformación, ¿se trata de un riesgo puntual o repetido?
- ¿Aumenta o disminuye en frecuencia este riesgo a medida que avanza la transformación?
- ¿Aumenta o disminuye la probabilidad del riesgo a lo largo del tiempo?
- ¿Se ve el riesgo afectado por el tiempo? Si no se aborda, ¿pasará o empeorará el riesgo?

Estas preguntas básicas darán lugar a muchas más. Después de mantener un diálogo adecuado, se recomienda registrar los riesgos pertinentes y, cuando sea posible, cuantificarlos.

**Costos de remediación de los riesgos.** Preguntas para determinar el costo de mitigar o eliminar el riesgo. Estas preguntas pueden ser bastante directas, en particular cuando se representan en un rango.

- ¿Hay alguna solución clara? Y, en caso afirmativo, ¿cuánto cuesta?
- ¿Existen opciones para evitar o minimizar este riesgo? ¿Cuál es el rango de costos para esas soluciones?
- ¿Qué se necesita de la empresa para seleccionar la mejor solución?
- ¿Qué se necesita de la empresa para validar los costos?
- ¿Qué otras ventajas puede aportar la solución enfocada a eliminar este riesgo?

Estas preguntas simplifican las soluciones técnicas necesarias para administrar o eliminar los riesgos. Sin embargo, comunican esas soluciones de maneras que la empresa pueda integrarse rápidamente en un proceso de toma de decisiones.

**Probabilidad de pérdida.** Preguntas para determinar la probabilidad de que el riesgo se vuelva realidad. Esta es el área más difícil de cuantificar. En su lugar, se sugiere que el equipo de gobernanza de la nube cree categorías para comunicar la probabilidad, según los datos con los que se cuenta. Las siguientes preguntas pueden ayudar a crear categorías que sean significativas para el equipo.

- ¿Se ha realizado alguna investigación sobre la probabilidad de que este riesgo se materialice?
- ¿Puede el proveedor proporcionar estadísticas o referencias de la probabilidad de impacto?
- ¿Hay otras empresas del sector pertinente o vertical que se hayan visto afectadas por este riesgo?
- Además, ¿existen otras empresas en general que puedan haber sido alcanzadas por este riesgo?
- ¿Es este riesgo propio a algo que esta empresa haya hecho mal?

Después de responder estas y otras preguntas, según lo establezca el equipo de gobernanza de la nube, probablemente surjan agrupaciones de probabilidad. A continuación encontrará algunos ejemplos de agrupación que le ayudarán a empezar a trabajar:

- **Sin indicación.** No se han realizado suficientes investigaciones para determinar la probabilidad.
- **Riesgo bajo.** La investigación actual indica que no es probable que se produzca el riesgo.
- **Riesgo futuro.** La probabilidad actual es de baja. Sin embargo, la adopción continua haría necesario un nuevo análisis.
- **Riesgo medio.** Es probable que el riesgo afecte al negocio.
- **Riesgo alto.** Con el tiempo, cada vez es más probable que el riesgo afecte al negocio.
- **Riesgo en declive.** El riesgo es de medio a alto. Sin embargo, las acciones del departamento de TI o de la empresa están reduciendo la probabilidad de impacto.

**Determinación de la tolerancia.**

Los tres conjuntos de preguntas anteriores deben hacer surgir datos suficientes para determinar las tolerancias iniciales. Cuando el riesgo y la probabilidad son bajos, y el costo de remediación es alto, es poco probable que la empresa invierta en remediarlo. Si el riesgo y la probabilidad son altos, es probable que la empresa considere la posibilidad de realizar una inversión, siempre y cuando los costos no superen los posibles riesgos.

## <a name="next-steps"></a>Pasos siguientes

Este tipo de conversación puede ayudar a las empresas y a TI a evaluar la tolerancia de forma más eficaz. Estas conversaciones pueden usarse durante la creación de directivas de MVP y durante las revisiones de directivas incrementales.

> [!div class="nextstepaction"]
> [Definición de la directiva corporativa](./policy-definition.md)
