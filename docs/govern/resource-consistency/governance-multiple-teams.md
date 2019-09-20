---
title: Diseño de gobernanza en Azure para varios equipos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Guía para configurar controles de gobernanza de Azure para varios equipos, varias cargas de trabajo y varios entornos.
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: d9b1dddff5cadd9219e6dffad87690145214b162
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031332"
---
# <a name="governance-design-for-multiple-teams"></a>Diseño de gobernanza para varios equipos

El objetivo de esta guía es ayudarle a obtener información sobre el proceso de diseño de un modelo de gobernanza de recursos en Azure que admita varios equipos, varias cargas de trabajo y varios entornos. Primero, veremos un conjunto de requisitos de gobernanza hipotéticos y, después, describiremos varias implementaciones de ejemplo que cumplen dichos requisitos.

Los requisitos son:

- La empresa planea la transición de nuevos roles y responsabilidades en la nube a un conjunto de usuarios y, por tanto, se requiere la administración de identidades para varios equipos con diferentes necesidades de acceso a los recursos de Azure. Este sistema de administración de identidades es necesario para almacenar la identidad de los usuarios siguientes:
  - La persona de la organización responsable de la propiedad de las **suscripciones**.
  - La persona de la organización responsable de los **recursos de la infraestructura compartida** utilizados para conectar la red local a una red virtual de Azure.
  - Dos personas de la organización responsables de administrar una **carga de trabajo**.
- Compatibilidad para varios **entornos**. Un entorno es una agrupación lógica de recursos, como máquinas virtuales, redes virtuales y servicios de enrutamiento de tráfico de red. Estos grupos de recursos tienen requisitos de seguridad y administración similares y se suelen usar para un propósito específico, como pruebas o producción. En este ejemplo, son necesarios tres entornos:
  - Un **entorno de infraestructura compartida** que incluya los recursos compartidos por las cargas de trabajo en otros entornos. Por ejemplo, una red virtual con una subred de puerta de enlace que proporciona conectividad con el entorno local.
  - Un **entorno de producción** con las directivas de seguridad más restrictivas. Puede incluir las cargas de trabajo de acceso interno o externo.
  - Un **entorno de desarrollo** para los trabajos de pruebas y prueba de concepto. Las directivas de seguridad, de cumplimiento normativo y de costos de este entorno difieren de los del entorno de producción.
- Un **modelo de permisos de privilegios mínimos** en el cual los usuarios no poseen permisos de forma predeterminada. El modelo debe admitir lo siguiente:
  - Un único usuario de confianza en el ámbito de la suscripción con permiso para asignar derechos de acceso a los recursos.
  - De forma predeterminada, a los propietarios de las cargas de trabajo se les deniega el acceso a los recursos. Los derechos de acceso a los recursos los concede explícitamente el usuario de confianza solo en el ámbito de la suscripción.
  - Acceso de administración a los recursos de la infraestructura compartida limitado al propietario de la infraestructura compartida.
  - Acceso de administración a cada carga de trabajo restringido al propietario de la carga de trabajo.
  - La empresa no quiere tener que administrar los roles de forma independiente en cada uno de los tres entornos, por lo tanto, solo se necesita el uso de los [roles de integrados](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles) que están disponibles en el control de acceso basado en rol (RBAC). Si la empresa ha usado roles personalizados de RBAC, será necesario un proceso adicional para sincronizar los roles personalizados en los tres entornos.
- Seguimiento de los costos por nombre de propietario de la carga de trabajo, entorno o ambos.

## <a name="identity-management"></a>Administración de identidades

Antes de diseñar la administración de identidades para nuestro modelo de gobernanza, es importante comprender las cuatro áreas principales que incluye:

- **Administración:** procesos y herramientas para crear, editar y eliminar identidades de usuario.
- **Autenticación:** validación de las credenciales, por ejemplo, nombre de usuario y contraseña, para comprobar la identidad del usuario.
- **Authorization:** determinación de cuáles son los recursos a los que puede acceder un usuario autenticado o qué operaciones está autorizado a realizar.
- **Auditoría:** revisión periódica de los registros y otra información para detectar problemas de seguridad relacionados con la identidad de los usuarios. Esto incluye la revisión de los patrones de uso sospechosos, la revisión periódica de los permisos de usuario para comprobar que son precisos, entre otras funciones.

Hay solo un servicio de Azure de confianza para la identidad y es Azure Active Directory (Azure AD). Los usuarios se agregan a Azure AD, que se usa para todas las funciones enumeradas anteriormente. Pero antes de ver cómo configurar Azure AD, es importante comprender las cuentas con privilegios que se utilizan para administrar el acceso a estos servicios.

Cuando la organización se registró para una cuenta de Azure, se asignó al menos un **propietario de la cuenta** de Azure. Además, se creó un **inquilino** de Azure AD, a menos que ya hubiera un inquilino asociado con el uso por parte de la organización de otros servicios de Microsoft como Office 365. Al crear el inquilino de Azure AD, se asocia un **administrador global** con permisos completos.

