---
title: Gobernanza, seguridad y cumplimiento en Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Aprenda a configurar la gobernanza, seguridad y cumplimiento para el entorno de Azure.
author: tvuylsteke
ms.author: kfollis
ms.date: 09/27/2019
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: fasttrack-edit, AQC
ms.localizationpriority: high
ms.openlocfilehash: b94c1cac96fa5458c722d0a66e1ef2dac9d167f9
ms.sourcegitcommit: 1dccf1aed8e98aa0f58c4f86d90c65f5fa5ac84d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2019
ms.locfileid: "71804483"
---
# <a name="governance-security-and-compliance-in-azure"></a>Gobernanza, seguridad y cumplimiento en Azure

A medida que se establece la directiva corporativa y se planean las estrategias de gobierno, se pueden usar herramientas y servicios como Azure Policy, Azure Blueprints y Azure Security Center para aplicar y automatizar las decisiones de gobierno de su organización. Antes de empezar a planear el gobierno, use la [herramienta de banco de pruebas comparativas de gobierno](https://cafbaseline.com) para identificar posibles brechas en el enfoque del gobierno en la nube de su organización. Para obtener más información sobre cómo desarrollar procesos de gobierno, consulte la [guía de gobernanza de la plataforma de adopción de la nube para Azure](../../govern/index.md).

# <a name="azure-blueprintstabazureblueprints"></a>[Azure Blueprints](#tab/AzureBlueprints)

Azure Blueprints permite a los arquitectos de nube y grupos de TI central definir un conjunto repetible de recursos de Azure que implementa y cumple los estándares, patrones y requisitos de la organización. Azure Blueprints permite a los equipos de desarrollo aprovisionar y crear rápidamente nuevos entornos sabiendo que se crean cumpliendo los estándares organizativos y que contienen un conjunto de componentes integrados, como las redes, para acelerar el desarrollo y la entrega.

Los planos técnicos son una manera declarativa de organizar la implementación de varias plantillas de recursos y de otros artefactos, como son:

- Asignaciones de roles.
- Asignaciones de directivas.
- Plantillas de Azure Resource Manager.
- Grupos de recursos.

## <a name="create-a-blueprint"></a>Creación de un plano técnico

Para crear un plano técnico, realice el siguiente procedimiento:

::: zone target="chromeless"

1. Vaya a **Introducción a planos técnicos**.
1. En la sección **Crear un plano técnico**, seleccione **Crear**.
1. Filtre la lista Planos técnicos para seleccionar el plano técnico adecuado.
1. Escriba el **Nombre del plano técnico** y seleccione la **Ubicación de definición** adecuada.
1. Haga clic en **Siguiente: Artefactos >>** y revise los artefactos incluidos en el plano técnico.
1. Haga clic en **Guardar borrador**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted]" submitText="Create a blueprint" :::

::: zone-end

::: zone target="docs"

1. Vaya a [Introducción a planos técnicos](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/GetStarted).
1. En la sección **Crear un plano técnico**, seleccione **Crear**.
1. Filtre la lista Planos técnicos para seleccionar el plano técnico adecuado.
1. Escriba el **Nombre del plano técnico** y seleccione la **Ubicación de definición** adecuada.
1. Haga clic en **Siguiente: Artefactos >>** y revise los artefactos incluidos en el plano técnico.
1. Haga clic en **Guardar borrador**.

::: zone-end

## <a name="publish-a-blueprint"></a>Publicación de un plano técnico

Para publicar artefactos de un plano técnico en su suscripción:

::: zone target="chromeless"

1. Vaya a **Planos técnicos - Definiciones del plano técnico**.
1. Seleccione el plano técnico que creó en los pasos anteriores.
1. Revise la definición del plano técnico y seleccione **Publicar plano técnico**.
1. Proporcione una **versión** (por ejemplo, _1.0_) y **notas de cambios** y, después, seleccione **Publicar**.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints]" submitText="Blueprint definitions" :::

::: zone-end

::: zone target="docs"

