---
title: Opciones de replicación
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Un proceso de la migración a la nube que se centra en las tareas de migración de cargas de trabajo.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 8d3722028761adb70797fc9f654bfbdc7e697fb2
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70836638"
---
# <a name="replication-options"></a>Opciones de replicación

Antes de realizar cualquier migración, debe asegurarse de que los sistemas principales sean seguros y de que continuarán ejecutándose sin problemas. Cualquier tiempo de inactividad interrumpe a los usuarios o clientes, y cuesta tiempo y dinero. La migración no es tan sencilla como desactivar las máquinas virtuales locales y copiarlas en Azure. Las herramientas de migración deben tener en cuenta la replicación sincrónica o asincrónica para asegurarse de que los sistemas activos se puedan copiar en Azure sin tiempo de inactividad. Y lo más importante de todo, los sistemas deben ir a la par con sus homólogos locales. Es posible que desee probar los recursos migrados en particiones aisladas de Azure para asegurarse de que las cargas de trabajo funcionan según lo previsto.

El contenido de Cloud Adoption Framework supone que Azure Migrate (o Azure Site Recovery) es la herramienta más adecuada para replicar recursos en la nube. No obstante, hay otras opciones disponibles. En este artículo se describen esas opciones para ayudarle con la toma de decisiones.

## <a name="azure-site-recovery-also-known-as-azure-migrate"></a>Azure Site Recovery (también conocido como Azure Migrate)

[Azure Site Recovery](/azure/site-recovery/site-recovery-overview) orquesta y administra la recuperación ante desastres de las máquinas virtuales de Azure y de las máquinas virtuales y servidores físicos locales. También puede usar Site Recovery para administrar la migración de máquinas locales y de otros proveedores de nube a Azure. Replique las máquinas locales en Azure o las máquinas virtuales de Azure en una región secundaria. Después, conmute por error la máquina virtual del sitio principal al secundario y complete el proceso de migración. Con Azure Site Recovery, puede conseguir varios escenarios de migración:

- **Migración desde un entorno local a Azure.** Puede migrar las máquinas virtuales de Hyper-V locales, las máquinas virtuales de VMware y los servidores físicos a Azure. Para ello, debe completar casi los mismos pasos que seguiría para una recuperación ante desastres completa. Lo único que no debe hacer es una conmutación por recuperación de las máquinas de Azure al sitio local.
- **Migración entre regiones de Azure.** Migre las máquinas virtuales de Azure de una región de Azure a otra. Una vez completada la migración, puede configurar la recuperación ante desastres de las máquinas virtuales de Azure en la región secundaria a la que ha migrado.
- **Migración desde otra nube a Azure.** Puede migrar las instancias de proceso aprovisionadas en otros proveedores de nube a máquinas virtuales de Azure. Site Recovery trata esas instancias como servidores físicos en lo que respecta a la migración.

![Azure Site Recovery](../../../_images/asr-replication-image.png)
*Movimiento de recursos de Azure Site Recovery a Azure o a otras nubes*

Después de haber evaluado la infraestructura local y en la nube para la migración, Azure Site Recovery contribuye a la estrategia de migración mediante la replicación de las máquinas locales. Con los siguientes pasos sencillos, puede configurar la migración de las máquinas virtuales locales, los servidores físicos y las instancias de máquina virtual en la nube a Azure:

- Compruebe los requisitos previos.
- Prepare los recursos de Azure.
- Prepare las instancias de máquinas virtuales locales o en la nube para la migración.
- Implemente un servidor de configuración.
- Habilite la replicación para máquinas virtuales.
- Pruebe la conmutación por error para asegurarse de que todo funciona.
- Ejecute una conmutación por error única en Azure.

## <a name="azure-database-migration-service"></a>Azure Database Migration Service

Este servicio ayuda a reducir la complejidad de la migración a la nube con un servicio completo en lugar de usar varias herramientas. [Azure Database Migration Service](/azure/dms/dms-overview) se ha diseñado como una solución integral para migrar bases de datos de SQL Server locales a la nube sin problemas. Es un servicio totalmente administrado diseñado para permitir migraciones completas desde varios orígenes de base de datos hasta las plataformas de datos de Azure con un tiempo de inactividad mínimo. Integra parte de la funcionalidad de los servicios y herramientas existentes, lo que proporciona a los clientes una solución completa y de alta disponibilidad.

El servicio utiliza Data Migration Assistant para generar informes de evaluación que proporcionen recomendaciones que le guíen a través de los cambios necesarios antes de realizar una migración. Es decisión suya aplicar las correcciones necesarias. Cuando esté listo para comenzar el proceso de migración, Azure Database Migration Service realizará todos los pasos asociados. Ya puede iniciar sus proyectos de migración y olvidarse de ellos con la tranquilidad de saber que el proceso utiliza los procedimientos recomendados que determina Microsoft.

## <a name="next-steps"></a>Pasos siguientes

Una vez completada la replicación, pueden comenzar las [actividades de ensayo](./stage.md).

> [!div class="nextstepaction"]
> [Actividades de ensayo durante una migración](./stage.md)
