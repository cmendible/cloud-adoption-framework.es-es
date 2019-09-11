---
title: 'Preparación para Azure: decisiones sobre el diseño de redes'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Preparación para Azure: decisiones sobre el diseño de redes'
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: 307cf3d276d22288d4556c1b2d3c5982767b6ddd
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70834698"
---
# <a name="networking-design-decisions"></a>Decisiones sobre el diseño de redes

El diseño y la implementación de las funcionalidades de redes de Azure es una parte fundamental de las labores de adopción de la nube. Deberá tomar decisiones sobre el diseño de redes para acomodar correctamente las cargas de trabajo y los servicios que se hospedarán en la nube. Los servicios y productos de redes de Azure admiten una amplia variedad de funcionalidades de red. La forma de estructurar estos servicios y las arquitecturas de red que elija depende de los requisitos de carga de trabajo, gobernanza y conectividad de su organización.

## <a name="identify-workload-networking-requirements"></a>Identificación de los requisitos de red de la carga de trabajo

Como parte de la evaluación y preparación de la zona de aterrizaje, debe identificar las funcionalidades de red que debe admitir la zona de aterrizaje. Este proceso supone evaluar cada una de las aplicaciones y servicios que componen las cargas de trabajo para determinar sus requisitos de control de red de conectividad. Después de identificar y documentar los requisitos, puede crear directivas para la zona de aterrizaje con el fin de controlar la configuración y los recursos de red permitidos en función de las necesidades de su carga de trabajo.

Para cada aplicación o servicio que vaya a implementar en el entorno de la zona de aterrizaje, use el siguiente árbol de decisión como punto de partida para que le ayude a determinar las herramientas o los servicios de red que debe usar:

![Árbol de decisión de servicios de red de Azure](../../_images/ready/network-decision-tree.png)

### <a name="key-questions"></a>Preguntas clave

Responda a las siguientes preguntas sobre las cargas de trabajo para tomar decisiones basadas en el árbol de decisión de servicios de red de Azure:

