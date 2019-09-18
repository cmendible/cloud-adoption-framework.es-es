---
title: Habilitar los servicios de administración en una única máquina virtual para su evaluación
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Habilitar los servicios de administración en una única máquina virtual para su evaluación
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: e9d5e17e87d79d8d1fdf7239298a973959103a37
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031897"
---
# <a name="enable-management-services-on-a-single-vm-for-evaluation"></a>Habilitar los servicios de administración en una única máquina virtual para su evaluación

Obtenga información sobre cómo habilitar los servicios de administración en una única máquina virtual para su evaluación.

> [!NOTE]
> Cree el [área de trabajo de Log Analytics y la cuenta de Azure Automation](./prerequisites.md#create-a-workspace-and-automation-account) necesarias antes de incorporar máquinas virtuales a los servicios de administración de Azure.

La incorporación de máquinas virtuales individuales a los servicios de administración de servidores de Azure es sencilla en Azure Portal. El portal le permite familiarizarse con estos servicios antes de incorporarlos a las máquinas virtuales. Al seleccionar una instancia de máquina virtual, todas las soluciones que se describen en la lista de [herramientas y servicios de administración](./tools-services.md) aparecen en el menú **Operaciones** o en el menú **Supervisión**. Puede seleccionar cada solución y seguir el asistente para incorporarla.

![Captura de pantalla de configuración de máquina virtual en Azure Portal](./media/onboarding-single-vm.png)

## <a name="related-resources"></a>Recursos relacionados

Para más información acerca de la incorporación de máquinas virtuales individuales a cada solución, consulte:

- [Incorporación de las soluciones Update Management, Change Tracking e Inventario desde una máquina virtual de Azure](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-vm)
- [Incorporar Azure Monitor para VM](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-single-vm)

## <a name="next-steps"></a>Pasos siguientes

Aprenda a usar Azure Policy para incorporar máquinas virtuales de Azure a escala.

> [!div class="nextstepaction"]
> [Configuración de servicios de administración de Azure para una suscripción](./onboard-at-scale.md)
