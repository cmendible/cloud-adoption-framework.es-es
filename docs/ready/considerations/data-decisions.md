---
title: 'Preparación para Azure: decisiones sobre el diseño de la base de datos'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Preparación para Azure: decisiones sobre el diseño de la base de datos'
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 95b5e9cd4c2c6c1e525d6ce65038881147eedc06
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224262"
---
# <a name="data-design-decisions"></a>Decisiones de diseño de datos

Cuando prepare el entorno de la zona de aterrizaje para la adopción de la nube, deberá determinar los requisitos de datos para hospedar las cargas de trabajo. Los productos y servicios de base de datos de Azure admiten una amplia variedad de escenarios y funcionalidades de almacenamiento de datos. El modo en que se configure el entorno de la zona de aterrizaje para satisfacer los requisitos de datos depende de los requisitos de gobierno, técnicos y empresariales de la carga de trabajo.

## <a name="identify-data-services-requirements"></a>Identificación de los requisitos de los servicios de datos

Como parte de la evaluación y preparación de la zona de aterrizaje, debe identificar los almacenes de datos que debe admitir la zona de aterrizaje. Este proceso supone evaluar cada una de las aplicaciones y servicios que componen las cargas de trabajo para determinar sus requisitos de acceso y almacenamiento de datos. Después de identificar y documentar estos requisitos, puede crear directivas para la zona de aterrizaje con el fin de controlar qué tipos de recursos se permiten en función de las necesidades de su carga de trabajo.

Para cada aplicación o servicio que vaya a implementar en el entorno de la zona de aterrizaje, use el siguiente árbol de decisión como punto de partida para que le ayude a determinar los servicios de almacenamiento de datos adecuados que usar:

![Árbol de decisión de los servicios de base de datos de Azure](../../_images/ready/data-decision-tree.png)

### <a name="key-questions"></a>Preguntas clave

Responda a las siguientes preguntas sobre las cargas de trabajo como ayuda para tomar decisiones basadas en el árbol de decisión de los servicios de base de datos de Azure:

- **¿Necesita control total o propiedad del software de base de datos o del sistema operativo del host?** Algunos escenarios requieren un alto grado de control o propiedad de la configuración de software y los servidores host para las cargas de trabajo de base de datos. En estos casos, puede implementar máquinas virtuales de infraestructura como servicio (IaaS) personalizadas para controlar completamente la implementación y la configuración de los servicios de datos. Si no tiene estos requisitos, los servicios de base de datos administrados por plataforma como servicio (PaaS) pueden reducir los costos de administración y operaciones.
- **¿Usarán las cargas de trabajo una tecnología de base de datos relacional?** Si es así, ¿qué tecnología planea usar? Azure proporciona capacidades de base de datos de PaaS administradas para [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview), [MySQL](https://docs.microsoft.com/azure/mysql/overview), [PostgreSQL](https://docs.microsoft.com/azure/postgresql/overview) y [MariaDB](https://docs.microsoft.com/azure/mariadb/overview).
- **¿Usarán las cargas de trabajo SQL Server?** En Azure, puede hacer que las cargas de trabajo se ejecuten en [SQL Server en Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines/sql-server) basadas en IaaS o en el [servicio hospedado de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) basado en PaaS. La elección de la opción que se vaya a usar es principalmente una pregunta sobre si desea administrar la base de datos, aplicar revisiones y realizar copias de seguridad, o si desea delegar esas operaciones a Azure. En algunos escenarios, los problemas de compatibilidad pueden requerir el uso de SQL Server con IaaS hospedado. Para obtener más información sobre cómo elegir la opción correcta para las cargas de trabajo, consulte [Selección de la opción de SQL Server correcta en Azure](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas).
- **¿Usarán las cargas de trabajo el almacenamiento de base de datos de clave-valor?** [Azure Redis Cache](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-overview) ofrece una solución de almacenamiento de datos clave-valor en caché de alto rendimiento que puede potenciar aplicaciones escalables y rápidas. [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) también proporciona capacidades de almacenamiento de clave-valor de uso general.
- **¿Las cargas de trabajo usarán datos de gráficos o documentos?** [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) es un servicio de base de datos multimodelo que admite una amplia variedad de tipos de datos y API. Azure Cosmos DB también proporciona capacidades de base de datos de documentos y de grafos.
- **¿Usarán las cargas de trabajo datos de familias de columnas?** [Apache HBase en Azure HDInsight](https://docs.microsoft.com/azure/hdinsight/hbase/apache-hbase-overview) se basa en Apache Hadoop. Admite grandes cantidades de datos no estructurados y semiestructurados en una base de datos sin esquemas organizada por familias de columnas.
- **¿Las cargas de trabajo requerirán funcionalidades de análisis de datos de alta capacidad?** Puede usar [Azure SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is) para almacenar y consultar de forma eficaz datos estructurados a escala de petabytes. En caso de cargas de macrodatos no estructuradas, puede usar [Azure Data Lake](https://azure.microsoft.com/solutions/data-lake) para almacenar y analizar archivos de tamaño de petabytes y billones de objetos.
- **¿Requerirán las cargas de trabajo capacidades del motor de búsqueda?** Puede usar [Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search) para compilar índices de búsqueda basados en la nube mejorados con inteligencia artificial que se pueden integrar en sus aplicaciones.
- **¿Usarán las cargas de trabajo los datos de serie temporal?** [Azure Time Series Insights](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-overview) se usa para almacenar, visualizar y consultar grandes cantidades de datos de series temporales, como los que generan los dispositivos de IoT.

> [!NOTE]
> Más información sobre cómo evaluar las opciones de base de datos para cada una de sus aplicaciones o servicios [en la guía de arquitectura de aplicaciones de Azure](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-comparison).

## <a name="common-database-scenarios"></a>Escenarios comunes de bases de datos

En la tabla siguiente se muestran algunos requisitos de escenarios de uso comunes y los servicios de base de datos recomendados para gestionarlos:

| **Escenario** | **Servicio de datos** |
|-----|-----|
| Necesito una base de datos multimodelo distribuida globalmente que admita opciones NoSQL. | [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) |
| Necesito una base de datos relacional totalmente administrada que se aprovisione con rapidez, admita escalado sobre la marcha e incluya inteligencia y seguridad integradas. | [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) |
| Necesito una base de datos relacional MySQL escalable y totalmente administrada, con alta disponibilidad y seguridad integrada sin costo adicional. | [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) |
| Necesito una base de datos relacional PostgreSQL escalable y totalmente administrada, con alta disponibilidad y seguridad integrada sin costo adicional. | [Azure Database para PostgreSQL](https://docs.microsoft.com/azure/postgresql/overview) |
| Tengo previsto hospedar aplicaciones de SQL Server empresarial en la nube y tener un control total sobre el sistema operativo del servidor. | [SQL Server en Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview) |
| Necesito almacenamiento de datos elástico totalmente administrado que disponga de seguridad en todos los niveles de escalado y sin costo adicional. | [Azure SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-overview-what-is) |
| Necesito recursos de almacenamiento de Data Lake que puedan admitir clústeres de Hadoop o datos de HDFS. | [Azure Data Lake](https://azure.microsoft.com/solutions/data-lake) |
| Necesito acceso a datos coherente, de baja latencia y alto rendimiento para mis datos para admitir aplicaciones rápidas y escalables. | [Azure Cache for Redis](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-overview) |
| Necesito una base de datos relacional MariaDB escalable y totalmente administrada, con alta disponibilidad y seguridad integrada sin costo adicional. | [Azure Database for MariaDB](https://docs.microsoft.com/azure/mariadb/overview) |

## <a name="regional-availability"></a>Disponibilidad regional

Azure le permite ofrecer servicios a la escala que necesita para llegar a sus clientes y asociados,  _dondequiera que se encuentren_. Uno de los factores clave a la hora de planear la implementación en la nube es determinar qué región de Azure hospedará los recursos de la carga de trabajo.

La mayoría de los servicios de base de datos están disponibles de forma general en la mayoría de las regiones de Azure. Sin embargo, hay algunas regiones, dirigidas principalmente a clientes gubernamentales, que solo admiten un subconjunto de estos productos. Antes de decidir en qué regiones va a implementar los recursos de base de datos, se recomienda que consulte la [página de regiones](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=data-factory,sql-server-stretch-database,redis-cache,database-migration,sql-data-warehouse,postgresql,mariadb,cosmos-db,mysql,sql-database)  para comprobar el estado más reciente de la disponibilidad regional.

Para obtener más información sobre la infraestructura global de Azure, consulte la [página Regiones de Azure](https://azure.microsoft.com/global-infrastructure/regions). También puede ver los  [productos disponibles por región](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=all) para obtener detalles específicos sobre los servicios generales que están disponibles en cada región de Azure.

## <a name="data-residency-and-compliance-requirements"></a>Requisitos de cumplimiento y residencia de datos

Los requisitos legales y contractuales que están relacionados con el almacenamiento de datos se aplicarán a menudo a sus cargas de trabajo. Estos requisitos pueden variar en función de la ubicación de su organización, la jurisdicción de los recursos físicos que hospedan sus almacenes de datos y su sector empresarial aplicable. Entre los componentes de las obligaciones de datos que deben tenerse en cuenta se incluyen la clasificación de datos, la ubicación de los datos y las responsabilidades correspondientes relativas a la protección de datos en el modelo de responsabilidad compartida. Para obtener ayuda con la comprensión de estos requisitos, consulte las notas del producto  [Consecución de la seguridad y la residencia de datos compatibles con Azure](https://azure.microsoft.com/resources/achieving-compliant-data-residency-and-security-with-azure).

Parte de sus esfuerzos de cumplimiento puede incluir el control del lugar donde sus recursos de base de datos se encuentran físicamente. Las regiones de Azure se organizan por grupos llamados zonas geográficas. Una  [zona geográfica de Azure](https://azure.microsoft.com/global-infrastructure/geographies)  garantiza que se cumplan los requisitos de residencia, soberanía, cumplimiento normativo y resistencia de los datos dentro de las fronteras geográficas y políticas. Si sus cargas de trabajo están sujetas a la soberanía de datos u otros requisitos de cumplimiento, debe implementar sus recursos de almacenamiento en regiones que se encuentren en una zona geográfica de Azure compatible.

## <a name="establish-controls-for-database-services"></a>Establecimiento de controles para servicios de base de datos

Al preparar el entorno de la zona de aterrizaje, puede establecer controles que limiten qué almacenes de datos puede implementar cada usuario. Los controles pueden ayudarle a administrar los costos y a limitar los riesgos de seguridad, al tiempo que permiten a los desarrolladores y equipos de TI implementar y configurar los recursos necesarios para admitir las cargas de trabajo.

Después de identificar y documentar los requisitos de la zona de aterrizaje, puede usar [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) para controlar los recursos de base de datos que permite que creen los usuarios. Los controles pueden tener la forma de [permitir o denegar la creación de tipos de recursos de base de datos](https://docs.microsoft.com/azure/governance/policy/samples/allowed-resource-types). Por ejemplo, puede restringir a los usuarios que solo creen recursos de Azure SQL Database. También puede usar directivas para controlar las opciones permitidas cuando se crea un recurso, como [restringir las SKU de SQL Database que se pueden aprovisionar](https://docs.microsoft.com/azure/governance/policy/samples/allowed-sql-db-skus) o [permitir que se instalen solo versiones específicas de SQL Server](https://docs.microsoft.com/azure/governance/policy/samples/require-sql-12) en una máquina virtual de IaaS.

Las directivas se pueden limitar a recursos, grupos de recursos, suscripciones y grupos de administración. Puede incluir las directivas en las definiciones de [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview) y aplicarlas varias veces a todo el patrimonio de la nube.