Ambas identidades de usuario, administrador global de Azure AD y propietario de la cuenta de Azure, se almacenan en un sistema de identidades de alta seguridad administrado por Microsoft. El propietario de la cuenta de Azure tiene autorización para crear, actualizar y eliminar suscripciones. El administrador global de Azure AD tiene autorización para realizar muchas acciones en Azure AD pero, para los fines de esta guía de diseño, nos centraremos en la creación y eliminación de identidades de usuario.

> [!NOTE]
> Puede que su organización ya tenga un inquilino de Azure AD si ya hay un licencia de Office 365 o Intune asociada a su cuenta.

El propietario de la cuenta de Azure tiene permiso para crear, actualizar y eliminar suscripciones:

![Cuenta de Azure con el administrador de cuentas de Azure y el administrador global de Azure AD](../../_images/govern/design/governance-3-0.png)
*Figura 1: Una cuenta de Azure con un administrador de cuentas y un administrador global de Azure AD.*

El **administrador global** de Azure AD tiene permiso para crear cuentas de usuario:

![Cuenta de Azure con el administrador de cuentas de Azure y el administrador global de Azure AD](../../_images/govern/design/governance-3-0a.png)
*Figura 2: El administrador global de Azure AD crea las cuentas de usuario necesarias en el inquilino.*

Las dos primeras cuentas, **propietario de la carga de trabajo de App1** y **propietario de la carga de trabajo de App2**, están asociadas a una persona de la organización responsable de administrar una carga de trabajo. La cuenta de **operaciones de red** pertenece a la persona responsable de los recursos de la infraestructura compartida. Por último, la cuenta del **propietario de la suscripción** está asociada con la persona responsable de la propiedad de las suscripciones.

## <a name="resource-access-permissions-model-of-least-privilege"></a>Modelo de permisos de acceso a recursos con privilegios mínimos

Ahora que tenemos las cuentas de usuario y el sistema de administración de identidades creados, hay que decidir cómo se aplicarán los roles del control de acceso basado en rol (RBAC) a cada cuenta para admitir un modelo de permisos con privilegios mínimos.

Otro requisito indica que los recursos asociados a cada carga de trabajo estén aislados entre sí para que ningún propietario de carga de trabajo tenga acceso administrativo a otras cargas de trabajo que no les pertenezcan. También hay un requisito para implementar este modelo solo con los roles integrados del control de acceso basado en rol de Azure.

Cada rol RBAC se aplica en uno de los tres ámbitos en Azure: **suscripción**, **grupo de recursos** y **recursos** individuales. Los roles se heredan en los ámbitos inferiores. Por ejemplo, si a un usuario se le asigna el [rol de propietario integrado](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) en el nivel de suscripción, ese rol también se asigna a ese usuario en el nivel de recurso individual y grupal, a menos que se invalide.

Por lo tanto, para crear un modelo de acceso con privilegios mínimos, hay que decidir qué acciones puede realizar un determinado tipo de usuario en cada uno de estos tres ámbitos. Por ejemplo, el requisito es que el propietario de una carga de trabajo tenga permiso para administrar el acceso únicamente a los recursos asociados con su carga de trabajo y no a otros. Si quisiéramos asignar el rol de propietario integrado en el ámbito de la suscripción, cada propietario de carga de trabajo tendría acceso de administración a todas las cargas de trabajo.

Veamos dos ejemplos de modelos de permisos para entender este concepto algo mejor. En el primer ejemplo, el modelo confía solo en el administrador de servicios para crear grupos de recursos. En el segundo ejemplo, el modelo asigna el rol de propietario integrado a cada propietario de carga de trabajo en el ámbito de la suscripción.

En ambos ejemplos, hay un administrador de servicios de suscripción al que se asigna el rol de propietario integrado en el ámbito de la suscripción. Recuerde que el rol de propietario integrado concede todos los permisos, incluida la administración del acceso a los recursos.
![Administrador del servicio de suscripciones con el rol de propietario](../../_images/govern/design/governance-2-1.png)
*Figura 3: Una suscripción con un administrador de servicios al que se le ha asignado el rol de propietario integrado.*

1. En el primer ejemplo, está el **propietario de carga de trabajo A** sin ningún permiso en el ámbito de suscripción. De forma predeterminada, no tienen derechos de administración de acceso a los recursos. Este usuario quiere volver a implementar y administrar los recursos de su carga de trabajo. Debe ponerse en contacto con el **administrador de servicios** para pedir la creación de un grupo de recursos.
    ![el propietario de la carga de trabajo solicita la creación del grupo de recursos A](../../_images/govern/design/governance-2-2.png)
2. El **administrador de servicios** revisa la solicitud y crea el **grupo de recursos A**. En este momento, el **propietario de carga de trabajo A** aún no tiene permiso para hacer nada.
    ![el administrador de servicios crea el grupo de recursos A](../../_images/govern/design/governance-2-3.png)
3. El **administrador de servicios** agrega el **propietario de carga de trabajo A** al **grupo de recursos A** y le asigna el [rol de colaborador integrado](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor). El rol de colaborador concede todos los permisos en el **grupo de recursos A** excepto la administración de los permisos de acceso.
    ![El administrador de servicios agrega el propietario de carga de trabajo A al grupo de recursos A](../../_images/govern/design/governance-2-4.png)
