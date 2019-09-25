---
title: Planeamiento de los requisitos previos de los servicios de administración de servidores de Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Herramientas y planeamiento de los requisitos previos de los servicios de administración de servidores de Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 17538d7c49278a00a5927b0110a2591a03d59e5c
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221467"
---
# <a name="phase-1-prerequisite-planning-for-azure-server-management-services"></a>Fase 1: Planeamiento de los requisitos previos de los servicios de administración de servidores de Azure

En esta fase, se familiarizará con el conjunto de servicios de administración de servidores de Azure y planeará la implementación de los recursos necesarios para implementar estas soluciones de administración.

## <a name="understand-the-tools-and-services"></a>Descripción de las herramientas y los servicios

Consulte [Herramientas y servicios de administración de servidores de Azure](./tools-services.md) para obtener información detallada de las áreas de administración que participan en las operaciones en curso de Azure, y los servicios y las herramientas de Azure que le ayudarán en estas áreas. Para cumplir los requisitos de administración será necesario usar varios de estos servicios. Nos referiremos a estas herramientas con frecuencia a lo largo de esta guía.

En las secciones siguientes se describen el planeamiento y la preparación necesarios para utilizar estas herramientas y los servicios.

## <a name="log-analytics-workspace-and-automation-account-planning"></a>Planeamiento del área de trabajo de Log Analytics y cuenta de Azure Automation

Muchos de los servicios que usará para incorporar los servicios de administración de Azure requieren un área de trabajo de Log Analytics y una cuenta de Azure Automation vinculada.

Un [área de trabajo de Log Analytics](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace) es un entorno único para almacenar los datos de registro de Azure Monitor. Cada área de trabajo tiene su propio repositorio y configuración de datos. Los orígenes de datos y las soluciones se configuran para almacenar sus datos en áreas de trabajo determinadas. Las soluciones de supervisión de Azure requieren que todos los servidores se conecten a un área de trabajo, para poder almacenar los datos de registro y obtener acceso a ellos.

Algunos de los servicios de administración requieren una cuenta de [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro). Con esta cuenta y las funcionalidades de Azure Automation, puede integrar los servicios de Azure y otros sistemas públicos para implementar, configurar y administrar los procesos de administración de servidores.

Los siguientes servicios de administración de servidores de Azure requieren un área de trabajo de Log Analytics vinculada y una cuenta de Automation:

