---
title: Procedimientos recomendados para la gestión de los costos y los ajustes de tamaño de las cargas de trabajo migradas a Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Procedimientos recomendados para la gestión de los costos y los ajustes de tamaño de las cargas de trabajo migradas a Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 99255722c28b9bb6c33f78e226cb8135e7c7be17
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70836782"
---
# <a name="best-practices-for-costing-and-sizing-workloads-migrated-to-azure"></a>Procedimientos recomendados para la gestión de los costos y los ajustes de tamaño de las cargas de trabajo migradas a Azure

Al planear y diseñar la migración a Azure, centrarse en los costos garantiza su éxito a largo plazo. Durante un proyecto de migración, es fundamental que todos los equipos (como finanzas, administración y equipos de desarrollo de aplicaciones) conozcan los costos asociados.

- Disponer de una estimación del gasto antes de la migración, con una base de referencia del presupuesto mensual, trimestral y anual, resulta fundamental para el éxito.
- Tras la migración, debe optimizar los costos, supervisar continuamente las cargas de trabajo y planear los patrones de uso futuro. Los recursos migrados podrían comenzar como un tipo de carga de trabajo y evolucionar a otro con el tiempo, en función del uso, los costos y requisitos empresariales cambiantes.

En este artículo se describen los procedimientos recomendados para la administración de los costos y el tamaño antes y después de la migración.

> [!IMPORTANT]
> Los procedimientos recomendados y las opiniones que se describen en este artículo se basan en la plataforma Windows Azure y las características disponibles en el momento de redactar el artículo. Las características y funcionalidades cambian con el tiempo. No todas las recomendaciones pueden aplicarse para una implementación, de modo que seleccione lo que sea válido en su caso.

## <a name="before-migration"></a>Antes de la migración

Antes de mover las cargas de trabajo a la nube, valore el costo mensual que supone ejecutarlas en Azure. Una administración proactiva de los costos de la nube le ayuda a cumplir su presupuesto para los gastos operativos. Si el presupuesto es limitado, debe tenerlo en cuenta antes de la migración. Considere la posibilidad de convertir las cargas de trabajo a las tecnologías sin servidor de Azure, cuando sea apropiado, para reducir los costos.

Los procedimientos recomendados de esta sección le ayudan a calcular los costos, realizar el ajuste de tamaño para las máquinas virtuales y el almacenamiento, utilizar las ventajas de Azure híbrido, usar máquinas virtuales reservadas y evaluar los gastos en la nube de las suscripciones.

## <a name="best-practice-estimate-monthly-workload-costs"></a>Procedimiento recomendado: Evalúe los costos de la carga de trabajo mensualmente

Para realizar la previsión de la factura mensual de las cargas de trabajo migradas, puede usar varias herramientas.

- **Calculadora de precios de Azure:** Seleccione los productos que desea calcular, por ejemplo las máquinas virtuales y el almacenamiento. Especifique los costos en la calculadora de precios, para calcular una estimación.

 ![Calculadora de precios de Azure](./media/migrate-best-practices-costs/pricing.png) *Azure pricing calculator*

- **Azure Migrate:** Para calcular los costos, debe revisar y tener en cuenta todos los recursos necesarios para ejecutar sus cargas de trabajo en Azure. A fin de obtener estos datos, cree un inventario de sus activos, incluidos los servidores, las máquinas virtuales, las bases de datos y el almacenamiento. Puede usar Azure Migrate para recopilar esta información.

- Azure Migrate detecta y evalúa el entorno local para proporcionar un inventario.
- Azure Migrate puede asignar y mostrar las dependencias entre las máquinas virtuales para que tenga una imagen completa.
- Una evaluación de Azure Migrate contiene el costo estimado.
  - Costos de proceso: con el tamaño de máquina virtual de Azure recomendado cuando se crea una evaluación, Azure Migrate usa la API de facturación para calcular los costos mensuales estimados de cada máquina virtual. El cálculo considera la configuración del sistema operativo, Software Assurance, las instancias reservadas, el tiempo de actividad de las máquinas virtuales, la ubicación y la moneda. Suma el costo de todas las máquinas virtuales de la valoración y calcula un costo de proceso total mensual.
  - Costo del almacenamiento: Azure Migrate calcula los costos de almacenamiento mensuales totales; para ello, suma los costos de almacenamiento de todas las máquinas virtuales de la evaluación. Puede sumar el costo mensual de todos los discos conectados a una máquina concreta para calcular el costo de almacenamiento mensual de dicha máquina.

    ![Azure Migrate](./media/migrate-best-practices-costs/assess.png)
    *Evaluación de Azure Migrate*

