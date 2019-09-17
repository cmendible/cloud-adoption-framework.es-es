---
title: ¿Cómo funciona Azure?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Explicación del funcionamiento interno de Azure
author: alexbuckgit
ms.author: abuck
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: overview
ms.custom: governance
ms.openlocfilehash: 6aabf9545aa6774b63d3dbd201373273c3f8f1ab
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70837754"
---
<!-- markdownlint-disable MD026 -->

# <a name="how-does-azure-work"></a>¿Cómo funciona Azure?

Azure es la plataforma pública en la nube de Microsoft. Azure ofrece una amplia gama de servicios entre los que se incluyen las funcionalidades de plataforma como servicio (PaaS), infraestructura como servicio (IaaS) y servicio de base de datos administrado. Pero, ¿qué es exactamente Azure y cómo funciona?

<!-- markdownlint-disable MD034 -->

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE2ixGo]

Azure, al igual que otras plataformas en la nube, se basa en una tecnología conocida como **virtualización**. La mayor parte del hardware de equipo puede emularse en el software porque es simplemente un conjunto de instrucciones codificadas de forma permanente o semipermanente en silicio. Mediante una capa de emulación que asigna instrucciones de software a instrucciones de hardware, el hardware virtualizado puede ejecutarse en el software como si fuera el propio hardware.

Básicamente, la nube es un conjunto de servidores físicos en uno o varios centros de datos que ejecutan hardware virtualizado en nombre de los clientes. Entonces, ¿cómo crea, inicia, detiene y elimina la nube millones de instancias de hardware virtualizado para millones de clientes a la vez?

Para comprenderlo, vamos a echar un vistazo a la arquitectura del hardware del centro de datos. En cada centro de datos hay una colección de servidores colocados en bastidores de servidores. Cada bastidor de servidor contiene muchas **hojas** de servidor, así como un conmutador de red que proporciona conectividad de red y una unidad de distribución de energía (PDU) que suministra la alimentación. A veces, los bastidores se agrupan conjuntamente en unidades más grandes que se conocen como **clústeres**.

En cada bastidor o clúster, la mayoría de los servidores están designados para ejecutar estas instancias de hardware virtualizado en nombre del usuario. Pero algunos de los servidores ejecutan software de administración en la nube conocido como controlador de tejido. El **controlador de tejido** es una aplicación distribuida con muchas responsabilidades. Asigna servicios, supervisa el mantenimiento del servidor y los servicios que se ejecutan en él, y recupera los servidores cuando se produce un error.

Cada instancia del controlador de tejido se conecta a otro conjunto de servidores que ejecutan software de orquestación en la nube, conocido normalmente como **front-end**. El front-end hospeda los servicios web, las API RESTful y las bases de datos internas de Azure utilizadas para todas las funciones que realiza la nube.

Por ejemplo, el front-end hospeda los servicios que controlan las solicitudes de cliente para asignar recursos de Azure como [máquinas virtuales](/azure/virtual-machines) y servicios como [Cosmos DB](/azure/cosmos-db/introduction). En un primer tiempo, el front-end valida el usuario y comprueba que esté autorizado para asignar los recursos solicitados. Si es así, el front-end consulta una base de datos para buscar un bastidor de servidores con capacidad suficiente y, luego, indica al controlador de tejido de ese bastidor que asigne el recurso.

Así que, básicamente, Azure es una inmensa colección de servidores y hardware de red que ejecuta un complejo conjunto de aplicaciones distribuidas para orquestar la configuración y el funcionamiento del hardware y el software virtualizado de esos servidores. Es esta orquestación la que hace que Azure sea tan eficaz: los usuarios ya no son responsables de mantener y actualizar el hardware, ya que de todo esto se encarga Azure en segundo plano.

## <a name="next-steps"></a>Pasos siguientes

Ahora que comprende el funcionamiento interno de Azure, obtenga información sobre la gobernanza de recursos en la nube.

> [!div class="nextstepaction"]
> [Obtenga información sobre la gobernanza de recursos](../governance/resource-consistency/what-is-governance.md)

<!-- links -->

[docs-add-users-to-aad]: /azure/active-directory/add-users-azure-active-directory?toc=/azure/architecture/cloud-adoption-guide/toc.json
