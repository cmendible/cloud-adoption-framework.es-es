---
title: Configuración de servicios de administración de Azure para una suscripción
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Configuración de servicios de administración de Azure para una suscripción
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: a5b1d551f52ae8800e9a29d4c8a92c14965645cc
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221498"
---
# <a name="configure-azure-management-services-at-scale"></a>Configuración de servicios de administración de Azure a escala

La incorporación de los servicios de administración de Azure a los servidores implica dos tareas: la implementación de agentes de servicio en los servidores y la habilitación de las soluciones de administración. En este artículo se tratan los siguientes procesos que le permitirán realizar estas tareas:

- [Implementación de los agentes necesarios en máquinas virtuales de Azure con Azure Policy](#deploy-extensions-to-azure-vms-using-azure-policy)
- [Implementación de los agentes necesarios en servidores locales](#install-required-agents-on-on-premises-servers)
- [Habilitación y configuración de soluciones](#enable-and-configure-solutions)

> [!NOTE]
> Cree el [área de trabajo de Log Analytics y la cuenta de Azure Automation](./prerequisites.md#create-a-workspace-and-automation-account) necesarias antes de incorporar máquinas virtuales a los servicios de administración de Azure.

## <a name="deploy-extensions-to-azure-vms-using-azure-policy"></a>Implementación de extensiones en máquinas virtuales de Azure con Azure Policy

Todas las soluciones de administración descritas en el artículo sobre [servicios y herramientas de administración de Azure](./tools-services.md) requieren que el agente de Log Analytics se instale en máquinas virtuales (VM) de Azure y en servidores locales. Puede incorporar sus máquinas virtuales de Azure a escala mediante Azure Policy. Asigne una directiva para asegurarse de que el agente se instala en todas las máquinas virtuales de Azure y se conecta al área de trabajo de Log Analytics correcta.

Azure Policy tiene una [iniciativa de directiva](/azure/governance/policy/index#initiative-definition) integrada que incluye el agente de Log Analytics y [Microsoft Dependency Agent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#the-microsoft-dependency-agent), que se requiere con Azure Monitor para VM.

<!-- TODO: Add these when available.
- [Preview]: Enable Azure Monitor for virtual machine scale sets.
- [Preview]: Enable Azure Monitor for VMs.
 -->

> [!NOTE]
> Para obtener más información sobre distintos agentes de supervisión de Azure, consulte [Introducción a los agentes de supervisión de Azure](https://docs.microsoft.com/azure/azure-monitor/platform/agents-overview).

### <a name="assign-policies"></a>Asignación de directivas

Para asignar las directivas enumeradas en la sección anterior:

1. En Azure Portal, vaya a **Azure Policy** > **Asignaciones** > **Asignar iniciativa**.

    ![Captura de pantalla de la interfaz de directivas del portal](./media/onboarding-at-scale1.png)

2. En la página **Asignar directiva**, haga clic en los puntos suspensivos (…) para seleccionar una opción de **Ámbito** y seleccione una suscripción y un grupo de administración. Opcionalmente, seleccione un grupo de recursos. Un ámbito determina los recursos o el grupo de recursos a los que se asigna la directiva. Luego elija **Seleccionar** en la parte inferior de la página **Ámbito**.

3. Seleccione los puntos suspensivos (…) que aparecen junto a **Definición de directiva** para abrir la lista de definiciones disponibles. Puede filtrar la definición de iniciativa escribiendo **Azure Monitor** en el cuadro de **búsqueda**:

    ![Captura de pantalla de la interfaz de directivas del portal](./media/onboarding-at-scale2.png)

4. **Nombre de asignación** se rellena automáticamente con el nombre de directiva seleccionado, pero puede cambiarlo. También puede agregar una descripción opcional para proporcionar más información sobre esta asignación de directiva. El campo **Asignado por** se rellena automáticamente en función de quién inicie sesión. Este campo es opcional y se pueden especificar valores personalizados.

5. Para esta directiva, seleccione **Área de trabajo de Log Analytics** como agente de Log Analytics que se va a asociar.

    ![Captura de pantalla de la interfaz de directivas del portal](./media/onboarding-at-scale3.png)

6. Seleccione **Ubicación de la identidad administrada**. Si esta directiva es el tipo [DeployIfNotExists](https://docs.microsoft.com/azure/governance/policy/concepts/effects#deployifnotexists), necesitará una identidad administrada para implementar la directiva. En el portal, la cuenta se creará como se indica con la selección de la casilla.

7. Seleccione **Asignar**.

Después de completar el asistente, la asignación de directiva se implementará en el entorno. La directiva puede tardar hasta 30 minutos en surtir efecto. Para probarla, cree máquinas virtuales después de 30 minutos y compruebe si Microsoft Monitoring Agent (MMA) se habilita en la máquina virtual de forma predeterminada.

## <a name="install-required-agents-on-on-premises-servers"></a>Instalación de los agentes necesarios en servidores locales

> [!NOTE]
> Cree el [área de trabajo de Log Analytics y la cuenta de Azure Automation](./prerequisites.md#create-a-workspace-and-automation-account) necesarias antes de incorporar servidores a los servicios de administración de Azure.

En el caso de los servidores locales, habrá que descargar e instalar manualmente el [agente de log Analytics y Microsoft Dependency Agent](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-enable-hybrid-cloud) y configurarlos para que se conecten al área de trabajo correcta. Para ello, especifique el identificador del área de trabajo y la información de la clave, que puede encontrar en el área de trabajo de log Analytics de Azure Portal, y seleccione **Configuración** > **Configuración avanzada**.

![Captura de pantalla de Configuración avanzada del área de trabajo de Log Analytics en Azure Portal](./media/onboarding-on-premises.png)

## <a name="enable-and-configure-solutions"></a>Habilitación y configuración de soluciones

Para habilitar las soluciones, tiene que configurar el área de trabajo Log Analytics. Las máquinas virtuales de Azure y los servidores locales incorporados obtendrán las soluciones de las áreas de trabajo de Log Analytics a las que se conecten.

En esta sección se tratan las soluciones siguientes:

- [Administración de actualizaciones](#update-management)
- [Change Tracking e Inventario](#change-tracking-and-inventory-solutions)
- [Registro de actividad de Azure](#azure-activity-log)
- [Agent Health para Azure Log Analytics](#azure-log-analytics-agent-health)
- [Evaluación de antimalware](#antimalware-assessment)
- [Azure Monitor para VM](#azure-monitor-for-vms)
- [Azure Security Center](#azure-security-center)

### <a name="update-management"></a>Administración de actualizaciones

Las soluciones Update Management, Change Tracking e Inventario requieren un área de trabajo de Log Analytics y una cuenta de Automation. Para asegurarse de que estos recursos se configuran correctamente, se recomienda incorporalos a través de la cuenta de Automatización. Para obtener más información, consulte [Incorporación de las soluciones Update Management, Change Tracking e Inventario](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account).

Se recomienda habilitar la solución Update Management para todos los servidores. Update Management es gratis para las máquinas virtuales de Azure y los servidores locales. Si habilita Update Management a través de su cuenta de Automation, se creará una [configuración de ámbito](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account#scope-configuration) en el área de trabajo. Tendrá que actualizar manualmente el ámbito para incluir las máquinas que cubre el servicio de actualización.

Para cubrir todos los servidores existentes, así como los servidores futuros, debe quitar la configuración de ámbito. Para ello, vea la cuenta de Automation en Azure Portal y seleccione **Update Management** > **Administrar máquinas** > **Habilitar en todas las máquinas disponibles y futuras**. Al habilitar esta opción, se permite que todas las máquinas virtuales de Azure conectadas al área de trabajo usen Update Management.

![Captura de pantalla de Update Management en Azure Portal](./media/onboarding-configuration1.png)

### <a name="change-tracking-and-inventory-solutions"></a>Soluciones Change Tracking e Inventory

Para incorporar soluciones de Change Tracking e Inventory, siga los mismos pasos que para Update Management. Para obtener más información sobre la incorporación de estas soluciones desde su cuenta de Automation, consulte [Incorporación de las soluciones Update Management, Change Tracking e Inventory](https://docs.microsoft.com/azure/automation/automation-onboard-solutions-from-automation-account).

La solución Change Tracking es gratuita para las máquinas virtuales de Azure y cuesta 6 USD por nodo al mes para los servidores locales. Este costo cubre Change Tracking e Inventory y Desired State Configuration. Si solo quiere inscribir determinados servidores locales, puede participar en esos servidores. Se recomienda que incorpore todos los servidores de producción.

#### <a name="opt-in-via-the-azure-portal"></a>Participación a través de Azure Portal

1. Vaya a la cuenta de Automation que tiene Change Tracking e Inventory habilitada.
2. Seleccione **Seguimiento de cambios**.
3. Seleccione **Administrar máquinas** en el panel superior derecho.
4. Seleccione **Habilitar en las máquinas seleccionadas** y seleccione las máquinas que quiere habilitar haciendo clic en **Agregar** junto al nombre de la máquina.
5. Seleccione **Habilitar** para habilitar la solución para esas máquinas.

![Captura de pantalla de Change Tracking en Azure Portal](./media/onboarding-configuration2.png)

#### <a name="opt-in-by-using-saved-searches"></a>Participación mediante búsquedas guardadas

También puede establecer la configuración de ámbito para participar en servidores locales. La configuración de ámbito usa búsquedas guardadas.

Para crear o modificar la búsqueda guardada, siga estos pasos:

1. Vaya al área de trabajo de Log Analytics que está vinculada a la cuenta de Automation que configuró en los pasos anteriores.

2. En **General**, seleccione **Búsquedas guardadas**.

3. En el cuadro **Filtro**, escriba **Change Tracking** para filtrar la lista de búsquedas guardadas. En los resultados, seleccione **MicrosoftDefaultComputerGroup**.

4. Escriba el VMUUID o el nombre del equipo para incluir los equipos en los que quiere participar con Change Tracking.

    ```kusto
    Heartbeat
    | where AzureEnvironment=~"Azure" or Computer in~ ("list of the on-premises server names", "server1")
    | distinct Computer
    ```

    > [!NOTE]
    > El nombre del servidor debe coincidir exactamente con el valor incluido en la expresión y no debe contener un sufijo de nombre de dominio.

5. Seleccione **Guardar**.

6. De forma predeterminada, la configuración de ámbito está vinculada a la búsqueda guardada de **MicrosoftDefaultComputerGroup** y se actualizará automáticamente.

### <a name="azure-activity-log"></a>Azure Activity Log

[Registro de actividad de Azure](https://docs.microsoft.com/azure/azure-monitor/platform/activity-logs-overview) es una de las secciones de Azure Monitor. Proporciona información sobre los eventos de nivel de suscripción que se producen en Azure.

Para agregar esta solución:

1. En Azure Portal, abra **Todos los servicios** y seleccione **Administración y gobernanza** > **Soluciones**.
2. En la vista **Soluciones**, seleccione **Agregar**.
3. Busque **Activity Log Analytics** y selecciónela.
4. Seleccione **Crear**.

Deberá especificar el **Nombre del área de trabajo** que creó en la sección anterior donde está habilitada la solución.

### <a name="azure-log-analytics-agent-health"></a>Agent Health para Azure Log Analytics

La solución Agent Health para Azure Log Analytics ofrece información sobre el mantenimiento, el rendimiento y la disponibilidad de los servidores Windows y Linux.

Para agregar esta solución:

1. En Azure Portal, abra **Todos los servicios** y seleccione **Administración y gobernanza** > **Soluciones**.
2. En la vista **Soluciones**, seleccione **Agregar**.
3. Busque **Agent Health para Azure Log Analytics** y selecciónela.
4. Seleccione **Crear**.

Deberá especificar el **nombre del área de trabajo** que creó en la sección anterior donde está habilitada la solución.

Una vez completada la creación, la instancia de recurso del área de trabajo muestra **AgentHealthAssessment** al seleccionar **Vista** > **Soluciones**.

### <a name="antimalware-assessment"></a>Evaluación antimalware

La solución Antimalware Assessment le ayuda a identificar los servidores que están infectados o que presentan mayor riesgo de infección por malware.

Para agregar esta solución:

1. En Azure Portal, abra **Todos los servicios** y seleccione **Administración y gobernanza** > **Soluciones**.
2. En la vista **Soluciones**, seleccione **Agregar**.
3. Busque **Antimalware Assessment** y selecciónela.
4. Seleccione **Crear**.

Deberá especificar el **nombre del área de trabajo** que creó en la sección anterior donde está habilitada la solución.

Una vez completada la creación, la instancia de recurso del área de trabajo muestra **AntiMalware** al seleccionar **Vista** > **Soluciones**.

### <a name="azure-monitor-for-vms"></a>Azure Monitor para máquinas virtuales

Puede habilitar [Azure Monitor para VM](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) a través de la página de vista de la instancia de máquina virtual, tal y como se describe en el artículo anterior sobre [habilitación de los servicios de administración en una sola máquina virtual para su evaluación](./onboard-single-vm.md). No debe habilitar soluciones directamente desde la página **Soluciones** como hizo para las otras soluciones que se describen en este artículo. Para implementaciones a gran escala, puede ser más fácil usar [automatización](./onboarding-automation.md) para habilitar las soluciones correctas en el área de trabajo.

### <a name="azure-security-center"></a>Azure Security Center

En esta guía, se recomienda incorporar todos los servidores en el nivel *Gratis* de Azure Security Center de forma predeterminada. Esta opción le ofrece un nivel básico de evaluaciones de seguridad y recomendaciones de seguridad prácticas para su entorno. La actualización al nivel *Estándar* de Security Center ofrece ventajas adicionales, que se describen en detalle en la [página de precios de Security Center](https://docs.microsoft.com/azure/security-center/security-center-pricing).

Siga estos pasos para habilitar el nivel Gratis de Azure Security Center:

1. Vaya a la página **Security Center** del portal.
2. En **POLICY & COMPLIANCE** (DIRECTIVA Y CUMPLIMIENTO), seleccione **Directiva de seguridad**.
3. Busque el recurso del área de trabajo de Log Analytics que ha creado en el panel de la derecha.
4. Seleccione **Editar configuración >** para esa área de trabajo.
5. Seleccione **Plan de tarifa**.
6. Seleccione la opción **Gratis**.
7. Seleccione **Guardar**.

## <a name="next-steps"></a>Pasos siguientes

Aprenda a usar la automatización para incorporar servidores y crear alertas.

> [!div class="nextstepaction"]
> [Automatización de la incorporación y configuración de alertas](./onboarding-automation.md)
