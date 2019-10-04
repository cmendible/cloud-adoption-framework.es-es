---
title: Centralización de operaciones de administración
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Instrucciones para centralizar las operaciones de administración
author: JnHs
ms.author: jenhayes
ms.date: 09/27/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: b8e4e37ba9a771937b11f08f1abae45de2f818ab
ms.sourcegitcommit: 1dccf1aed8e98aa0f58c4f86d90c65f5fa5ac84d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2019
ms.locfileid: "71806261"
---
# <a name="centralize-management-operations"></a>Centralización de operaciones de administración

Para la mayoría de las organizaciones, el uso de un único inquilino de Azure Active Directory (Azure AD) para todos los usuarios simplifica las operaciones de administración y reduce los costos de mantenimiento, ya que todas las tareas de administración las pueden realizar usuarios designados, grupos de usuarios o entidades de servicio dentro de ese inquilino. Si es posible, se recomienda usar un inquilino de Azure AD en cada organización.

No obstante, hay situaciones en las que puede ser necesario que una organización mantenga varios inquilinos de Azure AD. Por ejemplo, es posible que se requieran varios inquilinos por los siguientes motivos:

- Subsidiarias totalmente independientes.
- Funcionamiento de forma independiente en varias zonas geográficas.
- Requisitos de cumplimiento o de tipo legal.
- Adquisiciones de otras organizaciones (a veces temporal hasta que se define una estrategia de consolidación de inquilinos a largo plazo).

En los casos en que se requiere una arquitectura de multiinquilino, [Azure Lighthouse](https://docs.microsoft.com/azure/lighthouse/overview) proporciona una manera de centralizar y simplificar las operaciones de administración. Se pueden incorporar suscripciones de varios inquilinos para la [administración de recursos delegados de Azure](https://docs.microsoft.com/azure/lighthouse/concepts/azure-delegated-resource-management), lo que permite a los usuarios especificados de un inquilino de administración realizar [funciones de administración que afectan a varios inquilinos](https://docs.microsoft.com/azure/lighthouse/concepts/cross-tenant-management-experience) de forma centralizada y escalable.

Por ejemplo, suponga que su organización tiene un solo inquilino, *Inquilino A*. Posteriormente, la organización adquiere dos inquilinos adicionales, *Inquilino B* e *Inquilino C* y, por motivos empresariales, ambos deben mantenerse como inquilinos independientes.

Su organización quiere usar las mismas definiciones de directiva, prácticas de copia de seguridad y procesos de seguridad en todos los inquilinos. Dado que ya tiene usuarios (incluidos los grupos de usuarios y las entidades de servicio) que son responsables de realizar estas tareas en el Inquilino A, puede incorporar todas las suscripciones en el Inquilino B y el Inquilino C, con el fin de que los mismos usuarios del Inquilino A puedan realizar esas tareas. El inquilino A se convierte en el inquilino de administración para el inquilino B y el inquilino C.

![Los usuarios del Inquilino A administran los recursos del Inquilino B y del Inquilino C](../_images/manage/enterprise-azure-lighthouse.jpg)

Para más información, consulte [Azure Lighthouse en escenarios empresariales](https://docs.microsoft.com/azure/lighthouse/concepts/enterprise).
