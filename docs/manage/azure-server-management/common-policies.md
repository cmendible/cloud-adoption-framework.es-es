---
title: Ejemplos comunes de Azure Policy
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ejemplos comunes de Azure Policy
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 9eee6f81922c88304c0ca5bf7edd6572daf493d8
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031616"
---
# <a name="common-azure-policy-examples"></a>Ejemplos comunes de Azure Policy

[Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) permite aplicar la gobernanza a los recursos en la nube. Con este servicio es más fácil crear barreras que garanticen que toda la compañía cumple los requisitos de la directiva de gobierno. Para crear directivas, use los cmdlets de PowerShell o Azure Portal. En este artículo se proporcionan ejemplos de cmdlets de PowerShell.

> [!NOTE]
> Con Azure Policy, las directivas de cumplimiento (**deployIfNotExists**) no se implementan automáticamente en las máquinas virtuales existentes. Es necesario corregirlo para mantener estas máquinas virtuales en cumplimiento. Para más información, vea [Corregir los recursos no conformes con Azure Policy](https://docs.microsoft.com/azure/governance/policy/how-to/remediate-resources).

## <a name="common-policy-examples"></a>Ejemplos de directivas comunes

En estas secciones se describen algunas de las directivas más comunes.

### <a name="restrict-resource-regions"></a>Restricción de regiones de recursos

La regulación y el cumplimiento de directivas a menudo dependerán del control de la ubicación física en la que se implementan los recursos. Puede usar una directiva integrada para permitir que los usuarios creen recursos solo en regiones de Azure de la lista blanca. Encontrará esta directiva en el portal si busca "ubicación" en la página de definición de directivas.

También puede ejecutar este cmdlet para encontrar la directiva:

```powershell
Get-AzPolicyDefinition | Where-Object { ($_.Properties.policyType -eq "BuiltIn") -and ($_.Properties.displayName -like "*location*") }
```

El siguiente script muestra cómo asignar la directiva. Para usarlo, cambie el valor `$SubscriptionID` para que apunte a la suscripción a la que quiere asignar la directiva. Antes de ejecutar el script, debe iniciar sesión con el cmdlet [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0).

```powershell
#Specify the value for $SubscriptionID.
$SubscriptionID = <subscription ID>
$scope = "/subscriptions/$SubscriptionID"

#Replace the -Name GUID with the policy GUID you want to assign.
$AllowedLocationPolicy = Get-AzPolicyDefinition -Name "e56962a6-4747-49cd-b67b-bf8b01975c4c"

#Replace the locations with the ones you want to specify.
$policyParam = '{"listOfAllowedLocations":{"value":["eastus","westus"]}}'
New-AzPolicyAssignment -Name "Allowed Location" -DisplayName "Allowed locations for resource creation" -Scope $scope -PolicyDefinition $AllowedLocationPolicy -Location eastus -PolicyParameter $policyparam
```

Puede usar este mismo script para aplicar las otras directivas que se describen en este artículo. Solo tiene que reemplazar el GUID de la línea que establece `$AllowedLocationPolicy` con el GUID de la directiva que quiere aplicar.

### <a name="block-certain-resource-types"></a>Bloquear determinados tipos de recursos

Otra directiva integrada común que se usa para controlar los costos permite bloquear determinados tipos de recursos. Encontrará esta directiva en el portal si busca "tipos de recursos permitidos" en la página de definición de directivas.

También puede ejecutar este cmdlet para encontrar la directiva:

```powershell
Get-AzPolicyDefinition | Where-Object { ($_.Properties.policyType -eq "BuiltIn") -and ($_.Properties.displayName -like "*allowed resource types") }
```

Después de identificar la directiva que quiere usar, puede modificar el ejemplo de PowerShell en la sección [Restringir regiones de recursos](#restrict-resource-regions) para asignar la directiva.

### <a name="restrict-vm-size"></a>Restringir tamaño de máquina virtual

Azure ofrece una amplia gama de tamaños de máquina virtual para admitir varios tipos de cargas de trabajo. Para controlar el presupuesto, puede crear una directiva que permita solamente un subconjunto de tamaños de máquina virtual en las suscripciones.

### <a name="deploy-antimalware"></a>Implementar antimalware

Puede usar esta directiva para implementar una extensión de Microsoft IaaSAntimalware con una configuración predeterminada en las máquinas virtuales que no están protegidas por antimalware.

El GUID de la directiva es `2835b622-407b-4114-9198-6f7064cbe0dc`.

El siguiente script muestra cómo asignar la directiva. Para usarlo, cambie el valor `$SubscriptionID` para que apunte a la suscripción a la que quiere asignar la directiva. Antes de ejecutar el script, debe iniciar sesión con el cmdlet [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0).

```powershell
#Specify the value for $SubscriptionID.
$SubscriptionID = <subscription ID>
$scope = "/subscriptions/$SubscriptionID"

$AntimalwarePolicy = Get-AzPolicyDefinition -Name "2835b622-407b-4114-9198-6f7064cbe0dc"

#Replace location “eastus” with the value you want to use.
New-AzPolicyAssignment -Name "Deploy Antimalware" -DisplayName "Deploy default Microsoft IaaSAntimalware extension for Windows Server" -Scope $scope -PolicyDefinition $AntimalwarePolicy -Location eastus –AssignIdentity

```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información sobre otros servicios y herramientas de administración de servidores que hay disponibles.

> [!div class="nextstepaction"]
> [Servicios y herramientas de administración de servidores de Azure](./tools-services.md)
