---
title: Habilitar el seguimiento y las alertas de los cambios críticos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Habilitar el seguimiento y las alertas de los cambios críticos
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 93449f754e3908e092fa64c55ad62fc604b4ba5b
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032290"
---
# <a name="enable-tracking-and-alerting-for-critical-changes"></a>Habilitar el seguimiento y las alertas de los cambios críticos

Azure Change Tracking e Inventario proporciona alertas sobre el estado de configuración de su entorno híbrido y sobre los cambios que se realizan en ese entorno. Puede supervisar los cambios críticos en los archivos, los servicios, el software y el Registro que pueden afectar a los servidores implementados.

De forma predeterminada, el servicio de inventario de Azure Automation no supervisa la configuración del Registro o los archivos. La solución proporciona una lista de las claves del Registro que se recomienda supervisar. Para ver esta lista, vaya a la cuenta de Automation en Azure Portal y seleccione **Inventario** > **Editar configuración**:

![Captura de pantalla de la vista de inventario de Azure Automation en Azure Portal](./media/change-tracking1.png)

Para más información sobre cada una de las claves del Registro, consulte [Seguimiento de cambios en las claves del Registro](https://docs.microsoft.com/azure/automation/automation-change-tracking#registry-key-change-tracking). Puede evaluar y, a continuación, habilitar cada clave seleccionándola. La configuración se aplica a todas las máquinas virtuales habilitadas en el área de trabajo actual.

También puede realizar un seguimiento de los cambios críticos en los archivos. Por ejemplo, puede que desee realizar el seguimiento del archivo C:\Windows\System32\Drivers\etc\hosts porque el sistema operativo lo usa para asignar nombres de host a direcciones IP. Cualquier cambio en este archivo podría provocar problemas de conectividad o redirigir el tráfico a sitios web peligrosos.

Para habilitar el seguimiento del contenido del el archivo de hosts, siga los pasos descritos en [Habilitación del seguimiento del contenido de los archivos](https://docs.microsoft.com/azure/automation/change-tracking-file-contents#enable-file-content-tracking).

También puede agregar una alerta para cambios realizados en los archivos de los que está realizando el seguimiento. Por ejemplo, suponga que desea establecer una alerta para los cambios realizados en el archivo de hosts. Para empezar, seleccione **Log Analytics** en la barra de comandos o abra la búsqueda de registros para el área de trabajo de Log Analytics vinculada para ir a Log Analytics. Una vez en Log Analytics, busque cambios en el contenido del archivo de hosts con la siguiente consulta:

```kusto
ConfigurationChange | where FieldsChanged contains "FileContentChecksum" and FileSystemPath contains "hosts"
```

![Captura de pantalla del editor de consultas de Log Analytics en Azure Portal](./media/change-tracking2.png)

Esta consulta busca cambios en el contenido de los archivos que tienen una ruta de acceso que contiene la palabra "hosts". También puede buscar un archivo específico cambiando el parámetro de ruta de acceso. (Por ejemplo, `FileSystemPath ==  "c:\\windows\\system32\\drivers\\etc\\hosts"`).
  
Después de que la consulta devuelva los resultados, seleccione **Nueva regla de alertas** para abrir el editor de reglas de alertas. También puede acceder a este editor mediante Azure Monitor en Azure Portal.

En el editor de reglas de alertas, revise la consulta y cambie la lógica de la alerta si es necesario. En este caso, queremos que se genere la alerta si se detectan cambios en cualquier máquina del entorno.

![Captura de pantalla del editor de reglas de alertas de Log Analytics en Azure Portal](./media/change-tracking3.png)

Después de establecer la lógica de la condición, puede asignar grupos de acciones para realizar acciones como respuesta a la alerta. En este ejemplo, cuando se genera la alerta, se envían mensajes de correo electrónico y se crea un vale de ITSM. Se pueden realizar muchas otras acciones útiles, como desencadenar una función de Azure, un runbook de Azure Automation, un webhook o una aplicación lógica.

![Captura de pantalla del resumen de la regla de alerta de ejemplo en Azure Portal](./media/change-tracking4.png)

Una vez configurados todos los parámetros y la lógica, aplique la alerta al entorno.

## <a name="more-tracking-and-alerting-examples"></a>Más ejemplos de alertas y seguimiento

A continuación, se muestran otros escenarios habituales de seguimiento y alertas que conviene tener en cuenta:

### <a name="driver-file-changed"></a>Archivo de controlador modificado

Detecta si se modifican, agregan o quitan archivos de controlador. Útil para el seguimiento de cambios en archivos críticos del sistema.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Files" and FileSystemPath contains " c:\\windows\\system32\\drivers\\"
  ```

### <a name="specific-service-stopped"></a>Servicio específico detenido

Útil para el seguimiento de cambios en servicios críticos del sistema.

  ```kusto
  ConfigurationChange | where SvcState == "Stopped" and SvcName contains "w3svc"
  ```

### <a name="new-software-installed"></a>Nuevo software instalado

Útil para entornos que necesitan bloquear configuraciones de software.

  ```kusto
  ConfigurationChange | where ConfigChangeType == "Software" and ChangeCategory == "Added"
  ```

### <a name="specific-software-version-is-or-isnt-installed-on-a-machine"></a>Una versión de software específica está o no está instalada en una máquina

Útil para evaluar la seguridad. Tenga en cuenta que esta consulta hace referencia a `ConfigurationData`, que contiene los registros de Inventario e indica el último estado de configuración notificado, pero no cambios.

  ```kusto
  ConfigurationData | where SoftwareName contains "Monitoring Agent" and CurrentVersion != "8.0.11081.0"
  ```

### <a name="known-dll-changed-through-registry"></a>Archivo DLL conocido modificado a través del Registro

Útil para detectar cambios en claves del Registro conocidas.

  ```kusto
  ConfigurationChange | where RegistryKey == "HKEY_LOCAL_MACHINE\\System\\CurrentControlSet\\Control\\Session Manager\\KnownDlls"
  ```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo administrar las actualizaciones de los servidores mediante la [creación de programaciones de actualizaciones](./update-schedules.md) con Azure Automation.

> [!div class="nextstepaction"]
> [Creación de programaciones de actualizaciones](./update-schedules.md)
