---
title: Mecanismos de control de costos centrados en la migración
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Aprenda a configurar presupuestos y pagos, y a comprender las facturas de los recursos de Azure.
author: bandersmsft
ms.author: banders
ms.date: 08/08/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: c6b195a69622a4934f257090650a8ba6ce884025
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024804"
---
# <a name="migration-focused-cost-control-mechanisms"></a>Mecanismos de control de costos centrados en la migración

La nube presenta algunos cambios en nuestra forma de trabajar, independientemente de nuestro rol en el equipo tecnológico. El costo es un buen ejemplo de este cambio. En el pasado, solo al liderazgo financiero y de TI le preocupaban el costo de los recursos de TI (infraestructura, aplicaciones y datos). La nube permite a todos los miembros de TI tomar decisiones que mejoren el soporte técnico para el usuario final y actuar sobre ellas. Si embargo, con esa eficacia aparece la responsabilidad de tener en cuenta el costo al tomar esas decisiones.

En este artículo se presentan las herramientas que pueden ayudar a tomar decisiones inteligentes relativas al costo antes, durante y después de una migración a Azure.

Entre las herramientas de este artículo, se incluyen:

> - Azure Migrate
> - Calculadora de precios de Azure
> - Calculadora de TCO de Azure
> - Azure Cost Management
> - Azure Advisor

También es posible que los procesos descritos en este artículo requieran una asociación con propietarios de aplicaciones de línea de negocio, de finanzas o administradores de TI. Para obtener instrucciones sobre cómo asociarse a estos roles, consulte el artículo de la Plataforma de adopción de la nube sobre el establecimiento de una organización con control de costo (a partir del 3T de 2019).

<!-- markdownlint-disable MD024 MD025 -->

# <a name="estimate-vm-costs-prior-to-migrationtabestimatevmcosts"></a>[Estimación de costos de máquina virtual antes de la migración](#tab/EstimateVMCosts)

Antes de la migración de cualquier recurso (infraestructura, aplicación o datos), hay una oportunidad de estimar los costos y refinar el ajuste de tamaño en función de los criterios de rendimiento observados para esos recursos. La estimación de costos cumple dos propósitos: permite el control de costos y proporciona un punto de control para garantizar que los presupuestos actuales tengan en cuenta los requisitos de rendimiento necesarios.

## <a name="cost-calculators"></a>Calculadoras de costos

Para los cálculos de costos manuales, hay dos prácticas calculadoras que pueden proporcionar una estimación del costo rápida en función de la arquitectura de la carga de trabajo que se va a migrar.