- [Azure Update Management](https://docs.microsoft.com/azure/automation/automation-update-management)
- [Change Tracking e Inventario](https://docs.microsoft.com/azure/automation/change-tracking)
- [Trabajo híbrido de runbook](https://docs.microsoft.com/azure/automation/automation-hybrid-runbook-worker)
- [Desired State Configuration](https://docs.microsoft.com/azure/virtual-machines/extensions/dsc-overview)

La segunda fase de esta guía se centra en la implementación de los servicios y los scripts de automatización. Muestra cómo crear un área de trabajo de Log Analytics y una cuenta de Azure Automation. En esta guía también se muestra cómo usar Azure Policy para asegurarse de que las nuevas máquinas virtuales estén conectadas al área de trabajo correcta.

Los ejemplos que se describen en esta guía dan por hecho que hay una implementación que aún no tiene servidores implementados en la nube. Para más información sobre los principios y las consideraciones que conlleva el planeamiento de las áreas de trabajo, consulte [Administración de los datos de registro y las áreas de trabajo en Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access).

## <a name="planning-considerations"></a>Consideraciones de planeación

Al preparar las áreas de trabajo y las cuentas que cree para incorporar los servicios de administración, consulte las siguientes discusiones de problemas:

- **Zonas geográficas de Azure y cumplimiento normativo**. Las regiones de Azure se organizan por *zonas geográficas*. Una [zona geográfica de Azure](https://azure.microsoft.com/global-infrastructure/geographies) garantiza que se cumplan los requisitos de residencia, soberanía, cumplimiento normativo y resistencia de los datos dentro de las fronteras geográficas. Si las cargas de trabajo están sujetas a la soberanía de datos u otros requisitos de cumplimiento, las cuentas de Azure Automation y el área de trabajo deben implementarse en regiones dentro de la misma ubicación geográfica de Azure que los recursos de la carga de trabajo a los que corresponden.
- **Número de áreas de trabajo**. Como regla general, cree el número mínimo de áreas de trabajo necesarias por ubicación geográfica de Azure. Se recomienda al menos un área de trabajo para cada zona geográfica de Azure donde se encuentren los recursos de proceso o almacenamiento. Esta alineación inicial ayuda a evitar problemas normativos futuros al migrar datos a zonas geográficas diferentes.
- **Límite y retención de los datos**. También es posible que deba tener en cuenta las directivas de retención de datos o los requisitos de límite de datos al crear áreas de trabajo o cuentas de Azure Automation. Para más información sobre los principios y las consideraciones adicionales que conlleva el planeamiento de las áreas de trabajo, consulte [Administración de los datos de registro y las áreas de trabajo en Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/manage-access).
- **Asignación de región**. Solo se puede vincular un área de trabajo de Log Analytics y una cuenta de Azure Automation entre determinadas regiones de Azure. Por ejemplo, si el área de trabajo de Log Analytics se hospeda en la región *EastUS*, la cuenta de Azure Automation vinculada se debe crear en la región *EastUS2* para poder usarse con los servicios de administración. Si tiene una cuenta de Azure Automation creada en otra región, no podrá vincularla a un área de trabajo en *EastUS*. La elección de la región de implementación puede afectar significativamente a los requisitos de zona geográfica de Azure. Consulte la [tabla de asignación de regiones](https://docs.microsoft.com/azure/automation/how-to/region-mappings) para decidir qué región debe hospedar las áreas de trabajo y las cuentas de Automation.
- **Hospedaje múltiple de áreas de trabajo**. El agente de Log Analytics admite el hospedaje múltiple en algunos escenarios, pero esta configuración presenta varias limitaciones y problemas. A menos que Microsoft recomiende usar el hospedaje múltiple para su escenario, no se recomienda configurarlo en el agente de Log Analytics.

## <a name="resource-placement-examples"></a>Ejemplos de ubicación de recursos

Hay varios modelos diferentes para elegir la suscripción en la que se colocan el área de trabajo de Log Analytics y la cuenta de Automation. En resumen, debe colocar el área de trabajo y la cuenta de Automation en una suscripción que sea propiedad del equipo responsable de la implementación de los servicios Update Management y Change Tracking e Inventario.

En los ejemplos siguientes se muestran algunas formas en las que se pueden implementar las áreas de trabajo y las cuentas de Automation.

### <a name="placement-by-geography"></a>Ubicación por zona geográfica

En el caso de entornos pequeños y medianos con una sola suscripción y varios cientos de recursos que abarcan varias ubicaciones geográficas de Azure, cree un área de trabajo de Log Analytics y una cuenta de Azure Automation en cada zona geográfica.

Puede crear un área de trabajo y una cuenta de Azure Automation (un par) en cada grupo de recursos, e implementar el par en la zona geográfica correspondiente a las máquinas virtuales. Como alternativa, si las directivas de cumplimiento de datos no dictan que los recursos residan en regiones específicas, puede crear un par para administrar todas las máquinas virtuales. También se recomienda colocar los pares de área de trabajo y cuenta de Automation en grupos de recursos independientes para proporcionar un control de acceso basado en rol (RBAC) más detallado.

El ejemplo del diagrama siguiente tiene una suscripción con dos grupos de recursos, cada uno de los cuales se encuentra en una zona geográfica diferente.

![Modelo de área de trabajo para entornos pequeños a medianos](./media/workspace-model-small.png)

### <a name="placement-in-a-management-subscription"></a>Ubicación en una suscripción de administración

En entornos de mayor tamaño que abarquen varias suscripciones y que tengan un departamento de TI central que sea responsable de la supervisión y el cumplimiento, cree pares de áreas de trabajo y cuentas de Automation en una suscripción de administración de TI. En este modelo, los recursos de máquina virtual situados en una zona geográfica almacenan sus datos en el área de trabajo de la zona geográfica correspondiente, en la suscripción de administración de TI. Los equipos de aplicaciones que necesitan ejecutar tareas de automatización, pero que no requieren un área de trabajo vinculada ni cuentas de Automation, pueden crear cuentas de Automation independientes en sus propias suscripciones de aplicación.

![Modelo de área de trabajo para entornos de gran tamaño](./media/workspace-model-large.png)

### <a name="decentralized-placement"></a>Ubicación descentralizada

En un modelo alternativo para entornos de gran tamaño, la responsabilidad de la administración y aplicación de revisiones puede recaer en el equipo de desarrollo de aplicaciones. En este caso, debe colocar los pares de área de trabajo y cuentas de Automation en las suscripciones del equipo de aplicaciones, junto con los demás recursos.

  ![Modelo de cuenta de área de trabajo para entornos descentralizados](./media/workspace-model-decentralized.png)

## <a name="create-a-workspace-and-automation-account"></a>Creación de un área de trabajo y una cuenta de Automation

Después de decidir cómo ubicar y organizar los pares de área de trabajo y cuenta, deberá asegurarse de crear estos recursos antes de iniciar el proceso de incorporación. En los ejemplos de automatización que se incluyen más adelante en esta guía se crea un par de área de trabajo y cuenta de Automation. Sin embargo, si aún no tiene un par de área de trabajo y cuenta de Automation, tendrá que crear uno si desea realizar la incorporación mediante el portal.

Para crear un área de trabajo de Log Analytics en Azure Portal, consulte [Creación de un área de trabajo](https://docs.microsoft.com/azure/azure-monitor/learn/quick-create-workspace#create-a-workspace). A continuación, cree la cuenta de Automation correspondiente a cada área de trabajo siguiendo los pasos descritos en [Creación de una cuenta de Azure Automation](https://docs.microsoft.com/azure/automation/automation-quickstart-create-account).

> [!NOTE]
> Al crear una cuenta de Automation mediante Azure Portal, el comportamiento predeterminado es intentar crear cuentas de ejecución para los recursos de Azure Resource Manager y el modelo de implementación clásica. Si no tiene máquinas virtuales clásicas en su entorno y no es coadministrador de la suscripción, el portal creará una cuenta de ejecución para Resource Manager, pero generará un error al implementar la cuenta de ejecución clásica. Si no desea admitir recursos clásicos, puede omitir este error.
>
> También puede crear una cuenta de ejecución con [PowerShell](https://docs.microsoft.com/azure/automation/manage-runas-account#create-run-as-account-using-powershell).

## <a name="next-steps"></a>Pasos siguientes

Aprenda cómo [incorporar sus servidores](./onboarding-overview.md) a los servicios de administración de Azure.

> [!div class="nextstepaction"]
> [Incorporación a los servicios de administración de servidores de Azure](./onboarding-overview.md)
