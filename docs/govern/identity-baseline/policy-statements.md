---
title: Declaraciones de directivas de ejemplo de base de referencia de identidad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Declaraciones de directivas de ejemplo de base de referencia de identidad
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: fae5bb8283487ef7724f872fc293def2c1a80071
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032527"
---
# <a name="identity-baseline-sample-policy-statements"></a>Declaraciones de directivas de ejemplo de base de referencia de identidad

Las declaraciones individuales de directiva de nube son directrices para abordar los riesgos específicos identificados durante el proceso de evaluación de riesgos. Estas declaraciones deben proporcionar un breve resumen de los riesgos y los planes para resolverlos. La definición de cada declaración debe incluir estos fragmentos de información:

- **Riesgo técnico**: Un resumen del riesgo que esta directiva abordará.
- **Declaración de directiva**: Una explicación clara que resuma los requisitos de la directiva.
- **Opciones de diseño**: Recomendaciones que requieren acción, especificaciones u otras instrucciones que los equipos de TI y los desarrolladores pueden usar al implementar la directiva.

Las siguientes declaraciones de la directiva de ejemplo abordan algunos riesgos empresariales comunes relacionados con la identidad. Estas declaraciones son ejemplos a los que se puede hacer referencia al elaborar el borrador de las declaraciones de directiva para satisfacer las necesidades de su organización. Estos ejemplos no pretenden ser excluyentes y hay varias opciones posibles de directiva para solucionar cada riesgo concreto identificado. Trabaje estrechamente con los equipos de TI y de dirección para identificar las mejores directivas para su conjunto de riesgos en particular.

## <a name="lack-of-access-controls"></a>Falta de controles de acceso

**Riesgo técnico:** una configuración de control de acceso insuficiente o ad hoc puede plantear riesgos de acceso no autorizado a recursos confidenciales o críticos.

**Declaración de directiva**: todos los recursos que se implementan en la nube deben controlarse mediante identidades y roles aprobados por las directivas de gobernanza actuales.

**Opciones de diseño posibles:** el [acceso condicional de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/conditional-access/overview) es el mecanismo de control de acceso predeterminado en Azure.

## <a name="overprovisioned-access"></a>Acceso sobreaprovisionado

**Riesgo técnico:** los usuarios y grupos que controlan los recursos más allá de su área de responsabilidad pueden dar lugar a que se produzcan modificaciones no autorizadas que provoquen interrupciones o vulnerabilidades de seguridad.

**Declaración de directiva**: se implementarán las siguientes directivas:

- Un modelo de acceso con privilegios mínimos se aplicará a cualquier recurso involucrado en aplicaciones críticas o datos protegidos.
- Los permisos elevados deben ser una excepción, y todas las excepciones deberán notificarse al equipo de gobernanza de la nube. Las excepciones se auditarán con regularidad.

**Opciones de diseño posibles:** consulte los [procedimientos recomendados de Azure Identity Management](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices) para implementar una estrategia de control de acceso basado en rol (RBAC) que restringe el acceso en función de los principios de [necesidad de saber](https://wikipedia.org/wiki/Need_to_know) y [seguridad con privilegios mínimos](https://wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="lack-of-shared-management-accounts-between-on-premises-and-the-cloud"></a>Ausencia de cuentas de administración compartidas entre el entorno local y la nube

**Riesgo técnico:** el personal administrativo y de administración de TI con cuentas en el entorno local de Active Directory que no tenga acceso suficiente a los recursos en la nube es posible que no pueda resolver con eficacia los problemas operativos o de seguridad.

**Declaración de directiva**: todos los grupos de la infraestructura local de Active Directory que tienen privilegios elevados deben asignarse a un rol RBAC aprobado.

**Opciones de diseño posibles:** implemente una solución de identidad híbrida entre Azure Active Directory basado en la nube y Active Directory local, y agregue los grupos locales necesarios a los roles de RBAC precisos para realizar su trabajo.

## <a name="weak-authentication-mechanisms"></a>Mecanismos de autenticación no seguros

**Riesgo técnico:** los sistemas de administración de identidad con métodos de autenticación de usuarios que no son suficientemente seguros, como las combinaciones de usuario y contraseña, pueden generar contraseñas comprometidas o pirateadas, planteando un riesgo mayor de acceso no autorizado a sistemas en la nube seguros.

**Declaración de directiva**: todas las cuentas deben iniciar sesión en recursos protegidos con un método de autenticación multifactor.

**Opciones de diseño posibles:** para Azure Active Directory, implemente [Azure Multi-factor Authentication](https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks) como parte del proceso de autorización de usuario.

## <a name="isolated-identity-providers"></a>Proveedores de identidades aislados

**Riesgo técnico:** los proveedores de identidades incompatibles pueden provocar la incapacidad de compartir recursos o servicios con clientes u otros asociados empresariales.

**Declaración de directiva**: la implementación de las aplicaciones que requieren autenticación de cliente debe usar un proveedor de identidades aprobado que sea compatible con el proveedor de identidades principal para usuarios internos.

**Opciones de diseño posibles:** implemente la [federación con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-fed) entre los proveedores de identidades internos y de cliente.

## <a name="identity-reviews"></a>Revisiones de identidad

**Riesgo técnico:** con los cambios empresariales a lo largo del tiempo, la adición de nuevas implementaciones en la nube u otros problemas de seguridad puede aumentar los riesgos de acceso no autorizado a recursos seguros.

**Declaración de directiva**: los procesos de gobernanza en la nube deben incluir revisiones trimestrales con los equipos de administración de identidad para así poder identificar usuarios malintencionados o patrones de uso que deban evitarse mediante la configuración de recursos en la nube.

**Opciones de diseño posibles:** celebrar una reunión de revisión de seguridad trimestral en la que participen los miembros del equipo de gobernanza y el personal de TI responsable de administrar los servicios de identidad. Revisar las métricas y los datos de seguridad existentes para identificar deficiencias en las herramientas y la directiva de administración de identidad, y actualizar la directiva para remediar todos los riesgos nuevos.

## <a name="next-steps"></a>Pasos siguientes

Use los ejemplos mencionados en este artículo como punto de partida para desarrollar directivas que aborden los riesgos empresariales específicos que se alinean con los planes de adopción de la nube.

Para comenzar a desarrollar sus propias declaraciones de directiva personalizadas relacionadas con la base de referencia de identidad, descargue la [plantilla de base de referencia de identidad](./template.md).

Para acelerar la adopción de esta materia, elija la [guía accionable de gobernanza](../guides/index.md) que más se ajuste a su entorno. Después, modifique el diseño para incorporar las decisiones de directiva específicas de su organización.

A partir de los riesgos y la tolerancia, establezca un proceso para gobernar y comunicar la adhesión a la directiva de línea de base de identidad.

> [!div class="nextstepaction"]
> [Establecimiento de procesos para el cumplimiento de directivas](./compliance-processes.md)
