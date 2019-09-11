---
title: Lista de comprobación del ámbito ampliado de la migración a la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Lista de comprobación del ámbito ampliado de la migración a la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 125c6d044fd766896971aced5bedbc515c14417f
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817339"
---
# <a name="expanded-scope-for-cloud-migration"></a>Ámbito ampliado para la migración a la nube

La [guía de migración a Azure](../azure-migration-guide/index.md) en Cloud Adoption Framework es el punto inicial sugerido para los lectores que estén interesados en una migración a Azure, también conocida como migración "lift and shift". Esta guía le guiará a través de una serie de requisitos previos, herramientas y enfoques para la migración de máquinas virtuales a la nube.

Si bien esta guía es una base de referencia eficaz para familiarizarse con este tipo de migración, hace varias suposiciones. Estos supuestos alinean la guía con un gran porcentaje de lectores de Cloud Adoption Framework al proporcionar un enfoque simplificado de las migraciones. En esta sección de Cloud Adoption Framework se abordan algunos escenarios de migración de ámbito ampliado, que ayudan a guiar los esfuerzos cuando esos supuestos no se aplican.

## <a name="cloud-migration-expanded-scope-checklist"></a>Lista de comprobación del ámbito ampliado de la migración a la nube

En la siguiente lista de verificación se describen las áreas comunes de complejidad que podrían requerir que el ámbito de la migración se ampliara más allá de la [guía de migración a Azure](../azure-migration-guide/index.md).

- **Cambios en el ámbito orientados a los negocios:**
  - [Equilibrio de la cartera](./balance-the-portfolio.md)
  - [Compatibilidad con los mercados internacionales](./multiple-regions.md)
  - Conciencia de costos durante una migración *(A partir del 3T de 2019)*
- **Cambios en el ámbito orientados a las referencias culturales:**
  - Administración de cambios y procesos de aprobación *(A partir del 3T de 2019)*
  - Preparación ejecutiva *(A partir del 3T de 2019)*
  - [Preparación de las aptitudes](./suggested-skills.md)
  - Alineación del soporte técnico (asociados, servicios y soporte técnico) *(A partir del 3T de 2019)*
- **Cambios en el ámbito orientados a la estrategia técnica:**
  - Restricciones de centro de datos existente *(A partir del 3T de 2019)*
  - Migración a escala: gran volumen o velocidad de las migraciones *(A partir del 3T de 2019)*
  - [Varios centros de datos](./multiple-datacenters.md)
  - [Los requisitos de datos superan la capacidad de la red](./network-capacity-exceeded.md)
  - Documentación sobre soluciones y administración de cambios *(A partir del 3T de 2019)*
  - [Estrategia de cumplimiento o de gobernanza](./governance-or-compliance.md)
- **Cambios en el ámbito específicos de las cargas de trabajo:**
  - Diseño de las cargas de trabajo para proporcionar resistencia *(A partir del 3T de 2019)*
  - Alineación de la migración a patrones de aplicación *(A partir del 3T de 2019)*

Si alguna de estas complejidades se alinea con el escenario, esta sección de Cloud Adoption Framework probablemente le proporcionará el tipo de guía necesaria para alinear adecuadamente el ámbito en los procesos de migración.

Cada uno de estos escenarios se aborda en los distintos artículos de esta sección de Cloud Adoption Framework.

## <a name="scope-options-explained"></a>Opciones de ámbito explicadas

Para ayudarle a entender cada escenario de expansión del ámbito, la siguiente lista resumirá brevemente los títulos utilizados en la lista de comprobación anterior.

### <a name="business-driven-scope-changes"></a>Cambios en el ámbito orientados a los negocios

- **Equilibrio de la cartera de adopción de la nube:** El equipo de estrategia en la nube está interesado en invertir más en la migración (rehospedaje de cargas de trabajo y aplicaciones existentes con un mínimo de modificaciones) o en la innovación (refactorización o recompilación de esas cargas de trabajo y aplicaciones mediante la tecnología moderna de la nube). A menudo, el equilibrio entre las dos prioridades es la clave del éxito. En esta guía, el tema del equilibrio de la cartera de adopción de la nube es un tema común, que se trata en cada uno de los procesos de migración.
- **Apoyo de los mercados globales:** El negocio opera en varias regiones geográficas con diferentes requisitos de soberanía de datos. Para cumplir esos requisitos, deberían tenerse en cuenta consideraciones adicionales en el examen de los requisitos previos y la distribución de los recursos durante la migración.

