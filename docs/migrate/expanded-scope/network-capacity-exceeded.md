---
title: Capacidad de red superada
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Los requisitos de almacenamiento superan la capacidad de red durante un esfuerzo de migración.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: eb6a5adeac25293539edd5d97c816fad2865345c
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70836706"
---
# <a name="storage-requirements-exceed-network-capacity-during-a-migration-effort"></a>Los requisitos de almacenamiento superan la capacidad de red durante un esfuerzo de migración

En una migración a la nube, los recursos se replican y sincronizan a través de la red entre el centro de datos existente y la nube. No es poco frecuente que los requisitos de tamaño de datos existentes de varias cargas de trabajo superen la capacidad de la red. En dicho escenario, el proceso de migración se puede ralentizar de manera considerable o, en algunos casos, se puede detener por completo. En las instrucciones siguientes se expandirá el ámbito de la [Guía de migración a Azure](../azure-migration-guide/index.md) para proporcionar una solución que funcione en torno a las limitaciones de la red.

## <a name="general-scope-expansion"></a>Expansión del ámbito general

La mayor parte de este esfuerzo requerido en esta expansión del ámbito se producirá durante los procesos de requisitos previos, evaluación y migración de una migración.

## <a name="suggested-prerequisites"></a>Requisitos previos sugeridos

