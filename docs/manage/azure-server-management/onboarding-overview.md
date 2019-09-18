---
title: Incorporación a los servicios de administración de servidores de Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Incorporación a los servicios de administración de servidores de Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 330e297b4fb63eaa376e8b6dac0ccf77c2a16ef4
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031618"
---
# <a name="phase-2-onboarding-azure-server-management-services"></a>Fase 2: Incorporación a los servicios de administración de servidores de Azure

Cuando esté familiarizado con las [herramientas](./tools-services.md) y el [planeamiento](./prerequisites.md) implicados en los servicios de administración de Azure, estará listo para la segunda fase, que proporciona instrucciones paso a paso para la incorporación de estos servicios para su uso con sus recursos de Azure. Empiece por evaluar este proceso de incorporación antes de adoptarlo ampliamente en su entorno.

> [!NOTE]
> Los enfoques de automatización descritos en secciones posteriores de esta guía se orientan a implementaciones que aún no tienen servidores implementados en la nube. Estos enfoques requieren que tenga el rol de propietario en una suscripción para crear todos los recursos y directivas necesarios. Si ya ha creado recursos de área de trabajo de Log Analytics y de cuenta de Automation, se recomienda que pase estos recursos en los parámetros adecuados al iniciar los scripts de automatización de ejemplo.

## <a name="onboarding-processes"></a>Procesos de incorporación

En esta sección de la guía se tratan los siguientes procesos de incorporación tanto para máquinas virtuales de Azure como para servidores locales:

- **Habilitar los servicios de administración en una única máquina virtual para su evaluación con el portal**. Utilice este proceso para familiarizarse con los servicios de administración de servidores de Azure.
- **Configuración de servicios de administración para una suscripción con el portal**. Este proceso le ayuda a configurar el entorno de Azure para que las nuevas máquinas virtuales que se aprovisionan usen automáticamente los servicios de administración. Use este enfoque si prefiere la experiencia de Azure Portal a scripts y líneas de comandos.
- **Configuración de servicios de administración para una suscripción con Azure Automation**. Este proceso está totalmente automatizado. Solo tiene que crear una suscripción y los scripts configurarán el entorno para usar los servicios de administración para cualquier máquina virtual que se haya aprovisionado recientemente. Use este enfoque si está familiarizado con los scripts de PowerShell y las plantillas de Azure Resource Manager, o si desea aprender a usarlos.

Los procedimientos para cada uno de estos enfoques son diferentes.

> [!NOTE]
> La secuencia de pasos de incorporación al usar Azure Portal difiere de los pasos de incorporación automatizados, ya que el portal ofrece una experiencia de incorporación más sencilla.

En el diagrama siguiente se muestra el modelo de implementación recomendado para los servicios de administración. 

![Diagrama del modelo de implementación recomendado](./media/recommended-deployment.png)

> [!NOTE]
> Como se muestra en el diagrama anterior, el agente de Log Analytics tiene una configuración de *inscripción automática* y otra *opcional* para los servidores locales. *Inscripción automática* significa que cuando el agente de Log Analytics se instala en un servidor y se configura para conectarse a un área de trabajo, las soluciones habilitadas en esa área de trabajo se aplicarán automáticamente al servidor. *Opcional* significa que, aunque el agente esté instalado y conectado al área de trabajo, la solución no se aplicará a menos que se agregue a la configuración de ámbito del servidor en el área de trabajo.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información sobre cómo incorporar una única máquina virtual mediante el portal para evaluar el proceso de incorporación.

> [!div class="nextstepaction"]
> [Incorporación de una única máquina virtual de Azure para su evaluación](./onboard-single-vm.md)