### <a name="culture-driven-scope-changes"></a>Cambios en el ámbito orientados a las referencias culturales

- **Administración de cambios y procesos de aprobación:** Cuando la referencia cultural de la organización es compleja, está altamente estructurada en matrices o aislada, los procesos relacionados con la gestión del cambio y las aprobaciones se convierten en un reto. Se puede encontrar una guía sobre la administración de esta complejidad en la evaluación, migración y optimización de procesos.
- **Preparación ejecutiva:** Los niveles adecuados de soporte y liderazgo ejecutivos son fundamentales para el éxito de un esfuerzo de migración. Si el equipo ejecutivo no está listo para interactuar, es poco probable que el soporte llegue después. Esta complejidad se aborda durante el requisito previo y la evaluación de los procesos.
- **Preparación de las aptitudes:** Si el equipo de adopción de la nube u otros equipos de soporte no están preparados para la ejecución, esto puede suponer un rápido incremento de la complejidad del esfuerzo de migración. Este desafío se aborda durante cada uno de los procesos de migración en una página específica sobre la preparación para la migración.
- **Alineación del soporte técnico (asociados, servicios y soporte técnico):** Dentro de cada uno de los procesos descritos, hay formas en las que un asociado, los servicios del proveedor de nube y el soporte técnico del proveedor de nube pueden ayudar en la ejecución. En cada una de las secciones de los procesos, en una página sobre la alineación del soporte se tratarán más a fondo las opciones.

### <a name="technical-strategy-driven-scope-changes"></a>Cambios en el ámbito orientados a la estrategia técnica

- **Restricciones de centro de datos existente:** Con frecuencia, las empresas optan por migrar a la nube porque la capacidad, la velocidad y la estabilidad de un centro de datos existente ya no son satisfactorias. Lamentablemente, esas mismas limitaciones agregan complejidad al proceso de migración y requieren un planeamiento adicional durante los procesos de evaluación y migración.
- **Migración a escala:** Es probable que las migraciones que superen los 2000 recursos tropiecen con limitaciones que requieren un planeamiento adicional y un enfoque disciplinado de la ejecución. Los procesos de evaluación y migración se ajustan para tener en cuenta la complejidad de la escala.
- **Varios centros de datos:** La migración de múltiples centros de datos añade una gran cantidad de complejidad. Durante los procesos de evaluación, migración, optimización y administración, se describen consideraciones adicionales.
- **Documentación sobre soluciones y administración de cambios:** Los grandes inventarios de patrimonio digital, las arquitecturas de soluciones complejas, las deudas técnicas a largo plazo y las interdependencias pueden crear una complejidad que debe abordarse durante la evaluación, la migración y la optimización de los procesos.
- **Estrategia de cumplimiento o de gobernanza:** Dado que la gobernanza y el cumplimiento son vitales para el éxito de una migración, se requiere una alineación adicional entre los equipos de gobernanza de TI y el equipo de adopción de la nube.

### <a name="workload-specific-scope-changes"></a>Cambios en el ámbito específicos de las cargas de trabajo

- **Diseño de las cargas de trabajo para proporcionar resistencia:** Los principios comunes de diseño en la nube pueden ayudar a preparar cargas de trabajo críticas para mejorar la resistencia. En este artículo se explicará el impacto en un proceso de migración cuando la resistencia es un requisito de la carga de trabajo. También comparte algunos principios comunes para incluir en la configuración general del entorno a fin de mejorar la resistencia del medio ambiente.
- **Alineación de la migración a patrones de aplicación:** El patrón de migración de una carga de trabajo puede afectar a la ruta de migración elegida. En este artículo se describen algunos cambios de ámbito que se integrarían en el nivel de los elementos de trabajo de un trabajo pendiente migratorio para reflejar los diferentes enfoques de la migración por carga de trabajo.

## <a name="next-steps"></a>Pasos siguientes

Busque la tabla de contenido de la izquierda para abordar las necesidades específicas o los cambios en el ámbito. Alternativamente, la primera mejora del ámbito en la lista, [el equilibrio de la cartera](./balance-the-portfolio.md) es un buen punto de partida cuando se revisan estos escenarios.

> [!div class="nextstepaction"]
> [Equilibrio de la cartera](./balance-the-portfolio.md)