**Validación de los riesgos de la capacidad de la red:** La [racionalización del patrimonio digital](../../digital-estate/rationalize.md) es un requisito previo muy recomendado, especialmente si existen preocupaciones con respecto a sobrecargar la capacidad de red disponible. Durante la racionalización del patrimonio digital, se recopila un [inventario de los recursos digitales](../../digital-estate/inventory.md). Dicho inventario debe incluir los requisitos de almacenamiento existentes en todo el patrimonio digital. Tal como se describe en [Riesgos de replicación: física de replicación](../migration-considerations/migrate/replicate.md#replication-risks---physics-of-replication), ese inventario se puede usar para calcular el **tamaño total de los datos de la migración**, que se puede comparar con el **ancho de banda total disponible para la migración**. Si esa comparación no se alinea con el **tiempo requerido para el cambio empresarial**, la información de este artículo puede ayudar a acelerar la velocidad de la migración, lo que disminuye el tiempo requerido para migrar el centro de datos.

**Transferencia sin conexión de almacenes de datos independientes:** en el diagrama siguiente se muestran ejemplos de transferencias de datos en línea y sin conexión con Azure Data Box. Estos enfoques se pueden usar para enviar grandes volúmenes de datos a la nube antes de la migración de las cargas de trabajo. En una transferencia de datos sin conexión, los datos de origen se copian a Azure Data Box, el que se envía físicamente a Microsoft para su transferencia a una cuenta de almacenamiento de Azure como archivo o blob. Este proceso se puede usar para enviar datos que no estén vinculados directamente a una carga de trabajo específica, antes de los demás esfuerzos de migración. Esto reduce la cantidad de datos que se deben enviar a través de la red, en un esfuerzo por completar una migración dentro de las restricciones de la red.

Este enfoque se podría usar para transferir HDFS de datos, copias de seguridad, archivos, servidores de archivos, aplicaciones, etc. Una guía técnica existente explica cómo usar este enfoque para transferir datos desde [un almacén de HDFS](/azure/storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster) o desde discos con [SMB](/azure/databox/data-box-deploy-copy-data), [NFS](/azure/databox/data-box-deploy-copy-data-via-nfs), [REST](/azure/databox/data-box-deploy-copy-data-via-rest) o el [servicio de copia de datos](/azure/databox/data-box-deploy-copy-data-via-copy-service) a Data Box.

También hay [soluciones de asociados de terceros](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box) que usan Azure Data Box para una migración de tipo "inicialización y fuente", donde un gran volumen de datos se mueve a través de una transferencia sin conexión pero que más adelante se sincroniza a una escala inferior a través de la red.

![Transferencia de datos en línea y sin conexión con Azure Data Box](../../_images/migration/databox.png)

## <a name="assess-process-changes"></a>Evaluación de los cambios del proceso

Si los requisitos de almacenamiento de una carga de trabajo (o cargas de trabajo) superan la capacidad de la red, de todos modos es posible usar Azure Data Box en una transferencia de datos sin conexión.

La posición general de Microsoft es que el enfoque recomendado es la transmisión a través de la red, a menos que esta no esté disponible. Esta sugerencia es resultado de las velocidades de transferencia. La transferencia de datos a través de la red (incluso si el ancho de banda está restringido) suele ser más rápida que el envío físico de la misma cantidad de datos a través de un mecanismo de transferencia sin conexión, como Data Box.

Si hay disponible conectividad con Azure, se debe realizar un análisis antes de usar Data Box, especialmente si la migración de la carga de trabajo está sujeta a una limitación temporal. Solo se recomienda usar Data Box cuando el tiempo para transferir los datos necesarios supera el tiempo para llenar, enviar y restaurar los datos mediante Data Box.

### <a name="suggested-action-during-the-assess-process"></a>Acción sugerida durante el proceso de evaluación

**Análisis de la capacidad de red:** cuando los requisitos de transferencia de datos relacionados con la carga de trabajo están en riesgo de superar la capacidad de la red, el equipo de adopción de la nube podría agregar una tarea de análisis adicional al proceso de evaluación, llamado Análisis de la capacidad de red. Durante este análisis, un miembro del equipo con experiencia en la materia sobre la red local y la conectividad de la red podría calcular la cantidad de capacidad de red disponible y el tiempo necesario para la transferencia de datos. Esa capacidad disponible se compararía con los requisitos de almacenamiento de todos los recursos que se van a migrar durante la liberación actual. Si los requisitos de almacenamiento superan el ancho de banda disponible, los recursos que admiten la carga de trabajo se seleccionarían para una transferencia sin conexión.

> [!IMPORTANT]
> Al concluir el análisis, es posible que sea necesario actualizar el plan de liberación para que refleje el tiempo necesario para enviar, restaurar y sincronizar los recursos que se van a transferir sin conexión.

**Análisis de la desviación:** cada archivo que se va a transferir sin conexión se debe analizar para conocer la desviación del almacenamiento y la configuración. La desviación del almacenamiento es la cantidad de cambios en el almacenamiento subyacente a lo largo del tiempo. La desviación de la configuración es el cambio en la configuración del recurso a lo largo del tiempo. Desde el momento en que se copia el almacenamiento al momento en que el recurso se promueve a producción, se puede perder cualquier desviación. Si es necesario reflejar esa desviación en el recurso migrado, es posible que se requiera alguna forma de sincronización entre el recurso local y el recurso migrado. Esto se debe marcar para considerarlo durante la ejecución de la migración.

## <a name="migrate-process-changes"></a>Cambios en el proceso de migración

Cuando se usan mecanismos de transferencia sin conexión, es probable que no se necesiten [procesos de replicación](../migration-considerations/migrate/replicate.md). Sin embargo, es posible que los [procesos de sincronización](../migration-considerations/migrate/replicate.md) sigan siendo requisito. Entender los resultados del análisis de desviación completado durante el proceso de evaluación informará las tareas necesarias durante la migración, si hay algún recurso que se transfiere sin conexión.

### <a name="suggested-action-during-the-migrate-process"></a>Acción sugerida durante el proceso de migración

**Copia del almacenamiento:** este enfoque se podría usar para transferir HDFS de datos, copias de seguridad, archivos, servidores de archivos, aplicaciones, etc. Una guía técnica existente explica cómo usar este enfoque para transferir datos desde [un almacén de HDFS](/azure/storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster) o desde discos con [SMB](/azure/databox/data-box-deploy-copy-data), [NFS](/azure/databox/data-box-deploy-copy-data-via-nfs), [REST](/azure/databox/data-box-deploy-copy-data-via-rest) o el [servicio de copia de datos](/azure/databox/data-box-deploy-copy-data-via-copy-service) a Data Box.

También hay [soluciones de asociados de terceros](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box) que usan Azure Data Box para una migración de tipo "inicialización y sincronización", donde un gran volumen de datos se mueve a través de una transferencia sin conexión pero que más adelante se sincroniza a una escala inferior a través de la red.

**Envío del dispositivo:** una vez que se copian los datos, el dispositivo se puede [enviar a Microsoft](/azure/databox/data-box-deploy-picked-up). Una vez que los datos se reciben e importan, estarán disponibles en una cuenta de almacenamiento de Azure.

**Restauración del recurso:** [compruebe que los datos](/azure/databox/data-box-deploy-picked-up#verify-data-upload-to-azure) estén disponible en la cuenta de almacenamiento. Una vez que se compruebe, los datos se podrán usar como blob o en Azure Files. Si los datos son un archivo VHD/VHDX, el archivo se puede convertir en discos administrados. Esos discos administrados se pueden usar para crear instancias de una máquina virtual, que crea una réplica del recurso local original.

**Sincronización:** si la sincronización de la desviación es requisito para un recurso migrado, una de las [soluciones de asociados de terceros](https://azuremarketplace.microsoft.com/campaigns/databox/azure-data-box) se podría usar para sincronizar los archivos hasta que se restaure el recurso.

## <a name="optimize-and-promote-process-changes"></a>Cambios en los procesos de optimización y promoción

Este cambio del ámbito probablemente no afecte a las actividades de optimización.

## <a name="secure-and-manage-process-changes"></a>Cambios en el proceso de protección y administración

Este cambio del ámbito probablemente no afecte a las actividades de protección y administración.

## <a name="next-steps"></a>Pasos siguientes

Vuelva a la [lista de comprobación del ámbito ampliado](./index.md) para asegurarse de que el método de migración está totalmente alineado.

> [!div class="nextstepaction"]
> [Lista de comprobación del ámbito ampliado](./index.md)
