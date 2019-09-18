---
title: Conceptos básicos de Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Conozca los conceptos y términos fundamentales que se usan en Azure y cómo esos conceptos se relacionan entre sí.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 47148153d63137e6281b37bcb2be28e63bc6586c
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025172"
---
# <a name="azure-fundamental-concepts"></a>Conceptos básicos de Azure

Conozca los conceptos y términos fundamentales que se usan en Azure y cómo esos conceptos se relacionan entre sí.

## <a name="azure-terminology"></a>Terminología de Azure

Al comenzar las labores de adopción de la nube de Azure, resulta útil conocer las siguientes definiciones:

- **Recursos**: entidad administrada por Azure. Algunos ejemplos son máquinas virtuales, redes virtuales y cuentas de almacenamiento de Azure.
- **Suscripción**: contenedor lógico para los recursos. Cada recurso de Azure está asociado a una sola suscripción. La creación de una suscripción es el primer paso en la adopción de Azure.
- **Cuenta de Azure**: la dirección de correo electrónico que proporciona al crear una suscripción a Azure es la cuenta de Azure de la suscripción. La entidad que está asociada a la cuenta de correo electrónico es responsable de los costos mensuales que generan los recursos de la suscripción. Cuando se crea una cuenta de Azure, se proporciona información de contacto y detalles de facturación, como una tarjeta de crédito. Puede usar la misma cuenta de Azure (dirección de correo electrónico) con varias suscripciones. Cada suscripción está asociada solo a una cuenta de Azure.
- **Administrador de cuenta**: la entidad asociada a la dirección de correo electrónico que se usa para crear una suscripción a Azure. El administrador de la cuenta es responsable del pago de todos los costos que generan los recursos de la suscripción.
- **Azure Active Directory** (Azure AD): el servicio de administración de acceso e identidades de Microsoft, basado en la nube. Azure AD ayuda a sus empleados a iniciar sesión y a acceder a los recursos.
- **Inquilino de Azure AD**: instancia dedicada y de confianza de Azure AD. Se crea automáticamente cuando su organización se suscribe por primera vez a un servicio en la nube de Microsoft, como Microsoft Azure, Microsoft Intune u Office 365. Un inquilino de Azure representa una organización individual.
- **Directorio de Azure AD**: todos los inquilinos de Azure AD tienen un directorio dedicado y de confianza. El directorio incluye los usuarios, los grupos y las aplicaciones del inquilino. Se usa para realizar funciones de administración de identidades y acceso para los recursos del inquilino. Un directorio puede asociarse a varias suscripciones, pero cada suscripción solo está asociada a un directorio.
- **Grupos de recursos**: contenedores lógicos que se usan para agrupar los recursos relacionados de una suscripción. Cada recurso solo puede existir en un grupo de recursos.
- **Grupos de administración**: contenedores lógicos que se usan para una o varias suscripciones. Puede definir una jerarquía de grupos de administración, suscripciones, grupos de recursos y recursos para administrar de forma eficaz el acceso, las directivas y el cumplimiento a través de la herencia.
- **Región**: conjunto de centros de datos de Azure que se implementan dentro de un perímetro definido por la latencia. Los centros de datos se conectan a través de una red dedicada, regional y de baja latencia. La mayoría de los recursos de Azure se ejecutan en una región específica de Azure.

## <a name="azure-subscription-purposes"></a>Objetivos de la suscripción a Azure

Una suscripción a Azure sirve a varios fines. Una suscripción de Azure es:

