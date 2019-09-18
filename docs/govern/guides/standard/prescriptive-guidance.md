---
title: 'Guía para empresa estándar: Guías prescriptivas explicadas'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Más información sobre las guías prescriptivas para la gobernanza en empresas estándar.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 8cc3c5564d51a096f2794ec62e50c19a2a8e740c
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032213"
---
# <a name="standard-enterprise-guide-prescriptive-guidance-explained"></a>Guía para empresa estándar: Guías prescriptivas explicadas

La guía de gobernanza empieza con un conjunto de [directivas corporativas](./initial-corporate-policy.md) iniciales. Estas directivas se usan para establecer un producto viable mínimo de gobernanza que refleje los [procedimientos recomendados](./index.md).

En este artículo, se abordarán las estrategias generales necesarias para crear un MVP de gobernanza. En el centro del MVP de gobernanza se encuentra la materia de [aceleración de la implementación](../../deployment-acceleration/index.md). Las herramientas y los patrones que se aplican en esta etapa darán lugar a las mejoras graduales necesarias para expandir la gobernanza en el futuro.

## <a name="governance-mvp-initial-governance-foundation"></a>Producto viable mínimo de gobernanza (base de gobernanza inicial)

La rápida adopción de las directivas corporativas y de gobernanza es factible gracias a unos pocos principios sencillos y a las herramientas de gobernanza basadas en la nube. Estas son las tres primeras materias a las que se debe prestar atención en cualquier proceso de gobernanza. Cada una de las materias se describirá más detalladamente en este artículo.

Para establecer el punto de partida, en este artículo se tratarán las estrategias generales que subyacen a la línea de base de identidad, la línea de base de seguridad y la aceleración de implementación que son necesarias para crear un MVP de gobernanza, lo que servirá como base para toda la adopción.

![Ejemplo de un MVP de gobernanza incremental](../../../_images/govern/governance-mvp.png)

## <a name="implementation-process"></a>Proceso de implementación

La implementación del MVP de gobernanza tiene dependencias de identidad, seguridad y redes. Una vez resueltas las dependencias, el equipo de gobernanza de la nube decidirá algunos aspectos de la gobernanza. Las decisiones del equipo de gobernanza de la nube y de los equipos auxiliares se implementarán a través de un único paquete de recursos de cumplimiento.

![Ejemplo de un MVP de gobernanza incremental](../../../_images/govern/governance-mvp-implementation-flow.png)

Esta implementación también se puede describir con una simple lista:

1. Solicitar decisiones con respecto a las dependencias principales: Identidad, redes, supervisión y cifrado.
2. Determinar el patrón que se usará durante el cumplimiento de las directivas corporativas.
3. Determinar los patrones de gobernanza apropiados para las materias de coherencia de los recursos, etiquetado de recursos y registro e informes.
4. Implementar las herramientas de gobernanza alineadas con el patrón elegido de cumplimiento de directivas para aplicar las decisiones dependientes y las decisiones de gobernanza.

[!INCLUDE [implementation-process](../../../../includes/implementation-process.md)]

## <a name="application-of-governance-defined-patterns"></a>Aplicación de patrones definidos por gobernanza

El equipo de gobernanza de la nube es responsable de las siguientes decisiones e implementaciones. Muchas requieren aportaciones de otros equipos, pero es probable que el equipo de gobernanza de la nube sea el responsable de la decisión y la implementación. En las siguientes secciones se describen las decisiones tomadas para este caso de uso y los detalles de cada decisión.

### <a name="subscription-design"></a>Detalles de la suscripción

