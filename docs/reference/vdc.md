---
title: Centro de datos virtual de Azure
description: Recursos para el centro de datos virtual de Microsoft Azure
author: tracsman
ms.author: jonor
ms.date: 06/12/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: reference
keywords: Azure
layout: LandingPage
ms.openlocfilehash: 39cb6ac3c31873431206d8c6c525c9ce3467653f
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031355"
---
# <a name="azure-virtual-datacenter-and-the-enterprise-control-plane"></a>Centro de datos virtual de Azure y el plano de control empresarial

El centro de datos virtual de Azure permite sacar el máximo partido a las funcionalidades de Azure al tiempo que respeta sus directivas de seguridad y de red actuales. A la hora de implementar cargas de trabajo empresariales en la nube, las organizaciones de TI y las unidades de negocio deben equilibrar la gobernanza y la agilidad de los desarrolladores. El centro de datos virtual de Azure ofrece modelos que contribuyen a lograr este equilibrio con cierto énfasis en la gobernanza.

## <a name="resources"></a>Recursos

<!-- markdownlint-disable MD033 -->

<table>
<tr>
    <td style="width: 64px; vertical-align: middle;"><a href="https://aka.ms/VDC/Concepts"><img src="../_images/vdc/virtual-datacenter.svg" alt="Virtual Datacenter e-book" /></a></td>
    <td>
        <h3><a href="https://aka.ms/VDC/Concepts">Centro de datos virtual de Azure: Conceptos</a></h3>
        <p>Este libro electrónico muestra cómo implementar cargas de trabajo empresariales en la plataforma de nube de Azure, al tiempo que se respetan las directivas existentes de red y de seguridad.</p>
    </td>
</tr>
<tr>
    <td style="width: 64px; vertical-align: middle;"><a href="./networking-vdc.md"><img src="../_images/vdc/vdc-network.png" alt="Network Perspective" /></a></td>
    <td>
        <h3><a href="./networking-vdc.md">Centro de datos virtual de Azure: Una perspectiva de la red</a></h3>
        <p>Este artículo en línea proporciona información general sobre patrones y diseños de red que pueden utilizarse para resolver los conceptos de arquitectura de escala, rendimiento y seguridad que muchos clientes abordan al pensar en moverse masivamente a la nube.</p>
    </td>
</tr>
<tr>
    <td style="width: 64px; vertical-align: middle;"><a href="https://aka.ms/VDC/Lift"><img src="../_images/vdc/vdc-lift-and-shift.png" alt="Lift and Shift Guide" /></a></td>
    <td>
        <h3><a href="https://aka.ms/VDC/Lift">Centro de datos virtual de Azure: Guía para una migración lift-and-shift</a></h3>
        <p>En estas notas del producto se explica el proceso empresarial que el personal de TI y los responsables de decisiones pueden utilizar para identificar y planear la migración de las aplicaciones y los servidores a Azure mediante un método de tipo "lift-and-shift", para minimizar los posibles costos de desarrollo adicionales y optimizar las opciones de hospedaje en la nube.</p>
    </td>
</tr>
<tr>
    <td style="width: 64px; vertical-align: middle;"><a href="https://aka.ms/VDC/Deck"><img src="../_images/vdc/vdc-deck.png" alt="Presentation Deck" /></a></td>
    <td>
        <h3><a href="https://aka.ms/VDC/Deck">Centro de datos virtual de Azure: Presentación</a></h3>
        <p>Esta presentación ofrece una guía y herramientas para el centro de datos virtual de Azure. Describe los objetivos de un centro de datos virtual, los controladores de cliente, las regiones de Azure, los elementos de automatización de un centro de datos virtual, los centros de datos virtuales de Azure industrializados y de confianza, y termina con un plan de acción para guiar a los responsables de informática. También se proporciona información de soporte técnico y aprendizaje.</p>
    </td>
</tr>
</table>

<!-- markdownlint-enable MD033 -->

<!-- markdownlint-disable MD026 -->

## <a name="what-is-the-azure-virtual-datacenter"></a>¿Qué es el centro de datos virtual de Azure?

Implementar cargas de trabajo en la nube conlleva la necesidad de desarrollar y mantener la confianza en la nube en la misma medida en que confía en sus centros de datos existentes. El primer modelo de la guía del centro de datos virtual de Azure se ha diseñado como puente entre los sistemas fijos y las infraestructuras virtuales. Este enfoque no es para todos. Se ha diseñado específicamente para guiar a los grupos de TI empresariales a extender su infraestructura local a la nube pública de Azure. Llamamos a este enfoque el modelo de extensión del centro de datos de confianza. Con el tiempo, se ofrecerán otros modelos, incluidos aquellos que permiten el acceso seguro a Internet directamente desde un centro de datos virtual.

<!-- markdownlint-disable MD033 -->

<img src="../_images/vdc/vdc-components.svg" alt="Virtual Datacenter components" style="max-width:700px;"/>

<!-- markdownlint-enable MD033 -->

Estos cuatro componentes hacen posible los centros de datos virtuales de Azure: identidad, cifrado, redes definidas por software y cumplimiento (incluidos registros e informes).

En el modelo de centro de datos virtual de Azure, puede aplicar directivas de aislamiento, hacer que la nube se parezca más a los centros de datos físicos que conoce y lograr los niveles de seguridad y confianza que necesita. Esto es posible gracias a cuatro componentes que cualquier equipo de TI empresarial reconocería: redes definidas por software, cifrado, administración de identidades y las normas y certificaciones de cumplimiento subyacentes a la plataforma de Azure. Estos cuatro componentes son fundamentales para hacer que un centro de datos virtual sea una extensión de confianza de su infraestructura existente.

Siga leyendo el libro electrónico [Centro de datos virtual de Azure: conceptos](https://azure.microsoft.com/resources/azure-virtual-datacenter).