4. Supongamos que el **propietario de carga de trabajo A** necesita que un par de miembros del equipo vean los datos de supervisión del tráfico de red y la CPU como parte de la planeación de la capacidad para la carga de trabajo. Dado que el **propietario de carga de trabajo A** tiene asignado el rol de colaborador, no tiene permiso para agregar un usuario al **grupo de recursos A**. Debe enviar esta solicitud al **administrador de servicios**.
    ![el propietario de la carga de trabajo solicita que los colaboradores de carga de trabajo se añadan al grupo de recursos](../../_images/govern/design/governance-2-5.png)
5. El **administrador de servicios** revisa la solicitud y agrega los dos usuarios **colaboradores de carga de trabajo** al **grupo de recursos A**. Ninguno de estos dos usuarios necesitan permiso para administrar los recursos, por lo que se les asigna el [rol de lector integrado](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor).
    ![el administrador de servicios añade colaboradores de carga de trabajo al grupo de recursos A](../../_images/govern/design/governance-2-6.png)
6. El **propietario de carga de trabajo B** también necesita un grupo de recursos para incluir los recursos de su carga de trabajo. Al igual que con el **propietario de carga de trabajo A**, el **propietario de carga de trabajo B** inicialmente no tiene permisos para realizar ninguna acción en el ámbito de la suscripción, por lo que debe enviar una solicitud al **administrador de servicios**.
    ![el propietario de carga de trabajo B solicita la creación del grupo de recursos B](../../_images/govern/design/governance-2-7.png)
7. El **administrador de servicios** revisa la solicitud y crea el **grupo de recursos B**.  ![el administrador de servicios crea el grupo de recursos B](../../_images/govern/design/governance-2-8.png)
8. El **administrador de servicios** agrega el **propietario de carga de trabajo B** al **grupo de recursos B** y le asigna el rol de colaborador integrado.
    ![El administrador de servicios agrega el propietario de carga de trabajo B al grupo de recursos B](../../_images/govern/design/governance-2-9.png)

En este momento, cada uno de los propietarios de carga de trabajo está aislado en su propio grupo de recursos. Ninguno de los propietarios de carga de trabajo ni los miembros del equipo tienen acceso administrativo a los recursos de otros grupos de recursos.

![Suscripción con los grupos de recursos A y B](../../_images/govern/design/governance-2-10.png)
*Figura 4: Una suscripción con dos propietarios de cargas de trabajo aisladas con su propio grupo de recursos.*

Este modelo es un modelo de privilegios mínimos; a cada usuario se le asignan los permisos correctos en el ámbito de administración de recursos correcto.

Sin embargo, tenga en cuenta que todas las tareas del ejemplo las realizó el **administrador de servicios**. Este es un ejemplo sencillo y quizás esto no parezca un problema porque hay solo dos propietarios de cargas de trabajo, pero es fácil imaginar los tipos de problemas que habría en una organización grande. Por ejemplo, el **administrador de servicios** puede convertirse en un cuello de botella con muchas solicitudes acumuladas que, como resultado, producen retrasos.

Veamos otro ejemplo que reduce el número de tareas realizadas por el **administrador de servicios**.

1. En este modelo, al **propietario de la carga de trabajo A** se le asigna el rol de propietario integrado en el ámbito de la suscripción, lo que le permite crear su propio grupo de recursos: **grupo de recursos A**.  ![El administrador de servicios agrega el propietario de carga de trabajo A a la suscripción](../../_images/govern/design/governance-2-11.png)
2. Cuando se crea el **grupo de recursos A**, se agrega el **propietario de la carga de trabajo A** de forma predeterminada y se hereda el rol de propietario integrado del ámbito de la suscripción.
    ![El propietario de carga de trabajo A crea el grupo de recursos A](../../_images/govern/design/governance-2-12.png)
3. El rol de propietario integrado concede al **propietario de la carga de trabajo A** permisos para administrar el acceso al grupo de recursos. El **propietario de la carga de trabajo A** agrega dos **colaboradores de carga de trabajo** y les asigna a cada uno el rol de lector integrado.
    ![El propietario de carga de trabajo A agrega colaboradores de carga de trabajo](../../_images/govern/design/governance-2-13.png)
4. Ahora, el **administrador de servicios** agrega el **propietario de carga de trabajo B** a la suscripción con el rol de propietario integrado.
    ![El administrador de servicios agrega el propietario de carga de trabajo B a la suscripción](../../_images/govern/design/governance-2-14.png)
5. El **propietario de carga de trabajo B** crea el **grupo de recursos B** y se agrega de forma predeterminada. Una vez más, el **propietario de carga de trabajo B** hereda el rol de propietario integrado del ámbito de la suscripción.
    ![El propietario de carga de trabajo B crea el grupo de recursos B](../../_images/govern/design/governance-2-15.png)

Tenga en cuenta que, en este modelo, el **administrador de servicios** realizó menos acciones que en el primer ejemplo debido a que se delegó la administración del acceso a cada uno de los propietarios de carga de trabajo individuales.

