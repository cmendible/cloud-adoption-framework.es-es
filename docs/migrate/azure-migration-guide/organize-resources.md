---
title: Organización de los recursos de Azure de forma eficaz
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Procedimientos recomendados para organizar de forma eficaz los recursos de Azure para administrarlos de forma fácil.
author: laraaleite
ms.author: kfollis
ms.date: 04/09/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 19299c5855600524f3335b00272974790d83c8fa
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022768"
---
# <a name="organize-your-azure-resources"></a>Organización de los recursos de Azure

Utilice las siguientes características y procedimientos recomendados para proteger los recursos que son críticos para el sistema. Etiquetar recursos para que pueda realizar su seguimiento según los valores que encajan con su organización.

<!-- markdownlint-disable MD024 MD025 -->

# <a name="azure-management-groups-and-hierarchytabazuremanagmentgroupsandhierarchy"></a>[Jerarquía y grupos de administración de Azure](#tab/AzureManagmentGroupsAndHierarchy)

La estructura organizativa de los recursos de Azure tiene cuatro niveles: grupos de administración, suscripciones, grupos de recursos y recursos. La imagen siguiente muestra la relación de estos niveles.

![Diagrama que muestra la relación de la jerarquía de administración](./media/organize-resources/scope-levels.png)

- **Grupos de administración:** Estos son contenedores que ayudan a administrar el acceso, las directivas y el cumplimiento de varias suscripciones. Todas las suscripciones de un grupo de administración heredan automáticamente las condiciones que se aplican al grupo de administración.
- **Suscripciones:** Una suscripción agrupa las cuentas de usuario y los recursos creados por esas cuentas de usuario. Para cada suscripción, hay límites o cuotas con respecto a la cantidad de recursos, puede crear y usar. Las organizaciones pueden usar las suscripciones para administrar los costos y los recursos creados por los usuarios, equipos o proyectos.
- **Grupos de recursos:** Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como aplicaciones web, bases de datos y cuentas de almacenamiento.
- **Recursos:** Los recursos son instancias de servicios que se crean como máquinas virtuales, almacenamiento o bases de datos SQL.

## <a name="scope-of-management-settings"></a>Ámbito de configuración de administración

Puede aplicar la configuración de administración, como directivas y controles de acceso basado en rol, en cualquiera de los niveles de administración. El nivel que seleccione determina el grado de amplitud con que se aplica la configuración. Los niveles inferiores heredan la configuración de los niveles superiores. Por ejemplo, al aplicar una directiva a una suscripción, esta directiva se aplica también a todos los grupos de recursos y a los recursos de la suscripción.

Normalmente, tiene sentido aplicar la configuración crítica en niveles superiores y los requisitos específicos del proyecto en niveles inferiores. Por ejemplo, quizás quiera asegurarse de que todos los recursos de la organización se implementan en determinadas regiones. Para hacerlo, aplique una directiva a la suscripción que especifique las ubicaciones permitidas. Cuando otros usuarios de su organización agreguen nuevos grupos de recursos y recursos, se aplicarán automáticamente las ubicaciones permitidas. Más información acerca de las directivas en la sección de gobernanza, seguridad y cumplimiento de esta guía.

Al planear la estrategia de cumplimiento, le recomendamos que trabaje con personas de su organización que desempeñen estos roles: seguridad y cumplimiento, administración de TI, arquitecto empresarial, redes, finanzas y adquisiciones.

::: zone target="docs"

## <a name="create-a-management-level"></a>Creación de un nivel de administración

Puede crear un grupo de administración, suscripciones adicionales o grupos de recursos.

### <a name="create-management-group"></a>Creación de un grupo de administración

Cree un grupo de administración que le ayude a administrar el acceso, las directivas y el cumplimiento de varias suscripciones.

