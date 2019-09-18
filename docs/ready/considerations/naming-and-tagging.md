---
title: 'Párese: Convenciones recomendadas de nomenclatura y etiquetado'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: En este artículo se proporcionan recomendaciones detalladas sobre nomenclatura y etiquetado de recursos orientadas específicamente a la compatibilidad con las labores de adopción de la nube empresarial.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: readiness
ms.openlocfilehash: fc4d337f844cef3408c9bc073e3848ee4612fca3
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032424"
---
# <a name="ready-recommended-naming-and-tagging-conventions"></a>Párese: Convenciones recomendadas de nomenclatura y etiquetado

La organización de los recursos basados en la nube de forma que ayuden a la administración operativa y admitan los requisitos de contabilidad es un desafío común que afrontan las enormes labores de adopción de la nube. Al aplicar convenciones de etiquetado de metadatos y nomenclatura bien definidas a recursos hospedados en la nube, el personal de TI puede buscar y administrar los recursos rápidamente. Los nombres y etiquetas bien definidos también ayudan a alinear los costos de uso de la nube con los equipos empresariales mediante mecanismos de contabilidad de contracargo y visualización de costos.

En la guía de [convenciones de nomenclatura de recursos de Azure](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) del Centro de arquitectura de Azure se proporcionan recomendaciones generales sobre las convenciones de nomenclatura y se analizan las limitaciones de los nombres y las reglas de plataforma. El siguiente análisis amplía esa guía genérica con recomendaciones más detalladas dirigidas específicamente a respaldar las labores de adopción de la nube empresarial.

Los nombres de los recursos pueden ser difíciles de cambiar. Antes de comenzar con una implementación de gran tamaño en la nube, su prioridad debe ser que los equipos de adopción de la nube establezcan una convención de nomenclatura completa.

> [!NOTE]
> Cada empresa tiene diferentes requisitos de organización y administración. Las recomendaciones de este artículo sirven como punto de partida para los análisis dentro de los equipos de adopción de la nube.
>
> A medida que estos análisis progresan, use la siguiente plantilla para capturar las decisiones sobre nomenclatura y etiquetado que tome al alinear estas recomendaciones con sus necesidades empresariales específicas.
>
> Descargue la [plantilla de seguimiento de convención de nomenclatura y etiquetado](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/CAF%20Readiness%20Naming%20and%20Tagging%20tracking%20template.xlsx).

## <a name="naming-and-tagging-resources"></a>Nomenclatura y etiquetado de recursos

Una estrategia de nomenclatura y etiquetado incluye detalles empresariales y operativos como componentes de nombres de recursos y etiquetas de metadatos:

- La parte relacionada con la empresa de esta estrategia garantiza que los nombres y las etiquetas de los recursos incluyen la información organizativa necesaria para identificar a los equipos. Use un recurso junto con los propietarios de la empresa responsables de los costos de los recursos.
- El lado operativo garantiza que los nombres y las etiquetas incluyen información que los equipos de TI usan para identificar la carga de trabajo, la aplicación, el entorno, la importancia y otra información útil para administrar los recursos.

### <a name="resource-naming"></a>Nombres de recursos

