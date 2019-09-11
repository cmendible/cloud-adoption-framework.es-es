---
title: Guía de decisiones de nomenclatura y etiquetado de recursos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información acerca de la organización y el etiquetado de recursos como servicio principal en las migraciones de Azure.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: cd4d6e7a017c9a71c090110720c28701082ce792
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817560"
---
# <a name="resource-naming-and-tagging-decision-guide"></a>Guía de decisiones de nomenclatura y etiquetado de recursos

La organización de los recursos basados en la nube es una de las tareas más importantes para TI, a menos que solo tenga implementaciones simples. Organizar los recursos tiene tres objetivos principales:

- **Administración de recursos:** Los equipos de TI deberán encontrar rápidamente los recursos asociados con cargas de trabajo específicas, entornos, grupos de propiedad u otra información importante. Organizar los recursos es fundamental para la asignación de roles de la organización y los permisos de acceso para la administración de recursos.
- **Automation:** Además de facilitar la administración de los recursos para TI, un esquema organizativo correcto le permite aprovechar las ventajas de la automatización como parte de la creación de recursos, la supervisión operativa y la creación de procesos de DevOps.
- **Contabilidad:** Para que los grupos empresariales conozcan el consumo de recursos en la nube se requiere que TI comprenda qué cargas de trabajo y equipos usan determinados recursos. Para admitir otros enfoques como la contabilidad chargeback y showback, se deben organizar los recursos en la nube para reflejar la propiedad y el uso.

## <a name="tagging-decision-guide"></a>Guía de decisiones de identidades

![Trazado de opciones de identidades de menos a más complejas, alineadas con vínculos](../../_images/discovery-guides/discovery-guide-tagging.png)

