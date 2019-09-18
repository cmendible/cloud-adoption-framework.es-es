---
title: Organización de los recursos de Azure de forma eficaz
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Procedimientos recomendados para organizar de forma eficaz los recursos de Azure para administrarlos de forma fácil.
author: laraaleite
ms.author: kfollis
ms.date: 04/09/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: 8be46c21a009b7dca11cfc628476ae46315b23e5
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025226"
---
# <a name="organize-your-azure-resources"></a>Organización de los recursos de Azure

La organización de los recursos basados en la nube es fundamental para proteger, administrar y realizar un seguimiento de los costos relacionados con las cargas de trabajo. Para organizar los recursos, use las jerarquías de administración de la plataforma Azure, implemente convenciones de nomenclatura bien concebidas y aplique el etiquetado de recursos.

<!-- markdownlint-disable MD024 MD025 -->

# <a name="azure-management-groups-and-hierarchytabazuremanagmentgroupsandhierarchy"></a>[Jerarquía y grupos de administración de Azure](#tab/AzureManagmentGroupsAndHierarchy)

Azure proporciona cuatro niveles de ámbito administración: grupo de administración, suscripciones, grupos de recursos y recursos. La imagen siguiente muestra la relación de estos niveles.

   ![Diagrama que muestra la relación de la jerarquía de administración](./media/organize-resources/scope-levels.png)

- **Grupos de administración:** estos grupos son contenedores que ayudan a administrar el acceso, las directivas y el cumplimiento de varias suscripciones. Todas las suscripciones de un grupo de administración heredan automáticamente las condiciones que se aplican al grupo de administración.
- **Suscripciones:** una suscripción agrupa las cuentas de usuario y los recursos creados por esas cuentas de usuario. Cada suscripción tiene límites o cuotas con respecto a la cantidad de recursos que se pueden crear y usar. Las organizaciones pueden usar las suscripciones para administrar los costos y los recursos creados por los usuarios, equipos o proyectos.
- **Grupos de recursos:** Un grupo de recursos es un contenedor lógico en el que se implementan y se administran recursos de Azure como aplicaciones web, bases de datos y cuentas de almacenamiento.
- **Recursos:** Los recursos son instancias de servicios que se crean como máquinas virtuales, almacenamiento o bases de datos SQL.

## <a name="scope-of-management-settings"></a>Ámbito de configuración de administración

Puede aplicar la configuración de administración, como directivas y controles de acceso basado en rol, en cualquiera de los niveles de administración. El nivel que seleccione determina el grado de amplitud con que se aplica la configuración. Los niveles inferiores heredan la configuración de los niveles superiores. Por ejemplo, al aplicar una directiva a una suscripción, esta directiva se aplica también a todos los grupos de recursos y a los recursos de la suscripción.

Normalmente, tiene sentido aplicar la configuración crítica en niveles superiores y los requisitos específicos del proyecto en niveles inferiores. Por ejemplo, quizás quiera asegurarse de que todos los recursos de su organización se implementan en determinadas regiones. Para hacerlo, aplique una directiva a la suscripción que especifique las ubicaciones permitidas. Cuando otros usuarios de su organización agreguen nuevos grupos de recursos y recursos, se aplicarán automáticamente las ubicaciones permitidas. Más información acerca de las directivas en la sección de gobernanza, seguridad y cumplimiento de esta guía.

Si solo tiene algunas suscripciones, es relativamente sencillo administrarlas de forma independiente. Si el número de suscripciones que usa aumenta, considere la posibilidad de crear una jerarquía de grupos de administración para simplificar la administración de las suscripciones y los recursos. Para más información sobre cómo administrar varias suscripciones, consulte [Escalado con varias suscripciones de Azure](../considerations/scaling-subscriptions.md).

Al planear la estrategia de cumplimiento, trabaje con personas de su organización que desempeñen estos roles: seguridad y cumplimiento, administración de TI, arquitecto empresarial, redes, finanzas y adquisiciones.

::: zone target="docs"

## <a name="create-a-management-level"></a>Creación de un nivel de administración

Puede crear un grupo de administración, suscripciones adicionales o grupos de recursos.

### <a name="create-a-management-group"></a>Creación de un grupo de administración

Cree un grupo de administración que le ayude a administrar el acceso, las directivas y el cumplimiento de varias suscripciones.

