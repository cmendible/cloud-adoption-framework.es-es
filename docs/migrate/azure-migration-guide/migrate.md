---
title: Migración de recursos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migración de recursos
author: matticusau
ms.author: mlavery
ms.date: 08/08/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-new, AQC
ms.localizationpriority: high
ms.openlocfilehash: ce8338fbcd0e21cf0875a207633ce7c9ddf2ff9e
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818768"
---
# <a name="migrate-assets-infrastructure-apps-and-data"></a>Migración de recursos (infraestructura, aplicaciones y datos)

En esta fase del recorrido, se usa el resultado de la fase de evaluación para iniciar la migración del entorno. Esta guía ayuda a identificar las herramientas adecuadas para llegar a un "estado listo", incluidas herramientas nativas, herramientas de terceros y herramientas de administración de proyectos.

# <a name="native-migration-toolstabtools"></a>[Herramientas de migración nativas](#tab/Tools)

En las secciones siguientes se describen las herramientas de Azure nativas disponibles para realizar la migración o ayudar en ese proceso. Para información sobre cómo elegir las herramientas adecuadas para admitir los esfuerzos de migración, consulte la [Guía para la toma de decisiones de las herramientas de migración de la Plataforma de adopción de la nube](../../decision-guides/migrate-decision-guide/index.md).

## <a name="azure-migrate"></a>Azure Migrate

Azure Migrate ofrece una experiencia de migración unificada y extensible. Azure Migrate proporciona una experiencia dedicada única para hacer el seguimiento del recorrido de la migración en las fases de evaluación y migración a Azure. Ofrece la opción de usar las herramientas que prefiera y de hacer seguimiento del progreso de la migración en estas herramientas.

Azure Migrate proporciona la funcionalidad siguiente:

1. Funcionalidades mejoradas de evaluación y migración:
    - Evaluaciones de Hyper-V.
    - Evaluación mejorada de VMware.
    - Migración sin agentes de máquinas virtuales de VMware a Azure.
1. Evaluación unificada, migración y seguimiento del progreso.
1. Enfoque ampliable con integración de ISV (como Cloudamize).

Para realizar una migración mediante Azure Migrate siga estos pasos:

1. Busque Azure Migrate en **Todos los servicios**. Seleccione **Azure Migrate** para continuar.
1. Seleccione **Agregar una herramienta** para empezar el proyecto de migración.
1. Seleccione la suscripción, el grupo de recursos y la geografía donde hospedar la migración.
1. Seleccione **Seleccione una herramienta de evaluación** > **Azure Migrate: Server Assessment** >  **Siguiente**.
1. Seleccione **Review + add tool(s)** (Revisar y agregar herramientas) y compruebe la configuración. Haga clic en **Add tool(s)** (Agregar herramientas) para iniciar el trabajo de crear el proyecto de migración y registrar las soluciones seleccionadas.

<!-- TODO: TBA -->

### <a name="read-more"></a>Más información

- [Tutorial de Azure Migrate: Migración de servidores físicos o virtualizados a Azure](/azure/migrate/tutorial-migrate-physical-virtual-machines)

## <a name="azure-site-recovery"></a>Azure Site Recovery

El servicio Azure Site Recovery puede administrar la migración de los recursos locales a Azure. También puede administrar y coordinar la recuperación ante desastres de máquinas virtuales locales y máquinas virtuales de Azure con fines de continuidad empresarial y recuperación ante desastres (BCDR).

En los pasos siguientes se describe el proceso para usar Site Recovery para la migración:

> [!TIP]
> Estos pasos pueden diferir ligeramente según el escenario. Para obtener más información, consulte el artículo [Migración de máquinas locales a Azure](/azure/site-recovery/migrate-tutorial-on-premises-azure).

### <a name="prepare-azure-site-recovery-service"></a>Preparación del servicio Azure Site Recovery

1. En Azure Portal, seleccione **+Crear un recurso > Herramientas de administración > Backup and Site Recovery**.
1. Si todavía no crea un almacén de recuperación, complete el asistente para crear un recurso de **almacén de Recovery Services**.
1. En el menú **Recurso**, seleccione **Site Recovery > Preparar infraestructura > Objetivo de protección**.
1. En **Objetivo de protección**, seleccione el contenido que quiera migrar.
    1. **VMware:** seleccione **To Azure > Yes, with VMware vSphere Hypervisor (En Azure > Sí, con VMware vSphere Hypervisor)** .
    1. **Máquina física:** seleccione **To Azure > Not virtualized/Other (En Azure > No virtualizado/Otro)** .
    1. **Hyper-V:** seleccione **To Azure > Yes, with Hyper-V (En Azure > Sí, con Hyper-V)** . Si VMM administra las máquinas virtuales de Hyper-V, seleccione **Sí**.

