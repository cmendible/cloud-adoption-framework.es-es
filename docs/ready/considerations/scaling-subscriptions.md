---
title: Escalado con varias suscripciones de Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Aprenda a escalar con varias suscripciones de Azure.
author: alexbuckgit
ms.author: abuck
ms.date: 05/20/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: e795074526db2b5aec88052dc15aa9fa4140a91f
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025141"
---
# <a name="scaling-with-multiple-azure-subscriptions"></a>Escalado con varias suscripciones de Azure

A menudo las organizaciones necesitan más de una suscripción de Azure, como resultado de los límites de recursos y otras consideraciones de gobernanza. Es importante tener una estrategia para escalar las suscripciones.

## <a name="production-and-nonproduction-workloads"></a>Cargas de trabajo de producción y no producción

Al implementar la primera carga de trabajo de producción en Azure, debe empezar con dos suscripciones: una para el entorno de producción y otra para el entorno de no producción (desarrollo/pruebas).

![Modelo de suscripción básico que muestra llaves junto a cuadros de producción y no producción](../../_images/ready/basic-subscription-model.png)

Se recomienda este enfoque por varios motivos:

- Azure tiene ofertas de suscripción específicas para cargas de trabajo de desarrollo y pruebas. Estas ofertas proporcionan tarifas con descuento sobre los servicios y las licencias de Azure.
- Los entornos de producción y no producción probablemente tendrán diferentes conjuntos de directivas de Azure. El uso de suscripciones independientes simplifica la aplicación de cada conjunto de directivas distinto en el nivel de suscripción.
- Puede que quiera tener determinados tipos de recursos de Azure en una suscripción de desarrollo/pruebas para realizar pruebas. Con una suscripción independiente, puede usar esos tipos de recursos sin que estén disponibles en el entorno de producción.
- Puede usar las suscripciones de desarrollo y pruebas como entornos de espacio aislado. Estos espacios aislados permiten a los administradores y desarrolladores crear y eliminar rápidamente conjuntos completos de recursos de Azure. Este aislamiento también puede ayudar con la protección de datos y los problemas de seguridad.
- Los umbrales de costo aceptables es probable que varíen entre las suscripciones de producción y desarrollo y pruebas.

## <a name="other-reasons-for-multiple-subscriptions"></a>Otras razones para tener varias suscripciones

Otras situaciones pueden requerir suscripciones adicionales. Tenga en cuenta lo siguiente al ampliar su espacio en la nube.

- Las suscripciones tienen límites diferentes para diferentes tipos de recursos. Por ejemplo, el número de redes virtuales de una suscripción es limitado. Cuando una suscripción se acerque a cualquiera de sus límites, tendrá que crear otra suscripción y colocar ahí los nuevos recursos.

  Para más información, consulte [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits).

- Cada suscripción puede implementar sus propias directivas para los tipos de recursos que se pueden implementar y las regiones compatibles.

- Las suscripciones en las regiones de la nube pública y en las regiones de la nube soberana o de administración pública tienen diferentes limitaciones. A menudo, están condicionadas por diferentes niveles de clasificación de datos entre entornos.

- Si separa por completo diferentes conjuntos de usuarios por motivos de seguridad o cumplimiento, puede que necesite suscripciones independientes. Por ejemplo, las organizaciones del gobierno nacional pueden tener que limitar el acceso de una suscripción a solo los ciudadanos.

- Distintas suscripciones pueden tener distintos tipos de ofertas, cada una con sus propios términos y ventajas.

- Pueden existir problemas de confianza entre los propietarios de una suscripción y el propietario de los recursos que se van a implementar. El uso de otra suscripción con una propiedad diferente puede mitigar estos problemas; sin embargo, también es necesario tener en cuenta los problemas de red y protección de datos que surgirán en esta implementación.

- Los controles económicos o geopolíticos rígidos pueden exigir disposiciones financieras distintas para suscripciones específicas. Estos problemas pueden incluir consideraciones sobre la soberanía de los datos, empresas con varias subsidiarias, o contabilidad y facturación independientes para unidades de negocio de distintos países y con distintas monedas.

- Los recursos de Azure creados con el modelo de implementación clásica deben aislarse en su propia suscripción. La seguridad de los recursos clásicos es diferente de la de los recursos implementados mediante Azure Resource Manager. No se pueden aplicar directivas de Azure a los recursos clásicos.

- Los administradores de servicios que usan recursos clásicos tienen los mismos permisos que los propietarios de control de acceso basado en rol (RBAC) de una suscripción. Es difícil limitar lo suficiente el acceso de estos administradores de servicios en una suscripción que combina recursos clásicos y recursos de Resource Manager.

También puede optar por crear suscripciones adicionales por otras razones técnicas o empresariales específicas de su organización. Es posible que se generen costos adicionales por la entrada y salida de datos entre las suscripciones.

