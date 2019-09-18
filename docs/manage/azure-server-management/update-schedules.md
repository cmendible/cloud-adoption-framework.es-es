---
title: Creación de programaciones de actualizaciones
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Creación de programaciones de actualizaciones
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: a7a0212f3fa4ceda5d02fadaee70c4f50bd04fd3
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032228"
---
# <a name="create-update-schedules"></a>Creación de programaciones de actualizaciones

Puede administrar las programaciones de actualizaciones mediante Azure Portal o con los nuevos módulos de cmdlet de PowerShell.

Para crear una programación de actualización mediante Azure Portal, consulte [Programación de una implementación de actualizaciones](https://docs.microsoft.com/azure/automation/automation-tutorial-update-management#schedule-an-update-deployment).

El módulo Az.Automation ahora admite la configuración de la administración de actualizaciones mediante Azure PowerShell. La [versión 1.7.0](https://www.powershellgallery.com/packages/Az/1.7.0) del módulo agrega compatibilidad con el cmdlet [New-AzAutomationUpdateManagementAzureQuery](/powershell/module/az.automation/new-azautomationupdatemanagementazurequery?view=azps-1.7.0), que permite usar etiquetas, ubicaciones y búsquedas guardadas para configurar programaciones de actualizaciones para un grupo flexible de equipos.

## <a name="example-script"></a>Script de ejemplo

En el siguiente script de ejemplo se muestra el uso del etiquetado y la consulta para crear grupos dinámicos de equipos en los que se pueden aplicar programaciones de actualización. Realiza las siguientes acciones. Puede hacer referencia a las implementaciones de acciones específicas cuando cree sus propios scripts.

- Crea una programación de actualización de Azure Automation que se ejecuta todos los sábados a las 8:00 a.m.
- Crea una consulta para los equipos que coinciden con estos criterios:
  - Se ha implementado en las ubicaciones de Azure `westus`, `eastus` o `eastus2`.
  - Tiene aplicada una etiqueta `Owner` con un valor establecido en `JaneSmith`.
  - Tiene aplicada una etiqueta `Production` con un valor establecido en `true`.
- Aplica la programación de actualización a los equipos consultados y establece una ventana de actualización de dos horas.

Antes de ejecutar este script de ejemplo, debe iniciar sesión con el cmdlet [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount?view=azps-2.1.0). Al iniciar el script, deberá proporcionar la siguiente información:

- Identificador de la suscripción de destino
- Grupo de recursos de destino
- Nombre del área de trabajo de Log Analytics
- Nombre de la cuenta de Azure Automation

```powershell
<#
    .SYNOPSIS
        This script orchestrates the deployment of the solutions and the agents.
    .Parameter SubscriptionName
    .Parameter WorkspaceName
    .Parameter AutomationAccountName
    .Parameter ResourceGroupName

#>

param (
    [Parameter(Mandatory=$true)]
    [string]$SubscriptionId,

    [Parameter(Mandatory=$true)]
    [string]$ResourceGroupName,

    [Parameter(Mandatory=$true)]
    [string]$WorkspaceName,

    [Parameter(Mandatory=$true)]
    [string]$AutomationAccountName,

    [Parameter(Mandatory=$false)]
    [string]$scheduleName = "SaturdayCritialSecurity"
)

Import-Module Az.Automation

$startTime = ([DateTime]::Now).AddMinutes(10)
$schedule = New-AzAutomationSchedule -ResourceGroupName $ResourceGroupName `
                                     -AutomationAccountName $AutomationAccountName `
                                     -StartTime $startTime `
                                     -Name $scheduleName `
                                     -Description "Saturday patches" `
                                     -DaysOfWeek Saturday `
                                     -WeekInterval 1 `
                                     -ForUpdateConfiguration

# Using AzAutomationUpdateManagementAzureQuery to create dynamic groups.

$queryScope = @("/subscriptions/$SubscriptionID/resourceGroups/")

$query1Location =@("westus", "eastus", "eastus2")
$query1FilterOperator = "Any"
$ownerTag = @{"Owner"= @("JaneSmith")}
$ownerTag.add("Production", "true")

$DGQuery = New-AzAutomationUpdateManagementAzureQuery -ResourceGroupName $ResourceGroupName `
                                       -AutomationAccountName $AutomationAccountName `
                                       -Scope $queryScope `
                                       -Tag $ownerTag

$AzureQueries = @($DGQuery)

$UpdateConfig = New-AzAutomationSoftwareUpdateConfiguration -ResourceGroupName $ResourceGroupName `
                                                             -AutomationAccountName $AutomationAccountName `
                                                             -Schedule $schedule `
                                                             -Windows `
                                                             -Duration (New-TimeSpan -Hours 2) `
                                                             -AzureQuery $AzureQueries `
                                                             -IncludedUpdateClassification Security,Critical
```

## <a name="next-steps"></a>Pasos siguientes

Consulte ejemplos de cómo implementar [directivas comunes en Azure](./common-policies.md) que pueden ayudar a administrar los servidores.

> [!div class="nextstepaction"]
> [Directivas habituales en Azure](./common-policies.md)
