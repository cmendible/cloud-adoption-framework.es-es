---
title: 'Guía de gobernanza para empresas complejas: Guías prescriptivas explicadas'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Más información sobre las guías prescriptivas para la gobernanza en empresas complejas.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 9992d4ee6fbd955eea44e13a7f4f31c5836ce83a
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71220655"
---
# <a name="governance-guide-for-complex-enterprises-prescriptive-guidance-explained"></a>Guía de gobernanza para empresas complejas: Guías prescriptivas explicadas

La guía de gobernanza empieza con un conjunto de [directivas corporativas](./initial-corporate-policy.md) iniciales. Estas directivas se usan para establecer un producto viable mínimo (MVP) para la gobernanza que refleje los [procedimientos recomendados](./index.md).

En este artículo, se abordarán las estrategias generales necesarias para crear un MVP de gobernanza. En el centro del MVP de gobernanza se encuentra la materia de [aceleración de la implementación](../../deployment-acceleration/index.md). Las herramientas y los patrones que se aplican en esta etapa darán lugar a las mejoras graduales necesarias para expandir la gobernanza en el futuro.

## <a name="governance-mvp-initial-governance-foundation"></a>Producto viable mínimo de gobernanza (base de gobernanza inicial)

La rápida adopción de las directivas corporativas y de gobernanza es factible gracias a unos pocos principios sencillos y a las herramientas de gobernanza basadas en la nube. Se trata de la primera de las tres materias de gobernanza para enfocarse en cualquier proceso de gobernanza. Cada una de las materias se explicará más detalladamente en este artículo.

Para establecer el punto de partida, en este artículo se tratarán las estrategias generales que subyacen a la línea de base de identidad, la línea de base de seguridad y la aceleración de implementación que son necesarias para crear un MVP de gobernanza, lo que servirá como base para toda la adopción.

![Ejemplo de un MVP de gobernanza incremental](../../../_images/govern/governance-mvp.png)

## <a name="implementation-process"></a>Proceso de implementación

La implementación del MVP de gobernanza tiene dependencias de identidad, seguridad y redes. Una vez resueltas las dependencias, el equipo de gobernanza de la nube decidirá algunos aspectos de la gobernanza. Las decisiones del equipo de gobernanza de la nube y de los equipos auxiliares se implementarán a través de un único paquete de recursos de cumplimiento.

![Ejemplo de un MVP de gobernanza incremental](../../../_images/govern/governance-mvp-implementation-flow.png)

Esta implementación también se puede describir con una simple lista:

1. Solicitar decisiones con respecto a las dependencias principales: identidad, red y cifrado.
1. Determinar el patrón que se usará durante el cumplimiento de las directivas corporativas.
1. Determinar los patrones de gobernanza apropiados para las materias de coherencia de los recursos, etiquetado de recursos y registro e informes.
1. Implementar las herramientas de gobernanza alineadas con el patrón elegido de cumplimiento de directivas para aplicar las decisiones dependientes y las decisiones de gobernanza.

[!INCLUDE [implementation-process](../../../../includes/implementation-process.md)]

## <a name="application-of-governance-defined-patterns"></a>Aplicación de patrones definidos por gobernanza

El equipo de gobernanza de la nube será responsable de las siguientes decisiones e implementaciones. Muchas requieren aportaciones de otros equipos, pero es probable que el equipo de gobernanza de la nube sea el responsable de la decisión y la implementación. En las siguientes secciones se describen las decisiones tomadas para este caso de uso y los detalles de cada decisión.

### <a name="subscription-design"></a>Detalles de la suscripción

