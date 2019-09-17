---
title: Guía de decisión de identidad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información acerca de la identidad como un servicio principal en las migraciones de Azure.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: ceb9fb6ff6be481f665a0bb70e3afcc2eddb6e92
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71023896"
---
# <a name="identity-decision-guide"></a>Guía de decisión de identidad

En cualquier entorno, ya sea local, híbrido, o solo en la nube, el departamento de TI necesita controlar qué administradores, usuarios y grupos tienen acceso a los recursos. Los servicios de Administración de identidad y acceso (IAM) le permiten administrar el control de acceso en la nube.

![Trazado de opciones de identidad de menos a más complejas, alineadas con vínculos a continuación](../../_images/decision-guides/decision-guide-identity.png)

Vaya a: [Determinación de los requisitos de integración de identidades](#determine-identity-integration-requirements) | [Base de referencia en la nube](#cloud-baseline) | [Sincronización de directorios](#directory-synchronization) | [Servicios de dominios hospedados en la nube](#cloud-hosted-domain-services) | [Servicios de federación de Active Directory](#active-directory-federation-services) | [Más información](#learn-more)

Hay varias opciones disponibles para administrar la identidad en un entorno en la nube. Estas opciones varían en cuanto a costo y complejidad. Un factor decisivo para estructurar los servicios de identidad basados en la nube es el nivel de integración necesario con la infraestructura de identidad local existente.

En Azure, Azure Active Directory (Azure AD) proporciona un nivel básico de control de acceso y administración de identidades para los recursos en la nube. Sin embargo, si la infraestructura de Active Directory local de la organización tiene una compleja estructura de bosque o unidades organizativas (OU) personalizadas, las cargas de trabajo basadas en la nube pueden requerir la sincronización de directorios con Azure AD para tener un conjunto coherente de identidades, grupos y roles entre el entorno local y en la nube. Además, la compatibilidad con aplicaciones que dependen de mecanismos de autenticación heredados podría requerir la implementación de Active Directory Domain Services (AD DS) en la nube.

La administración de identidades basada en la nube es un proceso iterativo. Podría comenzar con una solución nativa en la nube con un pequeño conjunto de usuarios y roles correspondientes para una implementación inicial. A medida que madura la migración, es posible que deba integrar la solución de identidades mediante la sincronización de directorios o agregar servicios de dominios como parte de las implementaciones de nube. Vuelva a visitar su estrategia de identidad en cada iteración del proceso de migración.

## <a name="determine-identity-integration-requirements"></a>Determinación de los requisitos de integración de identidades

| Pregunta | Línea base en la nube | Sincronización de directorios | Servicios de dominio hospedados en la nube | Servicios de federación de Active Directory |
|------|------|------|------|------|
| ¿Actualmente carece de un servicio de directorios local? | Sí | No | No | Sin |
| ¿Las cargas de trabajo necesitan usar un conjunto común de usuarios y grupos entre el entorno en la nube y el local? | Sin | Sí | No | Sin |
| ¿Sus cargas de trabajo dependen de mecanismos de autenticación heredados, como Kerberos o NTLM? | Sin | No | Sí | Sí |
| ¿Necesita el inicio de sesión único entre varios proveedores de identidad? | Sin | No | No | Sí |

Como parte del planeamiento de la migración a Azure, deberá determinar la mejor manera de integrar sus servicios actuales de administración de identidad y de identidad en la nube. A continuación presentamos escenarios de integración comunes.

### <a name="cloud-baseline"></a>Línea base en la nube

Azure AD es el sistema de administración de identidad y acceso (IAM) nativo para conceder acceso a los usuarios y grupos a las características de administración en la plataforma de Azure. Si la organización no tiene una solución de identidades significativa en el entorno local y planea migrar las cargas de trabajo para que sean compatibles con los mecanismos de autenticación basados en la nube, debería comenzar a desarrollar la infraestructura de identidades con Azure AD como base.

**Suposiciones de la línea de base en la nube:** El uso de una infraestructura de identidad puramente nativo de la nube asume lo siguiente:

- Los recursos basados en la nube no tendrán dependencias de servicios de directorio locales o servidores de Active Directory o las cargas de trabajo se pueden modificar para eliminar esas dependencias.
- Las cargas de trabajo de servicio o aplicación que se están migrando admiten mecanismos de autenticación compatibles con Azure AD o se pueden modificar fácilmente para admitirlos. Azure AD se basa en mecanismos de autenticación por Internet como SAML, OAuth y OpenID Connect. Es posible que haya que refactorizar las cargas de trabajo existentes que dependen de métodos de autenticación heredados y usan protocolos como Kerberos o NTLM antes de migrarlas a la nube con el patrón de línea de base en la nube.

> [!TIP]
> Migrar completamente los servicios de identidad a Azure AD elimina la necesidad de mantener su propia infraestructura de identidades, con lo que se simplifica de manera significativa la administración de los servicios informáticos.
>
> Sin embargo, Azure AD no sustituye completamente una infraestructura de Active Directory local tradicional. Es posible que algunas características de directorios, como los métodos de autenticación heredados, la administración de equipos o la directiva de grupos no estén disponibles sin implementar herramientas o servicios adicionales en la nube.
>
> Para escenarios donde es necesario integrar las identidades locales o los servicios de dominio con las implementaciones en la nube, consulte los patrones de sincronización de directorios y de servicios de dominio hospedados en la nube que se explican a continuación.

### <a name="directory-synchronization"></a>Sincronización de directorios

Para organizaciones con una infraestructura de Active Directory local existente, la sincronización de directorios suele ser la mejor solución para conservar los usuarios existentes y la administración del acceso proporcionando al mismo tiempo las funcionalidades de IAM necesarias para administrar recursos en la nube. Este proceso replica continuamente la información de los directorios entre Azure AD y los servicios de directorio locales, lo que permite credenciales comunes para los usuarios y un sistema de identidades, roles y permisos coherente en toda la organización.

Nota: Es posible que las organizaciones que han adoptado Office 365 ya hayan implementado la [sincronización de directorios](https://docs.microsoft.com/office365/enterprise/set-up-directory-synchronization) entre su infraestructura de Active Directory local y Azure Active Directory.

**Suposiciones de sincronización de directorios:** Con el uso de una solución de identidad sincronizada se asume lo siguiente:

- Debe mantener un conjunto común de cuentas de usuario y grupos en la nube y la infraestructura de TI local.
- Los servicios de identidad locales admiten la replicación con Azure AD.

> [!TIP]
> Las cargas de trabajo basadas en la nube que dependen de mecanismos de autenticación heredados proporcionados por servidores de Active Directory locales y que no son compatibles con Azure AD, seguirán necesitando conectividad con servicios de dominio locales o servidores virtuales en el entorno en la nube que ofrecen estos servicios. El uso de servicios de identidad locales también presenta las dependencias en la conectividad entre las redes en la nube y local.

### <a name="cloud-hosted-domain-services"></a>Servicios de dominio hospedados en la nube

Si tiene cargas de trabajo que dependen de la autenticación basada en notificaciones y que usan protocolos heredados como Kerberos o NTLM, y no se pueden refactorizar tales cargas de trabajo para que acepten protocolos de autenticación modernos, como SAML o OpenID Connect y OAuth, es posible que necesite migrar algunos de los servicios de dominio a la nube como parte de su implementación en la nube.

Este patrón implica la implementación de máquinas virtuales que ejecutan Active Directory en las redes virtuales basadas en la nube para proporcionar Active Directory Domain Services (AD DS) para los recursos en la nube. Todas las aplicaciones y servicios existentes que se migran a la red en la nube deben ser capaces de utilizar estos servidores de directorio hospedados en la nube con modificaciones menores.

Es probable que los directorios y los servicios de dominio existentes sigan usándose en su entorno local. En este escenario, se recomienda que también use la sincronización de directorios para proporcionar un conjunto común de usuarios y roles tanto en el entorno local como en la nube.

**Suposiciones de servicios de dominio hospedados en la nube:** La realización de una migración de directorios asume lo siguiente:

- Las cargas de trabajo dependen de la autenticación basada en notificaciones que utilizan protocolos como Kerberos o NTLM.
- Las máquinas virtuales de su carga de trabajo deben estar unidas al dominio para la administración o aplicación de la directiva de grupo de Active Directory.

> [!TIP]
> Mientras que una migración de directorios combinada con servicios de dominio hospedados en la nube ofrece una gran flexibilidad al migrar las cargas de trabajo existentes, el hospedaje de máquinas virtuales dentro de la red virtual en la nube para proporcionar estos servicios aumenta la complejidad de las tareas de administración de TI. A medida que crezca su experiencia de migración en la nube, examine los requisitos de mantenimiento a largo plazo del hospedaje de estos servidores. Considere si la refactorización de cargas de trabajo existentes para ofrecer compatibilidad con proveedores de identidades en la nube como Azure Active Directory puede reducir la necesidad de estos servidores hospedados en la nube.

### <a name="active-directory-federation-services"></a>Servicios de federación de Active Directory

La federación de identidades establece relaciones de confianza entre varios sistemas de administración de identidades para permitir las funciones más comunes de autenticación y autorización. Así, puede admitir capacidades de inicio de sesión único entre varios dominios dentro de su organización o sistemas de identidad administrados por los clientes o socios comerciales.

Azure AD admite la federación de dominios de Active Directory locales con [Servicios de federación de Active Directory](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-fed-whatis) (AD FS). Consulte la arquitectura de referencia [Extensión de Servicios de federación de Active Directory (AD FS) a Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adfs) para ver cómo se puede implementar en Azure.

## <a name="learn-more"></a>Más información

Para más información acerca de los servicios de identidad en Azure, consulte:

- [Azure AD](https://azure.microsoft.com/services/active-directory). Azure AD proporciona servicios de identidad basados en la nube. Permite administrar el acceso a sus recursos de Azure y controlar la administración de identidades, el registro de dispositivos, el aprovisionamiento de usuarios, el control de acceso de la aplicación y la protección de datos.
- [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-hybrid-identity). La herramienta Azure AD Connect le permite conectarse a instancias de Azure AD con sus soluciones de administración de identidad existentes, permitiendo la sincronización del directorio actual en la nube.
- [Control de acceso basado en rol](https://docs.microsoft.com/azure/role-based-access-control/overview) (RBAC). Azure AD proporciona RBAC para administrar de forma eficaz y segura el acceso a los recursos en el plano de la administración. Los trabajos y las responsabilidades se organizan en roles, y los usuarios se asignan a estos roles. RBAC le permite controlar quién tiene acceso a un recurso, junto con las acciones que un usuario puede realizar en ese recurso.
- [Azure AD Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure) (PIM). PIM reduce el tiempo de exposición de los privilegios de acceso de recursos y aumenta la visibilidad de su uso mediante alertas e informes. Limita a los usuarios a que solo acepten sus privilegios "just-in-time" (JIT) o mediante la asignación de privilegios por un período de tiempo más corto, tras el cual se revocan automáticamente.
- [Integración de dominios locales de Active Directory con Azure Active Directory](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/azure-ad). Esta arquitectura de referencia proporciona un ejemplo de sincronización de directorios entre los dominios de Active Directory local y Azure AD.
- [Extensión de Active Directory Domain Services (AD DS) a Azure.](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adds-extend-domain) Esta arquitectura de referencia proporciona un ejemplo de cómo implementar servidores de AD DS para ampliar los servicios de dominio a los recursos basados en la nube.
- [Extensión de Servicios de federación de Active Directory (AD FS) a Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adfs). Esta arquitectura de referencia configura Servicios de federación de Active Directory (AD FS) para realizar la autenticación federada y la autorización con su directorio Azure AD.

## <a name="next-steps"></a>Pasos siguientes

La identidad es solo uno de los principales componentes de infraestructura que requieren decisiones de arquitectura durante un proceso de adopción de la nube. Visite la [introducción a las guías de decisión](../index.md) para obtener información sobre los patrones o los modelos alternativos que se usan al tomar decisiones de diseño para otros tipos de infraestructura.

> [!div class="nextstepaction"]
> [Guías de decisiones sobre arquitectura](../index.md)