1. Vaya a [Planos técnicos - Definiciones del plano técnico](https://portal.azure.com/#blade/Microsoft_Azure_Policy/BlueprintsMenuBlade/Blueprints).
1. Seleccione la definición del plano técnico que creó en los pasos anteriores.
1. Revise la definición del plano técnico y seleccione **Publicar plano técnico**.
1. Proporcione una **versión** (por ejemplo, _1.0_) y **notas de cambios** y, después, seleccione **Publicar**.

::: zone-end

::: zone target="docs"

## <a name="learn-more"></a>Más información

Para obtener más información, consulte:

- [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints)
- [Plataforma de adopción de la nube: Guía de decisiones de la coherencia de recursos](../../decision-guides/resource-consistency/index.md)
- [Ejemplos de planos técnicos basados en estándares](/azure/governance/blueprints/samples/index#standards-based-blueprint-samples)

::: zone-end

# <a name="azure-policytabazurepolicy"></a>[Azure Policy](#tab/AzurePolicy)

Azure Policy es un servicio que se usa para crear, asignar y administrar directivas. Dichas directivas aplican reglas a los recursos, con el fin de que estos sigan siendo compatibles con los estándares corporativos y los Acuerdos de Nivel de Servicio. Azure Policy escanea los recursos para identificar aquellos que no son compatibles con las directivas que implementa. Por ejemplo, puede haber una directiva que permita solo un tamaño de máquina virtual concreto para ejecutar en el entorno. Cuando implemente esta directiva, esta evaluará las máquinas virtuales existentes que se ejecutan en el entorno y cualquier nueva máquina virtual que se implemente. La evaluación de directivas genera eventos de cumplimiento para que se utilicen para la supervisión y los informes.

Tenga en cuenta las directivas comunes para:

- Aplicación del etiquetado para recursos y grupos de recursos.
- Restricción de las regiones para los recursos implementados.
- Restricción de SKU costosas para recursos específicos.
- Adición del uso de características opcionales importantes como discos administrados de Azure.

::: zone target="chromeless"

## <a name="action"></a>.

Asigne una directiva integrada a un grupo de administración, suscripción o grupo de recursos.

::: form action="OpenBlade[#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted]" submitText="Assign Policy" :::

::: zone-end

::: zone target="docs"

## <a name="apply-a-policy"></a>Aplicación de una directiva

Para aplicar una directiva a un grupo de recursos:

1. Vaya a [Azure Policy](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyMenuBlade/GettingStarted).
1. Seleccione **Asignar una directiva**.

## <a name="learn-more"></a>Más información

Para obtener más información, consulte:

- [Azure Policy](https://docs.microsoft.com/azure/azure-policy)
- [Plataforma de adopción de la nube: Guía de decisiones sobre el cumplimiento de directivas](../../decision-guides/policy-enforcement/index.md)

::: zone-end

# <a name="azure-security-centertabazuresecuritycenter"></a>[Azure Security Center](#tab/AzureSecurityCenter)

Azure Security Center desempeña un papel importante en su estrategia de gobernanza. Le ayuda a conocer la información más reciente sobre seguridad, ya que:

- Proporciona una vista unificada de seguridad en las cargas de trabajo.
- Recopila, busca y analiza datos de seguridad de una gran variedad de orígenes, incluidos firewalls y otras soluciones de asociados.
- Proporciona recomendaciones de seguridad prácticas para solucionar los problemas antes de que puedan aprovecharlos.
- Se puede usar para aplicar directivas de seguridad en las cargas de trabajo de nube híbrida para garantizar el cumplimiento con los estándares de seguridad.

Muchas de las características de seguridad, como la directiva de seguridad y las recomendaciones, están disponibles gratis. Algunas de las características más avanzadas, como el acceso a la máquina virtual Just-in-Time y la compatibilidad con cargas de trabajo híbridas, están disponibles en el nivel estándar de Security Center. El acceso a la máquina virtual Just-in-Time puede ayudar a reducir la superficie expuesta a ataques de la red al controlar el acceso a los puertos de administración en las máquinas virtuales de Azure.

> [!TIP]
> Azure Security Center está habilitado de forma predeterminada en todas las suscripciones. Le recomendamos habilitar la recopilación de datos de máquinas virtuales para permitir que Azure Security Center instale su agente y empiece a recopilar datos.

::: zone target="docs"

Para explorar Azure Security Center, vaya a [Azure Portal](https://portal.azure.com/#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0).

## <a name="learn-more"></a>Más información

Para obtener más información, consulte:

- [Azure Security Center](https://docs.microsoft.com/azure/security-center)
- [Acceso de máquina virtual Just-In-Time](https://docs.microsoft.com/azure/security-center/security-center-just-in-time#how-does-just-in-time-access-work)
- [Plan de tarifa Estándar y Gratis](https://azure.microsoft.com/pricing/details/security-center)
- [Plataforma de adopción de la nube: Materia sobre gobierno de línea de base de seguridad](../../govern/security-baseline/index.md)

::: zone-end

::: zone target="chromeless"

## <a name="action"></a>.

::: form action="OpenBlade[#blade/Microsoft_Azure_Security/SecurityMenuBlade/SecurityMenuBlade/0]" submitText="Explore Azure Security Center" :::

::: zone-end
