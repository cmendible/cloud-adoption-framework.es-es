---
title: Evaluación del patrimonio digital
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Evaluación del patrimonio digital
author: matticusau
ms.author: mlavery
ms.date: 08/08/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: c95134909838f11377b16e90c5deb68850388938
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818836"
---
# <a name="assess-the-digital-estate"></a>Evaluación del patrimonio digital

En una migración ideal, cada recurso (infraestructura, aplicación o datos) sería compatible con una plataforma en la nube y estaría listo para la migración. En la realidad, no todo se debe migrar a la nube. Además, no todos los recursos son compatibles con las plataformas en la nube. Antes de migrar una carga de trabajo a la nube, es importante evaluar la carga de trabajo y cada recurso relacionado (infraestructura, aplicaciones y datos).

Los recursos que aparecen en esta sección lo ayudarán a evaluar su entorno para determinar su idoneidad para la migración y los métodos que debe tener en cuenta.

# <a name="toolstabtools"></a>[Herramientas](#tab/Tools)

Las herramientas siguientes lo ayudarán a evaluar su entorno para determinar la idoneidad de la migración y el mejor enfoque a usar. Para información útil sobre cómo elegir las herramientas adecuadas para admitir los esfuerzos de migración, consulte la [Guía para la toma de decisiones de las herramientas de migración de la Plataforma de adopción de la nube](../../decision-guides/migrate-decision-guide/index.md).

## <a name="azure-migrate"></a>Azure Migrate

El servicio Azure Migrate evalúa la infraestructura, las aplicaciones y los datos locales para su migración a Azure. El servicio evalúa la idoneidad de la migración de los recursos locales, realiza el ajuste de tamaño basado en el rendimiento, y proporciona estimaciones del costo que supone la ejecución de recursos locales en Azure. Si considera migrar mediante lift-and-shift o se encuentra en las primeras fases de la evaluación de la migración, este es el servicio que debe elegir. Después de completar la evaluación, se pueden usar Azure Migrate para ejecutar la migración.

![Información general de Azure Migrate](./media/assess/azuremigrate-overview-1.png)

### <a name="create-a-new-server-migration-project"></a>Creación de un nuevo proyecto de migración de servidor

Para iniciar una evaluación de migración de servidor mediante Azure Migrate, siga estos pasos:

1. Seleccione **Azure Migrate**.
1. En **Información general**, haga clic en **Evaluar y migrar servidores**.
1. Seleccione **Agregar herramientas**.
1. En **Detectar, evaluar y migrar servidores**, haga clic en **Agregar herramientas**.
1. En **Migrar proyecto**, seleccione la suscripción a Azure y cree un grupo de recursos, en caso de que no lo tenga.
1. En **Detalles del proyecto**, especifique el nombre del proyecto y la zona geográfica en la que quiere crearlo; después, haga clic en **Siguiente**.
1. En **Seleccione una herramienta de evaluación**, seleccione **Omitir por ahora la adición de una herramienta de evaluación > Siguiente**.
1. En **Seleccione una herramienta de migración**, seleccione **Azure Migrate: Migración del servidor > Siguiente**.
1. En **Revisar y agregar herramientas**, revise la configuración y haga clic en **Agregar herramientas**.
1. Después de agregar la herramienta, aparece en el **proyecto de Azure Migrate > Servidores > Herramientas de migración**.

::: zone target="chromeless"

::: form action="Blade[#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview]" submitText="Assess and migrate servers" :::

::: zone-end

::: zone target="docs"

### <a name="read-more"></a>Más información

- [Información general de Azure Migrate](/azure/migrate/migrate-services-overview).
- [Migración de servidores físicos o virtualizados a Azure](/azure/migrate/tutorial-migrate-physical-virtual-machines)
- [Azure Migrate en Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Migrate/AmhResourceMenuBlade/overview).

::: zone-end

## <a name="service-map"></a>Mapa de servicio

Mapa de servicio detecta automáticamente los componentes de la aplicación en sistemas Windows y Linux y asigna la comunicación entre servicios. Con Service Map puede ver los servidores en la forma en que piensa en ellos: como sistemas interconectados que ofrecen servicios críticos. Service Map muestra las conexiones entre servidores, procesos, la latencia de conexión entrante y saliente y puertos en cualquier arquitectura conectada de TCP sin necesidad de ninguna configuración más allá de la instalación de un agente.

Azure Migrate utiliza Service Map para mejorar las funcionalidades de generación de informes y las dependencias en todo el entorno. Los detalles completos de esta integración se describen en [Visualización de dependencias](/azure/migrate/concepts-dependency-visualization). Si usa el servicio de migración de Azure, no se requieren pasos adicionales para configurar y obtener las ventajas de Service Map. Las instrucciones siguientes se proporcionan para su referencia si quiere usar Service Map para otros propósitos o proyectos.

### <a name="enable-dependency-visualization-using-service-map"></a>Habilitación de la visualización de dependencias con Service Map

Para usar la visualización de dependencias, debe descargar e instalar agentes en cada máquina local que vaya a analizar.