1. Vaya a [Grupos de administración](https://portal.azure.com/#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade).
2. Seleccione **Agregar grupo de administración**.

### <a name="create-subscription"></a>Creación de una suscripción

Use suscripciones para administrar los costos y los recursos creados por los usuarios, equipos o proyectos.

1. Vaya a [Suscripciones](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).
1. Seleccione **Agregar**.

### <a name="create-resource-group"></a>Creación de un grupo de recursos

Cree un grupo de recursos para contener recursos como aplicaciones web, bases de datos y cuentas de almacenamiento que comparten el mismo ciclo de vida, permisos y directivas.

1. Vaya a [Grupos de recursos](https://portal.azure.com/#create/Microsoft.ResourceGroup).
1. Seleccione **Agregar**.
1. Seleccione la **suscripción** en la que desea que se cree el grupo de recursos.
1. Escriba un nombre para el **grupo de recursos**.
1. Seleccione una **región** como ubicación del grupo de recursos.

## <a name="learn-more"></a>Más información

Para obtener más información, consulte:

- [Descripción de la administración del acceso a los recursos en Azure](../../govern/resource-consistency/resource-access-management.md)
- [Organización de los recursos con grupos de administración de Azure](https://docs.microsoft.com/azure/azure-resource-manager/management-groups-overview)
- [Límites del servicio de suscripción](https://docs.microsoft.com/azure/azure-subscription-service-limits)

::: zone-end

::: zone target="chromeless"

## <a name="actions"></a>Acciones

**Crear un grupo de administración:**

Cree un grupo de administración que le ayude a administrar el acceso, las directivas y el cumplimiento de varias suscripciones.

1. Vaya a **Grupos de administración**.
1. Seleccione **Agregar grupo de administración**.

::: form action="OpenBlade[#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade]" submitText="Go to Management groups" :::

**Crear una suscripción adicional:**

Use suscripciones para administrar los costos y los recursos creados por los usuarios, equipos o proyectos.

1. Vaya a **Suscripciones**.
1. Seleccione **Agregar**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Billing/SubscriptionsBlade]" submitText="Go to Subscriptions" :::

**Crear un grupo de recursos:**

Cree un grupo de recursos para contener recursos como aplicaciones web, bases de datos y cuentas de almacenamiento que comparten el mismo ciclo de vida, permisos y directivas.

1. Vaya a **Grupos de recursos**.
1. Seleccione **Agregar**.
1. Seleccione la **suscripción** en la que desea que se cree el grupo de recursos.
1. Escriba un nombre para el **grupo de recursos**.
1. Seleccione una **región** como ubicación del grupo de recursos.

::: form action="Create[#create/Microsoft.ResourceGroup]" submitText="Create a resource group" :::

::: zone-end

# <a name="naming-standardstabnamingstandards"></a>[Estándares de nomenclatura](#tab/NamingStandards)

Un buen estándar de nomenclatura lo ayuda a identificar los recursos en el portal, en una factura y en los scripts. Puede que ya tenga estándares de nomenclatura para la infraestructura local. Al agregar Azure a su entorno, debe extender estos estándares de nomenclatura a los recursos de Azure. Los estándares de nomenclatura le ayudan a administrar el entorno de forma más eficaz en todos los niveles. Puede usar Azure Policy como una herramienta para aplicar los estándares de nomenclatura en todo el entorno de Azure.

::: zone target="docs"

Se recomienda revisar y seguir las indicaciones de la [guía de patrones y procedimientos](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).

>[!TIP]
>Evite usar caracteres especiales (`-` o `_`) como primer o último carácter en ningún nombre. Estos caracteres hacen que la mayoría de las reglas de validación produzcan un error.

::: zone-end

| Entidad | Ámbito | Length | Uso de mayúsculas y minúsculas | Caracteres válidos | Patrón sugerido | Ejemplo |
| --- | --- | --- | --- | --- | --- | --- |
|Resource group |Subscription |1-90 |No distingue mayúsculas de minúsculas |Alfanuméricos, carácter de subrayado, paréntesis, guión, punto (excepto al final) y caracteres Unicode |`<service short name>-<environment>-rg` |`profx-prod-rg` |
|Conjunto de disponibilidad |Resource group |1-80 |No distingue mayúsculas de minúsculas |Alfanuméricos, carácter de subrayado y guión |`<service-short-name>-<context>-as` |`profx-sql-as` |
|Etiqueta |Entidad asociada |512 (nombre), 256 (valor) |No distingue mayúsculas de minúsculas |Alfanuméricas |`"key" : "value"` |`"department" : "Central IT"` |

# <a name="resource-tagstabresourcetags"></a>[Etiquetas del recurso](#tab/ResourceTags)

Las etiquetas son útiles para identificar rápidamente los recursos y grupos de recursos. Se aplican etiquetas a los recursos de Azure para organizarlos de forma lógica por categorías. Cada etiqueta consta de un nombre y un valor. Por ejemplo, puede aplicar el nombre "Environment" y el valor "Production" a todos los recursos en producción.

Después de aplicar las etiquetas, puede recuperar todos los recursos de la suscripción que tengan ese nombre y valor de etiqueta. Las etiquetas le permiten recuperar recursos relacionados de diferentes grupos de recursos, lo que resulta útil para organizar los recursos para la facturación o administración.

También puede utilizar etiquetas para muchas otras cosas. Entre los usos comunes se incluyen:

- **Metadatos y documentación:** los administradores pueden ver fácilmente detalles sobre los recursos en los que están trabajando aplicando una etiqueta como "ProjectOwner".
- **Automation:** es posible que cuente con scripts que se ejecuten regularmente y que puedan realizar una acción basada en un valor de etiqueta como "ShutdownTime" o "DeprovisionDate".
- **Facturación:** Las etiquetas pueden aparecer en la factura. Puede usarlas para ayudar a segmentar la factura mediante etiquetas como "CostCenter" o "BillTo".

Cada recurso o grupo de recursos puede tener un máximo de 15 pares de nombre/valor de etiqueta. No obstante, esta limitación solo afecta a las etiquetas que se aplican directamente al recurso o grupo de recursos.

Para más información sobre el etiquetado, consulte las [convenciones de nomenclatura del Centro de arquitectura de Azure para los recursos de Azure](../../ready/considerations/naming-and-tagging.md#metadata-tags).

::: zone target="docs"

## <a name="apply-a-resource-tag"></a>Aplicación de una etiqueta de recurso

Para aplicar una etiqueta a un grupo de recursos:

1. Vaya a [Grupos de recursos](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fsubscriptions%2FresourceGroups).
1. Seleccione un grupo de recursos.
1. Seleccione **Etiquetas**.
1. Escriba un nuevo nombre y valor o use la lista desplegable para seleccionar unos ya existentes.

## <a name="learn-more"></a>Más información

Para más información, consulte [Uso de etiquetas para organizar los recursos de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

::: zone-end

::: zone target="chromeless"

## <a name="action"></a>.

**Aplicación de una etiqueta de recurso:**

Para aplicar una etiqueta a un grupo de recursos:

1. Vaya a **Grupos de recursos**.
1. Seleccione un grupo de recursos.
1. Seleccione **Etiquetas**.
1. Escriba un nuevo nombre y valor o seleccione unos ya existentes.

::: form action="OpenBlade[#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fsubscriptions%2FresourceGroups]" submitText="Go to resource groups" :::

::: zone-end
