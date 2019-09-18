---
title: Herramientas de Cost Management en Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Herramientas de Cost Management en Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 230e36d1ca59c208109eedbbdf7466f6373f4b00
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032284"
---
# <a name="cost-management-tools-in-azure"></a>Herramientas de Cost Management en Azure

[Cost Management](./index.md) es una de las [cinco disciplinas de gobernanza en la nube](../governance-disciplines.md). Esta disciplina se centra en las formas de establecer planes de gastos en la nube, asignar presupuestos de nube, supervisar y exigir los presupuestos de nube, detectar anomalías costosas y ajustar el plan de gobernanza en la nube cuando el gasto real no esté alineado.

A continuación, se muestra una lista de herramientas nativas de Azure que pueden ayudar a desarrollar las directivas y los procesos que admiten la disciplina de gobernanza.

| Herramienta | [Azure Portal](https://azure.microsoft.com/features/azure-portal)  | [Azure Cost Management](https://docs.microsoft.com/azure/cost-management/overview-cost-mgt)  | [Paquete de contenido de Azure EA](https://docs.microsoft.com/power-bi/service-connect-to-azure-enterprise)  | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) |
|---------|---------|---------|---------|---------|
|¿Es necesario el Contrato Enterprise?     | Sin         | No         | Sí         | Sin         |
|Control del presupuesto     | Sin         | Sí         | Sin         | Sí         |
|Supervisión del gasto en un único recurso    | Sí         | Sí         | Sí         | Sin         |
|Supervisión del gasto en varios recursos    | Sin         | Sí        | Sí         | Sin         |
|Control del gasto en un único recurso     | Sí: ajuste de tamaño manual         | Sí         | Sin         | Sí         |
|Aplicación del gasto en varios recursos    | Sin         | Sí         | Sin         | Sí         |
|Aplicar los metadatos de contabilidad a los recursos    | Sin         | No         | No         | Sí         |
|Supervisión y detección de tendencias     | Sí: limitadas         | Sí        | Sí         | Sin         |
|Detección de anomalías en el gasto     | Sin         | Sí        | Sí         | Sin        |
|Socialización de desviaciones     | Sin        | Sí        | Sí        | Sin        |