Vaya a: [Convenciones de nomenclatura de línea de base](#baseline-naming-conventions) | [Patrones de etiquetado de recursos](#resource-tagging-patterns) | [Más información](#learn-more)

El enfoque del etiquetado puede ser simple o complejo, con un énfasis que puede ir desde la admisión de que los equipos de TI administren cargas de trabajo en la nube hasta la integración de la información relativa a todos los aspectos del negocio.

Un foco de etiquetado alineado con TI, como el etiquetado en función de la carga de trabajo, la función o el entorno, reduce la complejidad de la supervisión de los recursos y hacer más fácil tomar decisiones de administración según los requisitos operativos.

Los esquemas de etiquetado que incluyen un foco alineado con el negocio, como la contabilidad, la propiedad del negocio o la importancia empresarial, pueden requerir una mayor inversión de tiempo para crear estándares de etiquetado que reflejen los intereses del negocio y conserven esos estándares a lo largo del tiempo. Sin embargo, el resultado de este proceso es un sistema de etiquetado que proporciona una mejora en la capacidad para contabilizar los costos y el valor de los recursos de TI en el negocio en general. Esta asociación del valor de negocio de un recurso a su costo operativo es uno de los primeros pasos para cambiar la percepción del centro de costo de TI dentro de una organización mayor.

## <a name="baseline-naming-conventions"></a>Convenciones de nomenclatura de línea de base

Una convención de nomenclatura estandarizada es el punto de partida para organizar los recursos hospedados en la nube. Un sistema de nomenclatura estructurado correctamente permite identificar con rapidez los recursos para la administración y la contabilidad. Si existen convenciones de nomenclatura de TI en otras partes de la organización, considere si las convenciones de nomenclatura en la nube deben alinearse con ellas o si debe establecer estándares basados en la nube independientes.

Tenga en cuenta también que los diferentes tipos de recursos de Azure tienen diferentes [requisitos de nomenclatura](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions#naming-rules-and-restrictions). Las convenciones de nomenclatura deben ser compatibles con estos requisitos de nomenclatura.

## <a name="resource-tagging-patterns"></a>Patrones de etiquetado de recursos

Para una organización más sofisticada que la que solo una convención de nomenclatura coherente puede proporcionar, las plataformas de nube admiten la capacidad de etiquetar los recursos.

Las *etiquetas* son elementos de metadatos asociados a los recursos. Las etiquetas constan de cadenas de pares de clave y valor. Los valores incluidos en estos pares dependerán del usuario, pero la aplicación de un conjunto coherente de etiquetas globales, como parte de una directiva completa de nomenclatura y etiquetado, es una parte fundamental de una directiva de gobernanza general.

Como parte del proceso de planeación, utilice las siguientes preguntas para ayudar a determinar el tipo de información que deben admitir las etiquetas de recursos:

- ¿Es necesario integrar las directivas de nomenclatura y etiquetado con las directivas organizativas y de nomenclatura existentes dentro de la organización?
- ¿Va a implementar un sistema de contabilidad chargeback o showback? ¿Necesitará asociar los recursos con información contable por departamentos, grupos de negocio y equipos con más detalle que un desglose de nivel de suscripción simple?
- ¿Es necesario que el etiquetado represente detalles tales como los requisitos de cumplimiento normativo de un recurso? ¿Qué sucede con los detalles operativos tales como los requisitos de tiempo de actividad, las programaciones de aplicación de revisiones o los requisitos de seguridad?
- ¿Qué etiquetas serán necesarias para todos los recursos en función de la directiva de TI central? ¿Qué etiquetas serán opcionales? ¿Los equipos individuales pueden implementar sus propios esquemas de etiquetado personalizados?

Los patrones de etiquetado comunes que se enumeran a continuación proporcionan ejemplos de cómo se puede usar el etiquetado para organizar los recursos en la nube. Estos patrones no están diseñados para ser exclusivos y se pueden usar en paralelo, lo que proporciona varias maneras de organizar los recursos según las necesidades de la empresa.

<!-- markdownlint-disable MD033 -->

| Tipo de etiqueta | Ejemplos | DESCRIPCIÓN |
|-----|-----|-----|
| Funcional            | app = búsquedacatálogo1 <br/>tier = web <br/>webserver = apache<br/>env = prod <br/>env = almacenamientoprovisional <br/>env = des                 | Clasifique los recursos en relación con su finalidad dentro de una carga de trabajo, el entorno en el que se implementaron u otra funcionalidad y detalle operativo.                                 |
| clasificación        | confidentiality = privada<br/>sla = 24horas                                 | Clasifica un recurso por cómo se utiliza y qué directivas se le aplican.                               |
| Control            | department = finanzas <br/>project = búsquedacatálogo <br/>region = norteamérica | Permite asociar el recurso con grupos específicos dentro de una organización para la facturación. |
| Asociación           | owner = jsmith <br/>contactalias = catsearchowners<br/>stakeholders = usuario1;usuario2;usuario3<br/>                       | Proporciona información sobre los usuarios (fuera de TI) relacionados o que pueden verse afectados por el recurso.                      |
| Propósito               | businessprocess = compatibilidad<br/>businessimpact = moderado<br/>revenueimpact = alto   | Alinea los recursos con las funciones de negocio para admitir mejor las decisiones de inversión.  |

<!-- markdownlint-enable MD033 -->

## <a name="learn-more"></a>Más información

Para obtener más información sobre la nomenclatura y etiquetado en Azure, consulte:

- [Convenciones de nomenclatura para los recursos de Azure](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). Consulte esta guía para convenciones de nomenclatura recomendadas para los recursos de Azure.
- [Uso de etiquetas para organizar los recursos de Azure](/azure/azure-resource-manager/resource-group-using-tags?toc=/azure/billing/TOC.json). Puede aplicar etiquetas en Azure en los niveles de grupo de recursos y de recurso individual, lo que ofrece flexibilidad en la granularidad de los informes de contabilidad en función de las etiquetas aplicadas.

## <a name="next-steps"></a>Pasos siguientes

El etiquetado de recursos es solo uno de los principales componentes de infraestructura que requieren decisiones de arquitectura durante un proceso de adopción de la nube. Visite la [introducción a las guías de decisión](../index.md) para obtener información sobre los patrones o los modelos alternativos que se usan al tomar decisiones de diseño para otros tipos de infraestructura.

> [!div class="nextstepaction"]
> [Guías de decisiones sobre arquitectura](../index.md)
