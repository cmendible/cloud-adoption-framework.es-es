---
title: Control de acceso basado en rol recomendado
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Control de acceso basado en rol recomendado
author: rotycenh
ms.author: brblanch
ms.date: 11/28/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
manager: BrianBlanchard
tags: azure-resource-manager
ms.custom: virtual-network
ms.openlocfilehash: 98f456bf9af0ab5a7533acf9a9d49f445b7fe37b
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224318"
---
# <a name="role-based-access-control"></a>Control de acceso basado en rol

Los privilegios y los derechos de acceso basados en grupo son una buena práctica. Lidiar con grupos en lugar de con usuarios individuales simplifica el mantenimiento de las directivas de acceso, proporciona la administración de acceso coherente entre equipos y reduce los errores de configuración. Asignar usuarios a los grupos adecuados y eliminar aquellos de estos ayuda a mantener actualizados los privilegios de un usuario específico. El [control de acceso basado en rol (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/overview) de Azure ofrece administración de acceso específico para recursos organizados en torno a roles de usuario.

Para información general sobre las prácticas de RBAC recomendadas como parte de una estrategia de identidad y seguridad, consulte [Procedimientos recomendados para la administración de identidades y la seguridad del control de acceso en Azure](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices#use-role-based-access-control).

## <a name="overview-of-role-based-access-control"></a>Información general del control de acceso basado en rol

Mediante el [ control de acceso basado en rol](https://docs.microsoft.com/azure/role-based-access-control/overview), puede separar las tareas dentro de su equipo y otorgar solo acceso suficiente para usuarios, grupos, entidades de servicio o identidades administradas de Azure Active Directory (Azure AD) específicos para realizar sus trabajos. En lugar de proporcionar acceso no restringido a todos los empleados a los recursos o la suscripción de Azure, puede limitar los permisos para cada conjunto de recursos.

[Las definiciones de rol de RBAC](https://docs.microsoft.com/azure/role-based-access-control/role-definitions) enumeran las operaciones permitidas o no permitidas para los usuarios o grupos asignados a ese rol. El [ámbito](/azure/role-based-access-control/index#scope) de un rol especifica a qué recursos se aplican estos permisos definidos. Los ámbitos se pueden especificar en varios niveles: grupo de administración, suscripción, grupo de recursos o recurso. Los ámbitos se estructuran en una relación de elementos primarios y secundarios.

![Jerarquía de ámbitos RBAC](../../_images/azure-best-practices/rbac-scope.png)

Para instrucciones detalladas para la asignación de usuarios y grupos a roles específicos y la asignación de roles a ámbitos, consulte [Administración del acceso a los recursos de Azure mediante RBAC y Azure Portal](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal).

Al planear la estrategia de control de acceso, use un modelo de acceso con privilegios mínimos que solo conceda a los usuarios los permisos necesarios para realizar su trabajo. El siguiente diagrama muestra un patrón sugerido para usar RBAC a través de este enfoque.

![Patrón sugerido para usar RBAC](../../_images/azure-best-practices/rbac-least-privilege.png)

> [!NOTE]
> Los permisos más específicos o detallados son los que define y lo más probable es que los controles de acceso sean complejos y difíciles de administrar. Esto es especialmente cierto cuando los recursos en la nube aumentan de tamaño. Evite asignar permisos específicos de recursos. En su lugar, [utilice grupos de administración](https://docs.microsoft.com/azure/governance/management-groups) para control de acceso en toda la compañía y [grupos de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) para control de acceso en las suscripciones. Asimismo, evite permisos específicos del usuario. En su lugar, asigne acceso a [grupos en Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-manage-groups).

## <a name="using-built-in-rbac-roles"></a>Uso de roles de RBAC integrados

Azure proporciona muchas definiciones de roles integrados, con tres roles principales para proporcionar acceso:

- El rol [Propietario](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) puede administrarlo todo, incluido el acceso a los recursos.
- El rol [Colaborador](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) puede administrarlo todo, excepto el acceso a los recursos.
- El rol [Lector](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#reader) puede verlo todo, pero no realizar cambios.

A partir de estos niveles de acceso principales, los roles integrados adicionales proporcionan controles más detallados para acceder a determinados tipos de recursos o características de Azure. Por ejemplo, puede administrar el acceso a las máquinas virtuales mediante los siguientes roles integrados:

- El rol [Inicio de sesión de administrador de máquina virtual](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#virtual-machine-administrator-login) puede ver las máquinas virtuales en el portal e iniciar sesión como _administrador_.
- El rol [Colaborador de la máquina virtual](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) puede administrar máquinas virtuales, pero no puede acceder a ellas ni a la red virtual ni a la cuenta de almacenamiento a las que está conectado.
- El rol [Inicio de sesión de usuario de máquina virtual](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#virtual-machine-user-login) puede ver las máquinas virtuales en el portal e iniciar sesión como usuario normal.

Para ver otro ejemplo del uso de roles integrados para administrar el acceso a características concretas, consulte la explicación sobre cómo controlar el acceso a las características de seguimiento de costos en [Seguimiento de los costos a través de las unidades de negocio, entornos o proyectos](./track-costs.md#provide-the-right-level-of-cost-access).

Para una lista completa de todos los roles integrados, consulte [Roles integrados en los recursos de Azure](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles).

## <a name="using-custom-roles"></a>Uso de los roles personalizados

Aunque los roles integrados en el soporte técnico de Azure admiten una amplia variedad de escenarios de control de acceso, es posible que no satisfagan todas las necesidades de su organización o equipo. Por ejemplo, si tiene un único grupo de usuarios responsables de administrar máquinas virtuales y recursos de Azure SQL Database, es posible que desee crear un rol personalizado para optimizar la administración de los controles de acceso necesarios.

La documentación de RBAC de Azure contiene instrucciones sobre la [creación de roles personalizados](https://docs.microsoft.com/azure/role-based-access-control/custom-roles), junto con detalles sobre [cómo funcionan las definiciones de los roles](https://docs.microsoft.com/azure/role-based-access-control/role-definitions).

## <a name="separation-of-responsibilities-and-roles-for-large-organizations"></a>Separación de responsabilidades y roles para organizaciones de gran tamaño

RBAC permite a las organizaciones asignar distintos equipos a diversas tareas de administración en grandes recursos en la nube. Puede permitir que los equipos de TI centrales controlen las características de acceso y seguridad principales, concediendo al mismo tiempo grandes dosis de control sobre cargas de trabajo o grupos de recursos específicos a los desarrolladores de software y a otros equipos.

La mayoría de los entornos en la nube también pueden beneficiarse de una estrategia de control de acceso que utiliza varios roles y hace hincapié en una separación de responsabilidades entre estos roles. Este enfoque requiere que cualquier cambio significativo en los recursos o la infraestructura implique varios roles para completarse, lo que garantiza que más de una persona debe revisar y aprobar un cambio. Esta separación de responsabilidades limita la capacidad de una sola persona a acceder a datos confidenciales o a introducir vulnerabilidades sin que otros miembros del equipo lo sepan.

En la tabla siguiente se muestra un patrón común para dividir las responsabilidades de TI en roles personalizados independientes:

<!-- markdownlint-disable MD033 -->

| Grupo | Nombre común del rol | Responsabilidades |
| --- | --- | --- |
| Operaciones de seguridad | SecOps | Proporciona información general sobre la seguridad.<br/><br/> Establece y aplica las directivas de seguridad, como el cifrado en reposo.<br/><br/> Administra las claves de cifrado.<br/><br/> Administra las reglas de firewall. |
| Operaciones de red | NetOps | Administra la configuración y las operaciones de red dentro de las redes virtuales, como las rutas y los emparejamientos. |
| Operaciones del sistema | SysOps | Especifica las opciones de infraestructura de proceso y almacenamiento y mantiene los recursos que se han implementado. |
| Desarrollo, prueba y operaciones | DevOps | Compila e implementa características y aplicaciones de carga de trabajo.<br/><br/> Opera características y aplicaciones para cumplir los acuerdos de nivel de servicio (SLA) y otros estándares de calidad. |

<!-- markdownlint-enable MD033 -->

El desglose de las acciones y los permisos de estos roles estándar suelen ser los mismos en las aplicaciones, en las suscripciones o en todos los recursos en la nube, aunque estos roles los realicen diferentes personas en distintos niveles. En consecuencia, puede crear un conjunto común de definiciones de roles de RBAC para aplicarlos a distintos ámbitos dentro de su entorno. Después, se puede asignar a un rol común a los usuarios y grupos, pero solo para el ámbito de los recursos, los grupos de recursos, las suscripciones o los grupos de administración que son responsables de administrar.

Por ejemplo, en una [configuración de red de concentrador y radio](./hub-spoke-network-topology.md) con varias suscripciones, es posible que tenga un conjunto común de definiciones de roles para el concentrador y todos los radios de la carga de trabajo. El rol NetOps de una suscripción de concentrador se puede asignar a los miembros del personal de TI central de la organización, que son los responsables del mantenimiento de la red para los servicios compartidos que todas las cargas de trabajo usan. A continuación, se puede asignar el rol NetOps de una suscripción de radio de carga de trabajo a los miembros de ese equipo de carga de trabajo específico, lo que les permite configurar las redes dentro de esa suscripción para admitir mejor sus requisitos de carga de trabajo. Se usa la misma definición de rol para ambos, pero las asignaciones basadas en el ámbito garantizan que los usuarios solo tengan el acceso que necesitan para realizar su trabajo.