- La [calculadora de precios](https://azure.microsoft.com/pricing/calculator) proporciona estimaciones del costo en función de los productos de Azure especificados manualmente.
- En ocasiones, las decisiones requieren una comparación de los costos de la nube futuros y los costos locales actuales. La [calculadora del costo total de propiedad (TCO)](https://azure.microsoft.com/pricing/tco/calculator) puede proporcionar esta comparación.

Estas calculadoras de costos manuales se pueden usar por su cuenta para prever los posibles gastos y ahorros. También se pueden usar junto con las herramientas de previsión de costos de Azure Migrate para ajustar las expectativas en cuanto a los costos que se ajusten a arquitecturas alternativas o restricciones de rendimiento.

## <a name="azure-migrate-calculations"></a>Cálculos de Azure Migrate

**Requisitos previos:** el recordatorio de esta pestaña da por sentado que el lector ya ha rellenado Azure Migrate con una colección de recursos (infraestructura, aplicaciones y datos) que se van a migrar. En el artículo anterior sobre evaluaciones se proporcionan instrucciones de cómo recopilar los datos iniciales. Una vez que se rellenen los datos, siga los siguientes pasos para estimar los costos mensuales en función de los datos recopilados.

Azure Migrate calcula los **costos mensuales estimados** en función de los datos capturados por el recopilador y el mapa de servicio. Los siguientes pasos cargarán las estimaciones del costo:

1. Vaya a la hoja Evaluación de Azure Migrate en el portal.
1. En la página **Introducción** del proyecto, seleccione **+Crear evaluación**.
1. Haga clic en **View all** (Ver todo) para revisar la configuración de la valoración.
1. Cree el grupo y especifique un nombre para él.
1. Seleccione las máquinas que desee agregar al grupo.
1. Haga clic en **Crear evaluación** para crear el grupo y la evaluación.
1. Una vez creada la evaluación, puede verla en Introducción > Panel.
1. En la sección Detalles de la evaluación de la navegación por hojas, seleccione **Detalles del costo**.

La estimación resultante, mostrada a continuación, identifica los costos mensuales de proceso y almacenamiento, que suelen representar la parte más grande de los costos de la nube.

![compute-storage-monthly-cost-estimate.png](./media/manage-costs/compute-storage-monthly-cost-estimate.png)
*Figura 1: Imagen de la vista de detalles de costos de una evaluación en Azure Migrate.*

## <a name="additional-resources"></a>Recursos adicionales

- [Configuración y revisión de una evaluación con Azure Migrate](https://docs.microsoft.com/azure/migrate/tutorial-assess-vmware#set-up-an-assessment)
- Para obtener un plan más completo sobre la administración de costos en números más grandes de recursos (infraestructura, aplicaciones y datos), consulte el artículo sobre el [modelo de gobernanza de la Plataforma de adopción de la nube](../../govern/guides/index.md). En concreto, las instrucciones sobre la [materia de Cost Management](../../govern/cost-management/index.md) y la [guía de mejora de Cost Management en grandes empresas](../../govern/guides/complex/cost-management-improvement.md).

# <a name="estimate-and-optimize-vm-costs-during-and-after-migrationtabestimateoptimize"></a>[Estimación y optimización de costos de máquina virtual durante y después de la migración](#tab/EstimateOptimize)

La estimación del costo antes de la migración proporciona un destino sólido para las expectativas en cuanto al costo. También proporciona oportunidades para tener en cuenta las necesidades de costo y rendimiento de cada uno de los recursos (infraestructura, aplicaciones y datos) que se van a migrar. Sin embargo, sigue siendo una estimación. Una vez que el recurso se migra y está con carga, se pueden realizar cálculos de costos precisos, en función de la carga real o sintetizada.

## <a name="azure-advisor-cost-recommendations"></a>Recomendaciones sobre el costo de Azure Advisor

Dentro de un plazo de 24 horas de la migración de recursos (infraestructura, aplicaciones y datos) a Azure, Azure Advisor empieza a supervisar el rendimiento de cada recurso para proporcionarle comentarios sobre el recurso. Un elemento de los comentarios recopilados está relacionado con el equilibrio entre el costo y el uso.

Los siguientes pasos proporcionan recomendaciones sobre el costo para los recursos (infraestructura, aplicaciones y datos) de sus suscripciones actuales:

1. Vaya a la hoja **Azure Advisor** del portal. Para hacerlo, seleccione **Advisor** en el panel de navegación izquierdo de Azure Portal. Si no ve Asesor en el panel izquierdo, seleccione **Todos los servicios**. En el panel de menú de servicio, en **Supervisión y administración**, seleccione **Advisor**.
1. El panel de Advisor mostrará un resumen de las recomendaciones para todas las suscripciones seleccionadas. Puede elegir las suscripciones que desee que muestren las recomendaciones para usar el menú desplegable del filtro de suscripción.
1. Para ver las recomendaciones sobre el costo, seleccione la pestaña Costo.

## <a name="azure-cost-management"></a>Azure Cost Management

Azure Cost Management puede proporcionar una vista más holística de los hábitos de gasto, incluida una vista detallada de los costos y las tendencias de los gastos a lo largo del tiempo. En el caso de las migraciones grandes o complejas, esta vista puede proporcionar la información necesaria para tomar decisiones amplias sobre la administración de costos de rastreo.

Requisitos previos: el recordatorio de esta pestaña da por supuesto que el lector ha completado la configuración de Azure Cost Management durante la finalización de la guía de preparación de Azure. Para obtener más detalles sobre cómo configurar Azure Cost Management, consulte este [artículo en la guía de preparación de Azure](../../ready/azure-readiness-guide/manage-costs.md). Una vez que se rellenen los datos, siga los siguientes pasos para estimar los costos mensuales en función de los datos recopilados.

Los siguientes pasos cargarán los datos de análisis de costos de Azure Cost Management para sus suscripciones:

1. Vaya a la hoja **Cost Management + facturación** del portal. Si no ve Cost Management + facturación en el panel izquierdo, haga clic en **Todos los servicios**. En el panel de menú de servicio, en **Supervisión y administración**, haga clic en **Cost Management + facturación**.
1. En la hoja Cost Management + facturación, seleccione **Cost Management** en el panel de navegación izquierdo para que la hoja abierta empiece a analizar y optimizar los costos de la nube.
1. En la hoja Cost Management, seleccione **Análisis de costos**.
    1. Use la píldora **Ámbito** para cambiar a un ámbito diferente en el análisis de costos.

Este análisis le permitirá revisar los costos totales, el presupuesto (si esta disponible) y los costos acumulados. Cada cálculo puede verse por servicio, por recurso y a lo largo del tiempo. Lo más importante, los costos pueden analizarse por etiquetas. La nomenclatura y el etiquetado de recursos (infraestructura, aplicaciones y datos) es el punto inicial fundamental de todos los procesos de administración de costos y gobernanza de sonido. Las etiquetas adecuadas permiten una mejor administración de los costos e impactos más claros de las optimizaciones de costos y rendimiento.

## <a name="additional-resources"></a>Recursos adicionales

- Para obtener un plan más completo sobre la administración de costos en números más grandes de recursos (infraestructura, aplicaciones y datos), consulte el artículo sobre el [modelo de gobernanza de la Plataforma de adopción de la nube](../../govern/guides/index.md). En concreto, las instrucciones sobre la [materia de Cost Management](../../govern/cost-management/index.md) y la [guía de mejora incremental de Cost Management en grandes empresas](../../govern/guides/complex/cost-management-improvement.md).
- Para obtener más información sobre Azure Advisor, consulte [Reducción de los costos de servicio con Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations).
- Para obtener más información sobre Azure Cost Management, consulte [Descripción y uso de ámbitos](https://docs.microsoft.com/azure/cost-management/understand-work-scopes) y [Explore y analice los costos con Análisis de costos](https://docs.microsoft.com/azure/cost-management/quick-acm-cost-analysis).

# <a name="tips-and-tricks-to-optimize-coststabtipstricks"></a>[Trucos y sugerencias para optimizar los costos](#tab/TipsTricks)

Además de las herramientas mencionadas en este artículo, hay algunos trucos y sugerencias que pueden ayudar a reducir rápidamente los costos de la nube generales. A continuación se muestran algunas sugerencias de alto nivel para tener en cuenta lo siguiente:

## <a name="avoid-unnecessary-spending"></a>Evitación de costos innecesarios

La mayoría de los recursos (infraestructura, aplicaciones y datos) de un centro de datos existente podrían migrarse teóricamente a la nube. Sin embargo, eso no significa que tenga que hacerse. Durante la evaluación de cada carga de trabajo, compruebe si debe migrarse la carga de trabajo. El artículo de la Plataforma de adopción de la nube sobre la [racionalización incremental](../../digital-estate/rationalize.md) puede ayudar a determinar los recursos que deben migrarse.

## <a name="reduce-waste"></a>Reducción de los gastos residuales

Después de implementar la infraestructura en Azure, es importante asegurarse de que se está usando. La manera más fácil de empezar a ahorrar inmediatamente es revisar los recursos y eliminar los que no se usan.

## <a name="reduce-overprovisioning"></a>Reducción del aprovisionamiento en exceso

Incluso con los mejores enfoques de estimación, es probable que haya recursos sobreaprovisionados e infrautilizados (infraestructura, aplicaciones y datos). La revisión de esos recursos mediante las herramientas de las dos pestañas anteriores identificará posibles medios de reducir el tamaño de los recursos para una mejor coincidencia de los requisitos de rendimiento y la reducción de los costos.

## <a name="take-advantage-of-available-discounts"></a>Aproveche los descuentos disponibles

Habla con su representante de la cuenta de Microsoft para comprender cómo puede aprovechar las opciones de descuento actuales. A continuación se muestran algunos ejemplos de descuentos usados habitualmente para reducir los costos.

## <a name="azure-reservations"></a>Reservas de Azure

[Reservas de Azure](https://docs.microsoft.com/azure/billing/billing-save-compute-costs-reservations) le permiten realizar el pago por adelantado por un año o tres años de máquina virtual o capacidad de proceso de SQL Database. El pago por adelantado le permite obtener un descuento en los recursos que utiliza. Las reservas de Azure pueden reducir significativamente los costos de las máquinas virtuales o de proceso de SQL Database, hasta un 72 % con respecto a los precios de pago por uso con el compromiso por adelantado de uno o tres años. Las reservas ofrecen un descuento en la facturación y no afectan al estado del entorno de ejecución de las máquinas virtuales o bases de datos SQL.

## <a name="use-azure-hybrid-benefit"></a>Uso de la Ventaja híbrida de Azure

Si ya tiene licencias de Windows Server o de SQL Server en las implementaciones locales, puede usar el programa de [Ventaja híbrida de Azure](https://azure.microsoft.com/pricing/hybrid-benefit) para ahorrar en Azure. Con la ventaja de Windows Server, cada licencia cubre el costo del sistema operativo (en dos máquinas virtuales como máximo) y solo tiene que pagar los costos de proceso básicos. Puede usar licencias de SQL Server existentes para ahorrar hasta un 55 por ciento en las opciones de SQL Database basadas en núcleos virtuales. Las opciones incluyen SQL Server en Azure Virtual Machines y SQL Server Integration Services.

## <a name="low-priority-vms-with-batch"></a>Máquinas virtuales de prioridad baja con Batch

En el caso de los procesos en segundo plano de prioridad más baja, Batch ofrece un medio de administrar las máquinas virtuales del servicio en segundo plano y reducir los costos. Sin embargo, es importante comprender el impacto del rendimiento de las [máquinas virtuales de prioridad baja con Batch](https://docs.microsoft.com/azure/batch/batch-low-pri-vms) antes de elegir esta opción con descuento.

## <a name="additional-resources"></a>Recursos adicionales

Para obtener un plan más completo sobre la administración de costos en números más grandes de recursos (infraestructura, aplicaciones y datos), consulte el artículo sobre el [modelo de gobernanza de la Plataforma de adopción de la nube](../../govern/guides/index.md). En concreto, las instrucciones sobre la [materia de Cost Management](../../govern/cost-management/index.md) y la [guía de mejora incremental de Cost Management en la gobernanza de grandes empresas](../../govern/guides/complex/cost-management-improvement.md).
