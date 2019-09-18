---
title: Administración del acceso a recursos de Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Explicación de las construcciones de administración del acceso a los recursos de Azure: Azure Resource Manager, suscripciones, grupos de recursos y recursos'
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 46c6de1ecaba5b8278138114b6aa27a2608bfb74
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031288"
---
# <a name="resource-access-management-in-azure"></a>Administración del acceso a recursos de Azure

La [gobernanza de la nube](../index.md) describe sus cinco materias correspondientes, que incluye la administración de recursos. [Gobernanza del acceso a los recursos](./index.md) explica cómo la administración del acceso a los recursos está incluida en la materia sobre la administración de los recursos. Antes de continuar y aprender cómo se diseña un modelo de gobernanza, es importante comprender los controles de administración de acceso a los recursos de Azure. La configuración de estos controles de administración de acceso a los recursos constituye la base de su modelo de gobernanza.

Comience por examinar más de cerca cómo se implementan los recursos en Azure.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-an-azure-resource"></a>¿Qué es un recurso de Azure?

En Azure, el término _recurso_ hace referencia a una entidad administrada por Azure. Por ejemplo, las máquinas virtuales, las redes virtuales y las cuentas de almacenamiento se denominan recursos de Azure.

![Diagrama de un recurso](../../_images/govern/design/governance-1-9.png)
*Figura 1: Un recurso.* .

## <a name="what-is-an-azure-resource-group"></a>¿Qué es un grupo de recursos de Azure?

En Azure, todos los recursos deben pertenecer a un [grupo de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). Un grupo de recursos es simplemente una construcción lógica que agrupa varios recursos para poder administrarlos como una sola entidad. Por ejemplo, los recursos que comparten un ciclo de vida similar, como los recursos para una [aplicación de n niveles](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier), pueden crearse o eliminarse como un grupo.

![Diagrama de un grupo de recursos que contiene un recurso](../../_images/govern/design/governance-1-10.png)
*Figura 2: Un grupo de recursos contiene un recurso.*

Los grupos de recursos, y los recursos que contienen, están asociados a una **suscripción** de Azure.

## <a name="what-is-an-azure-subscription"></a>¿Qué es una suscripción de Azure?

Una suscripción de Azure es similar a un grupo de recursos en cuanto que se trata de una construcción lógica que agrupa los grupos de recursos y sus recursos. Sin embargo, una suscripción de Azure también está asociada con los controles que utiliza Azure Resource Manager. ¿Qué significa? Veamos más de cerca Azure Resource Manager y cómo se relaciona con una suscripción de Azure.

![Diagrama de una suscripción de Azure](../../_images/govern/design/governance-1-11.png)
*Figura 3: Una suscripción de Azure.*

## <a name="what-is-azure-resource-manager"></a>¿Qué es Azure Resource Manager?

En [¿Cómo funciona Azure?](../../getting-started/what-is-azure.md), aprendió que Azure incluye un "front-end" con muchos servicios que orquestan todas las funciones de Azure. Uno de estos servicios es [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager) y hospeda la API RESTful que los clientes utilizan para administrar los recursos.

![Diagrama de Azure Resource Manager](../../_images/govern/design/governance-1-12.png)
*Figura 4: Azure Resource Manager.*

