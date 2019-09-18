---
title: Declaraciones de la directiva de ejemplo de aceleración de la implementación
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Declaraciones de la directiva de ejemplo de aceleración de la implementación
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 4a2b1666332ca884dfb95b2b2372f3b5518bd635
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031218"
---
# <a name="deployment-acceleration-sample-policy-statements"></a>Declaraciones de la directiva de ejemplo de aceleración de la implementación

Las declaraciones individuales de directiva de nube son directrices para abordar los riesgos específicos identificados durante el proceso de evaluación de riesgos. Estas declaraciones deben proporcionar un breve resumen de los riesgos y los planes para resolverlos. La definición de cada declaración debe incluir estos fragmentos de información:

- **Riesgos técnicos**. Un resumen del riesgo que esta directiva abordará.
- **Declaración de directiva**. Una explicación clara que resuma los requisitos de la directiva.
- **Opciones de diseño**. Recomendaciones que requieren acción, especificaciones u otras instrucciones que los equipos de TI y los desarrolladores pueden usar al implementar la directiva.

Las siguientes declaraciones de la directiva de ejemplo abordan algunos riesgos empresariales comunes relacionados con la configuración. Estas declaraciones son ejemplos a los que se puede hacer referencia al elaborar el borrador de las declaraciones de directiva para satisfacer las necesidades de su organización. Estos ejemplos no pretenden ser excluyentes y hay varias opciones posibles de directiva para solucionar cada riesgo concreto identificado. Trabaje estrechamente con los equipos de TI y de dirección para identificar las mejores directivas para su conjunto de riesgos en particular.

## <a name="reliance-on-manual-deployment-or-configuration-of-systems"></a>Dependencia de la configuración o implementación manual de sistemas

**Riesgo técnico:** depender de la intervención humana durante la implementación o configuración aumenta la probabilidad de error humano y reduce la repetibilidad y previsión de las implementaciones y la configuración del sistema. Normalmente, también conlleva una implementación más lenta de los recursos del sistema.

**Declaración de directiva**: todos los recursos que se implementan en la nube deben implementarse mediante plantillas o scripts de automatización siempre que sea posible.

**Opciones de diseño posibles:** las [plantillas de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) proporcionan un enfoque de infraestructura como código para implementar los recursos en Azure. Los [bloques de creación de Azure](https://github.com/mspnp/template-building-blocks/wiki) proporcionan una herramienta de línea de comandos y un conjunto de plantillas de Resource Manager diseñadas para simplificar la implementación de los recursos de Azure.

## <a name="lack-of-visibility-into-system-issues"></a>Falta de visibilidad de los problemas del sistema

**Riesgo técnico:** una supervisión y un diagnóstico insuficientes de los sistemas empresariales impiden al personal de operaciones identificar y corregir problemas antes de que se produzca una interrupción del sistema, lo que puede aumentar considerablemente el tiempo necesario para resolver correctamente una interrupción.

**Declaración de directiva**: se implementarán las siguientes directivas:

- Se identificarán medidas de diagnóstico y métricas clave para todos los sistemas de producción y los componentes, y se aplicarán herramientas de supervisión y diagnóstico a estos sistemas, que el personal de operaciones se encargará de supervisar regularmente.
- El personal de operaciones considerará la opción de usar las herramientas de supervisión y diagnóstico en entornos que no sean de producción, como ensayo y control de calidad, a fin de identificar los problemas del sistema antes de que se produzcan en el entorno de producción.

**Opciones de diseño posibles:** [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor), que también incluye Log Analytics y Application Insights, proporciona herramientas para recopilar y analizar datos de telemetría para ayudarle a comprender cómo funcionan las aplicaciones e identificar proactivamente los problemas que les afectan y los recursos de los que dependen.

## <a name="configuration-security-reviews"></a>Revisiones de seguridad de configuración

**Riesgo técnico:** con el tiempo, los nuevos problemas y amenazas de seguridad pueden aumentar los riesgos de acceso no autorizado a recursos seguros.

**Declaración de directiva**: los procesos de gobernanza en la nube deben incluir revisiones trimestrales con los equipos de administración de configuración para así poder identificar usuarios malintencionados o patrones de uso que deban evitarse mediante la configuración de recursos en la nube.

**Opciones de diseño posibles:** celebrar una reunión de revisión de seguridad trimestral en la que participen los miembros del equipo de gobernanza y el personal de TI responsable de los recursos y las aplicaciones de configuración en la nube. Revisar las métricas y los datos de seguridad existentes para identificar deficiencias en las herramientas y la directiva de aceleración de la implementación y actualizar la directiva para remediar todos los nuevos riesgos.

## <a name="next-steps"></a>Pasos siguientes

Use los ejemplos mencionados en este artículo como punto de partida para desarrollar directivas que aborden los riesgos de negocio específicos que se alinean con los planes de adopción de la nube.

Para comenzar a desarrollar sus propias declaraciones de directiva personalizadas relacionadas con la administración de identidad, descargue la [plantilla de base de referencia de identidad](./template.md).

Para acelerar la adopción de esta materia, elija la [guía accionable de gobernanza](../guides/index.md) que más se ajuste a su entorno. Después, modifique el diseño para incorporar las decisiones de directiva específicas de su organización.

A partir de los riesgos y la tolerancia, establezca un proceso para regular y comunicar la adhesión a la directiva de aceleración de la implementación.

> [!div class="nextstepaction"]
> [Establecimiento de procesos para el cumplimiento de directivas](./compliance-processes.md)
