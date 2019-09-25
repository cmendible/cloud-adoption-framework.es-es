---
title: 'Migración del sistema central: Realizar el cambio desde sistemas centrales a Azure'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migrar aplicaciones de entornos del sistema central a Azure para sistemas que se ejecutan actualmente en sistemas centrales.
author: njray
ms.author: v-nanra
ms.date: 12/26/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 8416abd3429a0dafd50eda91323eb74bfb1bf9cd
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221528"
---
# <a name="make-the-switch-from-mainframes-to-azure"></a>Realizar el cambio desde sistemas centrales a Azure

Como plataforma alternativa para ejecutar aplicaciones de sistemas centrales tradicionales, Azure ofrece un proceso y el almacenamiento en hiperescala de un entorno de alta disponibilidad. Obtenga el valor y la agilidad de una plataforma moderna basada en la nube sin los costos asociados a un entorno de sistema central.

En esta sección se proporciona orientación técnica para hacer el cambio desde una plataforma de sistema central a Azure.

![Sistema central y Azure](../../_images/mainframe-migration/make-the-switch.png)

## <a name="mips-vs-vcpus"></a>MIPS vs. vCPU

No existe una fórmula de asignación universal para determinar la cantidad de unidades centrales de procesamiento virtual (vCPU) necesarias para ejecutar las cargas de trabajo del sistema central. Sin embargo, la métrica de un millón de instrucciones por segundo (MIPS) a menudo se asigna a las vCPU en Azure. El valor de MIPS mide la potencia del proceso global de un sistema central, y proporciona un valor constante del número de ciclos por segundo de una máquina determinada.

