---
title: 'Guía de supervisión de la nube: estrategia de supervisión para los modelos de implementación en la nube'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Decida cuándo usar Azure Monitor o System Center Operations Manager en Microsoft Azure.
author: MGoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 3659f5e965e5a80c3b490f8b106a4cc30f1711a9
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031346"
---
# <a name="cloud-monitoring-guide-monitoring-strategy-for-cloud-deployment-models"></a>Guía sobre la supervisión en la nube: estrategia de supervisión para los modelos de implementación en la nube

En este artículo se incluye la estrategia de supervisión recomendada para cada uno de los modelos de implementación en la nube, según los criterios siguientes:

- Necesita un compromiso continuo con Operations Manager u otra plataforma de supervisión empresarial. Esto se debe a la integración con los procesos, el conocimiento y la experiencia de sus operaciones de TI, o debido a que determinada funcionalidad todavía no está disponible en Azure Monitor.
- Debe supervisar las cargas de trabajo tanto en el entorno local como en la nube pública, o solo en la nube.
- La estrategia de migración a la nube incluye modernizar las operaciones de TI y trasladarse a nuestros servicios y soluciones de supervisión en la nube.
- Es posible que cuente con sistemas críticos que no tienen una conexión física o que están aislados físicamente, hospedados en una nube privada o en hardware físico, y que sea necesario supervisarlos.

Nuestra estrategia incluye compatibilidad con la supervisión de los recursos de infraestructura (cargas de trabajo de proceso, almacenamiento y servidor), aplicación (usuario final, excepciones y cliente) y red para ofrecer una perspectiva completa de supervisión orientada a servicios.

## <a name="azure-cloud-monitoring"></a>Supervisión de la nube de Azure

Azure Monitor es el servicio de plataforma que proporciona un único origen para la supervisión de recursos de Azure. Está diseñado para soluciones en la nube que se basan en Azure y que admiten una funcionalidad empresarial basada en cargas de trabajo de máquinas virtuales o en arquitecturas complejas que usan microservicios y otros recursos de la plataforma. Supervisa todos los niveles de la pila, empezando por los servicios de inquilino como Azure Active Directory Domain Services, y los eventos de suscripción y el estado del servicio de Azure. También supervisa los recursos de infraestructura, como las máquinas virtuales, el almacenamiento y los recursos de red, y, en el nivel superior, la aplicación. La supervisión de cada una de estas dependencias y la recopilación de las señales correctas que cada una puede emitir proporcionan la observabilidad de las aplicaciones y la infraestructura clave que necesita.

En la tabla siguiente se resume el enfoque recomendado para supervisar cada nivel de la pila.

<!-- markdownlint-disable MD033 -->

