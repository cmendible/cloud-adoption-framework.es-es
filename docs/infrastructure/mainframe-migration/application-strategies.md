---
title: 'Migración del sistema central: Migración de aplicaciones del sistema central'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migre aplicaciones desde entornos del sistema central a Azure, una infraestructura que se ha probado de alta disponibilidad y escalable para los sistemas que se ejecutan actualmente en sistemas centrales.
author: njray
ms.author: v-nanra
ms.date: 12/26/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 39b52cc79041a5d4df445c416ae7bf8cb8c14879
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70906328"
---
# <a name="mainframe-application-migration"></a>Migración de aplicaciones del sistema central

Al migrar aplicaciones de entornos de sistema central a Azure, la mayoría de los equipos siguen un enfoque pragmático: reutilizar siempre que sea posible y, después, iniciar una implementación por fases en la que las aplicaciones se reescriben o se reemplazan.

Normalmente, la migración de aplicaciones implica una o varias de las estrategias siguientes:

- **Rehospedaje:** puede trasladar el código, los programas y las aplicaciones existentes desde el sistema central y, después, recompilar el código que se ejecutará en un emulador de sistema central hospedado en una instancia de la nube. Normalmente, este enfoque comienza con el traslado de las aplicaciones a un emulador basado en la nube y, después, se migra la base de datos a una base de datos en la nube. Hay que hacer algunos trabajos de ingeniería y refactorización, además de las conversiones de datos y archivos.

    Como alternativa, puede rehospedar mediante un proveedor de hospedaje tradicional. Una de las principales ventajas de la nube es la subcontratación de la administración de la infraestructura. Puede encontrar un proveedor de centro de datos que hospede sus cargas de trabajo de sistema central. Este modelo puede darle algo de tiempo, reducir el bloqueo de los proveedores y producir un ahorro de los costos intermedios.

- **Retirada:** todas las aplicaciones que ya no son necesarias deberán retirarse antes de la migración.

- **Recompilación:** algunas organizaciones deciden volver a escribir los programas usando técnicas modernas. Dado el costo adicional y la complejidad de este enfoque, no es tan común como una migración mediante "lift-and-shift". Después de este tipo de migración, suele ser conveniente reemplazar los módulos y el código mediante motores de transformación de código.

- **Reemplazo:** este método reemplaza la funcionalidad del sistema central por las características en la nube equivalentes. El software como servicio (SaaS) es una opción, que consiste en usar una solución creada específicamente para abordar una cuestión empresarial; por ejemplo, finanzas, recursos humanos, producción o planeamiento de recursos empresariales. Además, ahora hay disponibles muchas aplicaciones específicas del sector para resolver los problemas que antes solían corregir las soluciones de sistema central personalizadas.

Plantéese comenzar con el planeamiento de las cargas de trabajo que desea migrar inicialmente y, después, determine los requisitos para trasladar las aplicaciones, las bases de código heredado y las bases de datos asociados.

## <a name="mainframe-emulation-in-azure"></a>Emulación de sistema central en Azure

Azure Cloud Services puede emular entornos de sistema central tradicionales, lo que le permite reutilizar las aplicaciones y el código existentes en el sistema central. Los componentes de servidor habituales que puede emular son procesamiento de transacciones en línea (OLTP), lotes y sistemas de ingesta de datos.

### <a name="oltp-systems"></a>Sistemas OLTP

Muchos sistemas centrales tienen sistemas OLTP que procesan miles o millones de actualizaciones para una cantidad inmensa de usuarios. Con frecuencia, estas aplicaciones usan software de procesamiento de transacciones, entrada de formularios y control de la pantalla, como los sistemas de control de información del cliente (CICS), sistemas de administración de la información (IMS) y procesadores de interfaz de terminal (TIP).

Al trasladar las aplicaciones de OLTP a Azure, hay disponibles emuladores de supervisión de procesamiento de transacciones (TP) de sistema central que se ejecutan como infraestructura como servicio (IaaS) con máquinas virtuales en Azure. Los servidores web también pueden implementar funcionalidades de control de la pantalla y entrada de formularios. Este enfoque puede combinarse con API de base de datos, como objetos de datos ActiveX (ADO), conectividad abierta de base de datos (ODBC) y conectividad de base de datos de Java (JDBC) para las transacciones y el acceso a los datos.