![Suscripción con los grupos de recursos A y B](../../_images/govern/design/governance-2-16.png)
*Figura 5: Una suscripción con un administrador de servicios y dos propietarios de cargas de trabajo, todos ellos con el rol de propietario integrado asignado.*

Sin embargo, como el **propietario de carga de trabajo A** y el **propietario de carga de trabajo B** tienen asignado el rol de propietario integrado en el ámbito de la suscripción, han heredado el rol de propietario integrado del grupo de recursos del otro. Esto significa que no solo tienen acceso total a los recursos del otro, también pueden delegar el acceso administrativo a los grupos de recursos del otro. Por ejemplo, el **propietario de carga de trabajo B** tiene derechos para agregar otros usuarios al **grupo de recursos A** y puede asignarles cualquier rol, como el rol de propietario integrado.

Si comparamos cada ejemplo con los requisitos, vemos que ambos ejemplos admiten un único usuario de confianza en el ámbito de la suscripción con permisos para conceder derechos de acceso a los recursos a los dos propietarios de carga de trabajo. Ninguno de los dos propietarios de carga de trabajo tenía acceso a la administración de recursos de forma predeterminada y necesitaron que el **administrador de servicios** les asignara los permisos explícitamente. Sin embargo, solo el primer ejemplo admite que los recursos asociados a cada carga de trabajo estén aislados entre sí de manera que ningún propietario de carga de trabajo tenga acceso a los recursos de otras cargas de trabajo.

## <a name="resource-management-model"></a>Modelo de administración de recursos

Ahora que hemos diseñado un modelo de permisos con privilegios mínimos, vamos a ver algunas aplicaciones prácticas de estos modelos de gobernanza. Recuerde que los requisitos son que debemos admitir los siguientes tres entornos:

1. **Infraestructura compartida:** un solo grupo de recursos que comparten todas las cargas de trabajo. Estos son recursos tales como puertas de enlace de red, firewalls y servicios de seguridad.
2. **Desarrollo:** varios grupos de recursos que representan varias cargas de trabajo que no están listas para producción. Estos recursos se utilizan para pruebas de concepto, pruebas y otras actividades de desarrollo. Estos recursos pueden tener un modelo de gobernanza más flexible para ofrecer más agilidad a los desarrolladores.
3. **Producción:** varios grupos de recursos que representan varias cargas de trabajo de producción. Estos recursos se utilizan para hospedar los artefactos de aplicación de acceso privado y público. Estos recursos normalmente tienen una gobernanza y modelos de seguridad más estrictos para proteger los recursos, el código de la aplicación y los datos contra accesos no autorizados.

En cada uno de estos tres entornos, hay que realizar el seguimiento de los datos de costo por **propietario de carga de trabajo**, **entorno** o ambos. Es decir, queremos saber el costo actual de la **infraestructura compartida**, los costos en los que incurren las personas tanto en el entorno de **desarrollo** como de **producción** y, por último, el costo total de **desarrollo** y **producción**.

Ya ha aprendido que el ámbito de los recursos se establece en dos niveles: **suscripción** y **grupo de recursos**. Por lo tanto, la primera decisión es cómo organizar los entornos por **suscripción**. Hay solo dos posibilidades: una sola suscripción o varias suscripciones.

Antes de adentrarnos en los ejemplos de cada uno de estos modelos, revisemos la estructura de administración de las suscripciones de Azure.

Recuerde que necesitamos tener una persona en la organización que sea responsable de las suscripciones y que este usuario tiene la cuenta de **propietario de la suscripción** en el inquilino de Azure AD. Sin embargo, esta cuenta no tiene permisos para crear suscripciones. Solo el **propietario de la cuenta de Azure** tiene permisos para hacerlo:

![Un propietario de la cuenta de Azure crea una suscripción](../../_images/govern/design/governance-3-0b.png)
*Figura 6. El propietario de la cuenta de Azure crea una suscripción.*

Una vez creada la suscripción, el **propietario de la cuenta de Azure** puede agregar la cuenta de **propietario de la suscripción** a la suscripción con el rol de **propietario**:

![El propietario de la cuenta de Azure agrega la cuenta de usuario de propietario de la suscripción a la suscripción con el rol de propietario. ](../../_images/govern/design/governance-3-0c.png)
*Figura 7: El propietario de la cuenta de Azure agrega la cuenta de usuario de **propietario de la suscripción** a la suscripción con el rol de **propietario**.*

Ahora, el **propietario de la suscripción** puede crear **grupos de recursos** y delegar la administración del acceso a los recursos.

Veamos primero un ejemplo de un modelo de administración de recursos con una sola suscripción. La primera decisión es cómo alinear los grupos de recursos con los tres entornos. Tiene dos opciones:

1. Alinear cada entorno con un único grupo de recursos. Todos los recursos de la infraestructura compartida se implementan en un único grupo de recursos de la **infraestructura compartida**. Todos los recursos asociados con las cargas de trabajo de desarrollo se implementan en un único grupo de recursos de **desarrollo**. Todos los recursos asociados con las cargas de trabajo de producción se implementan en un solo grupo de recursos de **producción** para el entorno de **producción**.
2. Crear grupos de recursos independientes para cada carga de trabajo, utilizando una convención de nomenclatura y etiquetas para alinear los grupos de recursos con cada uno de los tres entornos.