1. Vaya a [Grupos de administración](https://portal.azure.com/#blade/Microsoft_Azure_ManagementGroups/HierarchyBlade).
2. Seleccione **Agregar grupo de administración**.

### <a name="create-a-subscription"></a>una suscripción

Use suscripciones para administrar los costos y los recursos creados por los usuarios, equipos o proyectos.

1. Vaya a [Suscripciones](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).
1. Seleccione **Agregar**.

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

Cree un grupo de recursos para contener recursos como aplicaciones web, bases de datos y cuentas de almacenamiento que comparten el mismo ciclo de vida, permisos y directivas.

1. Vaya a [Grupos de recursos](https://portal.azure.com/#create/Microsoft.ResourceGroup).
1. Seleccione **Agregar**.
1. Seleccione la **suscripción** en la que desea que se cree el grupo de recursos.
1. Escriba un nombre para el **grupo de recursos**.
1. Seleccione una **región** como ubicación del grupo de recursos.

## <a name="learn-more"></a>Más información

Para obtener más información, consulte:

- [Aspectos básicos de Azure](../considerations/fundamental-concepts.md)
- [Escalado con varias suscripciones de Azure](../considerations/scaling-subscriptions.md)
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

Un buen estándar de nomenclatura le ayuda a identificar los recursos de Azure Portal, en una factura y en los scripts. La estrategia de nomenclatura debe incluir detalles empresariales y operativos como componentes de los nombres de recursos:

- La parte relacionada con la empresa de esta estrategia debe garantizar que los nombres de los recursos incluyen la información de la organización necesaria para identificar a los equipos. Use un recurso junto con los propietarios de la empresa responsables de los costos de los recursos.

- El lado operativo debe asegurarse de que los nombres incluyan la información que necesitan los equipos de TI. Use los detalles que identifiquen la carga de trabajo, la aplicación, el entorno, la importancia y otra información que resulte útil para administrar los recursos.

Los distintos tipos de recursos pueden tener distintos límites de longitud y caracteres permitidos, muchos de los cuales se enumeran en el [artículo sobre las convenciones de nomenclatura](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) de procedimientos recomendados de Azure. Para más información y recomendaciones centradas específicamente en la compatibilidad con las labores de adopción de la nube empresarial, consulte la [guía sobre nomenclatura y etiquetado](../considerations/naming-and-tagging.md) del marco de adopción de la nube.

En la tabla siguiente se incluyen patrones de nomenclatura para algunos tipos de ejemplos de recursos de Azure.

::: zone target="docs"

>[!TIP]
>Evite usar caracteres especiales (`-` o `_`) como primer o último carácter en ningún nombre. Estos caracteres hacen que la mayoría de las reglas de validación produzcan un error.

::: zone-end

| Entidad | Ámbito | Length | Uso de mayúsculas y minúsculas | Caracteres válidos | Patrón sugerido | Ejemplo |
| --- | --- | --- | --- | --- | --- | --- |
|Resource group |Subscription |1-90 |No distingue mayúsculas de minúsculas |Alfanuméricos, carácter de subrayado, paréntesis, guión, punto (excepto al final) y caracteres Unicode |`<service short name>-<environment>-rg` |`profx-prod-rg` |
|Conjunto de disponibilidad |Resource group |1-80 |No distingue mayúsculas de minúsculas |Alfanuméricos, carácter de subrayado y guión |`<service-short-name>-<context>-as` |`profx-sql-as` |
|Etiqueta |Entidad asociada |512 (nombre), 256 (valor) |No distingue mayúsculas de minúsculas |Alfanuméricas |`"key" : "value"` |`"department" : "Central IT"` |

# <a name="resource-tagstabresourcetags"></a>[Etiquetas del recurso](#tab/ResourceTags)

Las etiquetas son útiles para identificar rápidamente los recursos y grupos de recursos. Se aplican etiquetas a los recursos de Azure para organizarlos de forma lógica por categorías. Cada etiqueta consta de un nombre y un valor. Por ejemplo, puede aplicar el nombre "Environment" y el valor "Production" a todos los recursos en producción. Las etiquetas deben incluir contexto sobre la carga de trabajo o aplicación asociada del recurso, los requisitos operativos y la información de propiedad.

Después de aplicar las etiquetas, puede recuperar todos los recursos de la suscripción que tengan ese nombre y valor de etiqueta. Al organizar recursos para facturación o administración, las etiquetas pueden ayudarle a recuperar recursos relacionados de distintos grupos de recursos.

También puede utilizar etiquetas para muchas otras cosas. Entre los usos comunes se incluyen:

- **Metadatos y documentación:** los administradores pueden ver fácilmente detalles sobre los recursos en los que están trabajando mediante la aplicación de una etiqueta, como "ProjectOwner".
- **Automation:** es posible que cuente con scripts que se ejecuten regularmente y que puedan realizar una acción basada en un valor de etiqueta como "ShutdownTime" o "DeprovisionDate".
- **Facturación:** Las etiquetas pueden aparecer en la factura. Puede usarlas para ayudar a segmentar la factura mediante etiquetas como "CostCenter" o "BillTo".

Cada recurso o grupo de recursos puede tener hasta 15 pares de nombre/valor de etiqueta. Esta limitación solo se aplica a las etiquetas que se aplican directamente al recurso o grupo de recursos.

Para obtener más recomendaciones y ejemplos de etiquetado, consulte la [guía sobre el etiquetado](../considerations/naming-and-tagging.md) del marco de adopción de la nube.

::: zone target="docs"

## <a name="apply-a-resource-tag"></a>Aplicación de una etiqueta de recurso

Para aplicar una etiqueta a un grupo de recursos:

1. Vaya a [Grupos de recursos](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fsubscriptions%2FresourceGroups).
1. Seleccione un grupo de recursos.
1. Seleccione **Asignar etiquetas**.
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
