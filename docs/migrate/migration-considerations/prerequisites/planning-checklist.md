---
title: 'Entorno de migración: lista de comprobación del planeamiento'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Validación de la preparación del entorno antes de la migración
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 8d216d65685c7e58fc622a5d7f820f0c23097fa4
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70839030"
---
# <a name="migration-environment-planning-checklist---validate-environmental-readiness-prior-to-migration"></a>Lista de comprobación del planeamiento del entorno de migración: validación de la preparación del entorno antes de la migración

Como paso inicial en el proceso de migración, debe crear el entorno adecuado en la nube para recibir, hospedar y respaldar la migración de los recursos. En este artículo se proporciona una lista de aspectos que se deben validar en el entorno actual antes de la migración.

La siguiente lista de comprobación se alinea con las instrucciones encontradas en la [sección de preparación](../../../ready/index.md) del marco de adopción de la nube. Revise esa sección para obtener instrucciones sobre la ejecución de cualquiera de las siguientes opciones.

## <a name="effort-type-assumption"></a>Supuesto del tipo de esfuerzo

En este artículo y lista de comprobación se da por hecho un enfoque de _rehospedaje_ o de _transición a la nube_ en la migración a la nube.

## <a name="governance-alignment"></a>Alineación de la gobernanza

La primera decisión, y la más importante, con respecto a cualquier entorno preparado para la migración es la elección de la alineación de la gobernanza. ¿Se ha logrado un consenso con respecto a la alineación de la gobernanza con la base de la migración? Como mínimo, el equipo de adopción de la nube debe comprender si esta migración se va a realizar en un único entorno con gobernanza limitada, en una factoría con un entorno completamente regulado o en una opción entre medias. Para ver más opciones e instrucciones sobre la alineación de la gobernanza, consulte el artículo [Alineación de gobernanza y cumplimiento](../../expanded-scope/governance-or-compliance.md).

## <a name="cloud-readiness-implementation"></a>Implementación de la preparación de la nube

Tanto si elige alinearse con una estrategia de control de la nube más amplia como si no para la migración inicial, deberá asegurarse de que el entorno de implementación de la nube esté configurado para admitir las cargas de trabajo.

Si desde el principio tiene previsto alinear la migración con una estrategia de gobernanza de la nube, deberá aplicar [Las cinco disciplinas de la gobernanza de la nube](../../../governance/governance-disciplines.md) para ayudar a tomar decisiones sobre las directivas, cadenas de herramientas y mecanismos de cumplimiento que alinearán el entorno de nube con los requisitos corporativos generales. Consulte las [guías de diseño de gobernanza accionables](../../../governance/journeys/index.md) del marco de adopción de la nube para ver ejemplos de cómo implementar este modelo con los servicios de Azure.

Si las migraciones iniciales no están estrechamente alineadas con una estrategia de gobernanza de la nube más amplia, aún será necesario gestionar los problemas generales de planeamiento de la organización, acceso e infraestructura. Consulte la [guía de preparación de Azure](../../../ready/azure-readiness-guide/index.md) para obtener ayuda con estas decisiones de preparación de la nube.

> [!CAUTION]
> Se recomienda encarecidamente desarrollar una estrategia de gobernanza para todos aquellos aspectos que vayan más allá de la migración inicial de la carga de trabajo.

Con independencia del nivel de alineación de la gobernanza, deberá tomar decisiones relacionadas con los temas siguientes.

### <a name="resource-organization"></a>Organización de recursos

En función de la decisión sobre la alineación de la gobernanza, se debe establecer un enfoque para la organización y la implementación de recursos antes de la migración.

### <a name="nomenclature"></a>Nomenclatura

Antes de la migración, se debe establecer un enfoque coherente para asignar nombres a los recursos, junto con esquemas de nomenclatura coherentes.

### <a name="resource-governance"></a>Gobernanza de recursos

Antes de la migración, se debe tomar una decisión con respecto a las herramientas para regular los recursos. Aunque no es necesario que las herramientas estén totalmente implementadas, se deben seleccionar y probar en una dirección. Se recomienda que, antes de la migración, el equipo de gobernanza de la nube defina y exija la implementación de un producto mínimo viable (MVP) de las herramientas de gobernanza.

## <a name="network"></a>Red

Las cargas de trabajo basadas en la nube requerirán el aprovisionamiento de redes virtuales para admitir el acceso administrativo y del usuario final. En función de las decisiones sobre la organización y la gobernanza de los recursos, debe seleccionar un enfoque de red para alinearlo con los requisitos de seguridad de TI. Además, las decisiones de red deben estar en consonancia con cualquier restricción de red híbrida necesaria para operar las cargas de trabajo en el trabajo pendiente de migración y admitir cualquier acceso a los recursos hospedados de forma local.

## <a name="identity"></a>Identidad

Los servicios de identidad basados en la nube son un requisito previo para ofrecer administración de identidades y acceso (IAM) para los recursos en la nube. Alinee la estrategia de administración de identidades con los planes de adopción de la nube antes de continuar. Por ejemplo, al migrar recursos locales existentes, considere la posibilidad de admitir un enfoque de identidad híbrida mediante la [sincronización de directorios](../../../decision-guides/identity/index.md) para permitir un conjunto coherente de credenciales de usuario en el entorno local y en la nube durante y después de la migración.

## <a name="next-steps"></a>Pasos siguientes

Si el entorno cumple los requisitos mínimos, se puede considerar aprobado para la preparación de la migración. [La administración de la complejidad cultural y de los cambios](./culture-complexity.md) ayuda a alinear roles y responsabilidades para garantizar las expectativas adecuadas durante la ejecución del plan.

> [!div class="nextstepaction"]
> [Administración de la complejidad cultural y de los cambios](./culture-complexity.md)
