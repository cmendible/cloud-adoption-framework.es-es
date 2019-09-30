---
title: Automatizar la incorporación y la configuración de alertas
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Automatizar la incorporación y la configuración de alertas
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 242c8a1a054507c3b1134b1126ea95e3ead74d84
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221378"
---
# <a name="automate-onboarding"></a>Automatizar la incorporación

Para mejorar la eficacia de la implementación de los servicios de administración de servidores de Azure, considere la posibilidad de automatizar la implementación de servicios de administración siguiendo las recomendaciones descritas en las secciones anteriores de esta guía. El script y las plantillas de ejemplo que se proporcionan en las siguientes secciones son puntos de partida para desarrollar su propia automatización de procesos de incorporación.

## <a name="onboarding-by-using-automation"></a>Incorporación mediante Automation

Esta guía incluye un repositorio de código de ejemplo de GitHub de apoyo, [CloudAdoptionFramework](https://aka.ms/caf/manage/automation-samples), que proporciona scripts y plantillas de Azure Resource Manager de ejemplo con los que será más fácil automatizar la implementación de los servicios de administración de servidores de Azure.

En estos archivos de ejemplo se muestra cómo usar los cmdlets de Azure PowerShell para automatizar estas tareas:

1. Crear un [área de trabajo de Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access) (o usar un área de trabajo existente si cumple los requisitos; vea [Planeamiento de áreas de trabajo](./prerequisites.md#log-analytics-workspace-and-automation-account-planning)).

2. Crear una cuenta de Automation (o usar una cuenta existente si cumple los requisitos; vea [Planeamiento de áreas de trabajo](./prerequisites.md#log-analytics-workspace-and-automation-account-planning)).

3. Vincular la cuenta de Automation y el área de trabajo de Log Analytics (no es necesario si se incorpora a través del portal).

4. Habilitar Update Management y Change Tracking e inventario para el área de trabajo.

5. Incorporar máquinas virtuales de Azure mediante Azure Policy (una directiva instala Dependency Agent y el agente de Log Analytics en las máquinas virtuales de Azure).

6. Incorporar los servidores locales mediante la instalación del agente de Log Analytics en ellos.

Los archivos descritos en esta tabla se usan en este ejemplo y puede personalizarlos para que admitan sus propios escenarios de implementación.

| Nombre de archivo | DESCRIPCIÓN |
|-----------|-------------|
| New-AMSDeployment.ps1 | Script de orquestación principal que automatiza la incorporación. Este script de PowerShell necesita una suscripción existente, pero creará grupos de recursos, ubicaciones, áreas de trabajo y cuentas de Automation si no existen. |
| Workspace-AutomationAccount.json | Plantilla de Resource Manager que implementa el área de trabajo y los recursos de la cuenta de Automation. |
| WorkspaceSolutions.json | Plantilla de Resource Manager que habilita las soluciones que quiera en el área de trabajo de Log Analytics. |
| ScopeConfig.json | Plantilla de Resource Manager que usa el modelo de participación para servidores locales con la solución Change Tracking. El uso del modelo de participación es opcional. |
| Enable-VMInsightsPerfCounters.ps1 | Script de PowerShell que habilita VMInsight para los servidores y configura los contadores de rendimiento. |
| ChangeTracking-Filelist.json | Plantilla de Resource Manager que define la lista de archivos que se supervisarán mediante Change Tracking. |

Puede ejecutar New-AMSDeployment.ps1 con este comando:

```powershell
.\New-AMSDeployment.ps1 -SubscriptionName '{Subscription Name}' -WorkspaceName '{Workspace Name}' -WorkspaceLocation '{Azure Location}' -AutomationAccountName {Account Name} -AutomationAccountLocation {Account Location}
```

## <a name="next-steps"></a>Pasos siguientes

Aprenda a configurar alertas básicas para informar al equipo de problemas y eventos de administración esenciales.

> [!div class="nextstepaction"]
> [Configuración de alertas básicas](./setup-alerts.md)
