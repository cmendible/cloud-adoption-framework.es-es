---
title: Evaluación de la disponibilidad de las cargas de trabajo
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Un proceso de la migración a la nube que se centra en las tareas de migración de cargas de trabajo.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 186aa4d4dc5218e2166e7dfb4c9834917e647a02
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024660"
---
# <a name="evaluate-workload-readiness"></a>Evaluación de la disponibilidad de las cargas de trabajo

Esta actividad se centra en evaluar la disponibilidad de una carga de trabajo para migrar a la nube. Durante esta actividad, el equipo de adopción de la nube valida que todos los recursos y las dependencias asociadas sean compatibles con el modelo de implementación y el proveedor de nube elegidos. Durante el proceso, el equipo documenta los esfuerzos necesarios para [corregir](../migrate/remediate.md) los problemas de compatibilidad.

## <a name="evaluation-assumptions"></a>Suposiciones de evaluación

La mayor parte del contenido que describe los principios de la Plataforma de adopción de la nube está diseñada para no depender de la nube. Sin embargo, el proceso de evaluación de la disponibilidad debe ser muy específico para cada plataforma de nube específica. En la siguiente guía se presupone una intención de migrar a Azure. También se presupone el uso de Azure Migrate (también conocido como Azure Site Recovery) para las [actividades de replicación](../migrate/replicate.md). Para ver herramientas alternativas, consulte las [opciones de replicación](../migrate/replicate-options.md).

Este artículo no pretende capturar todas las actividades de evaluación posibles. Se presupone que cada entorno y resultado empresarial determinarán los requisitos específicos. Para ayudar a acelerar la creación de estos requisitos, el resto de este artículo comparte algunas actividades de evaluación comunes relacionadas con la evaluación de la [infraestructura](#common-infrastructure-evaluation-activities), la [base de datos](#common-database-evaluation-activities) y la [red](#common-network-evaluation-activities).

## <a name="common-infrastructure-evaluation-activities"></a>Actividades comunes de evaluación de la infraestructura

- Requisitos de VMware: [revise los requisitos de Azure Site Recovery para VMware](https://docs.microsoft.com/azure/site-recovery/vmware-physical-azure-support-matrix).
- Requisitos de Hyper-V: [revise los requisitos de Azure Site Recovery para Hyper-V](https://docs.microsoft.com/azure/site-recovery/hyper-v-azure-support-matrix).

Asegúrese de documentar cualquier discrepancia que haya en la configuración del host, la configuración de la máquina virtual replicada, los requisitos de almacenamiento o la configuración de red.

## <a name="common-database-evaluation-activities"></a>Actividades comunes de evaluación de bases de datos

- Documente los objetivos de punto de recuperación y los objetivos de tiempo de recuperación de la implementación de base de datos actual. Se usan en [actividades de arquitectura](./architect.md) como ayuda para tomar decisiones.
- Documente los requisitos de configuración de alta disponibilidad. Para entender los requisitos de SQL Server, consulte la [guía de soluciones de alta disponibilidad de SQL Server](https://docs.microsoft.com/sql/sql-server/failover-clusters/high-availability-solutions-sql-server).
- Evalúe la compatibilidad de PaaS. En la [Guía de migración de datos de Azure](https://datamigration.microsoft.com) se asignan bases de datos locales a soluciones de PaaS de Azure compatibles, como [Cosmos DB](https://docs.microsoft.com/azure/cosmos-db) o [Azure DB](https://docs.microsoft.com/azure/sql-database) for [MySQL](https://docs.microsoft.com/azure/mysql), [Postgres](https://docs.microsoft.com/azure/postgresql) o [MariaDB](https://docs.microsoft.com/azure/mariadb).
- Cuando la compatibilidad con PaaS es una opción sin necesidad de realizar ninguna corrección, consulte al equipo responsable de las [actividades de arquitectura](./architect.md). Las migraciones de PaaS pueden generar importantes ahorros de tiempo y disminuciones en el costo total de propiedad (TCO) de la mayoría de las soluciones en la nube.
- Cuando la compatibilidad con PaaS es una opción, pero se requiere una corrección, consulte a los equipos responsables de las [actividades de arquitectura](./architect.md) y las [actividades de corrección](../migrate/remediate.md). En muchos escenarios, las ventajas de las migraciones de PaaS para las soluciones de base de datos pueden superar el aumento en el tiempo de corrección.
- Documente el tamaño y la tasa de cambio de cada base de datos que se va a migrar.
- Siempre que sea posible, documente las aplicaciones u otros recursos que realicen llamadas a cada base de datos.

> [!NOTE]
> La sincronización de cualquier recurso consume ancho de banda durante los procesos de replicación. Una dificultad muy común es pasar por alto el consumo de ancho de banda necesario para mantener los recursos sincronizados entre el punto de replicación y la liberación. Las bases de datos son consumidores comunes de ancho de banda durante los ciclos de liberación y las bases de datos con grandes superficies de almacenamiento o una alta tasa de cambio están son de especial interés. Considere un enfoque de replicación de la estructura de datos, con actualizaciones controladas antes de las pruebas de aceptación de usuario (UAT) y las liberaciones. En estos escenarios, pueden ser más adecuadas alternativas a Azure Site Recovery. Para más información, consulte la [Guía de migración de datos de Azure](https://datamigration.microsoft.com).

## <a name="common-network-evaluation-activities"></a>Actividades comunes de evaluación de la red

- Calcule el almacenamiento total para todas las máquinas virtuales que se van a replicar durante las iteraciones que conducen a una liberación.
- Calcule la desviación o la tasa de cambio del almacenamiento para todas las máquinas virtuales que se van a replicar durante las iteraciones que conducen a una liberación.
- Calcule los requisitos de ancho de banda necesarios para cada iteración mediante la suma del almacenamiento y la desviación totales.
- Calcule el ancho de banda sin usar disponible en la red actual para validar por alineación de iteraciones.
- Documente el ancho de banda necesario para alcanzar la velocidad de migración esperada. Si se requiere alguna corrección para proporcionar el ancho de banda necesario, notifique al equipo responsable de las [actividades de corrección](../migrate/remediate.md).

> [!NOTE]
> El almacenamiento total afecta directamente a los requisitos de ancho de banda durante la replicación inicial. Sin embargo, la desviación del almacenamiento continúa desde el punto de replicación hasta la liberación. Esto significa que la desviación tiene un efecto acumulativo en el ancho de banda disponible.

## <a name="next-steps"></a>Pasos siguientes

Una vez que se completa la evaluación de un sistema, los resultados alimentan el desarrollo de una nueva [arquitectura de nube](./architect.md).

> [!div class="nextstepaction"]
> [Diseño de las cargas de trabajo antes de una migración](./architect.md)
