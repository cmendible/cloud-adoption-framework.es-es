---
title: Información general de ejemplos de migración de aplicaciones para Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Brinda información general sobre los ejemplos de migración de aplicaciones que se incluyen como parte de la sección Migración de la Plataforma de adopción de la nube.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: a6af51f1fa6526e2ea7cf13a824c7834d631aa59
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70835118"
---
# <a name="application-migration-patterns-and-examples"></a>Ejemplos y patrones de migración de aplicaciones

En esta sección de la Plataforma de adopción de la nube se proporcionan ejemplos de varios escenarios comunes de migración, en los que se muestra cómo migrar la infraestructura local a la nube de [Microsoft Azure](https://azure.microsoft.com/overview/what-is-azure).

## <a name="introduction"></a>Introducción

Azure proporciona acceso a un conjunto completo de servicios en la nube. Los desarrolladores y profesionales de TI pueden usar estos servicios para compilar, implementar y administrar aplicaciones en una variedad de herramientas y marcos, a través de una red mundial de centros de datos. A medida que su negocio se enfrenta a los desafíos asociados con el cambio digital, la nube de Azure le ayuda a encontrar la forma de optimizar los recursos y las operaciones, a comprometerse con sus clientes y empleados, y a transformar sus productos.

Sin embargo, Azure reconoce que incluso con todas las ventajas que la nube proporciona en términos de velocidad y flexibilidad, costos minimizados, rendimiento y confiabilidad, muchas organizaciones necesitarán ejecutar centros de datos locales durante algún tiempo. En respuesta a las barreras de adopción de la nube, Azure proporciona una estrategia híbrida de nube que construye puentes entre sus centros de datos locales y la nube pública de Azure. Por ejemplo, el uso de recursos de nube de Azure como Azure Backup para proteger los recursos locales, o el uso de Azure Analytics para obtener información sobre las cargas de trabajo locales.

Como parte de la estrategia de nube híbrida, Azure proporciona soluciones innovadoras para migrar aplicaciones locales y cargas de trabajo a la nube. Con pasos sencillos, puede evaluar exhaustivamente sus recursos locales para averiguar cómo se ejecutarán en la nube de Azure. Después, con una valoración profunda en la mano, puedes migrar recursos con seguridad a Azure. Cuando los recursos están funcionando en Azure, puede optimizarlos para retener y mejorar el acceso, la flexibilidad, la seguridad y la confiabilidad.

## <a name="migration-patterns"></a>Patrones de migración

Las estrategias para la migración a la nube abarcan cuatro patrones amplios: rehospedar, refactorizar, rediseñar o recompilar. La estrategia que adopte depende de los impulsores de negocio y los objetivos de la migración. Puede adoptar varios patrones. Por ejemplo, podría elegir rehospedar aplicaciones simples o aplicaciones que no son críticas para su empresa, pero rediseñar las que son más complejas y críticas para la empresa. Echemos un vistazo a estos patrones.

<!-- markdownlint-disable MD033 -->

**Patrón** | **Definición** | **Cuándo se deben usar**
--- | --- | ---
**Rehospedaje** | A menudo se denomina una migración mediante lift-and-shift. Esta opción no requiere cambios en el código y permite migrar las aplicaciones existentes a Azure rápidamente. Cada aplicación se migra tal cual, para aprovechar las ventajas que ofrece la nube, sin correr el riesgo ni incurrir en los costos asociados con los cambios de código. | Cuando necesite mover aplicaciones rápidamente a la nube.<br/><br/> Cuando quiera mover una aplicación sin modificación alguna.<br/><br/> Cuando la arquitectura de las aplicaciones se diseña de modo que puedan aprovechar la escalabilidad de [IaaS de Azure](https://azure.microsoft.com/overview/what-is-iaas) después de la migración.<br/><br/> Cuando las aplicaciones son importantes para su negocio, pero no es necesario realizar cambios inmediatamente en las funciones de la aplicación.
**Refactorización** | Este concepto con frecuencia se conoce como "reempaquetar" y requiere una mínima cantidad de cambios en las aplicaciones para que puedan conectarse a [PaaS de Azure](https://azure.microsoft.com/overview/what-is-paas) y usar las ofertas de la nube.<br/><br/> Por ejemplo, puede migrar sus aplicaciones existentes a Azure App Service o Azure Kubernetes Service (AKS).<br/><br/> O bien, podría refactorizar las bases de datos relacionales y no relacionales en opciones como, por ejemplo, Instancia administrada de Azure SQL Database, Azure Database for MySQL, Azure Database for PostgreSQL y Azure Cosmos DB. | Si la aplicación se puede reempaquetar fácilmente para que funcione en Azure.<br/><br/> Si quiere aplicar prácticas DevOps innovadoras proporcionadas por Azure, o piensa en DevOps con una estrategia de contenedor para las cargas de trabajo.<br/><br/> Para la refactorización, debe pensar en la portabilidad de la base de código existente y las capacidades de desarrollo disponibles.
**Rediseño** | El rediseño para la migración se centra en modificar y ampliar la funcionalidad de las aplicaciones y el código base con el fin de optimizar la arquitectura de aplicación para la escalabilidad en la nube.<br/><br/> Por ejemplo, podría dividir una aplicación monolítica en un grupo de microservicios que funcionan en conjunto y se escalan fácilmente.<br/><br/> O bien, puede rediseñar las bases de datos relacionales y no relacionales para adaptarlas a soluciones de bases de datos totalmente administradas, como Instancia administrada de Azure SQL Database, Azure Database for MySQL, Azure Database for PostgreSQL y Azure Cosmos DB. | Cuando las aplicaciones necesitan revisiones importantes para incorporar funcionalidades nuevas o para funcionar de forma eficaz en una plataforma de nube.<br/><br/> Si desea usar las inversiones existentes en las aplicaciones, cumplir los requisitos de escalabilidad, aplicar prácticas innovadoras de Azure DevOps y minimizar el uso de máquinas virtuales.
**Recompilación** | La recompilación va más lejos al recompilar una aplicación desde cero mediante tecnologías de nube de Azure.<br/><br/> Por ejemplo, puede compilar aplicaciones tipo green field con tecnologías [nativas de la nube](https://azure.com/cloudnative), Azure Functions, Azure AI, Instancia administrada de Azure SQL Database y Azure Cosmos DB. | Cuando quiera un desarrollo rápido, y las aplicaciones existentes tengan funcionalidad y ciclo de vida limitados.<br/><br/> Cuando esté listo para acelerar la innovación empresarial (como los procedimientos de DevOps que proporciona Azure), cree aplicaciones mediante tecnologías nativas-nube y aproveche los avances en inteligencia artificial, cadena de bloques e IoT.

<!-- markdownlint-enable MD033 -->

## <a name="migration-example-articles"></a>Artículos de ejemplo de una migración

En los artículos de esta sección se proporcionan ejemplos de varios escenarios comunes de migración. Cada uno de estos ejemplos incluye información general y escenarios de implementación detallados en los que se muestra cómo configurar una infraestructura de migración, valorar la idoneidad de los recursos locales para la migración. Con el tiempo, se agregarán más artículos en esta sección.

![Proyectos comunes de migración/modernización](./media/migration-patterns.png)

*Categorías comunes de proyectos de migración y modernización.*

Los artículos de la serie se resumen a continuación.

- A cada escenario de migración lo impulsan objetivos empresariales ligeramente distintos que determinan la estrategia de migración.
- Para cada escenario de implementación, se proporciona información sobre los impulsores y objetivos empresariales, una arquitectura propuesta, pasos para realizar la migración y una recomendación para la limpieza y los pasos siguientes una vez completada la migración.

### <a name="assessment"></a>Evaluación

**Artículo** | **Detalles**
--- | ---
[Valoración de los recursos locales para su migración a Azure](contoso-migration-assessment.md) | En este artículo se muestra cómo ejecutar la valoración de una aplicación local que se ejecuta en VMware. Aquí, una organización de ejemplo valora las máquinas virtuales de la aplicación mediante el servicio Azure Migrate, y la base de datos SQL Server de la aplicación con Data Migration Assistant.

### <a name="infrastructure"></a>Infraestructura

**Artículo** | **Detalles**
--- | ---
[Implementación de una infraestructura de Azure](contoso-migration-infrastructure.md) | En este artículo se muestra cómo una organización puede preparar su infraestructura local y su infraestructura de Azure para la migración. En el resto de los ejemplos que se proporcionan en esta sección se hace referencia al ejemplo de infraestructura que se establece en este artículo.

### <a name="windows-server-workloads"></a>Cargas de trabajo de Windows Server

**Artículo** | **Detalles**
--- | ---
[Rehospedaje de una aplicación en VM de Azure](contoso-migration-rehost-vm.md) | En este artículo se proporciona un ejemplo de migración de máquinas virtuales de aplicaciones locales a máquinas virtuales de Azure mediante el servicio Site Recovery.
[Rediseño de una aplicación local en un contenedor de Azure y Azure SQL Database](contoso-migration-rearchitect-container-sql.md) | En este artículo se proporciona un ejemplo de cómo migrar una aplicación a la vez que se rediseña el nivel web de la aplicación como un contenedor de Windows que se ejecuta en Azure Service Fabric y la base de datos con Azure SQL Database.

### <a name="linux-workloads"></a>Cargas de trabajo de Linux

**Artículo** | **Detalles**
--- | ---
[Rehospedaje de una aplicación Linux en VM de Azure y Azure Database for MySQL](contoso-migration-rehost-linux-vm-mysql.md) | En este artículo se proporciona un ejemplo de migración de una aplicación hospedada por Linux a máquinas virtuales de Azure mediante Site Recovery. Migra la base de datos de la aplicación a Azure Database for MySQL con MySQL Workbench.
[Rehospedaje de una aplicación Linux en máquinas virtuales de Azure](contoso-migration-rehost-linux-vm.md) | En este ejemplo se muestra cómo completar una migración mediante lift-and-shift de una aplicación basada en Linux a máquinas virtuales de Azure con el servicio Site Recovery.

### <a name="sql-server-workloads"></a>Cargas de trabajo de SQL Server

**Artículo** | **Detalles**
--- | ---
[Rehospedaje de una aplicación en una máquina virtual de Azure e Instancia administrada de Azure SQL Database](contoso-migration-rehost-vm-sql-managed-instance.md) | En este artículo se proporciona un ejemplo de migración de mediante lift-and-shift a Azure para una aplicación local. Esto implica la migración de la máquina virtual front-end de la aplicación mediante [Azure Site Recovery](/azure/site-recovery/site-recovery-overview) y la base de datos de la aplicación a una Instancia administrada de Azure SQL Database con el [servicio Azure Database Migration](/azure/dms/dms-overview).
[Rehospedaje de una aplicación en VM de Azure y en un grupo de disponibilidad AlwaysOn de SQL Server](contoso-migration-rehost-vm-sql-ag.md) | En este ejemplo se muestra cómo migrar una aplicación y datos mediante máquinas virtuales hospedadas de Azure SQL Server. Usa Site Recovery para migrar las VM de la aplicación y Azure Database Migration Service para migrar la base de datos de la aplicación a un clúster de SQL Server protegido por un grupo de disponibilidad AlwaysOn.

### <a name="aspnet--php--java-apps"></a>Aplicaciones de ASP.NET/PHP/Java

**Artículo** | **Detalles**
--- | ---
[Refactorización de una aplicación local a una aplicación web de Azure y Azure SQL Database](contoso-migration-refactor-web-app-sql.md) | En este ejemplo se muestra cómo migrar una aplicación local basada en Windows a una aplicación web de Azure y migrar la base de datos de la aplicación a una instancia de Azure SQL Server con Data Migration Assistant.
[Refactorización de una aplicación de Linux a varias regiones con Azure App Service, Azure Traffic Manager y Azure Database for MySQL](contoso-migration-refactor-linux-app-service-mysql.md) | En este ejemplo se muestra cómo migrar una aplicación local de Linux a una aplicación web de Azure en varias regiones de Azure con Azure Traffic Manager, integrado con GitHub para la entrega continua. La base de datos de la aplicación se migra a una instancia de Azure Database for MySQL.
[Recompilación de una aplicación en Azure](contoso-migration-rebuild.md) | En este artículo se proporciona un ejemplo de recompilación de una aplicación local con una variedad de servicios administrados y funcionalidades de Azure, como Azure App Service, Azure Kubernetes Service (AKS), Azure Functions, Azure Cognitive Services y Azure Cosmos DB.
[Refactorización de Team Foundation Server en Azure DevOps Services](contoso-migration-tfs-vsts.md) | En este artículo se muestra un ejemplo de migración de una implementación de Team Foundation Server local a Azure DevOps Services en Azure.

### <a name="migration-scaling"></a>Escalado de una migración

**Artículo** | **Detalles**
--- | ---
[Escalado de una migración a Azure](contoso-migration-scale.md) | En este artículo se muestra cómo una organización de ejemplo se prepara para escalar a una migración completa a Azure.

### <a name="demo-apps"></a>Aplicaciones de demostración

En los artículos de ejemplo que se proporcionan en esta sección se usan dos aplicaciones de demostración: SmartHotel360 y osTicket.

- **SmartHotel360:** Microsoft desarrolló esta aplicación como una aplicación de prueba que se puede usar cuando se trabaja con Azure. Se proporciona como código abierto y se puede descargar desde [GitHub](https://github.com/Microsoft/SmartHotel360). Se trata de una aplicación ASP.NET conectada a una base de datos de SQL Server. En los escenarios que se describen en estos artículos, la versión actual de esta aplicación está implementada en dos máquinas virtuales de VMware que ejecutan Windows Server 2008 R2 y SQL Server 2008 R2. Estas VM de la aplicación se hospedan en el entorno local y las administra vCenter Server.
- **osTicket:** se trata de una aplicación de incidencias de soporte técnico de código abierto que se ejecuta en Linux. Puede descargarlo en [GitHub](https://github.com/osTicket/osTicket). En los escenarios que se describen en estos artículos, la versión actual de esta aplicación se implementa de manera local en dos máquinas virtuales de VMware que ejecutan Ubuntu 16.04 LTS, con Apache 2, PHP 7.0 y MySQL 5.7.