- **¿Necesitarán las cargas de trabajo una red virtual?** Los tipos de recursos de plataforma como servicio (PaaS) administrados usan funcionalidades de red de la plataforma subyacente que no siempre necesitan una red virtual. Si las cargas de trabajo no necesitan características de red avanzadas y no es necesario implementar recursos de infraestructura como servicio (IaaS), las [funcionalidades de red nativas predeterminadas que proporcionan los recursos de PaaS](../../decision-guides/software-defined-network/paas-only.md) podrían satisfacer su requisitos de conectividad y administración del tráfico de la carga de trabajo.
- **¿Necesitarán las cargas de trabajo conectividad entre las redes virtuales y el centro de recursos local?** Azure proporciona dos soluciones para establecer las funcionalidades de red híbrida:  Azure VPN Gateway y Azure ExpressRoute. [Azure VPN Gateway](/azure/vpn-gateway/vpn-gateway-about-vpngateways) conecta las redes locales a Azure mediante VPN de sitio a sitio, de forma muy parecida a cómo podría configurar una sucursal remota y conectarse a ella. VPN Gateway tiene un ancho de banda máximo de 1,25 GBps. [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) ofrece una mayor confiabilidad y una menor latencia gracias al uso de una conexión privada entre Azure y la infraestructura local. Las opciones de ancho de banda de ExpressRoute van de 50 MBps a 100 GBps.
- **¿Necesitará inspeccionar y auditar el tráfico saliente mediante dispositivos de red locales?** En el caso de cargas de trabajo nativas de la nube, puede usar [Azure Firewall](/azure/firewall/overview) o [aplicaciones virtuales de red (NVA)](https://azure.microsoft.com/solutions/network-appliances/) de terceros hospedadas en la nube para inspeccionar y auditar el tráfico que entra en la red pública de Internet o sale de ella. Sin embargo, muchas de las directivas de seguridad de TI de la empresa requieren que el tráfico saliente enlazado a Internet pase por dispositivos administrados centralmente en el entorno local de la organización. La [tunelización forzada](/azure/virtual-network/virtual-networks-udr-overview) admite estos escenarios. No todos los servicios administrados admiten la tunelización forzada. Servicios y características, como [App Service Environment de Azure App Service](/azure/app-service/environment/intro), [Azure API Management](/azure/api-management/api-management-key-concepts), [Azure Kubernetes Service (AKS)](/azure/aks/intro-kubernetes), [Instancias administradas de Azure SQL Database](/azure/sql-database/sql-database-managed-instance-index), [Azure Databricks](/azure/azure-databricks/what-is-azure-databricks) y [Azure HDInsight](/azure/hdinsight/) admiten esta configuración cuando el servicio o la característica se implementa dentro de una red virtual.
- **¿Necesitará conectar varias redes virtuales?** Puede usar [emparejamiento de redes virtuales](/azure/virtual-network/virtual-network-peering-overview) para conectar varias instancias de [Azure Virtual Network](/azure/virtual-network/virtual-networks-overview). El emparejamiento puede admitir conexiones entre suscripciones y regiones. En el caso de escenarios en los que se proporcionan servicios que se comparten entre varias suscripciones o en los que es necesario administrar un gran número de emparejamientos de red, considere la posibilidad de adoptar una [arquitectura de red de concentrador y radio](../../decision-guides/software-defined-network/hub-spoke.md), o bien usar [Azure Virtual WAN](/azure/virtual-wan/virtual-wan-about). El emparejamiento de redes virtuales solo proporciona conectividad entre dos redes emparejadas. De forma predeterminada, no proporciona conectividad transitiva entre varios emparejamientos.
- **¿Serán accesibles sus cargas de trabajo a través de Internet?** Azure proporciona servicios que están diseñados para ayudarlo a administrar y proteger el acceso externo a sus aplicaciones y servicios:
  - [Azure Firewall](/azure/firewall/overview)
  - [Aplicaciones de red](https://azure.microsoft.com/solutions/network-appliances/)
  - [Azure Front Door Service](/azure/frontdoor/front-door-overview)
  - [Introducción a Puerta de enlace de aplicaciones](/azure/application-gateway/)
  - [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview)
- **¿Deberá admitir la administración de DNS personalizada?** [Azure DNS](/azure/dns/dns-overview) es un servicio de hospedaje para dominios DNS. Azure DNS proporciona resolución de nombres mediante la infraestructura de Azure. Si las cargas de trabajo requieren una resolución de nombres que supere las características proporcionadas por Azure DNS, puede que tenga que implementar otras soluciones. Si las cargas de trabajo también requieren servicios de Active Directory, considere la posibilidad de usar [Azure Active Directory Domain Services](/azure/active-directory-domain-services/overview) para aumentar las funcionalidades de Azure DNS. Para obtener más funcionalidades, también puede [implementar máquinas virtuales de IaaS personalizadas](/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances) para satisfacer sus necesidades.

## <a name="common-networking-scenarios"></a>Escenarios comunes de redes

Las redes de Azure se componen de varios productos y servicios que proporcionan diferentes funcionalidades de red. Como parte del proceso de diseño de redes, puede comparar los requisitos de carga de trabajo con los escenarios de red de la tabla siguiente para identificar las herramientas o los servicios de Azure que puede usar para proporcionar estas funcionalidades de red:

<!-- markdownlint-disable MD033 -->

| **Escenario** | **Producto o servicio de red** |
| --- | --- |
| Necesito que infraestructura de red conecte todo, desde máquinas virtuales a conexiones VPN entrantes. | [Azure Virtual Network](/azure/virtual-network) |
| Necesito equilibrar las conexiones entrantes y salientes y las solicitudes a mis aplicaciones o servicios. | [Equilibrador de carga de Azure](/azure/load-balancer) |
| Quiero optimizar la entrega desde las granjas de servidores de aplicaciones y aumentar al mismo tiempo la seguridad de las aplicaciones con un firewall de aplicaciones web. | [Introducción a Puerta de enlace de aplicaciones](/azure/application-gateway) <br/>[Azure Front Door Service](/azure/frontdoor) |
| Necesito usar Internet de forma segura para acceder a instancias de Azure Virtual Network con instancias de VPN Gateway de alto rendimiento. | [Acerca de VPN Gateway](/azure/vpn-gateway) |
| Quiero garantizar respuestas de DNS ultrarrápidas y una disponibilidad ultraalta para todas mis necesidades de dominio. | [DNS de Azure](/azure/dns) |
| Necesito acelerar la entrega de contenido de alto ancho de banda a clientes de todo el mundo, desde aplicaciones y contenido almacenado hasta streaming de vídeo. | [Azure Content Delivery Network](/azure/cdn) |
| Necesito proteger mis aplicaciones de Azure de ataques de DDoS. | [Azure DDoS Protection](/azure/virtual-network/ddos-protection-overview) |
| Necesito distribuir el tráfico de forma óptima a los servicios entre regiones globales de Azure, y proporcionar al mismo tiempo alta disponibilidad y capacidad de respuesta. | [Azure Traffic Manager](/azure/traffic-manager)<br/>[Azure Front Door Service](/azure/frontdoor) |
| Necesito agregar conectividad de red privada para acceder a los servicios en la nube de Microsoft desde mis redes corporativas, como si estuvieran en el entorno local y residieran en su propio centro de datos. | [Información técnica de ExpressRoute](/azure/expressroute) |
| Quiero supervisar y diagnosticar condiciones en un nivel de escenario de red. | [Azure Network Watcher](/azure/network-watcher) |
| Necesito funcionalidades nativas de firewall con alta disponibilidad integrada, escalabilidad en la nube sin restricciones y cero mantenimiento. | [Azure Firewall](/azure/firewall) |
| Necesito conectar de forma segura las oficinas de negocio, las ubicaciones comerciales y los sitios. | [Azure Virtual WAN](/azure/virtual-wan) |
| Necesito un punto de entrega escalable y con seguridad mejorada para aplicaciones web globales basadas en microservicios. | [Azure Front Door Service](/azure/frontdoor) |

<!-- markdownlint-enable MD033 -->

## <a name="choose-a-networking-architecture"></a>Elección de una arquitectura de red

Después de identificar los servicios de red de Azure que necesita para admitir sus cargas de trabajo, también debe diseñar la arquitectura que combinará estos servicios para proporcionar la infraestructura de red de la nube de la zona de aterrizaje. En la [Guía de decisiones sobre redes definidas por software](../../decision-guides/software-defined-network/index.md) del marco de adopción de la nube se proporcionan detalles sobre algunos de los patrones de arquitectura de red más comunes usados en Azure.

En la tabla siguiente se resumen los escenarios principales que admiten estos patrones:

| **Escenario** | **Arquitectura de red sugerida**
| --- | --- |
| Todas las cargas de trabajo hospedadas en Azure implementadas en la zona de aterrizaje se basarán por completo en PaaS, no requerirán una red virtual y no formarán parte de una labor mayor de adopción de la nube que incluirá los recursos de IaaS. | [Solo PaaS](../../decision-guides/software-defined-network/paas-only.md) |
| Las cargas de trabajo hospedadas en Azure implementarán recursos basados en IaaS, como máquinas virtuales, o requerirán una red virtual, pero no requieren conectividad con el entorno local. | [Nativo de la nube](../../decision-guides/software-defined-network/cloud-native.md) |
| Las cargas de trabajo hospedadas en Azure requieren acceso limitado a los recursos locales, pero es necesario tratar las conexiones de la nube como que no son de confianza. | [Red perimetral en la nube](../../decision-guides/software-defined-network/cloud-dmz.md) |
| Las cargas de trabajo hospedadas en Azure requieren acceso limitado a los recursos locales, y tiene pensado implementar directivas de seguridad maduras y proteger la conectividad entre la nube y el entorno local. | [Híbrido](../../decision-guides/software-defined-network/hybrid.md) |
| Necesita implementar y administrar un gran número de máquinas virtuales y cargas de trabajo, lo que puede superar posiblemente los [límites de suscripción de Azure](/azure/azure-subscription-service-limits), debe compartir los servicios entre las suscripciones, o necesita una estructura más segmentada para la segregación de roles, aplicaciones o permisos. | [Concentrador y radio](../../decision-guides/software-defined-network/hub-spoke.md) |
| Tiene muchas sucursales que necesitan conectarse entre sí y con Azure. | [Azure Virtual WAN](/azure/virtual-wan/virtual-wan-about) |

### <a name="azure-virtual-datacenter"></a>Centro de datos virtual de Azure

Además de usar uno de estos patrones de arquitectura, si el grupo de TI de la empresa administra entornos de nube de gran tamaño, considere la posibilidad de consultar la [guía del centro de datos virtual de Azure](https://docs.microsoft.com/azure/architecture/vdc) al diseñar la infraestructura de nube basada en Azure. El Centro de datos virtual de Azure proporciona un enfoque combinado para redes, seguridad, administración e infraestructura si su organización cumple los siguientes criterios:

- Su empresa está sujeta al cumplimiento normativo, que exige funcionalidades de supervisión y auditoría centralizadas.
- Su patrimonio de nube estará formado por más de 10 000 máquinas virtuales de IaaS o una escala equivalente de servicios PaaS.
- Debe habilitar funcionalidades de implementación ágiles para cargas de trabajo de apoyo a los equipos de operaciones y desarrolladores, y mantener el cumplimiento de gobernanza y directiva comunes, así como el control de TI centralizado sobre los servicios principales.
- Su sector depende de una compleja plataforma que requiere un conocimiento profundo de los dominios (por ejemplo, finanzas, petróleo y gas o fabricación).
- Las directivas de gobernanza de TI existentes requieren una paridad más ajustada con las características existentes, incluso durante la adopción en fases tempranas.

## <a name="follow-azure-networking-best-practices"></a>Seguimiento de los procedimientos recomendados de redes de Azure

Como parte del proceso de diseño de redes, consulte estos artículos:

- [Planeamiento de redes virtuales](/azure/virtual-network/virtual-network-vnet-plan-design-arm?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Obtenga información sobre cómo planear redes virtuales según los requisitos de aislamiento, conectividad y ubicación.
- [Procedimientos recomendados de seguridad de la red de Azure](/azure/security/azure-security-network-security-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Más información sobre los procedimientos recomendados de Azure que pueden ayudarlo a mejorar la seguridad de la red.
- [Procedimientos recomendados para la configuración de redes para las cargas de trabajo migradas a Azure](/azure/migrate/migrate-best-practices-networking?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json). Obtenga instrucciones adicionales sobre cómo implementar redes de Azure para admitir cargas de trabajo basadas en IaaS y en PaaS.