En la siguiente ilustración se muestran tres clientes: [PowerShell](https://docs.microsoft.com/powershell/azure/overview), [Azure Portal](https://portal.azure.com) y la [CLI de Azure](https://docs.microsoft.com/cli/azure):

![Diagrama de clientes de Azure que se conectan a la API de Azure Resource Manager](../../_images/govern/design/governance-1-13.png)
*Figura 5: Los clientes de Azure se conectan a la API RESTful de Azure Resource Manager.*

Aunque estos clientes se conectan a Azure Resource Manager mediante la API RESTful, Azure Resource Manager no incluye una funcionalidad para administrar los recursos directamente. En su lugar, la mayoría de los tipos de recursos de Azure tienen sus propios [**proveedores de recursos**](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#terminology).

![Proveedores de recursos de Azure](../../_images/govern/design/governance-1-14.png)
*Figura 6: Proveedores de recursos de Azure.*

Cuando un cliente realiza una solicitud para administrar un recurso específico, Azure Resource Manager conecta con el proveedor de recursos para ese tipo de recurso para completar la solicitud. Por ejemplo, si un cliente realiza una solicitud para administrar un recurso de máquina virtual, Azure Resource Manager conecta con el proveedor de recursos **Microsoft.Compute**.

![Conexión de Azure Resource Manager con el proveedor de recursos Microsoft.Compute](../../_images/govern/design/governance-1-15.png)
*Figura 7: Azure Resource Manager se conecta con el proveedor de recursos **Microsoft.Compute** para administrar el recurso especificado en la solicitud del cliente.*

Azure Resource Manager requiere que el cliente especifique un identificador de suscripción y de grupo de recursos para poder administrar el recurso de máquina virtual.

Ahora que ya comprende cómo funciona Azure Resource Manager, volvamos a la explicación de cómo una suscripción de Azure está asociada con los controles utilizados por Azure Resource Manager. Antes de que Azure Resource Manager pueda ejecutar ninguna solicitud de administración de recursos, se comprueban un conjunto de controles.

El primer control es que la solicitud debe realizarla un usuario validado y Azure Resource Manager tiene una relación de confianza con [Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory), que proporciona la funcionalidad de identidades de usuario.

![Azure Active Directory](../../_images/govern/design/governance-1-16.png)
*Figura 8: Azure Active Directory.*

Los usuarios de Azure AD se segmentan en **inquilinos**. Un inquilino es una construcción lógica que representa una instancia segura y dedicada de Azure AD, normalmente asociada a una organización. Cada suscripción está asociada a un inquilino de Azure AD.

![Inquilino de Azure AD asociado a una suscripción](../../_images/govern/design/governance-1-17.png)
*Figura 9: Inquilino de Azure AD asociado a una suscripción.*

Para poder procesar solicitudes de cliente para administrar un recurso en una determinada suscripción, el usuario debe tener una cuenta en el inquilino de Azure AD.

El control siguiente es una comprobación de que el usuario tiene permisos suficientes para realizar la solicitud. Los permisos se asignan a los usuarios con el [control de acceso basado en rol (RBAC)](https://docs.microsoft.com/azure/role-based-access-control).

![Usuarios asignados a roles RBAC](../../_images/govern/design/governance-1-18.png)
*Figura 10. Cada usuario del inquilino se asigna a uno o varios roles de RBAC.*

Un rol de RBAC especifica un conjunto de permisos que un usuario puede tener en un recurso específico. Cuando se asigna el rol al usuario, se aplican estos permisos. Por ejemplo, el [rol integrado **propietario**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) permite a un usuario realizar cualquier acción en un recurso.

El siguiente control es una comprobación de que la solicitud se permite de acuerdo con la configuración especificada para la [directiva de recursos de Azure](https://docs.microsoft.com/azure/governance/policy). Las directivas de recursos de Azure especifican las operaciones permitidas para un recurso específico. Por ejemplo, una directiva de recursos de Azure puede especificar que los usuarios solo pueden implementar un tipo específico de máquina virtual.

![Directiva de recursos de Azure](../../_images/govern/design/governance-1-19.png)
*Figura 11. Directiva de recursos de Azure.*

El siguiente control es una comprobación de que la solicitud no supera un [límite de suscripción de Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits). Por ejemplo, cada suscripción tiene un límite de 980 grupos de recursos por suscripción. Si se recibe una solicitud para implementar un grupo de recursos adicional una vez alcanzado el límite, se deniega.

![Límites de recursos de Azure](../../_images/govern/design/governance-1-20.png)
*Figura 12. Límites de recursos de Azure.*

El control final es una comprobación de que la solicitud está dentro del compromiso financiero asociado a la suscripción. Por ejemplo, si la solicitud es para implementar una máquina virtual, Azure Resource Manager comprueba que la suscripción tiene suficiente información de pago.

![Un compromiso financiero asociado a una suscripción.](../../_images/govern/design/governance-1-21.png)
*Figura 13. Una suscripción tiene asociado un compromiso financiero.*

## <a name="summary"></a>Resumen

En este artículo, ha aprendido cómo se administra el acceso a los recursos en Azure mediante Azure Resource Manager.

## <a name="next-steps"></a>Pasos siguientes

Ahora que comprende cómo administrar el acceso a los recursos en Azure, aprenda ahora cómo diseñar un modelo de gobernanza [para una carga de trabajo simple](./governance-simple-workload.md) o para [varios equipos](./governance-multiple-teams.md) con estos servicios.

> [!div class="nextstepaction"]
> [Introducción a la gobernanza](../index.md)