**Más información:**

- [Use](https://azure.microsoft.com/pricing/calculator) la calculadora de precios de Azure.
- [Obtenga información general](/azure/migrate/migrate-overview) de Azure Migrate.
- [Obtenga información sobre](/azure/migrate/concepts-assessment-calculation) evaluaciones de Azure Migrate.
- [Obtenga información](/azure/dms/dms-overview) sobre Azure Database Migration Service.

## <a name="best-practice-right-size-vms"></a>Procedimiento recomendado: Elección del tamaño adecuado para las máquinas virtuales

Puede elegir varias opciones al implementar las máquinas virtuales de Azure para admitir cargas de trabajo. Cada tipo tiene características específicas y combinaciones diferentes de CPU, memoria y discos. Las máquinas virtuales se agrupan como sigue:

**Tipo** | **Detalles** | **Uso**
--- | --- | ---
**Uso general** | Uso equilibrado de CPU y memoria. | Adecuada para desarrollo y pruebas, bases de datos de tamaño pequeño o mediano, y servidores web de tráfico bajo o medio.
**Optimizada para proceso** | Uso elevado de la CPU respecto a la memoria. | Adecuada para servidores web de tráfico con volumen medio, aplicaciones de red, procesos por lotes y servidores de aplicaciones.
**Optimizada para memoria** | Memoria alta en relación con CPU. | Adecuada para bases de datos relacionales, memorias caché de tamaño mediano a grande y análisis en memoria.
**Almacenamiento optimizado** | Alto rendimiento de disco y E/S. | Adecuada para bases de datos SQL y NoSQL y macrodatos.
**GPU optimizada** | Máquinas virtuales especializadas. Una o varias GPU. | Gráficos pesados y edición de vídeo.
**Alto rendimiento** | CPU más rápida y eficaz. Máquinas virtuales con interfaces de red de alto rendimiento (RDMA) opcionales. | Aplicaciones críticas de alto rendimiento.

- Es importante comprender las diferencias de precio entre estas máquinas virtuales y los efectos a largo plazo en el presupuesto.
- Cada tipo tiene varias series de máquinas virtuales.
- Además, cuando se selecciona una máquina virtual dentro de una serie, solo puede escalar la máquina virtual y reducirla verticalmente dentro de esa serie. Por ejemplo, DSv2\_2 puede ampliarse a DSv2\_4, pero no se puede cambiar a una serie diferente como Fsv2\_2.

**Más información:**

- [Obtenga más información](/azure/virtual-machines/windows/sizes) sobre los tipos de máquina virtual y el tamaño, y sobre la asignación de tamaños a los tipos.
- [Planee](/azure/cloud-services/cloud-services-sizes-specs) el tamaño de las máquinas virtuales.
- [Vea](/azure/migrate/contoso-migration-assessment) un ejemplo de valoración de la empresa ficticia Contoso.

## <a name="best-practice-select-the-right-storage"></a>Procedimiento recomendado: Selección del almacenamiento correcto

El ajuste y el mantenimiento del almacenamiento local (SAN o NAS) y las redes para admitirlo puede resultar costoso y lento. Los datos de los archivos (almacenamiento) normalmente se migran a la nube para ayudar a aliviar las dificultades de administración y operativas. Microsoft ofrece varias opciones para mover datos a Azure. Debe tomar decisiones acerca de esas opciones. Seleccionar el tipo correcto para el almacenamiento de los datos puede ahorrar a la organización varios miles de dólares al mes. Algunas consideraciones:

- Los datos a los que no se accede mucho y no son críticos para la empresa no tienen por qué colocarse en el almacenamiento más costoso.
- Por el contrario, los datos empresariales importantes deben ubicarse en las opciones de almacenamiento de nivel superior.
- Durante el planeamiento de la migración, realice un inventario de los datos y clasifíquelos según su importancia, con el fin de asignarlos al almacenamiento más adecuado. Considere el presupuesto y los costos, así como el rendimiento. El costo no debería ser necesariamente el factor principal a la hora de decidir. Seleccionar la opción menos cara podría exponer a la carga de trabajo a riesgos relacionados con la disponibilidad y el rendimiento.

### <a name="storage-data-types"></a>Tipos de datos de almacenamiento

Azure proporciona diferentes tipos de datos de almacenamiento.

<!--markdownlint-disable MD033 -->

**Tipo de datos** | **Detalles** | **Uso**
--- | --- |  ---
**Blobs** | Optimizado para almacenar grandes cantidades de datos de objetos no estructurados, como datos de texto o binarios.<br/><br/> | Permite el acceso a datos desde cualquier lugar a través de HTTP/HTTPS. | Se usa para escenarios de acceso aleatorio y streaming. Por ejemplo, para servir imágenes y documentos directamente a un explorador, secuencias de vídeo y audio, y almacenar los datos de recuperación ante desastres y copia de seguridad.
**Archivos** | Recursos compartidos de archivos administrados a los que se accede a través de SMB 3.0 | Se usa al migrar recursos compartidos de archivos locales y para proporcionar varios tipos de acceso y conexiones a los datos de los archivos.
**Discos** | En función de los blobs en páginas.<br/><br/> Tipo de disco (velocidad): Estándar (HDD o SSD) o Prémium (SSD).<br/><br/>Administración de discos: No administrado (se administra la configuración de los discos y el almacenamiento) o administrado (se selecciona el tipo de disco y Azure lo administra en su lugar). | Se usan discos Prémium para las máquinas virtuales. Se usan discos administrados para simplificar la administración y la escala.
**Colas** | Se almacenan y recuperan grandes cantidades de mensajes, a los que se accede a través de llamadas autenticadas (HTTP o HTTPS) | Se conectan componentes de aplicación con colas de mensajes asincrónicos.
**Tablas** | Se almacenan tablas. | Ahora forma parte de Table API de Azure Cosmos DB.

<!--markdownlint-enable MD033 -->

### <a name="access-tiers"></a>Niveles de acceso

Azure Storage ofrece diferentes opciones para obtener acceso a los datos de blob en bloques. Si selecciona el nivel de acceso adecuado, ayuda a garantizar que almacena los datos de blob en bloques de la manera más rentable.

<!--markdownlint-disable MD033 -->

**Tipo** | **Detalles** | **Uso**
--- | --- | ---
**Acceso frecuente** | Costo de almacenamiento mayor que en el nivel de acceso esporádico. Costos inferiores por el acceso que en el nivel de acceso esporádico.<br/><br/>Este es el nivel predeterminado. | Se emplea para datos en uso activo a los que se accede con frecuencia.
**Acceso esporádico** | El costo de almacenamiento es inferior que el del nivel de acceso frecuente. Los costos por el acceso son superiores a los del nivel de acceso frecuente.<br/><br/> El almacenamiento es para 30 días como mínimo. | El almacenamiento es a corto plazo y los datos están disponibles, pero se accede a ellos con poca frecuencia.
**Archivar** | Se usa para blobs en bloques individuales.<br/><br/> Es la opción más rentable para el almacenamiento. El acceso a los datos es más caro que en los niveles de acceso de uso frecuente y esporádico. | Se usa para los datos que pueden tolerar varias horas de latencia de recuperación y que permanecerán en el nivel durante al menos 180 días.

<!--markdownlint-enable MD033 -->

### <a name="storage-account-types"></a>Tipos de cuenta de almacenamiento

Azure proporciona diferentes tipos de cuentas de almacenamiento y niveles de rendimiento.

<!--markdownlint-disable MD033 -->

**Tipo de cuenta** | **Detalles** | **Uso**
--- | --- | ---
**Uso general v2 estándar** | Admite blobs (de bloques, páginas, anexos), archivos, discos, colas y tablas.<br/><br/> Admite los niveles de acceso frecuente, esporádico y archivo. Se admite ZRS. | Se usa para la mayoría de los escenarios y la mayoría de los tipos de datos. Las cuentas de almacenamiento estándar pueden basarse en HDD o en SSD.
**Uso general v2 Prémium** | Admite datos de Blob Storage (blobs en páginas). Admite los niveles de acceso frecuente, esporádico y archivo. Se admite ZRS.<br/><br/> Se almacena en SSD. | Microsoft recomienda usarlo para todas las máquinas virtuales.
**Uso general v1** | No se admiten los niveles de acceso. No admite ZRS. | Se usa si las aplicaciones necesitan el modelo de implementación clásica de Azure.
**Blob** | Es la cuenta de almacenamiento especializada para almacenar los objetos no estructurados. Proporciona los blobs en bloques y solo blobs anexos (ningún servicio de almacenamiento de archivo, cola, tabla o disco). Proporciona la misma durabilidad, disponibilidad, escalabilidad y rendimiento que el uso general v2. | En estas cuentas no se pueden almacenar blobs en páginas y, por lo tanto, no se pueden almacenar archivos de disco duro virtual. Puede establecer un nivel de acceso frecuente o esporádico.

<!--markdownlint-enable MD033 -->

### <a name="storage-redundancy-options"></a>Opciones de redundancia de almacenamiento

Las cuentas de almacenamiento pueden usar diferentes tipos de redundancia para lograr resistencia y alta disponibilidad.

**Tipo** | **Detalles** | **Uso**
--- | --- | ---
**Almacenamiento con redundancia local (LRS)** | Protege contra una interrupción local mediante la replicación dentro de una unidad de almacenamiento individual a un dominio de error y un dominio de actualización independientes. Mantiene varias copias de los datos en un centro de datos. Proporciona al menos una durabilidad de los objetos del 99,999999999 % (11 nueves) durante un año determinado. | Considere si la aplicación almacena datos que se pueden reconstruir fácilmente.
**Almacenamiento con redundancia de zona (ZRS)** | Protege contra una interrupción del centro de datos; para ello, replicar a través de tres clústeres de almacenamiento en una sola región. Cada clúster de almacenamiento está separado físicamente y ubicado en su propia zona de disponibilidad. Proporciona al menos una durabilidad del 99,9999999999 % (12 nueves) de los objetos durante un año determinado manteniendo varias copias de sus datos en varios centros de datos o en regiones diferentes. | Considere si necesita coherencia, durabilidad y alta disponibilidad. Podría no proteger frente a un desastre regional en el que varias zonas resulten afectadas permanentemente.
**Almacenamiento geográficamente redundante (GRS)** | Protege contra una interrupción de toda la región mediante la replicación de los datos en una región secundaria lejos de la réplica principal. Proporciona al menos una durabilidad de los objetos del 99,99999999999999 % (16 nueves) durante un año determinado. | No hay disponibles datos de réplica a menos que Microsoft inicie la conmutación por error para la región secundaria. Si se produce la conmutación por error, el acceso de lectura y de escritura está disponible.
**Almacenamiento con redundancia geográfica con acceso de lectura (RA-GRS)** | Similar a GRS. Proporciona al menos una durabilidad de los objetos del 99,99999999999999 % (16 nueves) durante un año determinado. | Proporciona una disponibilidad de lectura del 99,99 %, ya que permite el acceso de lectura desde la segunda región utilizada para GRS.

**Más información:**

- [Revise](https://azure.microsoft.com/pricing/details/storage) los precios de Azure Storage.
- [Obtenga información sobre](/azure/storage/common/storage-import-export-service) Azure Import/Export para grandes cantidades de migración de datos a los archivos y blobs de Azure.
- [Compare](/azure/storage/common/storage-decide-blobs-files-disks?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) blobs, archivos y tipos de datos de almacenamiento de disco.
- [Obtenga más información](/azure/storage/blobs/storage-blob-storage-tiers) sobre los niveles de acceso.
- [Revise](/azure/storage/common/storage-account-overview?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) los diferentes tipos de cuentas de almacenamiento.
- Obtenga información sobre [redundancia de almacenamiento](/azure/storage/common/storage-redundancy), [LRS](/azure/storage/common/storage-redundancy-lrs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), [ZRS](/azure/storage/common/storage-redundancy-zrs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json), [GRS](/azure/storage/common/storage-redundancy-grs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) y [GRS de solo lectura](/azure/storage/common/storage-redundancy-grs?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#read-access-geo-redundant-storage).
- [Obtenga más información](/azure/storage/files/storage-files-introduction) sobre Azure Files.

## <a name="best-practice-take-advantage-of-azure-hybrid-benefits"></a>Procedimiento recomendado: Aproveche las ventajas de Azure Hybrid

Debido a los años de inversión en software en sistemas como Windows Server y SQL Server, Microsoft se encuentra en una posición única para ofrecer a los clientes valor en la nube, con descuentos considerables que otros proveedores de nubes no necesariamente proporcionan.

La cartera de productos local o de Azure integrada de Microsoft genera ventajas competitivas y en el costo. Si actualmente tiene un sistema operativo u otras licencias de software con el programa de Software Assurance (SA), puede llevarse esas licencias con usted a la nube para aprovechar la Ventaja híbrida de Azure.

**Más información:**

- [Eche un vistazo a](https://azure.microsoft.com/pricing/hybrid-benefit) la Calculadora de ahorro de la Ventaja híbrida de Azure.
- [Obtenga más información](https://azure.microsoft.com/pricing/hybrid-benefit) sobre la Ventaja híbrida de Windows Server.
- [Revise](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) la guía de precios de las máquinas virtuales de Azure de SQL Server.

## <a name="best-practice-use-reserved-vm-instances"></a>Procedimiento recomendado: Uso de instancias reservadas de máquina virtual

La mayoría de las plataformas en la nube se configuran como de pago por uso. Este modelo presenta inconvenientes, dado que no se tiene por qué conocer hasta qué punto variarán las cargas de trabajo. Cuando se especifican intenciones claras para una carga de trabajo, se contribuye al plan de la infraestructura.

Si usa Azure Reserved VM Instances, paga por adelantado su uso durante un plazo de uno a tres años.

- El pago por adelantado proporciona un descuento por los recursos que se utilizan.
- Puede reducir considerablemente los costos de las máquinas virtuales, la capacidad de proceso de SQL Database, Azure Cosmos DB u otros recursos en hasta un 72 % con respecto a los precios de pago por uso.
- Las reservas permiten un descuento en la facturación y no afectan al estado del entorno de ejecución de los recursos.
- Puede cancelar las instancias reservadas.

![Instancias reservadas](./media/migrate-best-practices-costs/reserve.png)
*Azure Reserved VM*

**Más información:**

- [Aprenda más sobre](/azure/billing/billing-save-compute-costs-reservations) Azure Reservations.
- [Lea](https://azure.microsoft.com/pricing/reserved-vm-instances/#faq) las preguntas frecuentes sobre las instancias reservadas.
- [Consulte una orientación de los precios de](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance) las máquinas virtuales de SQL Server Azure.

## <a name="best-practice-aggregate-cloud-spend-across-subscriptions"></a>Procedimiento recomendado: Suma del gasto en la nube entre suscripciones

Resulta inevitable que al final tenga más de una suscripción de Azure. Por ejemplo, puede necesitar una suscripción adicional para separar los límites de desarrollo y producción, o podría tener una plataforma que requiera una suscripción independiente para cada cliente. Tener la capacidad de agregar informes de datos a través de todas las suscripciones en una sola plataforma es una característica valiosa.

Para ello, puede usar las API de Azure Cost Management. A continuación, después de agregar los datos en un único origen, como SQL Azure, puede usar herramientas como Power BI para mostrar los datos agregados. Puede crear informes de suscripción agregados e informes pormenorizados. Por ejemplo, para los usuarios que necesitan información proactiva sobre administración de costos, puede crear vistas específicas de los costos, por departamento, grupo de recursos, etc. No es necesario proporcionarles acceso total a los datos de facturación de Azure.

**Más información:**

- [Obtenga información general sobre](/azure/billing/billing-consumption-api-overview) la API de consumo de Azure.
- [Obtenga información sobre](/power-bi/desktop-connect-azure-consumption-insights) cómo conectarse a Azure Consumption Insights en Power BI Desktop.
- [Aprenda a ](/azure/billing/billing-manage-access) administrar el acceso a la información de facturación de Azure mediante el control de acceso basado en roles (RBAC).

## <a name="after-migration"></a>Después de la migración

Después de una migración correcta de las cargas de trabajo y un par de semanas de recopilar datos de consumo, tendrá una idea clara de los costos que suponen los recursos.

- Cuando analice los datos, podrá empezar a generar una base de referencia de presupuesto para los recursos y los grupos de recursos de Azure.
- A continuación, como ya sabe dónde se gasta su presupuesto en la nube, puede analizar cómo reducir aún más los costos.

Los procedimientos recomendados de esta sección tienen en cuenta el uso de Azure Cost Management para los presupuestos de los costos y el análisis, la supervisión de los recursos y la implementación de presupuestos para los grupos de recursos, así como para la optimización de la supervisión, el almacenamiento y las máquinas virtuales.

## <a name="best-practice-use-azure-cost-management"></a>Procedimiento recomendado: Uso de Azure Cost Management

Microsoft ofrece Azure Cost Management para ayudarle a realizar un seguimiento de los gastos:

- Le ayuda a supervisar y controlar el gasto de Azure y a optimizar el uso de los recursos.
- Revisa la suscripción completa y todos sus recursos, y sugiere recomendaciones.
- Proporciona una API completa para integrar las herramientas externas y los sistemas financieros para los informes.
- Realiza un seguimiento del uso de los recursos y de la administración de los costos en la nube con una sola vista unificada.
- Proporciona información valiosa operativa y financiera para ayudarle a tomar decisiones informadas.

En Cost Management, es posible:

- **Crear un presupuesto**: cree un presupuesto de responsabilidad financiera.
  - Puede tener en cuenta los servicios que consume o suscribirse por un periodo específico (mensual, trimestral o anual) y un ámbito (grupos de recursos o suscripciones). Por ejemplo, puede crear un presupuesto de suscripción de Azure durante un período mensual, trimestral o anual.
    - Después de crear un presupuesto, se muestra en el análisis de costos. Ver el presupuesto con respecto al gasto actual es uno de los primeros pasos necesarios al analizar los costos y los gastos.
  - Pueden enviarse notificaciones por correo electrónico cuando se alcanzan umbrales de presupuesto.
  - Puede exportar datos de administración de costos en Azure Storage, para analizarlos.

    ![Presupuesto de Cost Management](./media/migrate-best-practices-costs/budget.png)
    *Presupuesto de Azure Cost Management*

- **Realizar un análisis de los costos**: obtenga un análisis de los costos para explorar y analizar los gastos de la organización y ayudarle a entender cómo se acumulan, así como identificar las tendencias del gasto.
  - El análisis de costos está disponible para los usuarios del Contrato Enterprise.
  - Puede ver datos del análisis de costos para varios ámbitos, también por departamento, cuenta, suscripción o grupo de recursos.
  - Puede obtener un análisis de costos que muestre los costos totales del mes actual y los acumulados diariamente.

    ![Análisis de Cost Management](./media/migrate-best-practices-costs/analysis.png)
    *Análisis de Azure Cost Management*
- **Obtener recomendaciones:** obtenga recomendaciones de Azure Advisor que le muestran cómo puede optimizar y mejorar la eficacia.

**Más información:**

- [Consulte información general](/azure/cost-management/overview) de Azure Cost Management.
- [Aprenda a](/azure/cost-management/cost-mgt-best-practices) optimizar su inversión en la nube con Azure Cost Management.
- [Aprenda a](/azure/cost-management/use-reports) usar informes de Azure Cost Management.
- [Consulte un tutorial](/azure/cost-management/tutorial-acm-opt-recommendations?toc=/azure/billing/TOC.json) para optimizar costos a partir de las recomendaciones.
- [Revise](/rest/api/consumption/budgets) la API de consumo de Azure.

## <a name="best-practice-monitor-resource-utilization"></a>Procedimiento recomendado: Supervisar la utilización de recursos

En Azure se paga por lo que usa, cuando los recursos se utilizan, y no se paga cuando no se utilizan. En el caso de las máquinas virtuales, la facturación se produce cuando alguna se asigna y no se cobra una vez se desasigna. Teniendo esto en cuenta, debe supervisar las máquinas virtuales que se utilizan así como comprobar su tamaño.

- Evalúe continuamente las cargas de trabajo de las máquinas virtuales para determinar las bases de referencia.
- Por ejemplo, si la carga de trabajo se produce principalmente de lunes a viernes, de 8 a.m. a 6 p.m., pero apenas hay fuera de esas horas, las máquinas virtuales podrían cambiarse a una versión inferior fuera de las horas punta. Esto podría significar cambiar los tamaños de máquina virtual o el uso de conjuntos de escalado de máquinas virtuales para escalarlas de forma automática, ampliándolas o reduciéndolas.
- Algunas compañías "posponen" las máquinas virtuales, para lo cual las colocan en un calendario que especifica cuándo deben estar disponibles y cuándo no son necesarias.
- Además de supervisar las máquinas virtuales, debe supervisar otros recursos de red como ExpressRoute y las puertas de enlace de red para tener en cuenta cuándo se usan demasiado o demasiado poco.
- Para supervisar el uso de las máquinas virtuales, puede emplear herramientas de Microsoft como son Azure Cost Management, Azure Monitor y Azure Advisor. También hay disponibles herramientas de terceros.

**Más información:**

- Obtenga información general de [Azure Monitor](/azure/azure-monitor/overview) y [Azure Advisor](/azure/advisor/advisor-overview).
- [Consulte](/azure/advisor/advisor-cost-recommendations) recomendaciones sobre el costo de Azure Advisor.
- [Obtenga información sobre cómo [optimizar los costos a partir de las recomendaciones](/azure/cost-management/tutorial-acm-opt-recommendations?toc=/azure/billing/TOC.json) y [evitar cargos imprevistos](/azure/billing/billing-getting-started).
- Obtenga información sobre el [Kit de herramientas Azure Resource Optimization (ARO)](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

## <a name="best-practice-implement-resource-group-budgets"></a>Procedimiento recomendado: Implementar presupuestos para los grupos de recursos

A menudo, se usan grupos de recursos para representar límites de costos. Junto con este patrón de uso, el equipo de Azure sigue desarrollando formas nuevas y mejoradas de seguimiento y análisis de gastos a diferentes niveles, lo que incluye la capacidad de crear presupuestos con el grupo de recursos y con los recursos.

- Un presupuesto para un grupo de recursos le ayuda a realizar un seguimiento de los costos asociados al mismo.
- Puede desencadenar alertas y ejecutar una amplia variedad de cuadernos de estrategias a medida que el presupuesto se alcanza o se supera.

**Más información:**

- [Aprenda a](/azure/billing/billing-cost-management-budget-scenario) administrar los costos con la API de presupuestos de Azure.
- [Siga un tutorial](/azure/cost-management/tutorial-acm-create-budgets?toc=/azure/billing/TOC.json) para crear y administrar un presupuesto de Azure.

## <a name="best-practice-optimize-azure-monitor-retention"></a>Procedimiento recomendado: Optimizar la retención de Azure Monitor

A medida que mueve recursos a Azure y habilita el registro de diagnóstico para ellos, se genera una gran cantidad de datos de registro. Normalmente, estos datos de registro se envían a una cuenta de almacenamiento que se asigna a un área de trabajo de Log Analytics.

- Cuanto mayor sea el período de retención de los datos de registro, más datos tendrá.
- No todos los datos de registro son iguales y algunos recursos generarán más datos de registro que otros.
- Debido a cuestiones relativas a la normativa y al cumplimiento, es probable que deba conservar los datos de registro para algunos recursos más tiempo que para otros.
- Debe delimitar con cuidado la estrategia para optimizar los costos de almacenamiento de registro frente a mantener los datos de registro que necesita.
- Se recomienda evaluar y configurar el registro inmediatamente después de completar una migración, de modo que no invierta dinero en conservar registros sin importancia.

**Más información:**

- [Aprenda acerca de cómo](/azure/monitoring-and-diagnostics/monitoring-usage-and-estimated-costs) supervisar el uso y los costos previstos.

## <a name="best-practice-optimize-storage"></a>Procedimiento recomendado: Optimizar el almacenamiento

Si ha seguido los procedimientos recomendados para la selección de almacenamiento antes de la migración, probablemente esté disfrutando de algunas ventajas. Sin embargo, hay costos de almacenamiento adicionales que probablemente todavía se puedan optimizar. Con el tiempo, los blobs y archivos se vuelven obsoletos. Los datos podrían dejar de usarse, pero los requisitos normativos podrían implicar que tenga que conservarlos durante un período determinado. Por lo tanto, es posible que no necesite almacenarlos en el almacenamiento de alto rendimiento que usa para la migración original.

Identificar y mover los datos obsoletos a áreas de almacenamiento más económicas puede tener un efecto enorme en el presupuesto mensual de almacenamiento y en el ahorro en los costos. Azure ofrece muchas maneras para ayudarle a identificar y, a continuación, almacenar estos datos obsoletos.

- Aproveche las ventajas de los niveles de acceso para el almacenamiento de uso general v2, pasando los datos menos importantes del nivel de acceso frecuente a los niveles esporádico y de archivo.
- Use StorSimple para ayudar a mover los datos obsoletos en función de directivas personalizadas.

**Más información:**

- [Obtenga más información](/azure/storage/blobs/storage-blob-storage-tiers) sobre los niveles de acceso.
- [Obtenga información general sobre](/azure/azure-monitor/overview) StorSimple y sobre los [precios de StorSimple](https://azure.microsoft.com/pricing/details/storsimple).

## <a name="best-practice-automate-vm-optimization"></a>Procedimiento recomendado: Automatizar la optimización de las máquinas virtuales

El objetivo final de ejecutar una máquina virtual en la nube es maximizar la CPU, la memoria y el disco que utiliza. Si detecta que las máquinas virtuales no están optimizadas o hay con frecuencia períodos en los que no se utilizan, tiene sentido apagarlas o disminuir su nivel mediante conjuntos de escalado de máquinas virtuales.

Puede optimizar una máquina virtual con Azure Automation, conjuntos de escalas de máquinas virtuales, apagado automático y soluciones de terceros o con script.

**Más información:**

- [Obtenga información sobre cómo](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-vertical-scale-reprovision) usar la escalabilidad automática vertical.
- [Programe](https://azure.microsoft.com/updates/azure-devtest-labs-schedule-vm-auto-start) el inicio automático de una máquina virtual.
- [Aprenda a](/azure/automation/automation-solution-vm-management) iniciar o detener las máquinas virtuales fuera del horario laboral en Azure Automation.
- [Obtener más información] sobre [Azure Advisor](/azure/advisor/advisor-overview) y el [Kit de herramientas Azure Resource Optimization (ARO)](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

## <a name="best-practices-use-logic-apps-and-runbooks-with-budgets-api"></a>Procedimientos recomendados: Usar Runbooks y Logic Apps con la API de presupuestos

Azure proporciona una API REST que tiene acceso a la información de facturación del inquilino.

- Puede usar la API de presupuestos para integrar los sistemas externos y los flujos de trabajo que las métricas construidas a partir de los datos de la API desencadenen.
- Puede extraer datos de uso y de recursos, e incorporarlos en las herramientas de análisis de datos de su preferencia.
- Las API de RateCard y de uso de recursos de Azure pueden ayudarlo a predecir y administrar los costos de forma precisa.
- Las API se implementan como un proveedor de recursos y se incluyen entre las que Azure Resource Manager expone.
- La API de presupuestos pueden integrarse con Azure Logic Apps y los Runbooks.

**Más información:**

- [Más información acerca de](/rest/api/consumption/budgets) la API de presupuestos.
- [Obtenga información](/azure/billing/billing-usage-rate-card-overview) sobre el uso de Azure con la API de facturación.

## <a name="best-practice-implement-serverless-technologies"></a>Procedimiento recomendado: Implementar tecnologías sin servidor

A menudo, las cargas de trabajo de máquina virtual se migran "tal cual" para evitar tiempos de inactividad. Con frecuencia, pueden hospedar tareas intermitentes, que tardan poco en ejecutarse o a veces muchas horas. Por ejemplo, las máquinas virtuales que ejecutan tareas programadas, como las del programador de tareas de Windows o los scripts de PowerShell. Sin embargo, cuando estas tareas no se están ejecutando, está incurriendo en gastos por la máquina virtual y el almacenamiento en disco.

Tras la migración y después de una revisión exhaustiva de estos tipos de tareas, puede considerar migrarlas a tecnologías sin servidor, como son los trabajos de Azure Functions o Azure Batch. Con esta solución, ya no necesita administrar o mantener las máquinas virtuales, lo que supone un ahorro adicional en el costo.

**Más información:**

- Más información sobre [Azure Functions](https://azure.microsoft.com/services/functions).
- Más información sobre [Azure Batch](https://azure.microsoft.com/services/batch).

## <a name="next-steps"></a>Pasos siguientes

Examine otros procedimientos recomendados:

- [Procedimientos recomendados](migrate-best-practices-security-management.md) para la seguridad y administración después de la migración.
- [Procedimientos recomendados](migrate-best-practices-networking.md) para las redes después de la migración.
