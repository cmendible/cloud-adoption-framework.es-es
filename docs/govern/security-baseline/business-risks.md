---
title: Motivaciones y riesgos empresariales de la base de referencia de la seguridad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Motivaciones y riesgos empresariales de la base de referencia de la seguridad
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 937eb35c07996e57bc51f85090f8e1fd136848f8
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222283"
---
# <a name="security-baseline-motivations-and-business-risks"></a>Motivaciones y riesgos empresariales de la base de referencia de la seguridad

En este artículo se describen las razones por las que los clientes normalmente adoptan una materia sobre la base de referencia de la seguridad dentro de una estrategia de gobernanza de la nube. También se proporcionan algunos ejemplos de posibles riesgos empresariales que pueden motivar las declaraciones de directiva.

<!-- markdownlint-disable MD026 -->

## <a name="security-baseline-relevancy"></a>Importancia de la línea de base de seguridad

La seguridad es una preocupación clave en cualquier organización de TI. Las implementaciones en la nube se enfrentan a los mismos riesgos para la seguridad que las cargas de trabajo hospedadas en los centros de datos locales tradicionales. Sin embargo, por su naturaleza, las plataformas de nube pública no poseen la propiedad directa del hardware físico que almacena y ejecuta las cargas de trabajo, lo que implica que la seguridad en la nube necesita sus propias directivas y procesos.

Uno de los elementos principales que diferencia la gobernanza de la seguridad en la nube de las directivas de seguridad tradicionales es la facilidad con la que se pueden crear recursos, que agregan posibles vulnerabilidades si no se tiene en cuenta la seguridad antes de la implementación. La flexibilidad que las tecnologías tales como [las redes definidas por software (SDN)](../../decision-guides/software-defined-network/index.md) ofrecen para cambiar rápidamente la topología de una red basada en la nube puede modificar también la superficie de la red que queda expuesta a ataques fácilmente y de formas imprevistas. Las plataformas de nube también proporcionan herramientas y características que pueden mejorar las funcionalidades de seguridad de maneras no siempre es posible en entornos locales.

La inversión necesaria en directivas y procesos de seguridad dependerá mucho la naturaleza de su implementación en la nube. Las implementaciones de prueba iniciales solo necesitarán las directivas de seguridad más básicas, mientras que una carga de trabajo crítica implicará abordar necesidades de seguridad exhaustivas y complejas. Todas las implementaciones deberán aplicar la materia en algún nivel.

La materia sobre la base de referencia de la seguridad abarca las directivas corporativas y los procesos manuales que puede poner en marcha para proteger una implementación en la nube frente a los riesgos para la seguridad.

> [!NOTE]
>Aunque es importante comprender la [base de referencia de la identidad](../identity-baseline/index.md) en el contexto de la base de referencia de la seguridad, y cómo se relaciona con el control de acceso, las [cinco materias sobre la gobernanza de la nube](../index.md) consideran a la [base de referencia de la identidad](../identity-baseline/index.md) como una materia propia, independiente de la base de referencia de la seguridad.

## <a name="business-risk"></a>Riesgo empresarial

La materia sobre la base de referencia de la seguridad intenta abordar los riesgos relacionados con la seguridad empresarial. Trabaje con su empresa para identificar estos riesgos y supervise cada uno de ellos para determinar su pertinencia a medida que planee y aplique sus implementaciones en la nube.

Los riesgos variarán según la organización, pero los siguientes son algunos riesgos comunes relacionados con la seguridad que puede usar como punto de partida para debatir en el seno de su equipo de gobernanza de la nube:

- **Vulneración de los datos:** La exposición accidental o la pérdida de información confidencial hospedada en la nube puede provocar la pérdida de clientes, problemas contractuales o consecuencias legales.
- **Interrupción del servicio:** Las interrupciones y otros problemas de rendimiento debidos a una infraestructura no segura interrumpe las operaciones normales y puede dar lugar a la pérdida de productividad o la pérdida de negocio.

## <a name="next-steps"></a>Pasos siguientes

Utilice la [plantilla de administración de la nube](./template.md) para documentar los riesgos empresariales que probablemente se presentarán en el plan de adopción de la nube actual.

Una vez que se consigue una comprensión realista de los riesgos empresariales, el siguiente paso es documentar la tolerancia al riesgo de la empresa y los indicadores y métricas clave para supervisar esa tolerancia.

> [!div class="nextstepaction"]
> [Descripción de indicadores, métricas y tolerancia al riesgo](./metrics-tolerance.md)