La decisión sobre qué diseño de suscripción usar determina cómo se estructuran las suscripciones de Azure y cómo se usarán los grupos de administración de Azure para administrar de forma eficaz el acceso, las directivas y el cumplimiento de estas suscripciones. En este ejemplo, el equipo de gobernanza ha elegido el patrón de diseño de suscripciones **[Mixto](../../../decision-guides/subscriptions/index.md#mixed-patterns)** .

- Cuando surjan nuevas solicitudes de recursos de Azure, se debe establecer un "departamento" para cada unidad de negocio principal en cada ubicación geográfica operativa. Dentro de cada uno de los departamentos, deben crearse "suscripciones" para cada arquetipo de aplicación.
- Un arquetipo de aplicación es una forma de agrupar las aplicaciones con necesidades similares. Algunos ejemplos frecuentes son: Aplicaciones con datos protegidos, aplicaciones reguladas (por ejemplo, HIPAA o FedRAMP), aplicaciones de bajo riesgo, aplicaciones con dependencias en el entorno local, aplicaciones SAP u otros sistemas centrales en Azure, o aplicaciones que amplían SAP o los sistemas centrales locales. Cada organización tiene necesidades únicas según las clasificaciones de datos y los tipos de aplicaciones que respaldan al negocio. La asignación de dependencias del patrimonio digital puede ayudar a definir los arquetipos de aplicación en una organización.
- Debe acordarse una convención de nomenclatura común como parte del diseño de suscripción, en función de los dos puntos anteriores.

### <a name="resource-consistency"></a>Coherencia de recursos

Las decisiones relacionadas con la coherencia de los recursos determinan las herramientas, los procesos y el esfuerzo necesarios para garantizar que los recursos de Azure se implementan, configuran y administran de forma coherente dentro de una suscripción. En este caso, se ha elegido el patrón **[coherencia de la implementación](../../../decision-guides/resource-consistency/index.md#deployment-consistency)** como el principal patrón de coherencia de los recursos.

- Se crean grupos de recursos para las aplicaciones mediante el enfoque del ciclo de vida: todo lo que se crea, se mantiene y se retira de forma conjunta debe residir en un único grupo de recursos. Para más información sobre los grupos de recursos, consulte [aquí](../../../decision-guides/resource-consistency/index.md#basic-grouping).
- Azure Policy se debe aplicar a todas las suscripciones del grupo de administración asociado.
- Como parte del proceso de implementación, las plantillas de coherencia de recursos de Azure para el grupo de recursos deben almacenarse en el control de código fuente.
- Cada grupo de recursos se asocia con una aplicación o carga de trabajo específica que se basa en el enfoque del ciclo de vida que se indicó anteriormente.
- Los grupos de administración de Azure permiten actualizar los diseños de gobernanza a medida que madura la directiva corporativa.
- La amplia implementación de Azure Policy podría superar los compromisos temporales del equipo, y es posible que no proporcione mucho valor en este momento. Sin embargo, debe crearse una directiva predeterminada simple y aplicarse a cada grupo de administración para hacer cumplir el pequeño número de instrucciones de la directiva de gobernanza en la nube. Esta directiva definirá la implementación de los requisitos de gobernanza específicos. Esas implementaciones pueden aplicarse a todos los recursos implementados.

>[!IMPORTANT]
>Siempre que un recurso de un grupo deje de compartir el mismo ciclo de vida, se debe trasladar a otro grupo de recurso. Entre los ejemplos se incluyen bases de datos y componentes de red habituales. Aunque pueden servir a la aplicación que se está desarrollando, también pueden servir para otros fines y, por tanto, existir en otros grupos de recursos.

### <a name="resource-tagging"></a>Etiquetado de recursos

Las decisiones sobre el etiquetado de recursos determinan cómo se aplican los metadatos a los recursos de Azure de una suscripción con fines operativos, administrativos y contables. En este caso, se ha elegido el patrón **[Contabilidad](../../../decision-guides/resource-tagging/index.md#resource-tagging-patterns)** como modelo predeterminado del etiquetado de recursos.

- Los recursos implementados se deben etiquetar con valores para:
  - Departamentos o unidades de facturación
  - Geography
  - Clasificación de datos
  - Grado de importancia
  - Contrato de nivel de servicio
  - Entorno
  - Arquetipo de aplicación
  - Application
  - Application Owner
- Estos valores, junto con el grupo de administración y la suscripción de Azure asociados con un recurso implementado impulsarán las decisiones de gobernanza, operaciones y seguridad.

### <a name="logging-and-reporting"></a>Registro e informes

Las decisiones sobre registro e informes determinan cómo el almacén registra los datos y cómo se estructuran las herramientas de supervisión e informe que mantienen al personal de TI informado del estado operativo. En este caso, se sugiere un patrón de **[supervisión híbrida](../../../decision-guides/logging-and-reporting/index.md)** para el registro y los informes, pero no es obligatorio para ningún equipo de desarrollo en este momento.

- Actualmente, no hay establecido ningún requisito de gobernanza con respecto a los puntos de datos específicos que deben recopilarse para fines de registro o informes. Esto es específico de esta narración ficticia y debe considerarse un antipatrón. Los estándares de registro deben determinarse y cumplirse tan pronto como sea posible.
- Se requiere un análisis adicional antes de la publicación de datos protegidos o cargas de trabajo críticas.
- Antes de admitir datos protegidos o cargas de trabajo críticas, a la solución de supervisión operativa local existente se le debe conceder acceso al área de trabajo que se usó para el registro. Las aplicaciones deben satisfacer los requisitos de seguridad y registro asociados al uso de ese inquilino, si la aplicación contará con un SLA definido.

## <a name="incremental-of-governance-processes"></a>Mejora gradual de los procesos de gobernanza

Algunas de las instrucciones de directiva no pueden o no deben controlarse mediante herramientas automatizadas. Otras directivas exigirán un esfuerzo periódico de los equipos de seguridad de TI y de línea de base de identidad local. El equipo de gobernanza de la nube deberá supervisar los siguientes procesos para implementar las últimas ocho declaraciones de las directivas:

**Cambios en la directiva corporativa:** El equipo de gobernanza de la nube hará cambios en el diseño del producto viable mínimo de gobernanza para adoptar las nuevas directivas. El valor del MVP de gobernanza es que permitirá el cumplimiento automático de las nuevas directivas.

**Aceleración de la adopción:** El equipo de gobernanza de la nube ha estado revisando los scripts de implementación de varios equipos. Ha mantenido un conjunto de scripts que actúan como plantillas de implementación. Los equipos de adopción de la nube y los equipos de DevOps pueden usar esas plantillas para definir más rápidamente las implementaciones. Cada script contiene los requisitos para hacer cumplir las directivas de gobernanza, y no es necesario un esfuerzo adicional por parte de los ingenieros de adopción de la nube. Como curadores de estos scripts, pueden implementar más rápidamente los cambios de directiva. Además, se los considera aceleradores de la adopción. Esto garantiza implementaciones coherentes sin que se aplique la adhesión de manera estricta.

**Aprendizaje para ingenieros:** El equipo de gobernanza de la nube ofrece sesiones de aprendizaje cada dos meses y ha creado dos vídeos para ingenieros. Ambos recursos ayudan a los ingenieros a ponerse al día rápidamente con la cultura de gobernanza y con cómo se realizan las implementaciones. El equipo está agregando recursos de aprendizaje para mostrar las diferencias entre las implementaciones de producción y las que no son de producción, lo que ayuda a los ingenieros a comprender la manera en que las nuevas directivas afectan a la adopción. Esto garantiza implementaciones coherentes sin que se aplique la adhesión de manera estricta.

**Planeación de la implementación:** Antes de la implementación de cualquier recurso que contenga datos protegidos, el equipo de gobernanza de la nube será responsable de revisar los scripts de implementación para validar la alineación de gobernanza. Se auditará a los equipos existentes con implementaciones previamente aprobadas, mediante herramientas de programación.

**Auditoría mensual e informes:** Cada mes, el equipo de gobernanza realiza una auditoría de todas las implementaciones de la nube para validar la alineación continua con las directivas. Cuando se detectan desviaciones, se documentan y comparten con los equipos de la adopción de la nube. Cuando el cumplimiento no pone en riesgo una interrupción del negocio ni una pérdida de datos, las directivas se cumplen automáticamente. Al final de la auditoría, el equipo de gobernanza de la nube compila un informe para el equipo de estrategia de la nube y cada equipo de adopción de la nube para comunicar la adhesión general a las directivas. El informe también se almacena con fines de auditoría y legales.

**Revisión trimestral de la directiva:** Cada trimestre, el equipo de gobernanza de la nube y el equipo de estrategia de la nube revisan los resultados de la auditoría y sugieren cambios relacionados con la directiva corporativa. Muchas de las sugerencias son consecuencia de mejoras continuas y de la observación de los patrones de uso. Los cambios aprobados en la directiva se integran en las herramientas de gobernanza durante los ciclos de auditoría subsiguientes.

## <a name="alternative-patterns"></a>Patrones alternativos

Si cualquiera de los patrones seleccionados en esta guía de gobernanza no se adapta a los requisitos del lector, existen otras alternativas para cada patrón:

- [Patrones de cifrado](../../../decision-guides/encryption/index.md)
- [Patrones de identidad](../../../decision-guides/identity/index.md)
- [Patrones de registro e informes](../../../decision-guides/logging-and-reporting/index.md)
- [Patrones de cumplimiento de directivas](../../../decision-guides/policy-enforcement/index.md)
- [Patrones de coherencia de recursos](../../../decision-guides/resource-consistency/index.md)
- [Patrones de etiquetado de recursos](../../../decision-guides/resource-tagging/index.md)
- [Patrones de redes definidos por software](../../../decision-guides/software-defined-network/index.md)
- [Patrones de diseño de suscripciones](../../../decision-guides/subscriptions/index.md)

## <a name="next-steps"></a>Pasos siguientes

Una vez que se implemente esta guía, cada equipo de adopción de la nube puede continuar con una base sólida de gobernanza. Al mismo tiempo, el equipo de gobernanza de la nube trabajará para actualizar continuamente las directivas corporativas y las materias de gobernanza.

Ambos equipos usarán los indicadores de tolerancia para identificar el próximo conjunto de mejoras necesario para seguir impulsando la adopción de la nube. El siguiente paso para la empresa es la mejora gradual de su línea de base de gobernanza para dar servicio a aplicaciones con requisitos de autenticación multifactor heredada o de terceros.

> [!div class="nextstepaction"]
> [Mejora de la materia de línea de base de identidad](./identity-baseline-improvement.md)
