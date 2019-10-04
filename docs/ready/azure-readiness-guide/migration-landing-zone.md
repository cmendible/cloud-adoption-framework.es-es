---
title: Implementación de una zona de aterrizaje de migración en Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Aprenda a implementar una zona de aterrizaje de migración en Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit
ms.openlocfilehash: 329274859f50aa83ebb90e79597fa1ffe0973ab8
ms.sourcegitcommit: 1dccf1aed8e98aa0f58c4f86d90c65f5fa5ac84d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2019
ms.locfileid: "71811103"
---
# <a name="deploy-a-migration-landing-zone"></a>Implementación de una zona de aterrizaje para la migración

La *zona de aterrizaje de migración* es un término que se usa para describir un entorno que se ha aprovisionado y preparado para hospedar las cargas de trabajo que se van a migrar desde un entorno local a Azure. Una zona de aterrizaje de migración es la entrega final de la guía de preparación para Azure. En este artículo se unen todos los temas de preparación descritos en esta guía y se aplican las decisiones tomadas a la implementación de la primera zona de aterrizaje de migración.

En las secciones siguientes se describe una zona de aterrizaje que se suele usar para establecer un entorno adecuado para usarse durante una migración. El entorno o la zona de aterrizaje descritos en este artículo también se capturan en un plano técnico de Azure. Puede usar el plano técnico de la zona de aterrizaje de migración de la plataforma de adopción de la nube (CAF) para implementar el entorno definido con un solo clic.

## <a name="purpose-of-the-blueprint"></a>Finalidad del plano técnico

El plano técnico de la zona de aterrizaje de migración de la CAF crea una zona de aterrizaje. Esa zona de aterrizaje está limitada intencionadamente. Se ha diseñado para crear un punto inicial coherente que proporcione espacio para conocer la infraestructura como código. En algunos esfuerzos de migración, esta zona de aterrizaje podría ser suficiente para satisfacer sus necesidades. También es probable que deba cambiar algo en el plano técnico para cumplir las restricciones únicas.

## <a name="blueprint-alignment"></a>Alineación del plano técnico

En la imagen siguiente se muestra el plano técnico de la zona de aterrizaje de migración de la CAF en relación con los requisitos de cumplimiento y complejidad de la arquitectura.

![Alineación del plano técnico](../../_images/ready/blueprint-overview.png)