- **Un contrato legal**. Cada suscripción está asociada a una [oferta de Azure](https://azure.microsoft.com/support/legal/offer-details) (como evaluación gratuita o pago por uso). Cada oferta tiene un plan de tarifa, unas ventajas y unos términos y condiciones asociados específicos. Puede elegir una oferta de Azure al crear una suscripción.
- **Un acuerdo de pago**. Al crear una suscripción, se proporciona la información de pago de esa suscripción, como un número de tarjeta de crédito. Cada mes, los costos que generan los recursos implementados en esa suscripción se calculan y facturan mediante ese método de pago.
- **Un límite de escala**. Se definen límites de escala para una suscripción. Los recursos de la suscripción no pueden superar los límites de escala establecidos. Por ejemplo, hay un límite en el número de máquinas virtuales que puede crear en una sola suscripción.
- **Un límite administrativo**. Una suscripción puede actuar como límite de administración, seguridad y directiva. Azure también proporciona otros mecanismos para satisfacer estas necesidades, como grupos de administración, grupos de recursos y control de acceso basado en rol.

## <a name="azure-subscription-considerations"></a>Consideraciones sobre las suscripciones a Azure

Al crear una suscripción a Azure, puede elegir varias opciones clave sobre ella:

- **¿Quién es el responsable de pagar la suscripción?** La entidad asociada a la dirección de correo electrónico que proporcione al crear una suscripción es, de forma predeterminada, el administrador de la cuenta de la suscripción. La entidad asociada a esta dirección de correo electrónico es responsable de pagar todos los costos que generen los recursos de la suscripción.
- **¿Qué oferta de Azure me interesa?** Cada suscripción está asociada a una [oferta de Azure específica](https://azure.microsoft.com/support/legal/offer-details). Puede elegir la oferta de Azure que mejor se adapta a sus necesidades. Por ejemplo, si piensa usar una suscripción para ejecutar cargas de trabajo de no producción, puede elegir la oferta Desarrollo/pruebas - Pago por uso o la oferta Desarrollo/pruebas - Enterprise.

> [!NOTE]
> Al suscribirse a Azure, es posible que vea la frase *creación de una cuenta de Azure*. Puede crear una cuenta de Azure al crear una suscripción a Azure y asociar la suscripción a una cuenta de correo electrónico.

## <a name="azure-administrative-roles"></a>Roles administrativos de Azure

Azure define tres tipos de roles para administrar suscripciones, identidades y recursos:

- Roles de administrador de suscripciones clásicas
- Roles de control de acceso basado en rol (RBAC) de Azure
- Roles de administrador en Azure Active Directory (Azure AD)

El rol de administrador de cuenta de una suscripción a Azure se asigna a la cuenta de correo electrónico que se usa para crear dicha suscripción. El administrador de cuenta es el propietario de la facturación de la suscripción. El administrador de cuenta puede administrar los detalles de la suscripción en el [Centro de cuentas de Azure](https://account.azure.com/Subscriptions).

De forma predeterminada, el rol de administrador de servicios de una suscripción también se asigna a la cuenta de correo electrónico que se usa para crear la suscripción a Azure. El administrador de servicios tiene unos permisos para la suscripción equivalentes a los del rol de propietario basado en RBAC. El administrador de servicios tiene acceso completo a Azure Portal. El administrador de cuenta puede cambiar el administrador de servicios a una cuenta de correo electrónico diferente.

Al crear una suscripción a Azure, puede asociarla a un inquilino de Azure AD existente. De lo contrario, se crea un inquilino de Azure AD con un directorio asociado. El rol de administrador global en el directorio Azure AD se asigna a la cuenta de correo electrónico que se usa para crear la suscripción a Azure AD.

Una cuenta de correo electrónico puede asociarse a varias suscripciones de Azure. El administrador de cuenta puede transferir una suscripción a otra cuenta.

Para ver una descripción detallada de los roles definidos en Azure, consulte [Roles de administrador de suscripciones clásico de RBAC de Azure y de administrador de Azure AD](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

## <a name="subscriptions-and-regions"></a>Suscripciones y regiones

Cada recurso de Azure está asociado lógicamente a una sola suscripción. Al crear un recurso, puede elegir la suscripción a Azure en la que se va a implementar ese recurso. Posteriormente, puede mover un recurso a otra suscripción.

Una suscripción no está vinculada a una región específica de Azure. Sin embargo, cada recurso de Azure se implementa en una sola región. Puede tener recursos en varias regiones que estén asociadas a la misma suscripción.

> [!NOTE]
> La mayoría de los recursos de Azure se implementan en una región específica. Sin embargo, determinados tipos de recursos se consideran recursos globales, como las directivas que se establecen mediante los servicios de Azure Policy.

## <a name="related-resources"></a>Recursos relacionados

Los siguientes recursos proporcionan información detallada sobre los conceptos descritos en este artículo:

- [¿Cómo funciona Azure?](../../getting-started/what-is-azure.md)
- [Administración del acceso a recursos de Azure](../../govern/resource-consistency/resource-access-management.md)
- [Información general sobre Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)
- [Control de acceso basado en rol (RBAC) para recursos de Azure](https://docs.microsoft.com/azure/role-based-access-control/overview)
- [¿Qué es Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis)
- [Asociación o incorporación de una suscripción de Azure al inquilino de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-how-subscriptions-associated-directory)
- [Topologías de Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/plan-connect-topologies)
- [Suscripciones, licencias, cuentas e inquilinos para ofertas de nube de Microsoft](/office365/enterprise/subscriptions-licenses-accounts-and-tenants-for-microsoft-cloud-offerings)

## <a name="next-steps"></a>Pasos siguientes

Ahora que comprende los conceptos fundamentales de Azure, aprenda a [escalar con varias suscripciones de Azure](./scaling-subscriptions.md).

> [!div class="nextstepaction"]
> [Escalado con varias suscripciones de Azure](./scaling-subscriptions.md)
