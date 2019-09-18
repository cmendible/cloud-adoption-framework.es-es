---
title: Administración y seguridad en curso
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Administración y seguridad en curso
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 7b77181dd8ef6efe655b56489e5d4e6b210382b6
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031347"
---
# <a name="phase-3-ongoing-management-and-security"></a>Fase 3: Administración y seguridad en curso

Una vez que haya incorporado los servicios de administración de Azure, deberá centrarse en las configuraciones de operaciones y seguridad en las que se basarán las operaciones en curso. Empezaremos echando un vistazo a Azure Security Center para proteger el entorno. Después, configuraremos directivas para mantener el cumplimiento de los servidores y automatizar las tareas comunes. En esta sección se describen los temas siguientes:

- **[Recomendaciones de seguridad.](#address-security-recommendations)** Azure Security Center ofrece sugerencias para mejorar la seguridad del entorno. Si sigue estas recomendaciones, podrá ver su efecto reflejado en una puntuación de seguridad.
- **[Habilitar la directiva Configuración de invitado.](./guest-configuration-policy.md)** Habilite la característica Configuración de invitado de Azure Policy para auditar la configuración de una máquina virtual. Por ejemplo, puede comprobar si los certificados están a punto de expirar.
- **[Realizar un seguimiento de los cambios críticos y alertar sobre ellos.](./enable-tracking-alerting.md)** Cuando está solucionando un problema, la primera pregunta que debe tener en cuenta es "¿Qué ha cambiado?". En este artículo, aprenderá a realizar un seguimiento de los cambios y crear alertas para supervisar de forma proactiva los componentes críticos.
- **[Crear programaciones de actualización.](./update-schedules.md)** Programe la instalación de actualizaciones para asegurarse de que todos los servidores tengan las más recientes.
- **[Ejemplos comunes de Azure Policy.](./common-policies.md)** Proporciona ejemplos de directivas de administración comunes.

## <a name="address-security-recommendations"></a>Recomendaciones de seguridad

Azure Security Center es el lugar central para administrar la seguridad de su entorno. Allí encontrará una evaluación general y recomendaciones específicas.

Se recomienda revisar e implementar las recomendaciones proporcionadas por este servicio. Para más información sobre las ventajas adicionales de Azure Security Center, vea [Seguir las recomendaciones de Azure Security Center](https://docs.microsoft.com/azure/migrate/migrate-best-practices-security-management#best-practice-follow-azure-security-center-recommendations).

## <a name="next-steps"></a>Pasos siguientes

Obtenga información sobre cómo [habilitar la característica Configuración de invitado de Azure Policy](./guest-configuration-policy.md).

> [!div class="nextstepaction"]
> [Directiva de configuración de invitados](./guest-configuration-policy.md)
