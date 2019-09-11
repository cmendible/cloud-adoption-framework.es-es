---
title: Administración del acceso al entorno de Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Aprenda a configurar el control de acceso para el entorno de Azure con control de acceso basado en rol (RBAC).
author: LijuKodicheraJayadevan
ms.author: kfollis
ms.date: 04/09/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 8f16380af623a6d9cd01e5064599f2688f5136df
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70818666"
---
# <a name="manage-access-to-your-azure-environment-with-role-based-access-controls"></a>Administración del acceso al entorno de Azure con controles de acceso basado en rol

Administrar quién puede acceder a los recursos y suscripciones de Azure constituye una parte importante de la estrategia de gobernanza de Azure, y asignar privilegios y derechos de acceso basados en grupos es una buena práctica. Lidiar con grupos en lugar de con usuarios individuales simplifica el mantenimiento de las directivas de acceso, proporciona la administración de acceso coherente entre equipos y reduce los errores de configuración. El control de acceso basado en rol (RBAC) de Azure es el principal método de administrar el acceso en Azure.

RBAC ofrece una administración de acceso detallada a los recursos de Azure. Ayuda a administrar quién tiene acceso a los recursos de Azure, qué pueden hacer con esos recursos y a qué ámbitos pueden acceder.

Al planear su estrategia de control de acceso, conceda a los usuarios los privilegios mínimos necesarios para que realicen su trabajo. La siguiente imagen muestra un patrón sugerido para la asignación de RBAC.

![Diagrama que muestra los roles de RBAC](./media/manage-access/role-examples.png)

Al planear la metodología de control de acceso, le recomendamos que trabaje con personas de las organizaciones que desempeñen los roles siguientes: seguridad y cumplimiento, administración de TI y arquitecto empresarial.

La Plataforma de adopción de la nube ofrece instrucciones adicionales sobre cómo [usar el control de acceso basado en rol](../azure-best-practices/roles.md) como parte de sus esfuerzos de adopción de la nube.

::: zone target="chromeless"

## <a name="actions"></a>Acciones

**Concesión de acceso al grupo de recursos:**

Para otorgar a un usuario acceso a un grupo de recursos:

1. Vaya a **Grupos de recursos**.
1. Seleccione un grupo de recursos.
1. Seleccione **Access Control (IAM)** .
1. Seleccione **Agregar** > **Agregar asignación de roles**.
1. Seleccione un rol y, después, asigne acceso a un usuario, grupo o entidad de servicio.

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fsubscriptions%2FresourceGroups]" submitText="Go to resource groups" ::: form-end

**Concesión de acceso a la suscripción:**

Para otorgar a un usuario acceso a una suscripción:

1. Vaya a **Suscripciones**.
1. Seleccione una suscripción.
1. Seleccione **Access Control (IAM)** .
1. Seleccione **Agregar** > **Agregar asignación de roles**.
1. Seleccione un rol y, después, asigne acceso a un usuario, grupo o entidad de servicio.

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to subscriptions" ::: form-end

::: zone-end

::: zone target="docs"

## <a name="grant-resource-group-access"></a>Concesión de acceso al grupo de recursos

Para otorgar a un usuario acceso a un grupo de recursos:

1. Vaya a [Grupos de recursos](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fsubscriptions%2FresourceGroups).
1. Seleccione un grupo de recursos.
1. Seleccione **Access Control (IAM)** .
1. Seleccione **Agregar** > **Agregar asignación de roles**.
1. Seleccione un rol y, después, asigne acceso a un usuario, grupo o entidad de servicio.

## <a name="grant-subscription-access"></a>Concesión de acceso a la suscripción

Para otorgar a un usuario acceso a una suscripción:

1. Vaya a [Suscripciones](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).
1. Seleccione una suscripción.
1. Seleccione **Access Control (IAM)** .
1. Seleccione **Agregar** > **Agregar asignación de roles**.
1. Seleccione un rol y, después, asigne acceso a un usuario, grupo o entidad de servicio.

## <a name="learn-more"></a>Más información

Para obtener más información, consulte:

- [¿Qué es el control de acceso basado en rol (RBAC)?](/azure/role-based-access-control/overview)
- [Plataforma de adopción de la nube: Uso del control de acceso basado en rol](../azure-best-practices/roles.md)

::: zone-end