Comencemos evaluando la primera opción. Vamos a usar el modelo de permisos que analizamos en la sección anterior, con un único administrador de servicios de la suscripción que crea los grupos de recursos y agrega los usuarios a ellos con el rol integrado de **colaborador** o **lector**.

1. El primer grupo de recursos implementado representa el entorno de **infraestructura compartida**. El **propietario de la suscripción** crea un grupo de recursos para los recursos de la infraestructura compartida llamado `netops-shared-rg`.
    ![Creación de un grupo de recursos](../../_images/govern/design/governance-3-0d.png)
2. El **propietario de la suscripción** agrega la cuenta del **usuario de operaciones de red** al grupo de recursos y le asigna el rol de **colaborador**.
    ![Adición de un usuario de operaciones de red](../../_images/govern/design/governance-3-0e.png)
3. El **usuario de operaciones de red** crea una [puerta de enlace VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) y la configura para que se conecte al dispositivo VPN local. El **usuario de operaciones de red** también aplica un par de [etiquetas](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) a cada uno de los recursos: *environment:shared* y *managedBy:netOps*. Cuando el **administrador de servicios de suscripción** exporta un informe de costos, los costos se alinearán con cada una de estas etiquetas. Esto permite al **administrador de servicios de suscripción** dinamizar los costos con las etiquetas *environment* y *managedBy*. Observe el contador **límites de recursos** en la parte superior derecha de la ilustración. Cada suscripción de Azure tiene [límites de servicio](https://docs.microsoft.com/azure/azure-subscription-service-limits) y, para ayudarle a comprender el efecto de estos límites, seguiremos los límites de redes virtuales para cada suscripción. Hay un límite de 1000 redes virtuales por suscripción y, después de implementar la primera red virtual, quedan 999 disponibles.
    ![Creación de una puerta de enlace de VPN](../../_images/govern/design/governance-3-1.png)
4. Se implementan dos grupos de recursos más. El primero se llama `prod-rg`. Este grupo de recursos se alinea con el entorno de producción. El segundo se llama `dev-rg` y se alinea con el entorno de desarrollo. Todos los recursos asociados con las cargas de trabajo de producción se implementan en el entorno de producción y todos los recursos asociados con las cargas de trabajo de desarrollo se implementan en el entorno de desarrollo. En este ejemplo solo implementaremos dos cargas de trabajo en cada uno de estos dos entornos, por lo que no encontraremos ningún límite del servicio de suscripción de Azure. Sin embargo, hay que tener en cuenta que cada grupo de recursos tiene un límite de 800 recursos por grupo. Si continúa agregando cargas de trabajo a cada grupo de recursos, finalmente se alcanzará este límite.
    ![Creación de grupos de recursos](../../_images/govern/design/governance-3-2.png)
5. El primer **propietario de carga de trabajo** envía una solicitud al **administrador de servicios de suscripción** y se agrega a cada uno de los grupos de recursos de los entornos de desarrollo y producción con el rol de **colaborador**. Tal y como hemos visto, el rol de **colaborador** permite al usuario realizar cualquier operación distinta de la asignación de un rol a otro usuario. Ahora, el primer **propietario de carga de trabajo** puede crear los recursos asociados con la carga de trabajo.
    ![Adición de colaboradores](../../_images/govern/design/governance-3-3.png)
6. El primer **propietario de carga de trabajo** crea una red virtual en cada uno de los dos grupos de recursos con un par de máquinas virtuales en cada una. El primer **propietario de carga de trabajo** aplica las etiquetas *environment* y *managedBy* a todos los recursos. Tenga en cuenta que el contador de límite de servicio de Azure ahora está en 997 redes virtuales restantes.
    ![Creación de redes virtuales](../../_images/govern/design/governance-3-4.png)
7. Ninguna de las redes virtuales tiene conectividad local cuando se crean. En este tipo de arquitectura, se debe emparejar cada red virtual con la red virtual *hub-vnet* en el entorno de la **infraestructura compartida**. El emparejamiento de redes virtuales crea una conexión entre dos redes virtuales diferentes y permite que el tráfico de red viaje entre ellas. Tenga en cuenta que el emparejamiento de redes virtuales no es intrínsecamente transitivo. Un emparejamiento debe especificarse entre las dos redes virtuales que están conectadas y, si solo una de las redes virtuales especifica un emparejamiento, la conexión está incompleta. Para mostrar este efecto, el primer **propietario de carga de trabajo** especifica un emparejamiento entre **prod-vnet** y **hub-vnet**. Se crea el primer emparejamiento, pero el tráfico no circula porque el emparejamiento complementario de **hub-vnet** a **prod-vnet** todavía no se ha especificado. El primer **propietario de carga de trabajo** se pone en contacto con el usuario de **operaciones de red** y solicita esta conexión de emparejamiento complementaria.
    ![Creación de una conexión de emparejamiento](../../_images/govern/design/governance-3-5.png)
8. El usuario de **operaciones de red** revisa la solicitud, la aprueba y luego especifica el emparejamiento en la configuración de **hub-vnet**. La conexión de emparejamiento ya está completa y el tráfico de red circula entre las dos redes virtuales.
    ![Creación de una conexión de emparejamiento](../../_images/govern/design/governance-3-6.png)
9. Ahora, el segundo **propietario de carga de trabajo** envía una solicitud al **administrador de servicios de suscripción** y se agrega a los grupos de recursos existentes en los entornos de **desarrollo** y **producción** con el rol de **colaborador**. El segundo **propietario de carga de trabajo** tiene los mismos permisos en todos los recursos que el primer **propietario de carga de trabajo** en cada grupo de recursos.
    ![Adición de colaboradores](../../_images/govern/design/governance-3-7.png)
10. El segundo **propietario de carga de trabajo** crea una subred en la red virtual **prod-vnet** y luego agrega dos máquinas virtuales. El segundo **propietario de carga de trabajo** aplica las etiquetas *environment* y *managedBy* a todos los recursos.
    ![Creación de subredes](../../_images/govern/design/governance-3-8.png)

Este modelo de administración de recursos de ejemplo permite administrar los recursos en los tres entornos necesarios. Los recursos de la infraestructura compartida están protegidos porque hay un único usuario en la suscripción con permisos para acceder a esos recursos. Cada uno de los propietarios de cargas de trabajo puede utilizar los recursos de la infraestructura compartida sin tener permisos en los recursos compartidos en sí. Sin embargo, este modelo de administración no cumple el requisito de aislamiento de las cargas de trabajo; los dos **propietarios de cargas de trabajo** pueden acceder a los recursos de la otra carga de trabajo.

Hay otra consideración importante con este modelo puede no resultar obvio a simple vista. En el ejemplo, el **propietario de carga de trabajo app1** solicitó la conexión de emparejamiento de red con la red virtual **hub-vnet** para proporcionar conectividad al entorno local. El usuario de **operaciones de red** evaluó la solicitud según los recursos implementados con esa carga de trabajo. Cuando el **propietario de la suscripción** agregó al **propietario de carga de trabajo app2** con el rol de **colaborador**, ese usuario tenía derechos de acceso de administración a todos los recursos del grupo de recursos **prod-rg**.

![Diagrama que muestra los derechos de acceso de administración](../../_images/govern/design/governance-3-10.png)

Esto significa que el **propietario de carga de trabajo app2** tenía permisos para implementar su propia subred con máquinas virtuales en la red virtual **prod-vnet**. De forma predeterminada, esas máquinas virtuales ahora tienen acceso a la red local. El usuario de **operaciones de red** no es consciente de esas máquinas y no aprobó su conectividad al entorno local.

Ahora, veamos a un única suscripción con varios grupos de recursos para diferentes entornos y cargas de trabajo. Tenga en cuenta que, en el ejemplo anterior, los recursos de cada entorno se podían identificar fácilmente porque estaban en el mismo grupo de recursos. Ahora que ya no tenemos esa agrupación, tenemos que utilizar una convención de nomenclatura en el grupo de recursos para proporcionar esa funcionalidad.

1. Los recursos de la **infraestructura compartida** seguirán teniendo un grupo de recursos independiente en este modelo, por lo que esta parte sigue igual. Cada carga de trabajo requiere dos grupos de recursos: uno para cada uno de los entornos de **desarrollo** y **producción**. Para la primera carga de trabajo, el **propietario de la suscripción** crea dos grupos de recursos. El primero se llama **app1-prod-rg** y el segundo se llama **app1-dev-rg**. Tal y como se indicó anteriormente, esta convención de nomenclatura identifica los recursos como asociados con la primera carga de trabajo, **app1**, y el entorno **dev** o **prod**. Una vez más, el propietario de la *suscripción* agrega el **propietario de la carga de trabajo app1** al grupo de recursos con el rol de **colaborador**.
    ![Adición de colaboradores](../../_images/govern/design/governance-3-12.png)
2. De forma similar al primer ejemplo, el **propietario de carga de trabajo app1** implementa una red virtual llamada **app1-prod-vnet** en el entorno de **producción** y otra llamada **app1-dev-vnet** en el entorno de **desarrollo**. Una vez más, el **propietario de carga de trabajo app1** envía una solicitud al usuario de **operaciones de red** para crear una conexión de emparejamiento. Tenga en cuenta que el **propietario de carga de trabajo app1** agrega las mismas etiquetas que en el primer ejemplo, y el límite de contadores se ha reducido a 997 redes virtuales disponibles en la suscripción.
    ![Creación de una conexión de emparejamiento](../../_images/govern/design/governance-3-13.png)
3. El **propietario de la suscripción** ahora crea dos grupos de recursos para el **propietario de carga de trabajo app2**. Siguiendo las mismas convenciones que para el **propietario de carga de trabajo app1**, los grupos de recursos se llaman **app2-prod-rg** y **app2-dev-rg**. El **propietario de la suscripción** agrega el **propietario de carga de trabajo app2** a cada uno de los grupos de recursos con el rol de **colaborador**.
    ![Adición de colaboradores](../../_images/govern/design/governance-3-14.png)
4. El *propietario de carga de trabajo app2* implementa las redes virtuales y las máquinas virtuales en los grupos de recursos con las mismas convenciones de nomenclatura. Se agregan las etiquetas y el contador de límite se ha reducido a 995 redes virtuales disponibles en la *suscripción*.
    ![Implementación de redes virtuales y máquinas virtuales](../../_images/govern/design/governance-3-15.png)
5. El *propietario de carga de trabajo app2* envía una solicitud al usuario de *operaciones de red* para emparejar la *app2-prod-vnet* con *hub-vnet*. El usuario de *operaciones de red* crea la conexión de emparejamiento.
    ![Creación de una conexión de emparejamiento](../../_images/govern/design/governance-3-16.png)

El modelo de administración resultante es similar al primer ejemplo, con algunas diferencias importantes:

- Cada una de las dos cargas de trabajo se aísla por carga de trabajo y por entorno.
- Este modelo requiere dos redes virtuales más que el primer ejemplo de modelo. Aunque esto no supone mucha diferencia cuando solo hay dos cargas de trabajo, el límite teórico en el número de cargas de trabajo en este modelo es 24.
- Los recursos ya no se agrupan en un único grupo de recursos para cada entorno. Para agrupar los recursos es necesario conocer las convenciones de nomenclatura que se usan en cada entorno.
- El usuario de *operaciones de red* ha revisado y aprobado cada una de las conexiones de emparejamiento de red virtual.

Veamos ahora un ejemplo de un modelo de administración de recursos con varias suscripciones. En este modelo, alinearemos cada uno de los tres entornos con una suscripción diferente: una suscripción de **servicios compartidos**, una suscripción de **producción** y, por último, una suscripción de **desarrollo**. Las consideraciones para este modelo son similares a las del modelo con una sola suscripción en el sentido de que hay que decidir cómo alinear los grupos de recursos con las cargas de trabajo. Ya hemos determinado que crear un grupo de recursos para cada carga de trabajo satisface el requisito de aislamiento de las cargas de trabajo, por lo que nos quedaremos con ese modelo en este ejemplo.

1. En este modelo, hay tres *suscripciones*: *infraestructura compartida*, *producción* y *desarrollo*. Cada una de estas tres suscripciones requiere un *propietario de la suscripción* y, en el ejemplo sencillo, usaremos la misma cuenta de usuario para las tres. Los recursos de la *infraestructura compartida* se administran de manera similar a los primeros dos ejemplos anteriores, y la primera carga de trabajo se asocia con *app1-rg* en el entorno de *producción* y el segundo grupo de recursos con el mismo nombre en el entorno de *desarrollo*. El *propietario de carga de trabajo app1* se agrega a cada uno de los grupos de recursos con el rol de *colaborador*.
    ![Adición de colaboradores](../../_images/govern/design/governance-3-17.png)
2. Al igual que en los ejemplos anteriores, el *propietario de carga de trabajo app1* crea los recursos y solicita la conexión de emparejamiento con la red virtual de la *infraestructura compartida*. El *propietario de carga de trabajo app1* agrega solo la etiqueta *managedBy* porque ya no se necesita la etiqueta *environment*. Es decir, los recursos de cada entorno están agrupados en la misma *suscripción* y la etiqueta *environment* es redundante. El contador de límite se reduce a 999 redes virtuales disponibles.
    ![Creación de una conexión de emparejamiento](../../_images/govern/design/governance-3-18.png)
3. Por último, el *propietario de la suscripción* repite el proceso para la segunda carga de trabajo, y agrega el *propietario de carga de trabajo app2* a los grupos de recursos con el rol de colaborador. El contador de límite para cada una de las suscripciones del entorno se reducido a 998 redes virtuales disponibles.

Este modelo de administración tiene las ventajas del segundo ejemplo anterior. Sin embargo, la principal diferencia es que los límites suponen un problema menor porque se extienden a dos *suscripciones*. El inconveniente es que los datos de costos que se controlan con las etiquetas se deben agregar a las tres *suscripciones*.

Por lo tanto, puede seleccionar cualquiera de estos dos ejemplos de modelos de administración de recursos según la prioridad de sus requisitos. Si prevé que su organización no llegará a los límites de servicio para una sola suscripción, puede utilizar una sola suscripción con varios grupos de recursos. Por el contrario, si su organización anticipa muchas cargas de trabajo, puede ser mejor tener varias suscripciones para cada entorno.

## <a name="implementing-the-resource-management-model"></a>Implementación del modelo de administración de recursos

Ha aprendido varios modelos diferentes para gobernar el acceso a los recursos de Azure. Ahora veremos los pasos necesarios para implementar el modelo de administración de recursos con una suscripción para cada uno de los entornos de **infraestructura compartida**, **producción** y **desarrollo** con la guía de diseño. Tendremos un **propietario de la suscripción** para los tres entornos. Cada carga de trabajo se aislará en un **grupo de recursos** y se agregará **propietario de carga de trabajo** con el rol de **colaborador**.

> [!NOTE]
> Lea la [introducción al acceso a los recursos de Azure](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles) para más información sobre la relación entre las cuentas y las suscripciones de Azure.

Siga estos pasos:

1. Cree una [cuenta de Azure](https://docs.microsoft.com/azure/active-directory/sign-up-organization) si su organización aún no tiene una. La persona que se suscribe a la cuenta de Azure se convierte en el administrador de la cuenta de Azure y los responsables de su organización deben seleccionar la persona que asumirá este rol. Esta persona será responsable de:
    - Crear suscripciones
    - Crear y administrar los inquilinos de [Azure Active Directory (AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) que almacenan las identidades de usuario de esas suscripciones
2. El equipo directivo de su organización decide qué personas son responsables de:
    - Administrar las identidades de usuario; de forma predeterminada, se crea un [inquilino de Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant) cuando se crea la cuenta de Azure de su organización y el administrador de la cuenta se agrega como [administrador global de Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles). Su organización puede elegir que otro usuario administre las identidades de usuario; para ello, puede [asignar el rol de administrador global de Azure AD para ese usuario](https://docs.microsoft.com/azure/active-directory/active-directory-users-assign-role-azure-portal).
    - Suscripciones, lo que significa que estos usuarios son responsables de:
        - Administrar los costos asociados con el uso de recursos en esa suscripción
        - Implementar y mantener el modelo de permisos mínimos para el acceso a los recursos
        - Realizar un seguimiento de los límites de servicio.
    - Servicios de infraestructura compartida (si su organización decide usar este modelo), lo que significa que este usuario es responsable de:
        - La conectividad del entorno local a la red de Azure.
        - La propiedad de la conectividad de red dentro de Azure mediante el emparejamiento de redes virtuales.
    - Propietarios de cargas de trabajo.
3. El administrador global de Azure AD [crea las cuentas de usuario nuevas](https://docs.microsoft.com/azure/active-directory/add-users-azure-active-directory) para:
    - La persona que será el **propietario de la suscripción** para cada suscripción asociada con cada entorno. Tenga en cuenta que esto es necesario solo si el **administrador de servicios** de la suscripción no será responsable de administrar el acceso a los recursos para cada suscripción o entorno.
    - La persona que será el **usuario de operaciones de red**.
    - Las personas que serán **propietarios de cargas de trabajo**.
4. El administrador de la cuenta de Azure crea las siguientes tres suscripciones con el [portal de cuentas de Azure](https://account.azure.com):
    - Una suscripción para el entorno de **infraestructura compartida**.
    - Una suscripción para el entorno de **producción**.
    - Una suscripción para el entorno de **desarrollo**.
5. El administrador de la cuenta de Azure [agrega el propietario del servicio de suscripción a cada suscripción](https://docs.microsoft.com/azure/billing/billing-add-change-azure-subscription-administrator#assign-a-user-as-an-administrator-of-a-subscription).
6. Cree un proceso de aprobación para que **propietarios de cargas de trabajo** soliciten la creación de grupos de recursos. El proceso de aprobación se puede implementar de muchas maneras, por ejemplo, por correo electrónico, o bien puede usar una herramienta de administración de procesos como [flujos de trabajo de Sharepoint](https://support.office.com/article/introduction-to-sharepoint-workflow-07982276-54e8-4e17-8699-5056eff4d9e3). El proceso de aprobación puede seguir estos pasos:
    - El **propietario de la carga de trabajo** prepara una lista de materiales de los recursos de Azure que necesita en el entorno de **desarrollo**, de **producción** o ambos, y la envía al **propietario de la suscripción**.
    - El **propietario de la suscripción** revisa la lista de materiales y valida los recursos solicitados para asegurarse de que son los adecuados para el uso previsto; por ejemplo, comprueba que los [ tamaños de máquina virtual](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) solicitados son los correctos.
    - Si no se aprueba la solicitud, el **propietario de la carga de trabajo** recibe una notificación. Si se aprueba la solicitud, el **propietario de la suscripción** [crea el grupo de recursos solicitado](https://docs.microsoft.com/azure/azure-resource-manager/manage-resource-groups-portal#create-resource-groups) según las [convenciones de nomenclatura](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) de la organización, [agrega el **propietario de carga de trabajo**](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal#add-a-role-assignment) con el rol de [**colaborador**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) y notifica al **propietario de carga de trabajo** que se ha creado el grupo de recursos.
7. Crear un proceso de aprobación para que los propietarios de cargas de trabajo soliciten una conexión de emparejamiento de red virtual desde el propietario de la infraestructura compartida. Al igual que con el paso anterior, este proceso de aprobación se puede implementar mediante correo electrónico o con una herramienta de administración de procesos.

Ahora que ha implementado el modelo de gobernanza, puede implementar los servicios de infraestructura compartida.

## <a name="related-resources"></a>Recursos relacionados

[Roles integrados en los recursos de Azure](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles)

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Obtenga información sobre cómo implementar una infraestructura básica](../../infrastructure/virtual-machines/basic-workload.md)