La decisión sobre qué diseño de suscripción usar determina cómo se estructuran las suscripciones de Azure y cómo se usarán los grupos de administración de Azure para administrar de forma eficaz el acceso, las directivas y el cumplimiento de estas suscripciones. En este ejemplo, el equipo de gobernanza ha elegido el patrón de diseño de suscripciones de [producción y de no producción](../../../decision-guides/subscriptions/index.md#production-and-nonproduction-pattern).

- Es probable que no se necesiten los departamentos, dado el foco actual. Se espera que las implementaciones puedan restringirse en una sola unidad de facturación. En la fase de adopción, incluso podría no haber un contrato Enterprise para centralizar la facturación. Es probable que este nivel de adopción se administre mediante una única suscripción de pago por uso de Azure.
- Independientemente del uso de EA Portal o de la existencia de un contrato Enterprise, se debe definir y acordar un modelo de suscripción para minimizar la sobrecarga administrativa más allá de solo la facturación.
- Debe acordarse una convención de nomenclatura común como parte del diseño de suscripción, en función de los dos puntos anteriores.

### <a name="resource-consistency"></a>Coherencia de recursos

Las decisiones relacionadas con la coherencia de los recursos determinan las herramientas, los procesos y el esfuerzo necesarios para garantizar que los recursos de Azure se implementan, configuran y administran de forma coherente dentro de una suscripción. En este caso, se ha elegido el patrón **[coherencia de la implementación](../../../decision-guides/resource-consistency/index.md#deployment-consistency)** como el principal patrón de coherencia de los recursos.

- Se crean grupos de recursos para las aplicaciones mediante el enfoque del ciclo de vida: todo lo que se crea unido, se mantiene unido y se retira unido puede residir en un único grupo de recursos.
- Azure Policy se debe aplicar a todas las suscripciones del grupo de administración asociado.
- Como parte del proceso de implementación, las plantillas de coherencia de recursos de Azure para el grupo de recursos deben almacenarse en el control de código fuente.
- Cada grupo de recursos se asocia con una aplicación o carga de trabajo específica que se basa en el enfoque del ciclo de vida que se indicó anteriormente.
- Los grupos de administración de Azure permiten actualizar los diseños de gobernanza a medida que madura la directiva corporativa.
- La amplia implementación de Azure Policy podría superar los compromisos temporales del equipo, y es posible que no proporcione mucho valor en este momento. Sin embargo, debe crearse una directiva predeterminada simple y aplicarse a cada grupo de administración para hacer cumplir el pequeño número de instrucciones de la directiva de gobernanza en la nube. Esta directiva definirá la implementación de los requisitos de gobernanza específicos. Esas implementaciones pueden aplicarse a todos los recursos implementados.

>[!IMPORTANT]
>Siempre que un recurso de un grupo deje de compartir el mismo ciclo de vida, se debe trasladar a otro grupo de recurso. Entre los ejemplos se incluyen bases de datos y componentes de red habituales. Aunque pueden servir a la aplicación que se está desarrollando, también pueden servir para otros fines y, por tanto, existir en otros grupos de recursos.

### <a name="resource-tagging"></a>Etiquetado de recursos

Las decisiones sobre el etiquetado de recursos determinan cómo se aplican los metadatos a los recursos de Azure de una suscripción con fines operativos, administrativos y contables. En este caso, se ha elegido el patrón **[Clasificación](../../../decision-guides/resource-tagging/index.md#resource-tagging-patterns)** como modelo predeterminado del etiquetado de recursos.

- Los recursos implementados se deben etiquetar con:
  - Clasificación de datos
  - Grado de importancia
  - Contrato de nivel de servicio
  - Entorno
- Estos cuatro valores impulsarán las decisiones de gobernanza, operaciones y seguridad.
- Si esta guía de gobernanza se implementa en una unidad de negocio o un equipo dentro de una empresa más grande, el etiquetado también debe incluir los metadatos para la unidad de facturación.

### <a name="logging-and-reporting"></a>Registro e informes

Las decisiones sobre registro e informes determinan cómo el almacén registra los datos y cómo se estructuran las herramientas de supervisión e informe que mantienen al personal de TI informado del estado operativo. En este ejemplo, se sugiere un [patrón nativo en la nube](../../../decision-guides/logging-and-reporting/index.md#cloud-native)** para el registro y los informes.

## <a name="incremental-improvement-of-governance-processes"></a>Mejora gradual de los procesos de gobernanza

A medida que cambia la gobernanza, algunas declaraciones de las directivas no pueden o no deben controlarse mediante herramientas automatizadas. Con el tiempo, otras directivas generarán un esfuerzo por parte del equipo de seguridad de TI y el equipo de administración de identidades local. Para ayudar a administrar los nuevos riesgos que surjan, el equipo de gobernanza de la nube supervisará los procesos siguientes.

**Aceleración de la adopción:** El equipo de gobernanza de la nube ha estado revisando los scripts de implementación en varios equipos. Mantienen un conjunto de scripts que actúan como plantillas de implementación. Los equipos de adopción de la nube y de DevOps usan esas plantillas para definir más rápidamente las implementaciones. Cada uno de esos scripts contiene los requisitos necesarios para hacer cumplir un conjunto de directivas de gobernanza, sin ningún esfuerzo adicional por parte de los ingenieros de adopción de la nube. Como responsables de estos scripts, el equipo de gobernanza de la nube puede implementar más rápidamente los cambios de directivas. Como resultado de la protección de los scripts, se considera al equipo de gobernanza de la nube como una fuente de aceleración de la adopción. Esto genera coherencia entre las implementaciones, sin forzar la adhesión de manera estricta.

**Aprendizaje para ingenieros:** El equipo de gobernanza de la nube ofrece sesiones de aprendizaje cada dos meses y ha creado dos vídeos para ingenieros. Estos materiales ayudan a los ingenieros a aprender rápidamente la cultura de gobernanza y cómo se hacen las cosas durante las implementaciones. El equipo está agregando recursos de aprendizaje para mostrar la diferencia entre las implementaciones de producción y las que no son de producción, de modo que los ingenieros comprendan cómo afectarán las nuevas directivas al proceso de adopción. Esto genera coherencia entre las implementaciones, sin forzar la adhesión de manera estricta.

**Planeación de la implementación:** Antes de implementar cualquier recurso que contenga datos protegidos, el equipo de gobernanza de la nube revisará los scripts de implementación para validar la alineación con la gobernanza. Se auditará a los equipos existentes con implementaciones previamente aprobadas, mediante herramientas de programación.

**Auditoría mensual e informes:** Cada mes, el equipo de gobernanza realiza una auditoría de todas las implementaciones de la nube para validar la alineación continua con las directivas. Cuando se detectan desviaciones, se documentan y comparten con los equipos de la adopción de la nube. Cuando el cumplimiento no pone en riesgo una interrupción del negocio ni una pérdida de datos, las directivas se cumplen automáticamente. Al final de la auditoría, el equipo de gobernanza de la nube compila un informe para el equipo de estrategia de la nube y cada equipo de adopción de la nube para comunicar la adhesión general a las directivas. El informe también se almacena con fines de auditoría y legales.

**Revisión trimestral de las directivas:** Cada trimestre, el equipo de gobernanza y el equipo de estrategia de la nube revisan los resultados de la auditoría y sugieren cambios relacionados con las directivas corporativas. Muchas de las sugerencias son consecuencia de mejoras continuas y de la observación de los patrones de uso. Los cambios aprobados en la directiva se integran en las herramientas de gobernanza durante los ciclos de auditoría subsiguientes.

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

Una vez que se implemente esta guía, cada equipo de adopción de la nube puede continuar con una base sólida de gobernanza. El equipo de gobernanza de la nube trabajará en paralelo para actualizar continuamente las directivas corporativas y las materias de gobernanza.

Los dos equipos usarán los indicadores de tolerancia para identificar el próximo conjunto de mejoras necesario para seguir impulsando la adopción de la nube. Para la empresa ficticia de esta guía, el siguiente paso es mejorar la base de referencia de la seguridad para respaldar la migración de datos protegidos a la nube.

> [!div class="nextstepaction"]
> [Mejora de la materia de base de referencia de la seguridad](./security-baseline-improvement.md)
