---
title: Varios centros de datos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Varios centros de datos
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b2491d349628d2c9640097ddd2c94b79505a0921
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71024793"
---
# <a name="multiple-datacenters"></a>Varios centros de datos

A menudo, el ámbito de una migración implica la transición de varios centros de datos. La siguiente guía ampliará el ámbito de la [guía de migración de Azure](../azure-migration-guide/index.md) para dar respuesta a varios centros de datos.

## <a name="general-scope-expansion"></a>Ampliación del ámbito general

La mayor parte de este esfuerzo requerido en esta ampliación del ámbito se producirá durante los procesos de requisitos previos, evaluación y optimización de una migración.

## <a name="suggested-prerequisites"></a>Requisitos previos sugeridos

Antes de comenzar la migración, debe crear epopeyas dentro de la herramienta de administración de proyectos que representen a cada uno de los centros de datos que se van a migrar. Es importante comprender los resultados y motivaciones empresariales que justifican esta migración. Estas motivaciones se pueden usar para priorizar la lista de epopeyas (o centros de datos). Por ejemplo, si la migración está motivada por un deseo de abandonar un centro de datos antes de que haya que renovar el alquiler, cada epopeya se debería priorizar en función de la fecha de renovación del alquiler.

Dentro de cada epopeya, las cargas de trabajo que se van a evaluar y migrar se administrarán como características. Cada recurso dentro de esa carga de trabajo se administrará como un caso de usuario. El trabajo necesario para evaluar, migrar, optimizar, promover, proteger y administrar cada recurso se representará como tareas de cada recurso.

Los sprints o iteraciones se compondrán de una serie de tareas necesarias para migrar los recursos y los casos de usuario confirmados por el equipo de adopción de la nube. Los lanzamientos se compondrán de una o varias cargas de trabajo o características que se van a promocionar a producción.

## <a name="assess-process-changes"></a>Evaluación de los cambios en el proceso

El cambio más importante en el proceso de evaluación, cuando se amplía el ámbito para dar respuesta a varios centros de datos, está relacionado con el registro y la priorización precisos de cargas de trabajo y dependencias entre los centros de datos.

### <a name="suggested-action-during-the-assess-process"></a>Acción sugerida durante el proceso de evaluación

**Evaluación de las dependencias entre centros de datos:** Las [herramientas de visualización de dependencias de Azure Migrate](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization) pueden ayudar a identificar las dependencias. El uso de este conjunto de herramientas antes de la migración es un excelente procedimiento recomendado general. Sin embargo, cuando se trabaja con una complejidad global, se vuelve un paso necesario para el proceso de evaluación. A través de una [agrupación de dependencias](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies), la visualización puede ayudar a identificar los puertos y las direcciones IP de cualquiera de los recursos que se necesitan para admitir la carga de trabajo.

> [!IMPORTANT]
> Dos notas importantes: en primer lugar, se requiere que un experto en la materia que entienda los esquemas de dirección IP y la ubicación de los recursos identifique los recursos que residen en un centro de datos secundario. En segundo lugar, es importante evaluar tanto las dependencias de nivel inferior y clientes en el objeto visual para comprender las dependencias bidireccionales.

## <a name="migrate-process-changes"></a>Cambios en el proceso de migración

La migración de varios centros de datos se parece al proceso de consolidación. Después de la migración, la nube se convierte en la solución singular de centro de datos para varios recursos. La expansión de ámbito más probable durante el proceso de migración es la validación y la alineación de las direcciones IP.

### <a name="suggested-action-during-the-migrate-process"></a>Acción sugerida durante el proceso de migración

A continuación se indican las actividades que afectan en gran medida al éxito de una migración en la nube:

- **Evaluación de los conflictos de red:** Al consolidar centros de datos en un único proveedor de nube, existe la posibilidad de crear conflictos de red, DNS u otros. Durante la migración, es importante comprobar si hay conflictos para evitar interrupciones en los sistemas de producción hospedados en la nube.
- **Actualización de las tablas de enrutamiento:** A menudo, las modificaciones en las tablas de enrutamiento son necesarias al consolidar redes o centros de datos.

## <a name="optimize-and-promote-process-changes"></a>Optimización y promoción de los cambios del proceso

Durante la optimización, pueden ser necesarias pruebas adicionales.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Acción sugerida durante el proceso de optimización y promoción

Antes de la promoción, es importante proporcionar niveles adicionales de prueba durante la expansión de este ámbito. Durante las pruebas, es importante probar el enrutamiento u otros conflictos de red. Además, es importante aislar la aplicación implementada y volver a probar para comprobar que todas las dependencias se han migrado a la nube. En este caso, el aislamiento implica separar el entorno implementado de las redes de producción. Si lo hace, puede detectar recursos que se han pasado por alto y que se están ejecutando todavía en el entorno local.

## <a name="secure-and-manage-process-changes"></a>Cambios en el proceso de seguridad y administración

La ampliación de este ámbito no debe alterar los procesos de seguridad y administración.

## <a name="next-steps"></a>Pasos siguientes

Vuelva a la [lista de comprobación del ámbito ampliado](./index.md) para asegurarse de que el método de migración está totalmente alineado.

> [!div class="nextstepaction"]
> [Lista de comprobación del ámbito ampliado](./index.md)