Una convención de nomenclatura efectiva ensambla los nombres de recursos usando información importante del recursos como parte de su nombre. Por ejemplo, mediante las convenciones de nomenclatura recomendadas que se analizan [más adelante en este artículo](#sample-naming-convention), un recurso de IP pública para una carga de trabajo de producción de SharePoint se denomina así: `pip-sharepoint-prod-westus-001`.

A partir del nombre, puede identificar rápidamente el tipo del recurso, su carga de trabajo asociada, su entorno de implementación y la región de Azure que lo hospeda.

#### <a name="naming-scope"></a>Ámbito de nomenclatura

Todos los tipos de recursos de Azure tienen un ámbito que define cómo se pueden administrar estos recursos en relación con otros tipos de recursos. En términos de las convenciones de nomenclatura, esto significa que un recurso debe tener un nombre único dentro de su ámbito.

Por ejemplo, una red virtual tiene un ámbito de grupo de recursos, lo que significa que solo puede haber una red llamada `vnet-prod-westus-001` en un grupo de recursos determinado. Otros grupos de recursos pueden tener su propia red virtual llamada `vnet-prod-westus-001`. Las subredes, para proporcionar otro ejemplo, tienen como ámbito las redes virtuales, lo que significa que cada subred de una red virtual debe tener un nombre único.

Algunos nombres de recursos, como los servicios PaaS con puntos de conexión públicos o etiquetas DNS de máquina virtual, tienen ámbitos globales, lo que significa que deben ser únicos en toda la plataforma de Azure.

Los nombres de los recursos tienen límites de longitud. Equilibrar el contexto insertado en un nombre con su ámbito y longitud es importante al desarrollar las convenciones de nomenclatura. Para más información sobre las reglas de nomenclatura de los caracteres, los ámbitos y las longitudes de nombres permitidos para los tipos de recursos, consulte [Convenciones de nomenclatura para los recursos de Azure](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).

#### <a name="recommended-naming-components"></a>Componentes de nomenclatura recomendados

Cuando construya su convención de nomenclatura, identifique las partes clave de la información que quiere reflejar en el nombre de un recurso. Cada información es pertinente para un tipo de recurso. En la lista siguiente se proporcionan ejemplos de información que son útiles al construir nombres de recursos.

Mantenga corta la longitud de los componentes de nomenclatura para evitar que se superen los límites de longitud de los nombres de recursos.

| Componente de nomenclatura | DESCRIPCIÓN | Ejemplos |
| --- | --- | --- |
| Unidad de negocio | División de nivel superior de la empresa que posee la suscripción o la carga de trabajo a la que pertenece el recurso. En organizaciones más pequeñas, este componente podría representar un único elemento organizativo de nivel superior corporativo. | *fin*, *mktg*, *product*, *it*, *corp* |
| Tipo de suscripción | Descripción resumida del propósito de la suscripción que contiene el recurso. A menudo desglosado por tipo de entorno de implementación o cargas de trabajo específicas. | *prod,* s*hared, client* |
| Nombre de aplicación o servicio | Nombre de la aplicación, carga de trabajo o servicio del que forma parte el recurso. | *navigator*, *emissions*, *sharepoint*, *hadoop* |
| Entorno de implementación | Fase del ciclo de vida de desarrollo de la carga de trabajo que admite el recurso. | *prod, dev, qa, stage, test* |
| Region | La región de Azure en la que se implementa el recurso. | *westus, eastus2, westeurope, usgovia* |

#### <a name="recommended-resource-type-prefixes"></a>Prefijos de tipo de recurso recomendados

Cada carga de trabajo puede constar de muchos recursos y servicios individuales. La incorporación de prefijos de tipo de recurso a los nombres de recursos facilita la identificación visual de los componentes de aplicaciones o servicios.

En la lista siguiente se proporcionan los prefijos de tipo de recurso de Azure recomendados que se deben usar al definir las convenciones de nomenclatura.

| Tipo de recurso                       | Prefijo de nombre de recurso |
| ----------------------------------- | -------------------- |
| Resource group                      | rg-                  |
| Azure Virtual Network                     | vnet-                |
| Puerta de enlace de red virtual             | vnet-gw-             |
| Conexión de puerta de enlace                  | cn-                  |
| Subnet                              | snet-                |
| Grupo de seguridad de red              | nsg-                 |
| Azure Virtual Machines                    | vm-                  |
| Cuenta de almacenamiento de máquina virtual                  | stvm                 |
| Dirección IP pública                           | pip-                 |
| Azure Load Balancer                       | lb-                  |
| NIC                                 | nic-                 |
| Azure Service Bus                         | sb-                  |
| Colas de Azure Service Bus                  | sbq-                 |
| Aplicaciones de Azure App Service                    | azapp-               |
| Aplicaciones de Azure Functions                       | azfun-               |
| Azure Cloud Services                      | azcs-                |
| Azure SQL Database                  | sqldb-               |
| Azure Cosmos DB (anteriormente Azure DocumentDB) | cosdb-               |
| Azure Cache for Redis               | redis-               |
| Azure Database for MySQL            | mysql-               |
| Azure SQL Data Warehouse                  | sqldw-               |
| SQL Server Stretch Database         | sqlstrdb-            |
| Azure Storage                       | stor                 |
| Azure StorSimple                          | ssimp                |
| Azure Search                        | srch-                |
| Azure Cognitive Services                  | cs-                  |
| Área de trabajo de Azure Machine Learning    | aml-                 |
| Azure Data Lake Storage             | dls                  |
| Análisis con Azure Data Lake           | dla                  |
| Azure HDInsight: Spark                   | hdis-                |
| Azure HDInsight: Hadoop                  | hdihd-               |
| Azure HDInsight: R Server                | hdir-                |
| Azure HDInsight: HBase                   | hdihb-               |
| Power BI Embedded                   | pbiemb               |
| Azure Stream Analytics                    | asa-                 |
| Azure Data Factory                        | df-                  |
| Azure Event Hubs                           | evh-                 |
| Azure IoT Hub                       | aih-                 |
| Azure Notification Hubs                   | anh-                 |
| Espacio de nombres de Azure Notification Hubs          | anhns-               |

### <a name="metadata-tags"></a>Etiquetas de metadatos

Al aplicar etiquetas de metadatos a los recursos en la nube, puede incluir información sobre esos recursos que no se pudo incluir en el nombre del recurso. Puede usar esa información para realizar filtrados e informes más elaborados sobre los recursos. Quiere que estas etiquetas incluyan contexto sobre la carga de trabajo o la aplicación asociadas del recurso, los requisitos operativos y la información de propiedad. Esta información la pueden usar los equipos de TI o empresariales para encontrar recursos o generar informes sobre el uso y la facturación de los recursos.

Las etiquetas que se aplican a los recursos y las etiquetas que son necesarias u opcionales varían según la organización. En la lista siguiente se proporcionan ejemplos de etiquetas comunes que capturan contexto e información importantes sobre un recurso. Use esta lista como punto de partida para establecer sus propias convenciones de etiquetado.

| Nombre de etiqueta                  | DESCRIPCIÓN                                                                                                                                                                                                    | Clave               | Valor de ejemplo                                   |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------|
| Nombre de la aplicación          | Nombre de la aplicación, servicio o carga de trabajo a la que está asociado el recurso.                                                                                                                                 | *ApplicationName* | *{app name}*                                    |
| Nombre del aprobador             | Persona responsable de la aprobación de los costos relacionados con este recurso.                                                                                                                                               | *Approver*        | *{email}*                                       |
| Presupuesto requerido o aprobado  | Dinero asignado para esta aplicación, servicio o carga de trabajo.                                                                                                                                                    | *BudgetAmount*    | *{\$}*                                          |
| Unidad de negocio             | División de nivel superior de la empresa que posee la suscripción o la carga de trabajo a la que pertenece el recurso. En organizaciones más pequeñas, esta etiqueta puede representar un solo elemento organizativo de nivel superior corporativo o compartido. | *BusinessUnit*    | *FINANCE, MARKETING,{Product Name}, CORP, SHARED* |
| Centro de costos               | Centro de costo de contabilidad asociado a este recurso.                                                                                                                                                          | *CostCenter*      | *{number}*                                      |
| Recuperación ante desastres         | Importancia empresarial de la aplicación, la carga de trabajo o el servicio.                                                                                                                                                | *DR*              | *Mission-critical, Critical, Essential*         |
| Fecha de finalización del proyecto   | Fecha en la que la aplicación, la carga de trabajo o el servicio están programados para su retirada.                                                                                                                                  | *EndDate*         | *{date}*                                        |
| Entorno               | Entorno de implementación de la aplicación, la carga de trabajo o el servicio.                                                                                                                                              | *Env*             | *Prod, Dev, QA, Stage, Test*                    |
| Nombre del propietario                | Propietario de la aplicación, la carga de trabajo o el servicio.                                                                                                                                                                | *Propietario*           | *{email}*                                       |
| Nombre del solicitante            | Usuario que solicitó la creación de esta aplicación.                                                                                                                                                          | *Requestor*       | *{email}*                                       |
| Clase de servicio             | Nivel de contrato de nivel de servicio de la aplicación, la carga de trabajo o el servicio.                                                                                                                                       | *ServiceClass*    | *Dev, Bronze, Silver, Gold*                     |
| Fecha de inicio del proyecto | Fecha en que se implementó por primera vez la aplicación, la carga de trabajo o el servicio.                                                                                                                                           | *StartDate*       | *{date}*                                        |

## <a name="sample-naming-convention"></a>Ejemplo de convención de nomenclatura

En la siguiente sección se proporcionan ejemplos de esquemas de nomenclatura para tipos de recursos comunes de Azure que se implementan durante una implementación de nube de empresa.

### <a name="subscriptions"></a>Suscripciones

| Tipo de recurso   | Ámbito                        | Formato                                             | Ejemplos                                     |
|--------------|------------------------------|----------------------------------------------------|----------------------------------------------|
| Subscription | Cuenta o Contrato Enterprise | \<Unidad de negocio\>-\<Tipo de suscripción\>-\<\#\#\#\> | <ul><li>mktg-prod-001 </li><li>corp-shared-001 </li><li>fin-client-001</li></ul> |

### <a name="resource-groups"></a>Grupos de recursos

| Tipo de recurso     | Ámbito        | Formato                                                     | Ejemplos                                                                            |
|----------------|--------------|------------------------------------------------------------|-------------------------------------------------------------------------------------|
| Resource group | Subscription | rg-\<nombre de aplicación o servicio\>-\<tipo de suscripción\>-\<\#\#\#\> | <ul><li>rg-mktgsharepoint-prod-001 </li><li>rg-acctlookupsvc-share-001 </li><li>rg-ad-dir-services-shared-001</li></ul> |

### <a name="virtual-networking"></a>Redes virtuales

| Tipo de recurso               | Ámbito           | Formato                                                                | Ejemplos                                                                                              |
|--------------------------|-----------------|-----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| Azure Virtual Network          | Resource group  | vnet-\<tipo de suscripción\>-\<región\>-\<\#\#\#\>                      | <ul><li>vnet-shared-eastus2-001 </li><li>vnet-prod-westus-001 </li><li>vnet-client-eastus2-001</li></ul>                                  |
| Puerta de enlace virtual de red virtual     | Virtual network | vnet-gw-v-\<tipo de suscripción\>-\<región\>-\<\#\#\#\>                 | <ul><li>vnet-gw-v-shared-eastus2-001 </li><li>vnet-gw-v-prod-westus-001 </li><li>vnet-gw-v-client-eastus2-001</li></ul>                   |
| Puerta de enlace local de red virtual       | Puerta de enlace virtual | vnet-gw-l-\<tipo de suscripción\>-\<región\>-\<\#\#\#\>                 | <ul><li>vnet-gw-l-shared-eastus2-001 </li><li>vnet-gw-l-prod-westus-001 </li><li>vnet-gw-l-client-eastus2-001</li></ul>                   |
| Conexiones de sitio a sitio | Resource group  | cn-\<nombre de puerta de enlace local\>-to-\<nombre de puerta de enlace virtual\>                 | <ul><li>cn-l-gw-shared-eastus2-001-to-v-gw-shared-eastus2-001 </li><li>cn-l-gw-shared-eastus2-001-to-shared-westus-001</li></ul> |
| Conexiones de red virtual         | Resource group  | cn-\<suscripción1\>\<región1\>-to-\<subscripción2\>\<región2\>-      | <ul><li>cn-shared-eastus2-to-shared-westus </li><li>cn-prod-eastus2-to-prod-westus</li></ul>                                     |
| Subnet                   | Virtual network | snet-\<suscripción\>-\<subregión\>-\<\#\#\#\>                       | <ul><li>snet-shared-eastus2-001 </li><li>snet-prod-westus-001 </li><li>snet-client-eastus2-001</li></ul>                                  |
| Grupo de seguridad de red   | Subred o NIC   | nsg-\<nombre de directiva o nombre de aplicación\>-\<\#\#\#\>                             | <ul><li>nsg-weballow-001 </li><li>nsg-rdpallow-001 </li><li>nsg-sqlallow-001 </li><li>nsg-dnsbloked-001</li></ul>                                  |
| Dirección IP pública                | Resource group  | pip-\<nombre de máquina virtual o nombre de aplicación\>-\<entorno\>-\<subregión\>-\<\#\#\#\> | <ul><li>pip-dc1-shared-eastus2-001 </li><li>pip-hadoop-prod-westus-001</li></ul>                                                 |

### <a name="azure-virtual-machines"></a>Azure Virtual Machines

| Tipo de recurso         | Ámbito          | Formato                                                              | Ejemplos                                                                             |
|--------------------|----------------|---------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Azure Virtual Machines    | Resource group | vm\<nombre de directiva o nombre de aplicación\>\<\#\#\#\>                              | <ul><li>vmnavigator001 </li><li>vmsharepoint001 </li><li>vmsqlnode001 </li><li>vmhadoop001</li></ul>                              |
| Cuenta de almacenamiento de máquina virtual | Global         | stvm\<tipo de rendimiento\>\<nombre de aplicación o nombre de producto\>\<región\>\<\#\#\#\> | <ul><li>stvmstcoreeastus2001 </li><li>stvmpmcoreeastus2001 </li><li>stvmstplmeastus2001 </li><li>stvmsthadoopeastus2001</li></ul> |
| Etiqueta DNS          | Global         | \<un registro de vm\>.[\<región\>.cloudapp.azure.com]                  | <ul><li>dc1.westus.cloudapp.azure.com </li><li>web1.eastus2.cloudapp.azure.com</li></ul>                        |
| Azure Load Balancer      | Resource group | lb-\<nombre de aplicación o rol\>\<entorno\>\<\#\#\#\>                    | <ul><li>lb-navigator-prod-001 </li><li>lb-sharepoint-dev-001</li></ul>                                          |
| NIC                | Resource group | nic-\<\#\#\>-\<nombre de vm\>-\<suscripción\>\<\#\#\#\>                  | <ul><li>nic-01-dc1-shared-001 </li><li>nic-02-vmhadoop1-prod-001 </li><li>nic-02-vmtest1-client-001</li></ul>            |

### <a name="paas-services"></a>Servicios de PaaS

| Tipo de recurso     | Ámbito  | Formato                                                              | Ejemplos                                                                                 |
|----------------|--------|---------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| Azure App Service    | Global | azapp-\<nombre de aplicación\>-\<entorno\>-\<\#\#\#\>.[{azurewebsites.net}] | <ul><li>azapp-navigator-prod-001.azurewebsites.net </li><li>azapp-accountlookup-dev-001.azurewebsites.net</li></ul> |
| Aplicación Azure Functions   | Global | azfun-\<nombre de aplicación\>-\<entorno\>-\<\#\#\#\>.[{azurewebsites.net}] | <ul><li>azfun-navigator-prod-001.azurewebsites.net </li><li>azfun-accountlookup-dev-001.azurewebsites.net</li></ul> |
| Azure Cloud Services | Global | azcs-\<nombre de aplicación\>-\<entorno\>-\<\#\#\#\>.[{cloudapp.net}]       | <ul><li>azcs-navigator-prod-001.azurewebsites.net </li><li>azcs-accountlookup-dev-001.azurewebsites.net</li></ul>   |

### <a name="azure-service-bus"></a>Azure Service Bus

| Tipo de recurso         | Ámbito       | Formato                                                     | Ejemplos                           |
|--------------------|-------------|------------------------------------------------------------|------------------------------------|
| Azure Service Bus        | Global      | sb-\<nombre de aplicación\>-\<entorno\>.[{servicebus.windows.net}] | <ul><li>sb-navigator-prod </li><li>sb-emissions-dev</li></ul> |
| Colas de Azure Service Bus | Azure Service Bus | sbq-\<descriptor de consulta\>                                   | <ul><li>sbq-messagequery</li></ul>                   |

### <a name="databases"></a>Bases de datos

| Tipo de recurso                          | Ámbito              | Formato                                | Ejemplos                                       |
|-------------------------------------|--------------------|---------------------------------------|------------------------------------------------|
| Azure SQL Database                  | Global             | sqldb-\<nombre de aplicación\>-\<entorno\>    | <ul><li>sqldb-navigator-prod </li><li>sqldb-emissions-dev</li></ul>       |
| Azure Cosmos DB (anteriormente DocumentDB) | Global             | cosdb-\<nombre de aplicación\>-\<entorno\>    | <ul><li>cosdb-navigator-prod </li><li>cosdb-emissions-dev</li></ul>       |
| Azure Cache for Redis               | Global             | redis-\<nombre de aplicación\>-\<entorno\>    | <ul><li>redis-navigator-prod </li><li>redis-emissions-dev</li></ul>       |
| Azure Database for MySQL            | Global             | mysql-\<nombre de aplicación\>-\<entorno\>    | <ul><li>mysql-navigator-prod </li><li>mysql-emissions-dev</li></ul>       |
| Azure SQL Data Warehouse                  | Global             | sqldw-\<nombre de aplicación\>-\<entorno\>    | <ul><li>sqldw-navigator-prod </li><li>sqldw-emissions-dev</li></ul>       |
| SQL Server Stretch Database         | Azure SQL Database | sqlstrdb-\<nombre de aplicación\>-\<entorno\> | <ul><li>sqlstrdb-navigator-prod </li><li>sqlstrdb-emissions-dev</li></ul> |

### <a name="storage"></a>Storage

| Tipo de recurso                              | Ámbito  | Formato                                                                        | Ejemplos                                   |
|-----------------------------------------|--------|-------------------------------------------------------------------------------|--------------------------------------------|
| Cuenta de Azure Storage: uso general     | Global | st\<nombre de almacenamiento\>\<\#\#\#\>                                                  | <ul><li>stnavigatordata001 </li><li>stemissionsoutput001</li></ul>    |
| Cuenta de Azure Storage: registros de diagnóstico | Global | stdiag\<primeras dos letras del nombre de la suscripción y el número\>\<región\>\<\#\#\#\> | <ul><li>stdiagsh001eastus2001 </li><li>stdiagsh001westus001</li></ul> |
| Azure StorSimple                              | Global | ssimp\<nombre de aplicación\>\<entorno\>                                              | <ul><li>ssimpnavigatorprod </li><li>ssimpemissionsdev</li></ul>       |

### <a name="ai--machine-learning"></a>AI + Aprendizaje automático

| Tipo de recurso                       | Ámbito          | Formato                            | Ejemplos                               |
|----------------------------------|----------------|-----------------------------------|----------------------------------------|
| Azure Search                     | Global         | srch-\<nombre de aplicación\>-\<entorno\> | <ul><li>srch-navigator-prod </li><li>srch-emissions-dev</li></ul> |
| Azure Cognitive Services               | Resource group | cs-\<nombre de aplicación\>-\<entorno\>   | <ul><li>cs-navigator-prod </li><li>cs-emissions-dev</li></ul>     |
| Área de trabajo de Azure Machine Learning | Resource group | aml-\<nombre de aplicación\>-\<entorno\>  | <ul><li>aml-navigator-prod </li><li>aml-emissions-dev</li></ul>   |

### <a name="analytics"></a>Análisis

| Tipo de recurso                | Ámbito  | Formato                             | Ejemplos                                 |
|---------------------------|--------|------------------------------------|------------------------------------------|
| Azure Data Factory        | Global | df-\<nombre de aplicación\>\<entorno\>     | <ul><li>df-navigator-prod </li><li>df-emissions-dev</li></ul>       |
| Azure Data Lake Storage   | Global | dls\<nombre de aplicación\>\<entorno\>     | <ul><li>dlsnavigatorprod </li><li>dlsemissionsdev</li></ul>         |
| Análisis con Azure Data Lake | Global | dla\<nombre de aplicación\>\<entorno\>     | <ul><li>dlanavigatorprod </li><li>dlaemissionsdev</li></ul>         |
| Azure HDInsight: Spark         | Global | hdis-\<nombre de aplicación\>-\<entorno\>  | <ul><li>hdis-navigator-prod </li><li>hdis-emissions-dev </li></ul>  |
| Azure HDInsight: Hadoop        | Global | hdihd-\<nombre de aplicación\>-\<entorno\> | <ul><li>hdihd-hadoop-prod </li><li>hdihd-emissions-dev</li></ul>    |
| Azure HDInsight: R Server      | Global | hdir-\<nombre de aplicación\>-\<entorno\>  | <ul><li>hdir-navigator-prod </li><li>hdir-emissions-dev</li></ul>   |
| Azure HDInsight: HBase         | Global | hdihb-\<nombre de aplicación\>-\<entorno\> | <ul><li>hdihb-navigator-prod </li><li>hdihb-emissions-dev</li></ul> |
| Power BI Embedded         | Global | pbiemb\<nombre de aplicación\>\<entorno\>  | <ul><li>pbiem-navigator-prod </li><li>pbiem-emissions-dev</li></ul> |

### <a name="internet-of-things-iot"></a>Internet de las cosas (IoT)

| Tipo de recurso                         | Ámbito          | Formato                             | Ejemplos                                 |
|------------------------------------|----------------|------------------------------------|------------------------------------------|
| Azure Stream Analytics en IoT Edge | Resource group | asa-\<nombre de aplicación\>-\<entorno\>   | <ul><li>asa-navigator-prod </li><li>asa-emissions-dev</li></ul>     |
| Azure IoT Hub                      | Global         | aih-\<nombre de aplicación\>-\<entorno\>   | <ul><li>aih-navigator-prod </li><li>aih-emissions-dev</li></ul>     |
| Azure Event Hubs                          | Global         | evh-\<nombre de aplicación\>-\<entorno\>   | <ul><li>evh-navigator-prod </li><li>evh-emissions-dev</li></ul>     |
| Azure Notification Hubs                   | Resource group | anh-\<nombre de aplicación\>-\<entorno\>   | <ul><li>evh-navigator-prod </li><li>evh-emissions-dev</li></ul>     |
| Espacio de nombres de Azure Notification Hubs         | Global         | anhns-\<nombre de aplicación\>-\<entorno\> | <ul><li>anhns-navigator-prod </li><li>anhns-emissions-dev</li></ul> |
