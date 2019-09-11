---
title: Introducción sobre los servicios de administración de servidores de Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introducción sobre los servicios de administración de servidores de Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: operate
ms.openlocfilehash: 4d1ada9d47e54f4b0d3828ce93b2d55f3eda8a34
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70817220"
---
# <a name="overview-of-azure-server-management-services"></a>Introducción sobre los servicios de administración de servidores de Azure

Los servicios de administración de servidores de Azure proporcionan a los clientes una experiencia coherente para administrar sus servidores a escala. Estos servicios abarcan los sistemas operativos Linux y Windows y pueden usarse en entornos de producción, desarrollo y prueba. Además, pueden admitir máquinas virtuales IaaS de Azure, servidores físicos y máquinas virtuales hospedados de forma local o en otros entornos de hospedaje. 

El conjunto de servicios de administración de servidores de Azure incluye los servicios que se muestran en el siguiente diagrama. 

![Diagrama del modelo de operaciones de Azure](./media/operations-diagram.png)

Las instrucciones de esta sección de Microsoft Cloud Adoption Framework proporcionan un plan preceptivo y viable para la implementación de los servicios de administración de servidores en su entorno. Este plan está diseñado para ayudar a orientarse rápidamente con estos servicios y guiarle a través de un conjunto de fases de administración progresivas para todos los tamaños de entorno.

Para simplificar, se han clasificado las instrucciones en tres fases:

![Las tres fases de incorporación de los servicios de administración de servidores de Azure](./media/operations-stages.png)

<!-- markdownlint-disable MD026 -->

## <a name="why-use-azure-management-services"></a>¿Por qué usar los servicios de administración de Azure?

Los servicios de administración de Azure ofrecen las siguientes ventajas:

- **Nativos de Azure.** Los servicios de administración están integrados de forma nativa con Azure Resource Manager. Estos servicios se mejoran continuamente para proporcionar funcionalidades y características nuevas.
- **Windows y Linux**. Las máquinas Windows y Linux ofrecen la misma experiencia de administración coherente.
- **Híbridas.** Los servicios de administración abarcan máquinas virtuales IaaS de Azure, así como servidores físicos y virtuales hospedados en el entorno local o en otros entornos de hospedaje.
- **Seguridad.** Microsoft dedica bastantes recursos a todo lo que aporte seguridad. Esta inversión no sólo protege la infraestructura en la nube de Azure, sino que también extiende las tecnologías y conocimientos resultantes para proteger los recursos de los clientes allá donde se encuentren.

## <a name="next-steps"></a>Pasos siguientes

Familiarícese con las [herramientas, servicios y planeamiento](./prerequisites.md) relacionados con la adopción del paquete de administración de servidores de Azure.

> [!div class="nextstepaction"]
> [Requisitos previos de herramientas y planeamiento](./prerequisites.md)
