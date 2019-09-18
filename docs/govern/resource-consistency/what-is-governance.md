---
title: ¿Qué es la gobernanza de los recursos en la nube?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Explicación sobre la gobernanza de los recursos de la nube en Azure
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 083b18c0c8c5edc0dc21a198df32e8934929299c
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032362"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-cloud-resource-governance"></a>¿Qué es la gobernanza de los recursos en la nube?

En [¿Cómo funciona Azure?](../../getting-started/what-is-azure.md), ha aprendido que Azure es una colección de servidores y de hardware de red que ejecutan software y hardware virtualizado en nombre de los usuarios. Azure aporta agilidad a los departamentos de TI y desarrollo de su organización porque permite crear, leer, actualizar y eliminar fácilmente los recursos según sea necesario.

Sin embargo, aunque el acceso sin restricciones a los recursos puede aumentar la agilidad de los desarrolladores, también puede provocar costos inesperados. Por ejemplo, se podría aprobar que un equipo de desarrollo implemente un conjunto de recursos para pruebas pero olvida eliminarlos una vez completada la prueba. Estos recursos continuarán acumulando costos, aunque su uso no esté aprobado o no sea necesario.

La solución es la gobernanza del acceso a los recursos. **Gobernanza** es el proceso continuo de administrar, supervisar y auditar el uso de los recursos de Azure para cumplir los objetivos y requisitos de su organización.

<!-- markdownlint-disable MD034 -->

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE2ii94]

<!-- markdownlint-enable MD034 -->

Estos requisitos son únicos para cada organización por lo que no es posible diseñar una solución de gobernanza universal. En su lugar, cada organización debe decidir cuál usará para diseñar su modelo de gobernanza con las dos herramientas de gobernanza principales de Azure: el **control de acceso basado en rol (RBAC)** y la **directiva de recursos**.

RBAC define roles y los roles definen las operaciones permitidas para cada usuario asignado a ese rol. Por ejemplo, el rol **propietario** permite todas las operaciones (crear, leer, actualizar y eliminar) en un recurso, mientras que el rol **lector** solo permite operaciones de lectura. Los roles se pueden definir de manera generalizada y aplicarse a muchos tipos de recursos, o bien definirse de manera más limitada y aplicarse solo a unos pocos tipos de recursos.

Las directivas de recursos definen las reglas de creación de recursos. Por ejemplo, una directiva de recursos puede limitar la SKU de una máquina virtual a un tamaño determinado aprobado previamente. Otra una directiva de recursos puede exigir que se agregue una etiqueta a un centro de costos cuando se realiza una solicitud para crear el recurso.

Al configurar estas herramientas, es importante equilibrar la gobernanza y la agilidad de la organización. Cuanto más restrictiva sea la directiva de gobernanza, menos ágiles serán los desarrolladores y los trabajadores de TI. Una directiva de gobernanza restrictiva puede requerir más pasos manuales; por ejemplo, que el desarrollador rellene un formulario o que envíe un correo electrónico a un miembro del equipo de gobernanza para crear un recurso manualmente. El equipo de gobernanza tiene una capacidad finita y podría convertirse en un cuello de botella que provocaría una limitación de la productividad de los equipos de desarrollo mientras esperan a que se creen sus recursos o que los recursos no necesarios acumulen costos mientras esperan a ser eliminados.

## <a name="next-steps"></a>Pasos siguientes

Ahora que comprende el concepto de gobernanza de los recursos en la nube, aprenda cómo se administra el acceso a los recursos en Azure.

> [!div class="nextstepaction"]
> [Más información sobre el acceso a los recursos en Azure](./resource-access-management.md)