### <a name="configure-migration-settings"></a>Configuración de valores de migración

1. Configure el entorno de origen según corresponda.
1. Configure el entorno de destino.
    1. Haga clic en **Preparar infraestructura > Destino** y seleccione la suscripción de Azure que quiere usar.
    1. Especifique el modelo de implementación de Resource Manager.
    1. Site Recovery comprueba que tiene una o más redes y cuentas de Azure Storage compatibles.
1. Configurar una directiva de replicación.
1. Habilite la replicación.
1. Ejecute una migración de prueba (conmutación por error de prueba).

### <a name="migrate-to-azure-using-failover"></a>Migración a Azure mediante conmutación por error

1. En **Configuración > Elementos replicados**, seleccione la máquina > **Conmutación por error**.
1. En **Conmutación por error**, seleccione un **punto de recuperación** en el que realizar la conmutación por error. Seleccione el punto de recuperación más reciente.
1. Configure cualquier opción de clave de cifrado que sea necesaria.
1. Seleccione **Apague la máquina antes de comenzar con la conmutación por error**. Site Recovery intentará apagar las máquinas virtuales antes de desencadenar la conmutación por error. La conmutación por error continúa aunque se produzca un error de cierre. Puede seguir el progreso de la conmutación por error en la página Trabajos.
1. Compruebe que la máquina virtual de Azure aparece en Azure según lo previsto.
1. En **Elementos replicados**, haga clic con el botón derecho en la máquina virtual y elija **Completar migración**.
1. Realice los pasos posteriores a la migración que sean necesarios (consulte la información pertinente que aparece en esta guía).

::: zone target="chromeless"

::: form action="Create[#create/Microsoft.RecoveryServices]" submitText="Create a Recovery Services vault" :::

::: zone-end

::: zone target="docs"

Para más información, consulte:

- [Migración de máquinas locales a Azure](/azure/site-recovery/migrate-tutorial-on-premises-azure)

::: zone-end

## <a name="azure-database-migration-service"></a>Azure Database Migration Service

Azure Database Migration Service es un servicio totalmente administrado que permite migraciones completas desde varios orígenes de base de datos hasta las plataformas de datos de Azure con un tiempo de inactividad mínimo (migraciones en línea). Azure Database Migration Service realiza todos los pasos requeridos. Puede iniciar sus proyectos de migración con la garantía de que el proceso aprovecha los procedimientos recomendados de Microsoft.

### <a name="create-an-azure-database-migration-service-instance"></a>Creación de una instancia de Azure Database Migration Service

Si es la primera vez que usa Azure Database Migration Service, debe registrar el proveedor de recursos para la suscripción de Azure:

1. Seleccione **Todos los servicios**, luego **Suscripciones** y elija la suscripción de destino.
1. Seleccione **Proveedores de recursos**.
1. Busque `migration` y, a la derecha de **Microsoft.DataMigration**, seleccione **Registrar**.

::: zone target="chromeless"

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to Subscriptions" :::

::: zone-end

Después de registrar el proveedor de recursos, puede crear una instancia de Azure Database Migration Service.

1. Seleccione **+Crear un recurso** y busque **Azure Database Migration Service** en Marketplace.
1. Complete el asistente para **Crear el servicio de migración** y seleccione **Crear**.

El servicio ya está listo para migrar las bases de datos de origen compatibles (por ejemplo, SQL Server, MySQL, PostgreSQL o MongoDb).

::: zone target="chromeless"

::: form action="Create[#create/Microsoft.AzureDMS]" submitText="Create an Azure Database Migration Service instance" :::

::: zone-end

::: zone target="docs"

Para más información, consulte:

- [Introducción a Azure Database Migration Service](/azure/dms/dms-overview).
- [Creación de una instancia de Azure Database Migration Service](/azure/dms/quickstart-create-data-migration-service-portal).
- [Azure Migrate en Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade).
- [Azure Portal: Creación de un proyecto de migración](https://portal.azure.com/#create/Microsoft.AzureMigrate).

::: zone-end

## <a name="data-migration-assistant"></a>Data Migration Assistant

Data Migration Assistant (DMA) ayuda a actualizar a una plataforma de datos moderna mediante la detección de problemas de compatibilidad que pueden afectar la funcionalidad de la versión nueva de SQL Server o Azure SQL Database. DMA recomienda mejoras de rendimiento y confiabilidad para el entorno de destino y le permite migrar el esquema, los datos y objetos no contenidos desde el servidor de origen al servidor de destino.

> [!NOTE]
> En el caso de migraciones de gran tamaño (en términos de número y tamaño de bases de datos), se recomienda usar Azure Database Migration Service, que puede migrar bases de datos a escala.
>

Para empezar a trabajar con Data Migration Assistant, siga estos pasos.

1. Descargue e instale Data Migration Assistant desde el [Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=53595).
1. Para crear una evaluación, haga clic en el icono **Nuevo (+)** y seleccione el tipo de proyecto **Evaluación**.
1. Establezca el tipo de servidor de origen y de destino. Haga clic en **Create**(Crear).
1. Configure las opciones de evaluación según sea necesario (se recomiendan todos los valores predeterminados).
1. Agregue las bases de datos que se van a evaluar.
1. Haga clic en **Siguiente** para iniciar la evaluación.
1. Vea los resultados dentro del conjunto de herramientas de Data Migration Assistant.

En el caso de una empresa, se recomienda seguir el enfoque descrito en el artículo sobre cómo [evaluar una empresa y consolidar informes de evaluación con DMA](/sql/dma/dma-consolidatereports) para evaluar varios servidores, combinar los informes y, luego, usar los informes de Power BI proporcionados para analizar los resultados.

Para obtener más información, incluidos los pasos de uso detallados, consulte:

- [Información general de Data Migration Assistant](/sql/dma/dma-overview).
- [Evaluación de una empresa y consolidación de informes de evaluación con DMA](/sql/dma/dma-consolidatereports).
- [Análisis de informes de evaluación consolidados creados por Data Migration Assistant con Power BI](/sql/dma/dma-powerbiassesreport).

## <a name="sql-server-migration-assistant"></a>SQL Server Migration Assistant

Microsoft SQL Server Migration Assistant (SSMA) es una herramienta diseñada para automatizar la migración de bases de datos a SQL Server desde Microsoft Access, DB2, MySQL, Oracle y SAP ASE. El concepto general es recopilar, evaluar y revisar con estas herramientas; sin embargo, debido a las variaciones del proceso para cada uno de los sistemas de origen, recomendamos revisar la [documentación detallada de SQL Server Migration Assistant](/sql/ssma/sql-server-migration-assistant).

Para más información, consulte:

- [Información general de SQL Server Migration Assistant](/sql/ssma/sql-server-migration-assistant).

## <a name="database-experimentation-assistant"></a>Asistente para experimentación con bases de datos

Asistente para experimentación con bases de datos (DEA) es una nueva solución de pruebas A/B para las actualizaciones de SQL Server. Ayudará a evaluar una versión de SQL de destino para una carga de trabajo determinada. Los clientes que actualizan de versiones anteriores de SQL Server (SQL Server 2005 y versiones posteriores) a cualquier versión nueva de SQL Server pueden usar estas métricas de análisis.

El Asistente para experimentación con bases de datos contiene estas actividades de flujo de trabajo:

- **Captura:** el primer paso de las pruebas A/B de SQL Server es capturar un seguimiento en el servidor de origen. Por lo general, el servidor de origen es el servidor de producción.
- **Reproducción:** el segundo paso de las pruebas A/B de SQL Server es reproducir el archivo de seguimiento que se capturó en los servidores de destino. Luego, recopile seguimientos amplios a partir de las reproducciones para el análisis.
- **Análisis:** el último paso es generar un informe de análisis mediante el uso de los seguimientos de reproducción. El informe de análisis puede ayudarlo a obtener información sobre las implicaciones de rendimiento del cambio propuesto.

Para más información, consulte:

- [Información general del Asistente para experimentación con bases de datos](/sql/dea/database-experimentation-assistant-overview).

# <a name="third-party-migration-toolstabthird-party-tools"></a>[Herramientas de migración de terceros](#tab/third-party-tools).

Hay varias herramientas de migración de terceros y servicios de ISV que pueden ayudarlo con el proceso de migración. Cada uno ofrece distintas ventajas y fortalezas. Estas herramientas son:

## <a name="cloudamize"></a>Cloudamize

Cloudamize es un servicio de ISV que abarca todas las fases de la estrategia de migración.

[Más información](https://www.cloudamize.com)

## <a name="zerto"></a>Zerto

Zerto proporciona la replicación virtual que controla tanto entornos de Microsoft Hyper-V como de VMware vSphere.

[Más información](https://www.zerto.com/solutions/use-cases/data-center-migration-software)

## <a name="carbonite"></a>Carbonite

Carbonite proporciona soluciones de migración de datos y servidores para migrar cargas de trabajo hacia, desde o entre cualquier entorno físico, virtual o basado en la nube.

[Más información](https://www.carbonite.com/data-protection/data-migration-software)

## <a name="movere"></a>Movere

Movere es una solución de detección que proporciona los datos y la información que se necesitan para planear las migraciones a la nube y seguir optimizando, supervisando y analizando los entornos de TI con confianza.

[Más información](https://www.movere.io)

Visite el [Azure Migration Center](https://azure.microsoft.com/migration/support) para descubrir las organizaciones que ofrecen soluciones de tecnología de asociados listas para usar que se ajustan a sus escenarios de migración y obtener información sobre servicios de soporte técnico y herramientas de migración de terceros adicionales.

# <a name="project-management-toolstabproject-management-tools"></a>[Herramientas de administración de proyectos](#tab/project-management-tools)

Los proyectos que no se controlan ni administran tienen más probabilidades de tener problemas. Para garantizar un resultado correcto, creemos que es importante que use una herramienta de administración de proyectos. Hay muchas herramientas distintas disponibles y es posible que los jefes de proyecto de su organización ya tengan su favorita. Microsoft ofrece las siguientes herramientas de administración de proyectos, que pueden trabajar en conjunto para brindar funcionalidades más amplias:

- [Microsoft Planner](https://tasks.office.com): una manera visual sencilla para organizar el trabajo en equipo.
- [Microsoft Project](https://products.office.com/project/project-and-portfolio-management-software): Project and Portfolio Management, Resource Capacity Management, Financial Management, Timesheet and Schedule Management.
- [Microsoft Teams](https://products.office.com/microsoft-teams): herramienta de comunicación y colaboración en equipo. Teams también integra Planner y otras herramientas para mejorar la colaboración.
- [Azure DevOps](https://dev.azure.com): con Azure DevOps, puede administrar la infraestructura como código o usar los elementos de trabajo y paneles para realizar la administración de proyectos. A medida que madura, su organización puede aprovechar las funcionalidades de CI/CD.

Estas no son las únicas herramientas disponibles. Muchas otras herramientas de terceros se usan ampliamente en la comunidad de administración de proyectos.

## <a name="set-up-for-devops"></a>Configuración para DevOps

A medida que migra a las tecnologías de nube, se presenta una oportunidad excelente para configurar la organización para DevOps y CI/CD. Incluso si la organización solo administra la infraestructura, a medida que empieza a administrar la infraestructura como código y a usar los patrones y las prácticas del sector para DevOps, puede empezar a aumentar la agilidad mediante canalizaciones de CI/CD, lo que le permite adaptarse más rápido a los escenarios de cambios, crecimiento, liberación e, incluso, recuperación.

[Azure DevOps](https://dev.azure.com) brinda toda la funcionalidad e integración requerida con Azure, el entorno local o, incluso, otras nubes. Obtenga más información [aquí](https://azure.microsoft.com/services/devops). Para un aprendizaje guiado, consulte el [inicio rápido sobre CI y CD con Azure DevOps](https://microsoft.github.io/PartsUnlimited/pandp/200.1x-PandP-CICDQuickstartwithVSTS.html).

# <a name="cost-managementtabmanagecost"></a>[Administración de costos](#tab/ManageCost)

Cuando migre recursos al entorno en la nube, es importante que realice análisis de costos periódicos. Esto le permite evitar cargos por uso inesperados, ya que el proceso de migración puede incluir requisitos de uso adicionales en los servicios. También puede cambiar el tamaño de los recursos según sea necesario para equilibrar el costo y la carga de trabajo (lo que se analiza con mayor detalle en la sección **[Optimización y transformación](optimize-and-transform.md)** ).
