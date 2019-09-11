---
title: Retirar activos retirados
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Retirar activos retirados
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: ae2538263af35e8fdb2cf5c861a2c7b0537108d4
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70839050"
---
# <a name="decommission-retired-assets"></a>Retirar activos retirados

Después de promocionar una carga de trabajo a producción, ya no es necesario que los recursos que hospedaban previamente la carga de trabajo de producción admitan las operaciones empresariales. En ese momento, los recursos más antiguos se consideran retirados. Los recursos retirados se pueden dar de baja, lo cual reducirá los costos operativos. Dar de baja un recurso puede ser tan sencillo como apagarlo y desecharlo de manera responsable. Desafortunadamente, dar de baja los recursos a veces puede acarrear consecuencias no deseadas. Las siguientes instrucciones pueden ayudarle a dar de baja correctamente los recursos retirados, con interrupciones mínimas de la actividad empresarial.

## <a name="cost-savings-realization"></a>Conseguir ahorros de costos

Cuando el ahorro de costos es el motivo principal de una migración, dar de baja los recursos retirados es un paso importante. Hasta que se da de baja un recurso, este continúa consumiendo energía, apoyo ambiental y otros recursos que generan costos. Una vez dado de baja, se empieza a conseguir un ahorro de costos.

## <a name="continued-monitoring"></a>Supervisión continuada

Después de que se promocione una carga de trabajo migrada, se debe seguir supervisando los recursos que se van a retirar para comprobar que no hay ningún tráfico de producción adicional que se esté enrutando a los recursos equivocados.

## <a name="testing-windows-and-dependency-validation"></a>Períodos de prueba y validación de las dependencias

Incluso con el mejor planeamiento, es posible que las cargas de trabajo de producción sigan conteniendo dependencias de recursos que se han retirado. En tales casos, la desactivación de un recurso retirado podría producir errores inesperados en el sistema. Por lo tanto, la terminación de los recursos debe tratarse con el mismo nivel de rigor que una actividad de mantenimiento del sistema. Se deben establecer períodos de interrupción y pruebas adecuados para facilitar la terminación del recurso.

## <a name="holding-period-and-data-validation"></a>Período de conservación y validación de datos

No es raro que las migraciones pierdan datos durante los procesos de replicación. Esto es especialmente cierto para los datos más antiguos que no se usan de forma periódica. Una vez desactivado el recurso retirado, sigue siendo aconsejable conservar el recurso durante un tiempo para que actúe como una copia de seguridad temporal de los datos. Las empresas deben permitir al menos 30 días para pruebas y conservación antes de destruir los recursos retirados.

## <a name="next-steps"></a>Pasos siguientes

Después de dar de baja los recursos retirados, se completa la migración. Esto crea una buena oportunidad para mejorar el proceso de migración, y una [visión retrospectiva](./retrospective.md) puede hacer que el equipo de adopción de la nube revise el lanzamiento con el fin de aprender y mejorar.

> [!div class="nextstepaction"]
> [Retrospectiva](./retrospective.md)