- La letra A se encuentra dentro de una línea curva que marca el ámbito de este plano técnico. Ese ámbito está destinado a transmitir que este plano técnico abarca una complejidad limitada de la arquitectura, pero se basa en unos requisitos de cumplimiento de un nivel relativamente intermedio.
- Los clientes que tienen un alto grado de complejidad y estrictos requisitos de cumplimiento podrían recibir un mejor servicio mediante el plano técnico extendido de un asociado o uno de los [ejemplos de plano técnico basados en estándares](https://docs.microsoft.com/azure/governance/blueprints/samples).
- La mayoría de las necesidades de los clientes se encontrarán entre estos dos extremos. La letra B representa el proceso que se describe en los artículos de [consideraciones sobre zonas de aterrizaje](../considerations/index.md). Para los clientes de este espacio, puede usar las guías de decisión que se encuentran en estos artículos para identificar los nodos que se van a agregar al plano técnico de la zona de aterrizaje de migración de la CAF. Este enfoque permite personalizar el plano técnico para ajustarse a sus necesidades.

## <a name="use-this-blueprint"></a>Uso de este plano técnico

Antes de usar el plano técnico de la zona de aterrizaje de migración de la CAF, revise los siguientes supuestos, decisiones e instrucciones de implementación.

## <a name="assumptions"></a>Supuestos

Se usaron las siguientes suposiciones o restricciones cuando se definió esta zona de aterrizaje inicial. Si estas suposiciones van acordes con las restricciones, puede usar el plano técnico para crear la primera zona de aterrizaje. El plano técnico también se puede ampliar para crear un plano técnico de la zona de aterrizaje que cumpla las restricciones únicas.

- **Límites de suscripción:** no se espera que este esfuerzo de adopción supere los [límites de suscripción](https://docs.microsoft.com/azure/azure-subscription-service-limits). Dos indicadores comunes constituyen un exceso de 25 000 máquinas virtuales o 10 000 vCPU.
- **Cumplimiento:** no se necesita ningún requisito de cumplimiento de terceros en esta zona de aterrizaje.
- **Complejidad de la arquitectura:** la complejidad de la arquitectura no requiere suscripciones de producción adicionales.
- **Servicios compartidos:** no hay servicios compartidos en Azure que requieran que esta suscripción se trate como un radio en una arquitectura de concentrador y radio.

Si estas suposiciones parecen ir acordes con su entorno actual, este plano técnico podría ser un buen punto de partida para empezar a crear la zona de aterrizaje.

## <a name="decisions"></a>Decisiones

Las siguientes decisiones se representan en el plano técnico de la zona de aterrizaje.

| Componente | Decisiones | Enfoques alternativos |
|---------|---------|---------|
|Herramientas de migración|Azure Site Recovery se implementará y se creará un proyecto de Azure Migrate.|[Guía para la toma de decisiones de las herramientas de migración](../../decision-guides/migrate-decision-guide/index.md)|
|Registro y supervisión|La cuenta de almacenamiento de diagnóstico y el área de trabajo de Operational Insights se aprovisionarán.|         |
|Red|Se creará una red virtual con subredes para la puerta de enlace, el firewall, el jumpbox y la zona de aterrizaje.|[Decisiones respecto a las redes](../considerations/network-decisions.md)|
|Identidad|Se da por sentado que la suscripción ya está asociada a una instancia de Azure Active Directory.|[Procedimientos recomendados de administración de identidades](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json)         |
|Directiva|En la actualidad, en este plano técnico se da por hecho que no se aplicará ninguna directiva de Azure.|         |
|Detalles de la suscripción|N/A: diseñado para una sola suscripción de producción|[Escalado de suscripciones](../considerations/scaling-subscriptions.md)|
|Grupos de administración|N/A: diseñado para una sola suscripción de producción|[Escalado de suscripciones](../considerations/scaling-subscriptions.md)         |
|Grupos de recursos|N/A: diseñado para una sola suscripción de producción|[Escalado de suscripciones](../considerations/scaling-subscriptions.md)         |
|Datos|N/D|[Elección de la opción correcta de SQL Server en Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas?toc=https://docs.microsoft.com/azure/architecture/toc.json&bc=https://docs.microsoft.com/azure/architecture/bread/toc.json) y [Guía sobre Azure Data Lake Store](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview) |
|Storage|N/D|[Guía de Azure Storage](../considerations/storage-guidance.md)         |
|Estándares de nomenclatura y etiquetado|N/D|[Procedimientos recomendados de nomenclatura y etiquetado](../considerations/naming-and-tagging.md)         |
|Administración de costos|N/D|[Seguimiento de costos](../azure-best-practices/track-costs.md)|
|Proceso|N/D|[Opciones de proceso](../considerations/compute-decisions.md)|

## <a name="customize-or-deploy-a-landing-zone-from-this-blueprint"></a>Personalización o implementación de una zona de aterrizaje a partir de este plano técnico

Obtenga más información y descargue un ejemplo de referencia del plano técnico de la zona de aterrizaje de migración de la plataforma de adopción de la nube para realizar operaciones de implementación o personalización a partir de [ejemplos de Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/samples).

Los ejemplos de plano técnico también están disponibles en el portal. Para más información sobre cómo crear un plano técnico, consulte [Azure Blueprints](./govern-org-compliance.md?tabs=azureblueprints#create-a-blueprint).

Para obtener instrucciones sobre la personalización que se debe realizar en este plano técnico o la zona de aterrizaje resultante, consulte los artículos sobre las [consideraciones de zona de aterrizaje](../considerations/index.md).

## <a name="next-steps"></a>Pasos siguientes

Una vez implementada la zona de aterrizaje de migración, podrá migrar las cargas de trabajo a Azure.
Para obtener instrucciones sobre las herramientas y los procesos necesarios para migrar la primera carga de trabajo, consulte la [guía de migración de Azure](../../migrate/azure-migration-guide/index.md).

> [!div class="nextstepaction"]
> [Migración de la primera carga de trabajo con la guía de migración de Azure](../../migrate/azure-migration-guide/index.md)