Una organización pequeña puede requerir menos de 500 MIPS, mientras que una organización grande generalmente usa más de 5.000 MIPS. A 1000 USD por cada MIPS, una organización grande gasta aproximadamente 5 millones de USD al año para implementar una infraestructura de 5.000 MIPS. El costo anual estimado para una implementación típica de Azure de esta escala es aproximadamente una décima parte del costo de una infraestructura MIPS. Para obtener más información, consulte la Tabla 4 en las notas del producto [Demystifying Mainframe-to-Azure Migration](https://azure.microsoft.com/resources/demystifying-mainframe-to-azure-migration) (Desmitificar la migración del sistema central a Azure).

Un cálculo preciso de MIPS a vCPU con Azure depende del tipo de vCPU y la carga de trabajo exacta que está ejecutando. Sin embargo, los estudios del banco de pruebas proporcionan una buena base para estimar la cantidad y el tipo de vCPU que necesitará. Un reciente estudio de banco HPE zREF proporciona las siguientes estimaciones:

- 288 MIPS por núcleo basado en Intel que se ejecuta en servidores de HP Proliant para trabajos en línea (CICS).

- 170 MIPS por núcleo Intel para trabajos por lotes COBOL.

En esta guía se calculan 200 MIPS por vCPU para realizar el procesamiento en línea y 100 MIPS por vCPU para realizar el procesamiento por lotes.

> [!NOTE]
> Estas estimaciones pueden cambiar a medida que la nueva serie de máquinas virtuales (VM) esté disponible en Azure.

## <a name="high-availability-and-failover"></a>Alta disponibilidad y conmutación por error

Los sistemas centrales a menudo ofrecen cinco 9s de disponibilidad (99.999 por ciento) cuando se usan el acoplamiento de sistemas centrales y el Sysplex Paralelo. Sin embargo, los operadores de sistemas aún deben programar el tiempo de inactividad del mantenimiento y las cargas iniciales del programa (IPL). La disponibilidad real se acerca a dos o tres 9s, a la par con los servidores de gama alta, basados en Intel.

En comparación, Azure ofrece Acuerdos de Nivel de Servicio (SLA) basados en el compromiso, donde la disponibilidad de varios 9s es el valor predeterminado y está optimizada con la replicación de servicios locales o basados en información geográfica.

Azure proporciona disponibilidad adicional al replicar datos de varios dispositivos de almacenamiento, ya sea localmente o en otras regiones geográficas. Si se produce un error basado en Azure, los recursos del proceso pueden obtener acceso a los datos replicados a nivel regional o local.

Cuando usa la plataforma de Azure como recurso de un servicio (PaaS), como [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) y la [base de datos de Azure Cosmos](https://docs.microsoft.com/azure/cosmos-db/introduction), Azure puede administrar automáticamente las conmutaciones por error. Cuando se usa la infraestructura de Azure como servicio (IaaS), la conmutación por error se basa en las funciones específicas del sistema, como las características Always On de SQL Server, las instancias de clústeres de conmutación por error y los grupos de disponibilidad.

## <a name="scalability"></a>Escalabilidad

Los sistemas centrales suelen escalarse verticalmente, mientras que los entornos de nube se escalan horizontalmente. Los sistemas centrales también pueden escalarse horizontalmente si usan una instalación de acoplamiento (CF), pero debido a los elevados costos que conllevan el hardware y el almacenamiento, resulta caro escalarlos horizontalmente.

Una instalación de acoplamiento también ofrece un proceso estrechamente acoplado, mientras que las características de escalamiento horizontal de Azure están acopladas débilmente. La nube puede escalarse verticalmente u horizontalmente para que coincida con las especificaciones exactas del usuario, con la potencia del proceso, el almacenamiento y los servicios que se escalan a petición según un modelo de facturación basado en el uso.

## <a name="backup-and-recovery"></a>Copia de seguridad y recuperación

Los clientes del sistema central generalmente mantienen sitios de recuperación ante desastres o hacen uso de un proveedor de sistemas centrales independiente para hacer frente a situaciones de desastre. La sincronización con un sitio de recuperación ante desastres generalmente se realiza a través de copias de datos sin conexión. Ambas opciones conllevan costos elevados.

La redundancia geográfica automatizada también está disponible a través del servicio de acoplamiento del sistema central, aunque conlleva un gran costo y, generalmente, está reservada para sistemas críticos. En cambio, Azure tiene opciones fáciles de implementar y muy rentables para realizar la [copia de seguridad](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup), la [recuperación](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) y la [redundancia](https://docs.microsoft.com/azure/storage/common/storage-redundancy) a nivel local o regional, o por medio de la redundancia geográfica.

## <a name="storage"></a>Storage

Para comprender cómo funcionan los sistemas centrales, debe descodificar varios términos que se superponen. Por ejemplo, el almacenamiento central, la memoria real, el almacenamiento real y el almacenamiento principal generalmente se refieren al almacenamiento conectado directamente al procesador del sistema central.

El hardware del sistema central incluye procesadores y otros dispositivos, como dispositivos de almacenamiento de acceso directo (DASD), unidades de cinta magnética y varios tipos de consolas de usuario. Los programas de usuario usan las cintas y los DASD en las funciones del sistema.

Los tipos de almacenamiento físico para sistemas centrales incluyen:

- **Almacenamiento central**: ubicado directamente en el procesador del sistema central, también se conoce como procesador o almacenamiento real.
- **Almacenamiento auxiliar**: está separado del sistema central; este tipo incluye el almacenamiento en DASD y también se conoce como almacenamiento de paginación.

La nube ofrece una gama de opciones flexibles y escalables, y solo deberá pagar las opciones que necesite. [Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-introduction) ofrece un almacén de objetos que se puede escalar de forma masiva destinado a objetos de datos, un servicio de sistema de archivos para la nube, un almacén de mensajería para mensajería confiable y un almacén NoSQL. En cuanto a las máquinas virtuales, los discos administrados y no administrados proporcionan un almacenamiento de disco persistente y seguro.

## <a name="mainframe-development-and-testing"></a>Desarrollo y pruebas del sistema central

Un factor importante de los proyectos de migración del sistema central es la evolución del desarrollo de aplicaciones. Las organizaciones quieren que su entorno de desarrollo sea más ágil y pueda responder rápidamente a las necesidades comerciales.

Los sistemas centrales suelen tener particiones lógicas separadas (LPAR) para realizar el desarrollo y las pruebas, como el control de calidad y las LPAR de almacenamiento provisional. Las soluciones de desarrollo del sistema central incluyen compiladores (COBOL, PL/I, Assembler) y editores. El más común es el conjunto de herramientas Interactive System Productivity Facility (ISPF) para el sistema operativo z/OS que se ejecuta en los sistemas centrales de IBM. Otros incluyen las herramientas ROSCOE Programming Facility (RPF) y Computer Associates, como CA Librarian y CA-Panvalet.

Igualmente, los entornos de emulación y los compiladores están disponibles en plataformas x86, por lo que el desarrollo y las pruebas suelen estar entre las primeras cargas de trabajo que se usan para migrar de un sistema central a Azure. La disponibilidad y el uso generalizado de las [herramientas de DevOps en Azure](https://azure.microsoft.com/solutions/devops) está acelerando la migración de los entornos de desarrollo y prueba.

Cuando las soluciones se desarrollen y se prueben en Azure y estén listas para su implementación en el sistema central, deberá copiar el código en el sistema central y compilarlo allí.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Migrar la aplicación del sistema central](./application-strategies.md)