Nivel | Recurso | Ámbito | Método
---|---|---|----
Application | Aplicación basada en web que se ejecuta en la plataforma .NET, .NET Core, Java, JavaScript y Node.js en una instancia de Azure VM, Azure App Service, Azure Service Fabric, Azure Functions y Azure Cloud Services | Supervisa una aplicación web activa para detectar automáticamente anomalías de rendimiento, identificar problemas y excepciones de código, y recopilar telemetría de facilidad de uso. |  Application Insights
Contenedores | Instancias de Azure Kubernetes Service o Azure Container Instances | Supervisa la capacidad, la disponibilidad y el rendimiento de las cargas de trabajo que se ejecutan en contenedores e instancias de contenedor. | Azure Monitor para contenedores
Sistema operativo invitado | Sistema operativo de máquina virtual Linux y Windows | Supervisa la capacidad, la disponibilidad y el rendimiento. Asigna las dependencias hospedadas en cada máquina virtual, incluida la visibilidad de las conexiones de red activas entre servidores, la latencia de conexiones entrantes y salientes, y los puertos en cualquier arquitectura conectada a TCP. | Azure Monitor para máquinas virtuales
Recursos de Azure: PaaS | Servicios de Azure Database (por ejemplo, SQL o mySQL) | Métricas de rendimiento de Azure Database for SQL. | Habilita el registro de diagnósticos para transmitir datos de SQL a registros de Azure Monitor.
Recursos de Azure: IaaS | 1. Azure Storage<br/> 2. Azure Application Gateway<br/> 3. Azure Key Vault<br/> 4. Grupos de seguridad de red<br/> 5. Administrador de tráfico de Azure | 1. Capacidad, disponibilidad y rendimiento.<br/> 2. Registros de rendimiento y diagnóstico (actividad, acceso, rendimiento y firewall).<br/> 3. Supervisa cómo y cuándo se accede a los almacenes de claves y quién lo hace.<br/> 4. Supervisa los eventos que se producen cuando se aplican las reglas y el contador de la regla para determinar el número de veces que se aplica una regla a las acciones de denegar o permitir.<br/>5. Supervisa la disponibilidad del estado del punto de conexión. | 1. Métricas de almacenamiento para Blob Storage.<br/> 2. Habilita el registro de diagnóstico y configura la transmisión a los registros de Azure Monitor.<br/> 3. Habilita el registro de diagnóstico y configura la transmisión a los registros de Azure Monitor; habilita la [Solución Azure Key Vault Analytics](https://docs.microsoft.com/azure/azure-monitor/insights/azure-key-vault). <br/> 4. Habilita el registro de diagnóstico de los grupos de seguridad de red y configura la transmisión a los registros de Azure Monitor.<br/> 5. Habilita el registro de diagnóstico de los puntos de conexión de Traffic Manager y configura la transmisión a los registros de Azure Monitor.
Red| Comunicación entre la máquina virtual y uno o más puntos de conexión (otra máquina virtual, un nombre de dominio completo, un identificador uniforme de recursos o una dirección IPv4). | Supervisa la disponibilidad, la latencia y los cambios de la topología de red que se producen entre la máquina virtual y el punto de conexión. | Azure Network Watcher
Suscripción de Azure | Estado del servicio de Azure y estado básico de los recursos | <li> Acciones administrativas realizadas en un servicio o recurso.<br/><li> El mantenimiento del servicio con un servicio de Azure se encuentra en un estado degradado o no disponible.<br/><li> Problemas de estado detectados con un recurso de Azure desde la perspectiva del servicio de Azure.<br/><li> Operaciones realizadas con la escalabilidad automática de Azure que indican un error o una excepción. <br/><li> Operaciones realizadas con Azure Policy que indican que se ha producido una acción permitida o denegada.<br/><li> Registro de las alertas generadas por Azure Security Center. |Se entrega en el registro de actividad para la supervisión y alertas mediante el uso de Azure Resource Manager.
Inquilino de Azure|Azure Active Directory || Habilita el registro de diagnóstico y configura la transmisión a los registros de Azure Monitor.

<!-- markdownlint-enable MD033 -->

## <a name="hybrid-cloud-monitoring"></a>Supervisión de la nube híbrida

Esta sección está actualmente en desarrollo para ofrecer un conjunto completo de recomendaciones pensadas para responder a su interés sobre este modelo de nube; estará disponible en breve.  

## <a name="private-cloud-monitoring"></a>Supervisión de la nube privada

Puede lograr una supervisión holística de Azure Stack con System Center Operations Manager. En concreto, puede supervisar las cargas de trabajo que se ejecutan en el inquilino, en el nivel de recurso, en las máquinas virtuales y en la infraestructura que hospeda a Azure Stack (servidores físicos y conmutadores de red). También puede lograr una supervisión holística con una combinación de las [funcionalidades de supervisión de infraestructuras](https://docs.microsoft.com/azure/azure-stack/azure-stack-monitor-health) incluidas en Azure Stack. Estas funcionalidades ayudan a ver el estado y las alertas de una región de Azure Stack y el [servicio de Azure Monitor](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-metrics-azure-data) en Azure Stack, que proporciona registros y métricas de infraestructura de nivel básico para la mayoría de los servicios.

Si ya ha invertido en Operations Manager, use el módulo de administración de Azure Stack para supervisar la disponibilidad y el estado de mantenimiento de las implementaciones de Azure Stack. Esto incluye las regiones, los proveedores de recursos, las actualizaciones, las ejecuciones de actualización, las unidades de escalado, los nodos de unidad, los roles de infraestructura y sus instancias (entidades lógicas que constan de los recursos de hardware). Este módulo utiliza las API REST del proveedor de recursos de mantenimiento y actualización para comunicarse con Azure Stack. Para supervisar los servidores físicos y los dispositivos de almacenamiento, use el módulo de administración de los proveedores OEM (proporcionado, por ejemplo, por Lenovo, Hewlett Packard o Dell). Operations Manager puede supervisar de forma nativa los conmutadores de red para recopilar estadísticas básicas mediante el protocolo SNMP. Es posible supervisar las cargas de trabajo de inquilinos con el módulo de administración de Azure siguiendo dos pasos básicos. Configure la suscripción que desea supervisar y, a continuación, agregue los monitores de dicha suscripción.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Recopilación de los datos adecuados](./data-collection.md)