Puede mover muchos tipos de recursos de una suscripción a otra o usar implementaciones automatizadas para migrar recursos a otra suscripción. Para más información, consulte [Traslado de los recursos a un nuevo grupo de recursos o a una nueva suscripción](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources).

## <a name="managing-multiple-subscriptions"></a>Administración de varias suscripciones

Si solo tiene algunas suscripciones, administrarlas de forma independiente es relativamente sencillo. Pero si tiene muchas suscripciones, considere la posibilidad de crear una jerarquía de grupos de administración para simplificar la administración de suscripciones y recursos.

Los grupos de administración permiten una administración eficaz del acceso, las directivas y el cumplimiento de las suscripciones de una organización. Cada grupo de administración es un contenedor de una o más suscripciones.

Los grupos de administración están organizados en una sola jerarquía. Esta jerarquía se define en el inquilino de Azure Active Directory (Azure AD) para que se alinee con la estructura y las necesidades de la organización. El nivel superior se denomina *grupo de administración raíz*. Puede definir hasta seis niveles de grupos de administración en la jerarquía. Cada suscripción está contenida en un solo grupo de administración.

Azure proporciona cuatro niveles de ámbito administración: grupo de administración, suscripciones, grupos de recursos y recursos. Cualquier acceso o directiva aplicados en un nivel de la jerarquía se hereda por los niveles inferiores. El propietario de un recurso o de una suscripción no puede modificar una directiva heredada. Esta limitación ayuda a mejorar la gobernanza.

> [!NOTE]
> Tenga en cuenta que la herencia de etiquetas no está disponible en este momento, pero lo estará pronto.

Al confiar en este modelo de herencia, puede organizar las suscripciones de la jerarquía de forma que cada suscripción siga las directivas y los controles de seguridad adecuados.

![Los cuatro niveles de ámbito para organizar los recursos de Azure](../../ready/azure-readiness-guide/media/organize-resources/scope-levels.png)

Todas las asignaciones de acceso o directivas en el grupo de administración raíz se aplican a todos los recursos dentro del directorio. Considere cuidadosamente qué elementos define en este ámbito. Incluya solo las asignaciones que debe tener.

Al definir inicialmente la jerarquía de grupos de administración, primero debe crear el grupo de administración raíz. A continuación, mueva todas las suscripciones existentes en el directorio al grupo de administración raíz. Las nuevas suscripciones siempre se crean en el grupo de administración raíz. Posteriormente, puede moverlas a otro grupo de administración.

Cuando se mueve una suscripción a un grupo de administración existente, se heredan las asignaciones de directivas y roles de la jerarquía de grupos de administración que se encuentra por encima. Una vez que haya establecido varias suscripciones para las cargas de trabajo de Azure, debe crear suscripciones adicionales para que contengan los servicios de Azure que otras suscripciones comparten.

![Ejemplo de una jerarquía de grupos de administración](../../_images/ready/management-group-hierarchy.png)

Para más información, consulte [Organización de los recursos con grupos de administración de Azure](https://docs.microsoft.com/azure/governance/management-groups).

## <a name="tips-for-creating-new-subscriptions"></a>Sugerencias para crear suscripciones

- Identifique quién será responsable de crear las suscripciones.
- Decida qué recursos estarán en una suscripción de forma predeterminada.
- Decida el aspecto de todas las suscripciones estándar. Es necesario considerar el acceso RBAC, las directivas, las etiquetas y los recursos de infraestructura.
- Si es posible, [use una entidad de servicio](https://docs.microsoft.com/azure/azure-resource-manager/grant-access-to-create-subscription) para crear suscripciones. Defina un grupo de seguridad que pueda solicitar nuevas suscripciones a través de un flujo de trabajo automatizado.
- Si es cliente de un Contrato Enterprise (EA), pídale al servicio de soporte técnico de Azure que bloquee la creación de suscripciones no EA en su organización.

## <a name="related-resources"></a>Recursos relacionados

- [Conceptos básicos de Azure](./fundamental-concepts.md).
- [Organización de los recursos con grupos de administración de Azure](https://docs.microsoft.com/azure/governance/management-groups).
- [Elevación de los privilegios de acceso para administrar todas las suscripciones y los grupos de administración de Azure](https://docs.microsoft.com/azure/role-based-access-control/elevate-access-global-admin).
- [Traslado de recursos de Azure a otro grupo de recursos o a otra suscripción](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-move-resources).

## <a name="next-steps"></a>Pasos siguientes

Revise las [convenciones de recomendadas de nomenclatura y etiquetado](./naming-and-tagging.md) que se deben seguir al implementar los recursos de Azure.

> [!div class="nextstepaction"]
> [Convenciones recomendadas de nomenclatura y etiquetado](./naming-and-tagging.md)