- Es necesario tener instalado [Microsoft Monitoring Agent (MMA)](/azure/log-analytics/log-analytics-agent-windows) en cada máquina.
- Es necesario tener instalado [Dependency Agent](/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud#install-the-dependency-agent-on-windows) en cada máquina.
- Además, si tiene máquinas sin conectividad a Internet, debe descargar e instalar en ellas la puerta de enlace de Log Analytics.

<!-- markdownlint-disable MD024 -->

### <a name="read-more"></a>Más información

- [Uso de la solución Service Map en Azure](/azure/azure-monitor/insights/service-map)
- [Azure Migrate y Service Map: Visualización de dependencias](/azure/migrate/concepts-dependency-visualization)


# <a name="scenarios-and-stakeholderstabscenarios"></a>[Escenarios y partes interesadas](#tab/Scenarios)

## <a name="scenarios"></a>Escenarios

Esta guía se centra en los escenarios siguientes:

- **Hardware heredado:** lleva a cabo la migración para quitar una dependencia del hardware heredado que está llegando al final del soporte técnico o al final de su ciclo de vida.
- **Aumento de la capacidad:** debe aumentar la capacidad de los recursos (infraestructura, aplicaciones y datos) que la infraestructura actual no puede proporcionar.
- **Modernización del centro de datos:** debe ampliar su centro de datos o modernizarlo con la tecnología de nube para asegurarse de que su empresa sigue siendo actual y competitiva.
- **Modernización de aplicaciones o servicios:** quiere actualizar las aplicaciones para aprovechar las ventajas de la funcionalidad nativa de la nube. Incluso si una estrategia de migración de rehospedaje es su objetivo inicial, la capacidad de crear planes para la revisión de aplicaciones o servicios y una posible modernización es un proceso común en cualquier migración.

### <a name="organizational-alignment-and-stakeholders"></a>Alineación de la organización y partes interesadas

La lista completa de las partes interesadas varía entre los proyectos de migración. Es mejor suponer que no conocerá a todas las partes interesadas al principio del planeamiento de una migración, ya que las partes interesadas a menudo solo se identifican durante determinadas fases del proyecto. Sin embargo, antes de iniciar cualquier proyecto de migración, puede identificar a los principales líderes de la empresa de los grupos de aplicaciones, infraestructura de TI y finanzas que estarán interesados en los esfuerzos generales de migración a la nube de su organización.

Establecer un equipo de estrategia de la nube principal, basado en estas partes interesadas clave de alto nivel, puede ayudar a preparar su organización para la adopción de la nube y guiar los esfuerzos generales de migración a la nube. Este equipo es responsable de comprender las tecnologías de nube y los procesos de migración, identificar la justificación comercial de las migraciones y determinar las mejores soluciones de alto nivel para los esfuerzos de migración. También ayuda a identificar y trabajar con partes interesadas del ámbito empresarial y aplicaciones específicas para garantizar una migración correcta.

Para obtener más información sobre cómo preparar su organización para los esfuerzos de migración a la nube, consulte el artículo de la Plataforma de adopción de la nube sobre la [alineación inicial de la organización](../../ready/initial-org-alignment.md).

# <a name="timelinestabtimelines"></a>[Escalas de tiempo](#tab/Timelines)

Como afirmación general, los clientes consideran que el escenario de migración que se trata en esta guía se puede completar en un plazo que va de uno a seis meses.

Algunos de los factores que se deben tener en cuenta al evaluar la escala de tiempo de la migración son:

- **Los recursos (infraestructura, aplicaciones y datos)que se van a migrar:** la cantidad y diversidad de los recursos.
- **La preparación del personal:** ¿el personal está preparado para administrar el nuevo entorno o se necesita entrenamiento?
- **La financiación:** ¿tiene la aprobación y el presupuesto adecuados para completar la migración?
- **La administración de cambios:** ¿su empresa tiene requisitos específicos relacionados con la implementación y la aprobación de los cambios?
- **Las normativas relacionadas con los segmentos:** ¿tiene que cumplir con la normativa del segmento o del sector?

# <a name="cost-managementtabmanagecost"></a>[Administración de costos](#tab/ManageCost)

A medida que evalúa su entorno, se presenta una oportunidad perfecta para incluir un paso de análisis de costos. Con los datos recopilados por las actividades de evaluación, debería poder analizar y predecir los costos. Esta predicción de costos debe factorizar los costos de servicios de consumo, además de los costos de un solo uso (como una mayor entrada de datos).

Durante la migración, hay algunos factores que afectan a las actividades de decisiones y ejecución:

- **El tamaño del patrimonio digital:** comprender el tamaño del patrimonio digital afectará directamente a las decisiones y los recursos necesarios para realizar la migración.
- **Modelos de contabilidad:** cambiar de un modelo de gastos de capital estructurados a un modelo de gastos operativos fluidos.

::: zone target="docs"

En los recursos siguientes se proporciona información relacionada:

- [Estimación del costo de la nube](../migration-considerations/assess/estimate.md).

::: zone-end
