---
title: Alineación de los recursos con las cargas de trabajo prioritarias
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Alineación de los recursos con las cargas de trabajo prioritarias
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: 9d98a9e368f71310a05ae6242ef75a57771824d5
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70837618"
---
# <a name="align-assets-to-prioritized-workloads"></a>Alineación de los recursos con las cargas de trabajo prioritarias

Una carga de trabajo es una descripción conceptual de una colección de recursos: máquinas virtuales, aplicaciones y orígenes de datos. En el artículo anterior, [Definición y clasificación por prioridades de las cargas de trabajo](./workloads.md), se proporciona una guía para recopilar los datos que van a definir la carga de trabajo. Antes de la migración, algunas de las entradas técnicas de esa lista requieren una validación adicional. Este artículo ayuda con la validación de las siguientes entradas:

- **Aplicaciones**: enumere las aplicaciones incluidas en esta carga de trabajo.
- **Máquinas virtuales/servidores**: enumere las máquinas virtuales o los servidores incluidos en la carga de trabajo.
- **Orígenes de datos**: enumere los orígenes de datos incluidos en la carga de trabajo.
- **Dependencias**: enumere las dependencias de recursos no incluidas en la carga de trabajo.

Hay varias opciones para ensamblar estos datos. Estos son algunos de los enfoques más comunes.

## <a name="alternative-inputs-migrate-modernize-innovate"></a>Entradas alternativas: Migración, modernización e innovación

El objetivo de los puntos de datos anteriores es capturar el trabajo técnico relativo y las dependencias como ayuda para la clasificación por prioridades. En función de la transición que desee, puede que necesite recopilar puntos de datos alternativos para posibilitar una clasificación por prioridades correcta.

**Migración:** en el caso de los trabajos de migración puros, el inventario y las dependencias de recursos existentes sirven como medida equitativa de la complejidad relativa.

**Modernización:** cuando el objetivo de una carga de trabajo es modernizar aplicaciones u otros recursos, estos puntos de datos siguen siendo medidas sólidas de la complejidad. Sin embargo, podría ser aconsejable agregar una entrada para las oportunidades de modernización a la documentación de la carga de trabajo.

**Innovación:** cuando se lleva a cabo un cambio material en los datos o la lógica del negocio durante un trabajo de adopción de la nube, se considera un tipo de *innovación* de transformación. Lo mismo ocurre cuando se crean nuevos datos o una nueva lógica del negocio. En el caso de los escenarios de innovación, la migración de los recursos probablemente representará la menor cantidad de trabajo necesaria. En estos casos, el equipo debe diseñar un conjunto de entradas de datos técnicos para medir la complejidad relativa.

## <a name="azure-migrate"></a>Azure Migrate

Azure Migrate proporciona un conjunto de funciones de agrupación que pueden acelerar la agregación de aplicaciones, máquinas virtuales, orígenes de datos y dependencias. Una vez definidas conceptualmente las cargas de trabajo, se pueden usar como base para agrupar los recursos en función de la asignación de dependencias.

En la documentación de Azure Migrate se proporciona guía sobre [cómo agrupar máquinas en función de las dependencias](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies).

## <a name="configuration-management-database"></a>Base de datos de administración de configuración

Algunas organizaciones tienen una base de datos de administración de configuración (CMDB) bien mantenida en sus herramientas de administración de operaciones existentes. Podrían usar la CMDB alternativamente para proporcionar los puntos de datos de entrada que se han explicado anteriormente.

## <a name="next-steps"></a>Pasos siguientes

[Revise las decisiones de racionalización](./review-rationalization.md) en función de la alineación de recursos y las definiciones de las cargas de trabajo.

> [!div class="nextstepaction"]
> [Revisión de las decisiones de racionalización](./review-rationalization.md)