### <a name="time-constrained-batch-updates"></a>Actualizaciones por lotes con restricciones de tiempo

Muchos sistemas centrales realizan actualizaciones mensuales o anuales de millones de registros de cuentas, por ejemplo, las que se utilizan en banca, seguros y administraciones públicas. Los sistemas centrales pueden trabajar con estos tipos de cargas de trabajo mediante sistemas de control de datos con alta capacidad de procesamiento. Por su diseño, los trabajos por lotes de los sistemas centrales suelen procesarse en serie y su rendimiento depende de las operaciones de entrada y salida por segundo (IOPS) que proporcione la red troncal del sistema central.

Los entornos de procesamiento por lotes en la nube usan recursos de proceso en paralelo y redes de alta velocidad para obtener un mayor rendimiento. Si necesita optimizar el rendimiento del procesamiento por lotes, Azure dispone de varias opciones de red, almacenamiento y proceso.

### <a name="data-ingestion-systems"></a>Sistemas de ingesta de datos

Los sistemas centrales ingieren grandes lotes de datos de soluciones de venta minorista, servicios financieros y fabricación, entre otras, para su procesamiento. Con Azure, puede usar las utilidades de línea de comandos tales como [AzCopy](/azure/storage/common/storage-use-azcopy) para copiar los datos hacia y desde la ubicación de almacenamiento. También puede usar el servicio [Azure Data Factory](/azure/data-factory/introduction), que permite ingerir datos de distintos almacenes de datos para crear y programar flujos de trabajo basados en datos.

Además de los entornos de emulación, Azure proporciona servicios de análisis y de plataforma como servicio (PaaS) que pueden mejorar los entornos de sistema central existentes.

## <a name="migrate-oltp-workloads-to-azure"></a>Migración de cargas de trabajo OLTP a Azure

La migración mediante "lift-and-shift" permite migrar rápidamente las aplicaciones existentes a Azure sin tener que codificar. Cada aplicación se migra tal cual, lo que ofrece las ventajas de la nube sin el riesgo ni los costos que conlleva la modificación del código. Este enfoque es compatible con el uso de un emulador de supervisión de procesamiento de transacciones (TP) de sistema central en Azure.

Hay disponibles monitores de procesamiento de transacciones de varios proveedores que se ejecutan en máquinas virtuales, una opción de infraestructura como servicio (IaaS) de Azure. Los siguientes diagramas de antes y después muestran la migración de una aplicación en línea basada en IBM DB2, un sistema de administración de bases de datos relacionales (DBMS), en un sistema central IBM z/OS. DB2 para z/OS usa archivos de método de acceso a almacenamiento virtual (VSAM) para almacenar los datos, y el método de acceso secuencial indexado (ISAM) para archivos planos. Esta arquitectura también utiliza CICS para la supervisión de transacciones.

![Migración mediante "lift-and-shift" de un entorno de sistema central a Azure con software de emulación](../../_images/mainframe-migration/mainframe-vs-azure.png)

En Azure, se usan entornos de emulación para ejecutar el administrador de TP y los trabajos por lotes que usan JCL. En la capa de datos, DB2 se reemplaza por [Azure SQL Database](/azure/sql-database/sql-database-technical-overview), aunque también se puede usar Microsoft SQL Server, DB2 LUW u Oracle Database. Un emulador admite IMS, VSAM y SEQ. Las herramientas de administración del sistema central se reemplazan por los servicios de Azure, y software de otros proveedores, que se ejecutan en máquinas virtuales.

La funcionalidad de entrada de formularios y tratamiento de la pantalla normalmente se implementa mediante servidores web, que se pueden combinar con API de base de datos tales como ADO, ODBC y JDBC para el acceso a los datos y las transacciones. La gama exacta de componentes de IaaS de Azure que usará dependerá del sistema operativo que prefiera. Por ejemplo:

- Máquinas virtuales basadas en Windows: Internet Information Server (IIS) junto con ASP.NET para el control de la pantalla y la lógica empresarial. Use ADO.NET para las transacciones y el acceso a los datos.

- Máquinas virtuales basadas en Linux: los servidores de aplicaciones basadas en Java que hay disponibles, como Apache Tomcat para el control de la pantalla y la funcionalidad empresarial basada en Java. Use JDBC para las transacciones y el acceso a los datos.

## <a name="migrate-batch-workloads-to-azure"></a>Migración de cargas de trabajo por lotes a Azure

En Azure, las operaciones por lotes difieren del entorno típico de procesamiento por lotes de los sistemas centrales. Por su diseño, los trabajos por lotes de los sistemas centrales suelen procesarse en serie y su rendimiento depende del valor de IOPS que proporcione la red troncal del sistema central. Los entornos de procesamiento por lotes en la nube usan recursos de proceso en paralelo y redes de alta velocidad para obtener un mayor rendimiento.

Para optimizar el rendimiento del procesamiento por lotes con Azure, considere las siguientes opciones de [proceso](/azure/virtual-machines/windows/overview), [almacenamiento](/azure/storage/blobs/storage-blobs-introduction), [red](https://azure.microsoft.com/blog/maximize-your-vm-s-performance-with-accelerated-networking-now-generally-available-for-both-windows-and-linux) y [supervisión](/azure/azure-monitor/overview).

### <a name="compute"></a>Proceso

Uso:

- Máquinas virtuales con la mayor velocidad de reloj. Las aplicaciones del sistema central suelen ser de un único subproceso y las CPU de los sistemas centrales tienen una velocidad de reloj muy alta.

- Máquinas virtuales con gran capacidad de memoria para permitir el almacenamiento en caché de los datos y las áreas de trabajo de las aplicaciones.

- Máquinas virtuales con CPU virtuales de mayor densidad para aprovechar las ventajas del procesamiento multiproceso si la aplicación lo admite.

- Procesamiento paralelo, porque Azure se escala horizontalmente para el procesamiento paralelo y ofrece más capacidad de proceso para una ejecución por lotes.

### <a name="storage"></a>Storage

Uso:

- [SSD Premium de Azure ](/azure/virtual-machines/windows/premium-storage) o [SSD Ultra de Azure](/azure/virtual-machines/windows/disks-ultra-ssd) para tener el número máximo de IOPS disponible.

- Creación de particiones con varios discos para tener más E/S por segundo en cada tamaño de almacenamiento.

- Creación de particiones de almacenamiento, para distribuir la E/S entre varios dispositivos de almacenamiento de Azure.

### <a name="networking"></a>Redes

- Use [Azure Accelerated Networking](/azure/virtual-network/create-vm-accelerated-networking-powershell) para minimizar la latencia.

### <a name="monitoring"></a>Supervisión

- El uso de herramientas de supervisión, [Azure Monitor](/azure/azure-monitor/overview), [Azure Application Insights](/azure/application-insights/app-insights-overview) e incluso los registros de Azure permite a los administradores supervisar cualquiera el rendimiento de las ejecuciones por lotes y ayudar a eliminar los cuellos de botella.

## <a name="migrate-development-environments"></a>Migración de entornos de desarrollo

Las arquitecturas de nube distribuidas se basan en un conjunto de herramientas de desarrollo diferente que aportan las ventajas que ofrecen los procedimientos y lenguajes de programación modernos. Para facilitar esta transición, puede usar un entorno de desarrollo con otras herramientas que estén diseñadas para emular los entornos de IBM z/OS. La siguiente lista muestra las opciones de Microsoft y otros proveedores:

| Componente        | Opciones de Azure                                                                                                                                  |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| z/OS             | Windows, Linux o UNIX                                                                                                                      |
| CICS             | Servicios de Azure ofrecidos por Micro Focus, Oracle, GT Software (Fujitsu), TmaxSoft, Raincode y NTT Data, o reescribir con Kubernetes |
| IMS              | Servicios de Azure ofrecidos por Micro Focus y Oracle                                                                                  |
| Assembler        | Servicios de Azure ofrecidos por Raincode y TmaxSoft; o COBOL, C o Java; o asignación a las funciones del sistema operativo               |
| JCL              | JCL, PowerShell u otras herramientas de scripting                                                                                                   |
| COBOL            | COBOL, C o Java                                                                                                                            |
| Natural          | Natural, COBOL, C o Java                                                                                                                  |
| FORTRAN y PL/I | FORTRAN, PL/I, COBOL, C o Java                                                                                                           |
| REXX y PL/I    | REXX, PowerShell u otras herramientas de scripting                                                                                                  |

## <a name="migrate-databases-and-data"></a>Migración de bases de datos y datos

Normalmente, la migración de aplicaciones implica el rehospedaje de la capa de datos. Migre las bases de datos de SQL Server, de código abierto y otras bases de datos relacionales a soluciones de Azure totalmente administradas, como [Instancia administrada de Azure SQL Database](/azure/sql-database/sql-database-managed-instance), [Azure Database for PostgreSQL](/azure/postgresql/overview) y [Azure Database for MySQL](/azure/mysql/overview) con [Azure Database Migration Service](/azure/dms/dms-overview).

Por ejemplo, puede migrar si la capa de datos del sistema central usa:

- IBM DB2 o una base de datos IMS; use Azure SQL Database, SQL Server, DB2 LUW u Oracle Database en Azure.

- VSAM y otros archivos sin formato; use archivos planos de método de acceso secuencial indexado (ISAM) para Azure SQL, SQL Server, DB2 LUW u Oracle.

- Grupos de fechas de generación (GDG); migre a archivos de Azure que usen una convención de nomenclatura y extensiones de nombre de archivo que proporcionen una funcionalidad similar a los GDG.

La capa de datos de IBM incluye varios componentes clave que se deben migrar también. Por ejemplo, al migrar una base de datos, migre también una colección de los datos contenidos en grupos, cada uno de los cuales contiene dbextents, que son conjuntos de datos VSAM de z/OS. La migración debe incluir el directorio que identifica las ubicaciones de los datos en los grupos de almacenamiento. Además, el plan de migración debe tener en cuenta el registro de base de datos, que contiene un registro de las operaciones realizadas en la base de datos. Una base de datos puede tener uno, dos (doble o alternativo) o cuatro (dobles y alternativos) registros.

La migración de la base de datos también incluye los siguientes componentes:

- **Administrador de base de datos:** proporciona acceso a los datos de la base de datos. El administrador de base de datos se ejecuta en su propia partición en un entorno de z/OS.
- **Solicitante de aplicaciones:** acepta las solicitudes de aplicaciones antes de pasarlas a un servidor de aplicaciones.
- **Adaptador de recursos en línea:** incluye componentes de solicitante de aplicaciones para su uso en transacciones CICS.
- **Adaptador de recursos de procesamiento por lotes:** implementa componentes de solicitante de aplicaciones para aplicaciones de procesamiento por lotes en z/OS.
- **SQL interactivo (ISQL):** se ejecuta como una aplicación e interfaz CICS que permite a los usuarios para escribir instrucciones SQL o comandos de operador.
- **Aplicación CICS:** se ejecuta bajo el control de CICS, y usa los orígenes de datos y los recursos disponibles en CICS.
- **Aplicación de procesamiento por lotes:** ejecuta lógica de proceso sin comunicación interactiva con los usuarios, por ejemplo, crear actualizaciones masivas de datos o generar informes de una base de datos.

## <a name="optimize-scale-and-throughput-for-azure"></a>Optimización de la escala y la capacidad de proceso de Azure

Por lo general, los sistemas centrales se escalan verticalmente, mientras que la nube se escala horizontalmente. Para optimizar la escala y la capacidad de proceso de las aplicaciones del estilo de sistema central que se ejecutan en Azure, es importante que comprenda cómo los sistemas centrales separan y aíslan las aplicaciones. Un sistema central z/OS usa una característica llamada particiones lógicas (LPARS) para aislar y administrar los recursos para una aplicación específica en una sola instancia.

Por ejemplo, un sistema central podría usar una partición lógica (LPAR) para una región CICS con programas COBOL asociados y una LPAR separada para DB2. A menudo se usan LPAR diferentes para los entornos de desarrollo, pruebas y ensayo.

En Azure, es más habitual utilizar máquinas virtuales independientes con este propósito. Normalmente, las arquitecturas de Azure implementan máquinas virtuales para la capa de aplicación, un conjunto independiente de máquinas virtuales para la capa de datos, otro conjunto para el desarrollo, y así sucesivamente. Cada nivel de procesamiento se puede optimizar con el tipo de máquinas virtuales y las características más apropiados para ese entorno.

Además, cada nivel también puede proporcionar también los servicios de recuperación ante desastres adecuados. Por ejemplo, las máquinas virtuales de producción y base de datos pueden requerir una recuperación activa o semiactiva, mientras que las máquinas virtuales de desarrollo y pruebas permiten una recuperación pasiva.

En la siguiente ilustración se muestra una posible implementación de Azure con un sitio principal y uno secundario. En el sitio principal, las máquinas virtuales de producción, almacenamiento provisional y pruebas se implementan con alta disponibilidad. El sitio secundario es para recuperación ante desastres y copia de seguridad.

![Posible implementación de Azure con un sitio principal y uno secundario](../../_images/mainframe-migration/migration-backup-DR.png)

## <a name="perform-a-staged-mainframe-to-azure"></a>Migración preconfigurada de un sistema central a Azure

Trasladar las soluciones de un sistema central a Azure puede requerir una migración *preconfigurada*. En ella, se trasladan primero algunas aplicaciones y las demás se quedan en el sistema central de forma temporal o permanente. Normalmente, este enfoque requiere sistemas que permitan que las aplicaciones y las bases de datos interactúen entre el sistema central y Azure.

Un escenario común es trasladar una aplicación a Azure y mantener en el sistema central los datos que la aplicación utiliza. Se utiliza un software específico para que las aplicaciones que se encuentran en Azure puedan acceder a los datos del sistema central. Afortunadamente, existe una amplia gama de soluciones que proporcionan la integración entre Azure y los entornos de sistema central existentes, compatibilidad con escenarios híbridos y migración con el tiempo. Los partners de Microsoft, proveedores de software independientes e integradores pueden ayudarle en camino.

Una opción es [Microsoft Host Integration Server](/host-integration-server), una solución que proporciona la arquitectura distribuida de bases de datos relacionales (DRDA) necesaria para que las aplicaciones que se encuentran en Azure puedan acceder a los datos de DB2 que permanecen en el sistema central. Otras opciones para la integración entre el sistema central y Azure son algunas soluciones de IBM, Attunity, Codit u otros proveedores, y opciones de código abierto.

## <a name="partner-solutions"></a>Soluciones de socios

Si se está planteando migrar un sistema central, el ecosistema de asociados está disponible para ayudarlo.

Azure es una infraestructura probada que ofrece alta disponibilidad y escalabilidad para los sistemas que actualmente se ejecutan en sistemas centrales. Algunas cargas de trabajo se pueden migrar con relativa facilidad. Otras cargas de trabajo que dependen de software del sistema heredado, como CICS e IMS, pueden rehospedarse con las soluciones de los asociados y migrarse a Azure con el tiempo. Independientemente de la opción que elija, Microsoft y nuestros asociados están a su disposición para ayudarlo a optimizar su implementación en Azure, manteniendo la funcionalidad del software en el sistema central.

## <a name="learn-more"></a>Más información

Para obtener más información, consulte los siguientes recursos:

- [Comience a usar Azure](/azure)

- [Implementación de IBM DB2 pureScale en Azure](https://azure.microsoft.com/resources/deploy-ibm-db2-purescale-on-azure)

- [Documentación de Host Integration Server](/host-integration-server)
