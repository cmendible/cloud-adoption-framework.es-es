---
title: Procedimientos recomendados para la configuración de redes para las cargas de trabajo migradas a Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Después de migrar a Azure, consulte los procedimientos recomendados para la configuración de redes para las cargas de trabajo migradas.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/04/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 8fbdd20c435d4aed8a284174d813abc8d391171b
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022847"
---
# <a name="best-practices-to-set-up-networking-for-workloads-migrated-to-azure"></a>Procedimientos recomendados para la configuración de redes para las cargas de trabajo migradas a Azure

A la hora de planear y diseñar la migración, además de la migración propiamente dicha, uno de los pasos más importantes es el diseño y la implementación de redes de Azure. En este artículo se describen los procedimientos recomendados para las redes al migrar a implementaciones de IaaS y PaaS en Azure.

> [!IMPORTANT]
> Los procedimientos recomendados y las opiniones que se describen en este artículo se basan en la plataforma Azure y las características del servicio disponibles en el momento de redactar el artículo. Las características y funcionalidades cambian con el tiempo. Es posible que no todas las recomendaciones sean aplicables a su implementación, así que seleccione las que sean válidas en su caso.

## <a name="design-virtual-networks"></a>Diseño de redes virtuales

Azure ofrece redes virtuales:

- Los recursos de Azure se comunican de forma privada, directa y segura entre sí a través de redes virtuales.
- Puede configurar conexiones de punto de conexión en redes virtuales para máquinas virtuales y servicios que requieran comunicación por Internet.
- Una red virtual es un aislamiento lógico de Azure Cloud que se dedica a su suscripción.
- Puede implementar varias redes virtuales dentro de cada suscripción y región de Azure.
- Cada red virtual está aislada de otras redes virtuales.
- Las redes virtuales pueden contener direcciones IP públicas y privadas definidas en [RFC 1918](https://tools.ietf.org/html/rfc1918) y expresadas en notación CIDR. Las direcciones IP públicas especificadas en el espacio de direcciones de una red virtual no son accesibles directamente desde Internet.
- Las redes virtuales pueden conectarse entre sí con emparejamiento de VNET. Las redes virtuales conectadas pueden estar en una misma región o en distintas regiones. Por lo tanto, los recursos de una red virtual pueden conectarse a los recursos de otras redes virtuales.
- De forma predeterminada, Azure enruta el tráfico entre subredes, redes virtuales conectadas, redes locales e Internet.

Al planear la topología de la red virtual, debe tener en cuenta cómo organizar los espacios de direcciones IP, cómo implementar una red de concentrador y radio, cómo segmentar las redes virtuales en subredes, cómo configurar DNS y cómo implementar las zonas de disponibilidad de Azure.

## <a name="best-practice-plan-ip-addressing"></a>Procedimiento recomendado: Planeamiento de las direcciones IP

Al crear redes virtuales como parte de la migración, es importante planear el espacio de direcciones IP de la red virtual.

- Debe asignar un espacio de direcciones que no sea mayor que un intervalo de CIDR de /16 para cada red virtual. Las redes virtuales permiten el uso de 65536 direcciones IP, y asignar un prefijo menor que /16 tendría como resultado la pérdida de las direcciones IP. Es importante no desperdiciar direcciones IP, aunque se encuentren en los intervalos privados definidos en RFC 1918.
- El espacio de direcciones de red virtual no debe superponerse con intervalos de red local.
- No debe utilizarse la traducción de direcciones de red (NAT).
- La superposición de direcciones puede provocar que las redes no se puedan conectar y que el enrutamiento no funcione correctamente. Si las redes se superponen, tendrá que volver a diseñar la red o utilizar la traducción de direcciones de red (NAT).

**Más información:**

- [Obtenga información general ](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) sobre las redes virtuales de Azure.
- [Lea](https://docs.microsoft.com/azure/virtual-network/virtual-networks-faq) las preguntas más frecuentes sobre redes.
- [Obtenga más información sobre](https://docs.microsoft.com/azure/azure-subscription-service-limits?toc=%2fazure%2fvirtual-network%2ftoc.json#networking-limits) limitaciones de red.

## <a name="best-practice-implement-a-hub-and-spoke-network-topology"></a>Procedimiento recomendado: Implementación de una topología de red de concentrador y radio

Una topología de red de concentrador y radio aísla las cargas de trabajo mientras se comparten servicios tales como los de identidad y seguridad.

- El centro de conectividad es una red virtual de Azure que actúa como punto central de conectividad.
- Los radios son redes virtuales que se conectan a la red virtual del centro de conectividad con emparejamiento de VNET.
- Los servicios compartidos se implementan en el centro, mientras que las cargas de trabajo individuales se implementan como radios.

Tenga en cuenta lo siguiente.

- La implementación de una topología de red en estrella tipo hub-and-spoke en Azure centraliza la creación de servicios comunes tales como las conexiones a redes locales, los firewalls y el aislamiento entre redes virtuales. La red virtual del centro de conectividad proporciona un punto central de conectividad a redes locales y un lugar para el hospedaje de servicios que utilizan las cargas de trabajo hospedadas en redes virtuales de radio.
- Las empresas más grandes normalmente usan una configuración en estrella tipo hub-and-spoke. Para redes más pequeñas podría considerarse un diseño más sencillo para ahorrar en costos y complejidad.
- Las redes virtuales de radio pueden utilizarse para aislar cargas de trabajo, donde cada radio se administra independientemente de otros radios. Cada carga de trabajo puede incluir varios niveles y varias subredes que se conectan a través de equilibradores de carga de Azure.
- Las redes virtuales en estrella tipo hub-and-spoke se pueden implementar en distintos grupos de recursos e incluso en distintas suscripciones. Cuando se emparejan redes virtuales en distintas suscripciones, las suscripciones pueden estar asociadas al mismo inquilino de Azure Active Directory (Azure AD) o a uno diferente. Esto permite realizar una administración descentralizada de cada carga de trabajo, mientras se comparten los servicios que se mantienen en la red virtual del centro de conectividad.

![Administración de cambios](./media/migrate-best-practices-networking/hub-spoke.png)
*Topología de red en estrella tipo hub-and-spoke*

**Más información:**

- [Obtenga información sobre](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) una topología de red en estrella tipo hub-and-spoke.
- Obtenga recomendaciones de red para ejecutar máquinas virtuales [Windows](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/windows-vm) y [Linux](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/linux-vm) en Azure.
- [Obtenga más información sobre](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) el emparejamiento de VNET.

## <a name="best-practice-design-subnets"></a>Procedimiento recomendado: Diseño de subredes

Para proporcionar aislamiento en una red virtual, ha de segmentarla en una o varias subredes y asignar una parte del espacio de direcciones de la red virtual a cada subred.

- Puede crear varias subredes en cada red virtual.
- De forma predeterminada, Azure enruta el tráfico de red entre todas las subredes de una red virtual.
- Las decisiones de subred se basan en los requisitos técnicos y organizativos.
- Cree las redes con la notación CIDR.
- Al decidir el intervalo de red para las subredes, es importante tener en cuenta que Azure conserva cinco direcciones IP de cada subred que no se pueden usar. Por ejemplo, si crea la subred más pequeña disponible de /29 (con ocho direcciones IP), Azure conservará cinco direcciones, por lo que solo quedan tres direcciones utilizables que pueden asignarse a los hosts de la subred.
- En la mayoría de los casos, se recomienda usar /28 como subred más pequeña.

**Ejemplo:**

La tabla muestra un ejemplo de una red virtual con un espacio de direcciones de 10.245.16.0/20 segmentada en subredes, para una migración planeada.

**Subred** | **CIDR** | **Direcciones** | **Uso**
--- | --- | --- | ---
DEV-FE-EUS2 | 10.245.16.0/22 | 1019 | Máquinas virtuales de nivel web/front-end
DEV-APP-EUS2 | 10.245.20.0/22 | 1019 | Máquinas virtuales de nivel de aplicación
DEV-DB-EUS2 | 10.245.24.0/23 | 507 | VM de base de datos

**Más información:**

- [Obtenga más información sobre](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#segmentation) el diseño de subredes.
- [Vea cómo](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure) una compañía ficticia (Contoso) ha preparado su infraestructura de red para la migración.

## <a name="best-practice-set-up-a-dns-server"></a>Procedimiento recomendado: Configuración de un servidor DNS

Azure agrega un servidor DNS de forma predeterminada al implementar una red virtual. Esto le permite compilar redes virtuales e implementar recursos rápidamente. Aunque este servidor DNS solo proporciona servicios a los recursos en esa red virtual. Si quiere conectar varias redes virtuales entre sí o conectarse a un servidor local desde las redes virtuales, necesita funcionalidades adicionales de resolución de nombres. Por ejemplo, es posible que necesite Active Directory para resolver nombres DNS entre redes virtuales. Para ello, implemente su propio servidor DNS personalizado en Azure.

- Los servidores DNS de una red virtual pueden reenviar consultas de DNS a las resoluciones recursivas en Azure. Esto le permite resolver los nombres de host dentro de esa red virtual. Por ejemplo, un controlador de dominio que se ejecute en Azure puede responder a las consultas de DNS correspondientes a sus propios dominios y reenviar todas las demás consultas a Azure.
- El reenvío de DNS permite que las máquinas virtuales visualicen sus recursos locales (mediante el controlador de dominio) y los nombres de host proporcionados por Azure (mediante el reenviador). El acceso a las resoluciones recursivas de Azure se proporciona mediante la IP virtual 168.63.129.16.
- El reenvío de DNS también habilita la resolución de DNS entre redes virtuales y permite que las máquinas locales resuelvan nombres de host proporcionados por Azure.
  - Para resolver el nombre de host de una máquina virtual, la máquina virtual del servidor DNS debe residir en la misma red virtual y debe configurarse para reenviar consultas de nombre de host a Azure.
  - Como el sufijo DNS es diferente en cada red virtual, puede usar las reglas de reenvío condicional para enviar consultas de DNS a la red virtual correcta para su resolución.
- Al usar sus propios servidores DNS, puede especificar varios servidores DNS para cada red virtual. También puede especificar varios servidores DNS por interfaz de red (para Azure Resource Manager) o por servicio en la nube (para el modelo de implementación clásica).
- Los servidores DNS especificados para una interfaz de red o un servicio en la nube tienen prioridad sobre los servidores DNS especificados para la red virtual.
- En el modelo de implementación de Azure Resource Manager, puede especificar servidores DNS para una red virtual y una interfaz de red, pero el procedimiento recomendado consiste en usar la opción solo en las redes virtuales.

    ![Servidores DNS](./media/migrate-best-practices-networking/dns2.png) *servidores DNS para la red virtual*

**Más información:**

- [Obtenga más información sobre](https://docs.microsoft.com/azure/migrate/contoso-migration-infrastructure) la resolución de nombres al usar su propio servidor DNS.
- [Obtenga más información sobre](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-subscriptions) las reglas y restricciones de nomenclatura DNS.

## <a name="best-practice-set-up-availability-zones"></a>Procedimiento recomendado: Configuración de zonas de disponibilidad

Las zonas de disponibilidad aumentan la alta disponibilidad para proteger las aplicaciones y los datos de errores del centro de datos.

- Las zonas de disponibilidad son ubicaciones físicas exclusivas dentro de una región de Azure.
- Cada zona de disponibilidad consta de uno o varios centros de datos equipados con alimentación, refrigeración y redes independientes.
- Para garantizar la resistencia, hay un mínimo de tres zonas independientes en todas las regiones habilitadas.
- La separación física de las zonas de disponibilidad dentro de una región protege las aplicaciones y los datos frente a los errores del centro de datos.
- Los servicios con redundancia de zona replican las aplicaciones y los datos entre zonas de disponibilidad para protegerlos frente a únicos puntos de error. - - Con las zonas de disponibilidad, Azure ofrece un Acuerdo de Nivel de Servicio con un tiempo de actividad de VM del 99,99 %.

    ![Zona de disponibilidad](./media/migrate-best-practices-networking/availability-zone.png) *Availability zone*

- Puede planear y compilar alta disponibilidad en la arquitectura de la migración. Para ello, coloque los recursos de proceso, almacenamiento, red y datos dentro de una zona y replíquelos en otras zonas. Los servicios de Azure que admiten zonas de disponibilidad se dividen en dos categorías:
  - Servicios globales: Asocie un recurso a una zona específica. Por ejemplo, máquinas virtuales, discos administrados, direcciones IP.
  - Servicios con redundancia de zona: El recurso se replica automáticamente entre zonas. Por ejemplo, almacenamiento con redundancia de zona o Azure SQL Database.
- Puede implementar una carga de Azure estándar equilibrada con cargas de trabajo o capas de aplicación accesibles desde internet, para proporcionar tolerancia a errores de zona.

    ![Equilibrador de carga](./media/migrate-best-practices-networking/load-balancer.png) *Load balancer*

**Más información:**

- [Obtenga información general](https://docs.microsoft.com/azure/availability-zones/az-overview) sobre las zonas de disponibilidad.

## <a name="design-hybrid-cloud-networking"></a>Diseño de redes de nube híbrida

Para una migración correcta, es fundamental conectar las redes corporativas locales a Azure. Esto crea una conexión AlwaysOn conocida como red de nube híbrida, donde se ofrecen servicios de Azure Cloud a los usuarios corporativos. Hay dos opciones para crear este tipo de red:

- **VPN de sitio a sitio**: Esta conexión se establece entre el dispositivo VPN local compatible y una instancia de Azure VPN Gateway que está implementada en una red virtual. Todos los recursos locales autorizados tienen acceso a las redes virtuales. Las comunicaciones de sitio a sitio se envían a través de un túnel cifrado a través de internet.
- **Azure ExpressRoute:** Esta conexión se establece entre la red local y Azure, a través de un partner de ExpressRoute. Se trata de una conexión privada y el tráfico no pasa por Internet.

**Más información:**

- [Obtenga más información](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/vpn) sobre las redes de nube híbrida.

## <a name="best-practice-implement-a-highly-available-site-to-site-vpn"></a>Procedimiento recomendado: Implementación de una VPN de sitio a sitio de alta disponibilidad

Para implementar una VPN de sitio a sitio, configure una instancia de VPN Gateway en Azure.

- VPN Gateway es un tipo específico de puerta de enlace de red virtual que se usa para enviar tráfico cifrado entre una red virtual de Azure y una ubicación local a través de la red pública de Internet.
- También puede usar una instancia de VPN Gateway para enviar tráfico cifrado entre las redes virtuales de Azure a través de la red de Microsoft.
- Cada red virtual solo puede tener una instancia de VPN Gateway.
- Se pueden crear varias conexiones a la misma instancia. Al crear varias conexiones a la misma instancia de VPN Gateway, todos los túneles VPN comparten el ancho de banda de puerta de enlace disponible.
- Cada instancia de Azure VPN Gateway consta de dos instancias en una configuración activa-en espera.
  - En caso de mantenimiento planeado o interrupción imprevista de la instancia activa, se produce la conmutación por error y la instancia en espera toma el relevo automáticamente y reanuda la conexión de sitio a sitio o de red virtual a red virtual.
  - El cambio produce una breve interrupción.
  - En el caso del mantenimiento planeado, la conectividad se debe restaurar en un plazo de 10 a 15 segundos.
  - Si se trata de problemas imprevistos, la recuperación de la conexión llevará más tiempo, sobre un minuto o un minuto y medio en el peor de los casos.
  - Las conexiones de cliente VPN de punto a sitio (P2S) con la puerta de enlace se desconectarán y los usuarios tendrán que volver a conectarse desde las máquinas cliente.

Al configurar una VPN de sitio a sitio, haga lo siguiente:

- Necesita una red virtual cuyo intervalo de direcciones no se superponga con la red local a la que se conectará la VPN.
- Cree una subred de puerta de enlace en la red.
- Cree una instancia de VPN Gateway, especifique el tipo de puerta de enlace (VPN) y si la puerta de enlace está basada en directivas o en rutas. Se recomienda una VPN de tipo RouteBased como más capaz y mejor preparada para el futuro.
- Cree una puerta de enlace de red local en el entorno local y configure el dispositivo VPN local.
- Cree una conexión VPN de sitio a sitio de conmutación por error entre la puerta de enlace de red virtual y el dispositivo local. El uso de VPN basadas en rutas permite conexiones de tipo activa-pasiva o activa-activa con Azure. Las VPN basadas en rutas también admiten conexiones simultáneas de sitio a sitio (desde cualquier equipo) y de punto a sitio (desde un único equipo).
- Especifique la SKU de la puerta de enlace que quiere utilizar. Esto dependerá de los requisitos, las unidades de rendimiento, las características y los acuerdos de nivel de servicio de la carga de trabajo.
- Protocolo de puerta de enlace de borde (BGP) es una característica opcional que puede usar con Azure ExpressRoute e instancias de VPN Gateway basadas en rutas para propagar las rutas BGP locales a sus redes virtuales.

![VPN](./media/migrate-best-practices-networking/vpn.png)
*VPN de sitio a sitio*

**Más información:**

- [Revise ](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) los dispositivos VPN locales compatibles.
- [Obtenga información general](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) sobre las instancias de VPN Gateway.
- [Obtenga más información sobre](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-highlyavailable) las conexiones VPN de alta disponibilidad.
- [Obtenga más información sobre](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design) cómo planear y diseñar una instancia de VPN Gateway.
- [Revise](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsku) la configuración de VPN Gateway.
- [Revise](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#gwsku) las SKU de puerta de enlace.
- [Obtenga información sobre](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-bgp-overview) cómo configurar BGP con instancias de Azure VPN Gateway.

### <a name="best-practice-configure-a-gateway-for-vpn-gateways"></a>Procedimiento recomendado: Configuración de una puerta de enlace para instancias de VPN Gateway

Al crear una instancia de VPN Gateway en Azure, se debe usar una subred especial denominada GatewaySubnet. Al crear esta subred tenga en cuenta los procedimientos recomendados siguientes:

- La longitud de prefijo de la subred de puerta de enlace puede tener una longitud de prefijo máxima de 29 (por ejemplo, 10.119.255.248/29). La recomendación actual es utilizar una longitud de prefijo de 27 (por ejemplo, 10.119.255.224/27).
- Al definir el espacio de direcciones de la subred de puerta de enlace, use la última parte del espacio de direcciones de la red virtual.
- Cuando utilice Azure GatewaySubnet, no implemente nunca máquinas virtuales u otros dispositivos, como Application Gateway, en la subred de puerta de enlace.
- No asigne a un grupo de seguridad de red (NSG) a esta subred. Hará que la puerta de enlace deje de funcionar.

**Más información:**

- [Utilice esta herramienta](https://gallery.technet.microsoft.com/scriptcenter/Address-prefix-calculator-a94b6eed) para determinar el espacio de direcciones IP.

## <a name="best-practice-implement-azure-virtual-wan-for-branch-offices"></a>Procedimiento recomendado: Implementación de Azure Virtual WAN para las sucursales

En el caso de varias conexiones VPN, Azure Virtual WAN es un servicio de redes que ofrece conectividad de rama a rama automatizada y optimizada mediante Azure.

- Virtual WAN permite conectar y configurar los dispositivos de rama para comunicarse con Azure. Esto puede realizarse manualmente o con dispositivos del proveedor preferido a través un partner de Virtual WAN.
- El uso de dispositivos del proveedor preferido simplifica el uso, la conectividad y la administración de la configuración.
- El panel integrado de Azure WAN facilita información instantánea para la resolución de problemas que ahorra tiempo y ofrece una forma sencilla de realizar un seguimiento de la conectividad de sitio a sitio a gran escala.

**Más información:** 
[Obtenga más información sobre](https://docs.microsoft.com/azure/virtual-wan/virtual-wan-about) Azure Virtual WAN.

### <a name="best-practice-implement-expressroute-for-mission-critical-connections"></a>Procedimiento recomendado: Implementación de ExpressRoute para las conexiones críticas

El servicio Azure ExpressRoute amplía su infraestructura local a la nube de Microsoft mediante la creación de conexiones privadas entre el centro de datos virtual de Azure y redes locales.

- Las conexiones ExpressRoute pueden efectuarse a través de una red de conectividad universal (IP VPN), una red Ethernet de punto a punto o mediante un proveedor de conectividad. No pasan por la red pública de internet.
- Las conexiones ExpressRoute ofrecen mayor seguridad, confiabilidad y velocidades más altas (hasta 10 Gbps), con una latencia constante.
- ExpressRoute resulta útil para los centros de datos virtuales, ya que los clientes pueden aprovechar las reglas de cumplimiento asociadas a las conexiones privadas.
- Con ExpressRoute Direct puede conectarse directamente a los enrutadores de Microsoft a 100 Gbps, en caso de necesidades de ancho de banda mayores.
- ExpressRoute utiliza BGP para intercambiar rutas entre redes locales, instancias de Azure y direcciones públicas de Microsoft.

La implementación de conexiones ExpressRoute implica normalmente tomar contacto con un proveedor de servicios de ExpressRoute. Para comenzar rápidamente, es habitual usar inicialmente una VPN de sitio a sitio para establecer la conectividad entre el centro de datos virtual y los recursos locales y, luego, migrar a una conexión ExpressRoute cuando se haya establecido la interconexión física con el proveedor de servicios.

**Más información:**

- [Lea la información general](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) sobre ExpressRoute.
- [Obtenga más información sobre](https://docs.microsoft.com/azure/expressroute/expressroute-erdirect-about) ExpressRoute Direct.

### <a name="best-practice-optimize-expressroute-routing-with-bgp-communities"></a>Procedimiento recomendado: Optimización del enrutamiento de ExpressRoute con las comunidades de BGP

Cuando hay varios circuitos ExpressRoute, tiene más de una ruta de acceso para conectarse a Microsoft. Por consiguiente, puede producirse un enrutamiento no óptimo y es posible que el tráfico utilice una ruta de acceso más larga para conectarse con Microsoft y este a su vez, con su red. Cuanto más larga sea la ruta de acceso a la red, mayor será la latencia. La latencia tiene un efecto directo en la experiencia del usuario y en el rendimiento de las aplicaciones.

**Ejemplo:**

Vamos a ver un ejemplo:

- Tiene dos oficinas en Estados Unidos, una en Los Ángeles y la otra en Nueva York.
- Las oficinas están conectadas a una WAN, que puede ser su propia red troncal o la VPN de la dirección IP del proveedor de servicios.
- Tiene dos circuitos ExpressRoute, uno en el oeste de EE.UU. y otro en el este, que también están conectados a la red de área extensa. Obviamente, tiene dos rutas de acceso para conectarse a la red de Microsoft.

**Problema:**

Ahora supongamos que tiene una implementación de Azure (por ejemplo, Azure App Service) en el Oeste de EE. UU. y en el Este de EE. UU.

- Quiere que los usuarios de ambas oficinas tengan acceso a sus servicios de Azure más cercanos para disfrutar de una experiencia óptima.
- Así que desea conectar los usuarios de Los Ángeles a Azure Oeste de EE. UU. y los usuarios de Nueva York a Azure Este de EE. UU.
- Esto funciona para los usuarios de la costa este, pero no para los de la costa oeste. El problema es el siguiente:
  - En cada circuito ExpressRoute, se indican los prefijos de Azure Este de EE. UU. (23.100.0.0/16) y de Azure Oeste de EE. UU. (13.100.0.0/16).
  - Al no saber qué prefijo corresponde a cada región, los prefijos no se tratan de forma distinta.
  - La red WAN puede presuponer que ambos prefijos están más cerca del Este de EE. UU. que del Oeste de EE. UU. y, por tanto, enrutar a los usuarios de ambas oficinas al circuito ExpressRoute del Este de EE. UU., lo que proporciona una experiencia no tan óptima a los usuarios de la oficina de Los Ángeles.

![VPN](./media/migrate-best-practices-networking/bgp1.png)
*Conexión no optimizada de las comunidades de BGP*

**Solución:**

Para optimizar el enrutamiento para los usuarios de ambas oficinas, debe saber qué prefijo corresponde a Azure Oeste de EE. UU. y qué prefijo corresponde a Azure Este de EE. UU. Puede codificar esta información mediante los valores de la comunidad de BGP.

- Asigne un valor único de comunidad de BGP a cada región de Azure. Por ejemplo: 12076:51004 para el Este de EE. UU.; 12076:51006 para el Oeste de EE. UU.
- Ahora que ha quedado claro qué prefijo pertenece a cada región de Azure, puede configurar un circuito ExpressRoute preferido.
- Puesto que usa BGP para intercambiar información de enrutamiento, puede usar la preferencia local de BGP para influir en el enrutamiento.
- En nuestro ejemplo, se asigna un valor de preferencia local superior a 13.100.0.0/16 en el Oeste de EE. UU. que en el Este de EE. UU., y del mismo modo, un valor de preferencia local superior a 23.100.0.0/16 en el Este de EE. UU. que en el Oeste de EE. UU.
- Esta configuración garantiza que, cuando las dos rutas de acceso a Microsoft estén disponibles, los usuarios de Los Ángeles se conectarán a Azure Oeste de EE. UU. con el circuito oeste y los de Nueva York lo se conectarán a Azure Este de EE. UU. con el circuito este. Con lo cual, se obtendrá un enrutamiento óptimo en ambas regiones.

![VPN](./media/migrate-best-practices-networking/bgp2.png)
*Conexión optimizada de las comunidades de BGP*

**Más información:**

- [Más información sobre](https://docs.microsoft.com/azure/expressroute/expressroute-optimize-routing) cómo optimizar el enrutamiento.

## <a name="securing-vnets"></a>Protección de redes virtuales

La responsabilidad de proteger las redes virtuales se comparte entre Microsoft y usted. Microsoft facilita muchas características de red, además de servicios que ayudan a proteger los recursos. Al diseñar la seguridad de las redes virtuales, los procedimientos recomendados que debe seguir incluyen implementar una red perimetral, usar filtrado y grupos de seguridad, proteger el acceso a los recursos y las direcciones IP e implementar protección frente a ataques.

**Más información:**

- [Obtenga información general](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices) sobre procedimientos recomendados para seguridad de red.
- [Aprenda a](https://docs.microsoft.com/azure/virtual-network/virtual-network-vnet-plan-design-arm#security) diseñar redes seguras.

## <a name="best-practice-implement-an-azure-perimeter-network"></a>Procedimiento recomendado: Implementación de una red perimetral de Azure

Aunque Microsoft realiza importantes inversiones en la protección de la infraestructura en la nube, el usuario también debe proteger los servicios en la nube y los grupos de recursos. Un enfoque de varios niveles de seguridad proporciona la mejor defensa. La implementación de una red perimetral es un elemento importante de dicha estrategia de defensa.

- Una red perimetral protege los recursos de red internos de una red que no sea de confianza.
- Es la capa más externa que queda expuesta a Internet. Suele ubicarse entre Internet y la infraestructura de la empresa, normalmente con algún tipo de protección a ambos lados.
- En una topología red de empresa típica, la infraestructura principal está considerablemente reforzada en los perímetros, con varias capas de dispositivos de seguridad. El límite de cada nivel consta de dispositivos y puntos de aplicación de directivas.
- Cada capa puede incluir una combinación de las soluciones de seguridad de red que incluyen firewalls, prevención de ataques por denegación de servicio (DoS), sistemas de protección o detección de intrusiones (IDS/IPS) y dispositivos VPN.
- El cumplimiento de directivas en la red perimetral puede usar directivas de firewall, listas de control de acceso (ACL) o enrutamientos específicos.
- A medida que el tráfico entrante llega de Internet, se ve interceptado y controlado por una combinación de la solución de defensa que bloquea los ataques y el tráfico perjudicial, a la vez que permite las solicitudes legítimas en la red.
- El tráfico entrante puede enrutarse directamente a los recursos de la red perimetral. El recurso de la red perimetral puede entonces comunicarse con otros recursos más profundos de la red, lo que hace avanzar el tráfico hacia la red después de la validación.

En la siguiente ilustración se muestra un ejemplo de una sola red perimetral de subred en una red corporativa con dos límites de seguridad.

![VPN](./media/migrate-best-practices-networking/perimeter.png)
*Implementación de la red perimetral*

**Más información:**

- [Obtenga más información sobre](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) cómo implementar una red perimetral entre Azure y el centro de datos local.

## <a name="best-practice-filter-vnet-traffic-with-nsgs"></a>Procedimiento recomendado: Filtrado del tráfico de red virtual con NSG

Los grupos de seguridad de red (NSG) contienen varias reglas de seguridad entrante y saliente que filtran el tráfico hacia y desde los recursos. El filtrado puede ser por dirección IP de origen y destino, puerto y protocolo.

- Los NSG contienen reglas de seguridad que permiten o deniegan el tráfico de red entrante (o el tráfico de red saliente) de varios tipos de recursos de Azure. Para cada regla, puede especificar un origen y destino, un puerto y un protocolo.
- Las reglas de NSG se evalúan por prioridad con información de tupla de cinco elementos (origen, puerto de origen, destino, puerto de destino y protocolo) para permitir o denegar el tráfico.
- Se crea un registro de flujo para las conexiones existentes. Se permite o deniega la comunicación en función del estado de conexión del registro de flujo.
- Un registro de flujo permite que un NSG sea de tipo con estado. Por ejemplo, si especifica una regla de seguridad de salida para cualquier dirección a través del puerto 80, no tiene que especificar una regla de seguridad de entrada para la respuesta al tráfico saliente. Solo debe especificar una regla de seguridad de entrada si la comunicación se inicia de forma externa.
- Lo contrario también es cierto. Si se permite el tráfico entrante a través de un puerto, no hay que especificar una regla de seguridad de salida que responda al tráfico a través del puerto.
- Las conexiones existentes no se interrumpen cuando se quita una regla de seguridad que habilitó el flujo. Los flujos de tráfico se interrumpen cuando se detienen las conexiones y no fluye ningún tráfico en ninguna dirección durante al menos unos minutos.
- Al crear grupos de seguridad de red, cree el menor número posible pero tantos como sean necesarios.

### <a name="best-practice-secure-northsouth-and-eastwest-traffic"></a>Procedimiento recomendado: Protección del tráfico vertical de arriba abajo y horizontal de derecha a izquierda

Al proteger las redes virtuales, es importante tener en cuenta los vectores de ataque.

- El uso exclusivo de grupos de seguridad de red de subred simplifica el entorno, pero solo protege el tráfico en la subred. Esto se conoce como tráfico vertical de arriba abajo.
- El tráfico entre máquinas virtuales en la misma subred se conoce como tráfico horizontal de derecha a izquierda.
- Es importante usar ambos formatos de protección, de modo que si un hacker obtiene acceso desde el exterior, se detendrá cuando intente conectarse a máquinas ubicadas en la misma subred.

### <a name="use-service-tags-on-nsgs"></a>Uso de etiquetas de servicio en los NSG

Una etiqueta de servicio representa un grupo de prefijos de direcciones IP. El uso de una etiqueta de servicio contribuye a minimizar la complejidad al crear reglas de NSG.

- Puede utilizar etiquetas de servicio en lugar de direcciones IP específicas al crear reglas.
- Microsoft administra los prefijos de direcciones asociados a una etiqueta de servicio y actualiza la etiqueta automáticamente a medida que las direcciones cambian.
- No puede crear su propia etiqueta de servicio ni especificar qué direcciones IP se incluyen dentro de una etiqueta.

Las etiquetas de servicio eliminan el trabajo manual de asignar una regla a grupos de servicios de Azure. Por ejemplo, si quiere permitir que una subred de red virtual que incluye servidores web tenga acceso a una base de datos de Azure SQL, puede crear una regla de salida al puerto 1433 y usar la etiqueta de servicio **Sql**.

- Esta etiqueta **Sql** denota los prefijos de direcciones de los servicios Azure SQL Database y Azure SQL Data Warehouse.
- Si especifica **Sql** como valor, se permite o se deniega el tráfico a Sql.
- Si solo quiere permitir el acceso a **Sql** en una región determinada, puede especificarla. Por ejemplo, si quiere permitir el acceso a Azure SQL Database solo en la región Este de EE. UU., puede especificar **Sql.EastUS** como etiqueta de servicio.
- La etiqueta representa el servicio, no instancias específicas del mismo. Por ejemplo, la etiqueta representa el servicio Azure SQL Database, pero no un servidor o una base de datos SQL en particular.
- Todos los prefijos de dirección representados por esta etiqueta también se representan mediante la etiqueta **Internet**.

**Más información:**

- [Obtenga información sobre](https://docs.microsoft.com/azure/virtual-network/security-overview) los grupos de seguridad de red (NSG).
- [Revise](https://docs.microsoft.com/azure/virtual-network/security-overview#service-tags) las etiquetas de servicio disponibles para los NSG.

## <a name="best-practice-use-application-security-groups"></a>Procedimiento recomendado: Uso de grupos de seguridad de aplicaciones

Los grupos de seguridad de aplicaciones permiten configurar la seguridad de red como extensión natural de una estructura de aplicación.

- Puede agrupar las máquinas virtuales y definir directivas de seguridad de red basadas en grupos de seguridad de aplicaciones.
- Los grupos de seguridad de aplicaciones le permiten reutilizar la directiva de seguridad a escala sin mantenimiento manual de direcciones IP explícitas.
- Los grupos de seguridad de aplicaciones controlan la complejidad de las direcciones IP explícitas y de varios conjuntos de reglas, lo que le permite centrarse en su lógica de negocios.

**Ejemplo:**

![Grupo de seguridad de aplicaciones](./media/migrate-best-practices-networking/asg.png)
*Ejemplo de grupo de seguridad de aplicaciones*

**Interfaz de red** | **Grupo de seguridad de aplicaciones**
--- | ---
NIC1 | AsgWeb
NIC2 | AsgWeb
NIC3 | AsgLogic
NIC4 | AsgDb

- En nuestro ejemplo, cada interfaz de red pertenece a un único grupo de seguridad de aplicaciones, pero en realidad una interfaz puede pertenecer a varios grupos, de acuerdo con los límites de Azure.
- Ninguna de las interfaces de red tiene un grupo de seguridad de red asociado. NSG1 está asociado a ambas subredes y contiene las siguientes reglas.

<!--markdownlint-disable MD033 -->

**Nombre de la regla** | **Propósito** | **Detalles**
--- | --- | ---
Allow-HTTP-Inbound-Internet | Se permite el tráfico de Internet a los servidores web. La regla de seguridad predeterminada DenyAllInbound deniega el tráfico entrante desde Internet, por lo que no se necesita ninguna regla adicional para los grupos de seguridad de aplicaciones AsgLogic y AsgDb. | Prioridad: 100<br/><br/> Origen: Internet<br/><br/> Puerto de origen: *<br/><br/> Destino: AsgWeb<br/><br/> Puerto de destino: 80<br/><br/> Protocolo: TCP<br/><br/> Acceso: Permitir.
Deny-Database-All | La regla de seguridad predeterminada AllowVNetInBound permite todas las comunicaciones entre los recursos de la misma red virtual y es necesaria para denegar el tráfico desde todos los recursos. | Prioridad: 120<br/><br/> Origen: *<br/><br/> Puerto de origen: *<br/><br/> Destino: AsgDb<br/><br/> Puerto de destino: 1433<br/><br/> Protocolo: Todo<br/><br/> Acceso: Denegar.
Allow-Database-BusinessLogic | Se permite el tráfico desde el grupo de seguridad de aplicaciones AsgLogic al grupo de seguridad de aplicaciones AsgDb. La prioridad de esta regla es superior a la de la regla Deny-Database-All y se procesará antes, por lo que se permite el tráfico del grupo de seguridad de aplicaciones AsgLogic y se bloquea el resto del tráfico. | Prioridad: 110<br/><br/> Origen: AsgLogic<br/><br/> Puerto de origen: *<br/><br/> Destino: AsgDb<br/><br/> Puerto de destino: 1433<br/><br/> Protocolo: TCP<br/><br/> Acceso: Permitir.

<!--markdownlint-enable MD033 -->

- Las reglas que especifican un grupo de seguridad de aplicaciones como origen o destino solo se aplican a las interfaces de red que son miembros del grupo de seguridad de aplicaciones. Si la interfaz de red no es miembro de un grupo de seguridad de aplicaciones, la regla no se aplica a la interfaz de red aunque el grupo de seguridad de red esté asociado a la subred.

**Más información:**

- [Obtenga más información sobre](https://docs.microsoft.com/azure/virtual-network/security-overview#application-security-groups) los grupos de seguridad de aplicaciones.

### <a name="best-practice-secure-access-to-paas-using-vnet-service-endpoints"></a>Procedimiento recomendado: Protección del acceso a PaaS con puntos de conexión de servicio de red virtual

Los puntos de conexión de servicio de red virtual extienden el espacio de direcciones privadas y la identidad de la red virtual a los servicios de Azure a través de una conexión directa.

- Los puntos de conexión permiten proteger solo los recursos de servicio de Azure críticos en las redes virtuales. El tráfico desde la red virtual al servicio de Azure siempre permanece en la red troncal de Microsoft Azure.
- El espacio de direcciones privadas de red virtual se puede estar solapando y, por tanto, no se puede usar para identificar de forma única el tráfico que se origina en la red virtual.
- Una vez habilitados los puntos de conexión de servicio en la red virtual, puede proteger los recursos de servicio de Azure agregando una regla de red virtual a los recursos de servicio. Esto proporciona una mayor seguridad al quitar por completo el acceso de la red pública de Internet a los recursos y permitir solo el tráfico procedente de la red virtual.

![Puntos de conexión de servicio](./media/migrate-best-practices-networking/endpoint.png)
*Puntos de conexión de servicio*

**Más información:**

- [Obtenga más información sobre](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) los puntos de conexión de servicio de red virtual.

## <a name="best-practice-control-public-ip-addresses"></a>Procedimiento recomendado: Control de las direcciones IP públicas

Las direcciones IP públicas de Azure pueden asociarse a máquinas virtuales, equilibradores de carga, instancias de Application Gateway e instancias de VPN Gateway.

- Las direcciones IP públicas permiten la comunicación entrante de los recursos de Internet con los recursos de Azure y la comunicación saliente de los recursos de Azure con Internet.
- Las direcciones IP públicas se crean con una SKU básica o estándar, que tiene varias diferencias. Las SKU estándar pueden asignarse a cualquier servicio, pero normalmente se configuran en máquinas virtuales, equilibradores de carga e instancias de Application Gateway.
- Es importante tener en cuenta que una dirección IP pública básica no tiene un NSG configurado automáticamente. Tiene que configurar el suyo propio y asignarle reglas para controlar el acceso. Las direcciones IP de SKU estándar tienen asignados un NSG y reglas de forma predeterminada.
- Como procedimiento recomendado, las máquinas virtuales no deben configurarse con una dirección IP pública.
  - Si necesita un puerto abierto, debe ser solo para servicios web, como el puerto 80 o 443.
  - Los puertos de administración remota estándar, como SSH (22) y RDP (3389), deben establecerse para que denieguen, junto con los demás puertos, el uso de grupos de seguridad de red.
- Lo más recomendable es situar las máquinas virtuales detrás de un equilibrador de carga de Azure o una instancia de Application Gateway. Si después se necesita acceso a los puertos de administración remota, puede usar el acceso Just-In-Time a máquinas virtuales en Azure Security Center.

**Más información:**

- [Obtenga más información sobre](https://docs.microsoft.com/azure/virtual-network/virtual-network-ip-addresses-overview-arm#public-ip-addresses) las direcciones IP públicas en Azure.
- [Obtenga más información](https://docs.microsoft.com/azure/security-center/security-center-just-in-time) sobre el acceso Just-In-Time a máquinas virtuales en Azure Security Center.

## <a name="take-advantage-of-azure-security-features-for-networking"></a>Aproveche las ventajas de las características de seguridad de Azure para redes

Azure cuenta con características de seguridad de plataforma que son fáciles de usar y ofrecen contramedidas avanzadas a ataques de red comunes. Entre estas se incluyen Azure Firewall, firewall de aplicaciones web y Network Watcher.

## <a name="best-practice-deploy-azure-firewall"></a>Procedimiento recomendado: Implementación de Azure Firewall

Azure Firewall es un servicio de seguridad de red administrado y basado en la nube que protege los recursos de la red virtual. Se trata de un firewall administrado con estado completo, con alta disponibilidad integrada y una escalabilidad sin restricciones en la nube.

![Puntos de conexión de servicio](./media/migrate-best-practices-networking/firewall.png)
*Azure Firewall*

- En Azure Firewall, puede crear, aplicar y registrar centralmente directivas de conectividad de red y aplicación en todas las suscripciones y redes virtuales.
- Azure Firewall usa una dirección IP pública estática para los recursos de red virtual, lo que permite que los firewall externos identifiquen el tráfico procedente de la red virtual.
- Azure Firewall está totalmente integrado con Azure Monitor a efectos de registros y análisis.
- Como procedimiento recomendado al crear reglas de Azure Firewall, utilice las etiquetas FQDN para crear reglas.
  - Una etiqueta FQDN representa un grupo de FQDN asociados a conocidos servicios de Microsoft.
  - Puede usar una etiqueta FQDN para permitir que pase el tráfico de red saliente necesario a través del firewall.
- Por ejemplo, para permitir manualmente el tráfico de red de Windows Update a través del firewall, tendría que crear varias reglas de aplicación. Con las etiquetas FQDN, cree una regla de aplicación e incluya la etiqueta de Windows Update. Con esta regla en curso, el tráfico de red a los puntos de conexión de Microsoft Windows Update puede fluir a través del firewall.

**Más información:**

- [Obtenga información general](https://docs.microsoft.com/azure/firewall/overview) sobre Azure Firewall.
- [Obtenga más información sobre](https://docs.microsoft.com/azure/firewall/fqdn-tags) las etiquetas FQDN.

## <a name="best-practice-deploy-a-web-application-firewall-waf"></a>Procedimiento recomendado: Implementación de un firewall de aplicaciones web (WAF)

Las aplicaciones web son cada vez más los objetivos de ataques malintencionados que aprovechan vulnerabilidades habitualmente conocidas. Entre las vulnerabilidades de seguridad se incluyen los ataques por inyección de código SQL y los ataques de scripts de sitios. Impedir tales ataques en el código de aplicación puede ser un verdadero desafío y requerir tareas rigurosas de mantenimiento, aplicación de revisiones y supervisión en varias capas de la topología de aplicación. Un firewall de aplicaciones web centralizado simplifica enormemente la administración de la seguridad y ayuda a los administradores de aplicaciones a protegerse frente a amenazas o intrusiones. Un firewall de aplicaciones web puede reaccionar más rápidamente ante las amenazas de seguridad aplicando revisiones a las vulnerabilidades conocidas en una ubicación central en lugar de proteger cada una de las aplicaciones web por separado. Las puertas de enlace de aplicaciones existentes pueden transformarse rápidamente en puertas de enlace con un firewall de aplicaciones web habilitado.

El firewall de aplicaciones web (WAF) es una característica de Azure Application Gateway.

- WAF ofrece una protección centralizada de las aplicaciones web contra las vulnerabilidades de seguridad comunes.
- WAF protege sin modificación del código de back-end.
- Puede proteger varias aplicaciones web al mismo tiempo detrás de una puerta de enlace de aplicaciones.
- WAF se integra con Azure Security Center.
- Puede personalizar las reglas y grupos de reglas de WAF para que adapten a sus requisitos de aplicación.
- Como procedimiento recomendado, debe usar un WAF delante de cualquier aplicación accesible desde la web, como las aplicaciones en máquinas virtuales de Azure, o como Azure App Service.

**Más información:**

- [Obtenga más información sobre](https://docs.microsoft.com/azure/application-gateway/waf-overview) WAF.
- [Revise](https://docs.microsoft.com/azure/application-gateway/application-gateway-waf-configuration) las limitaciones y exclusiones de WAF.

## <a name="best-practice-implement-azure-network-watcher"></a>Procedimiento recomendado: Implementación de Azure Network Watcher

Azure Network Watcher ofrece herramientas para supervisar los recursos y las comunicaciones en una red virtual de Azure. Por ejemplo, puede supervisar las comunicaciones entre una máquina virtual y un punto de conexión, como otra máquina virtual o un FQDN, ver los recursos y las relaciones entre los recursos de una red virtual o diagnosticar problemas de tráfico de red.

![Network Watcher](./media/migrate-best-practices-networking/network-watcher.png)
*Network Watcher*

- Con Network Watcher puede supervisar y diagnosticar problemas de red sin iniciar sesión en las máquinas virtuales.
- Puede desencadenar la captura de paquetes estableciendo alertas y obtener acceso a información de rendimiento en tiempo real en el ámbito de paquete. Cuando vea un problema, podrá investigarlo en detalle.
- Como procedimiento recomendado, use Network Watcher para revisar los registros de flujo de NSG.
  - Los registros de flujo de NSG de Network Watcher le permiten visualizar información sobre el tráfico IP de entrada y de salida en un grupo de seguridad de red.
  - Los registros de flujo se escriben en formato JSON.
  - Los registros de flujo muestran los flujos de entrada y de salida en función de cada regla, la tarjeta de interfaz de red (NIC) a la que se aplica el flujo, información de tupla de cinco elementos sobre el flujo (dirección IP de origen o destino, puerto de origen o destino y protocolo), y si se permitió o denegó el tráfico.

**Más información:**

- [Obtenga información general](https://docs.microsoft.com/azure/network-watcher) sobre Network Watcher.
- [Obtenga más información](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) sobre los registros de flujo de NSG.

## <a name="use-partner-tools-in-the-azure-marketplace"></a>Uso de herramientas de partner en Azure Marketplace

En el caso de topologías de red más complejas, puede usar los productos de seguridad de partners de Microsoft, en aplicaciones virtuales de red (NVA) concretas.

- Una NVA es una máquina virtual que ejecuta una función de red, como, por ejemplo, un firewall, la optimización de WAN u otra función de red.
- Las NVA refuerzan las funciones de red y seguridad de las redes virtuales. Pueden implementarse para firewalls de alta disponibilidad, prevención de intrusiones, detección de intrusiones, firewalls de aplicaciones web (WAF), optimización de WAN, enrutamiento, equilibrio de carga, VPN, administración de certificados, Active Directory y autenticación multifactor.
- Las NVA están disponibles a través de numerosos proveedores en  [Azure Marketplace](https://azuremarketplace.microsoft.com).

## <a name="best-practice-implement-firewalls-and-nvas-in-hub-networks"></a>Procedimiento recomendado: Implementación de aplicaciones virtuales de red (NVA) y firewalls en redes de centro de conectividad

En el centro de conectividad, la red perimetral (con acceso a Internet) suele administrarse mediante un firewall de Azure, una granja de firewalls o firewalls de aplicaciones web (WAF). Tenga en cuenta las siguientes comparaciones.

<!--markdownlint-disable MD033 -->

**Tipo de firewall** | **Detalles**
--- | ---
WAF | Las aplicaciones web son comunes y tienden a experimentar vulnerabilidades de seguridad y de otro tipo.<br/><br/> Los WAF están diseñados para detectar ataques contra las aplicaciones web (HTTP/HTTPS), más específicamente que un firewall genérico.<br/><br/> En comparación con la tecnología de firewall tradicional, los WAF tienen un conjunto de características específicas que protegen los servidores web internos frente a amenazas.
Azure Firewall | Al igual que las granjas de firewalls de NVA, Azure Firewall usa un mecanismo de administración común y un conjunto de reglas de seguridad para proteger las cargas de trabajo hospedadas en redes de radio y para controlar el acceso a las redes locales.<br/><br/> Azure Firewall tiene escalabilidad integrada.
Firewalls de NVA | Como Azure Firewall, las granjas de firewalls de NVA cuentan con un mecanismo de administración común y un conjunto de reglas de seguridad para proteger las cargas de trabajo hospedadas en redes de radio y controlar el acceso a las redes locales.<br/><br/> Los firewalls de NVA se pueden escalar manualmente detrás de un equilibrador de carga.<br/><br/> Aunque un firewall de NVA tiene menos software especializado en comparación con un WAF, tiene un ámbito de aplicación más amplio para filtrar e inspeccionar cualquier tipo de tráfico de entrada y salida.<br/><br/> Si quiere utilizar una NVA, puede encontrarlas en Azure Marketplace.

<!--markdownlint-enable MD033 -->

Se recomienda usar un conjunto de instancias de Azure Firewall (o aplicaciones de red virtual) para el tráfico que se origina en Internet y otro para el tráfico que se origina en el entorno local.

- Utilizar únicamente un conjunto de firewalls para ambos es un riesgo de seguridad, ya que no proporciona ningún perímetro de seguridad entre los dos conjuntos de tráfico de red.
- El uso de capas de firewalls independientes reduce la complejidad de la comprobación de las reglas de seguridad y deja claro qué reglas se corresponden con cada solicitud de red entrante.

**Más información:**

- [Obtenga más información sobre](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) el uso de NVA en una red virtual de Azure.

## <a name="next-steps"></a>Pasos siguientes

Examine otros procedimientos recomendados:

- [Procedimientos recomendados](./migrate-best-practices-security-management.md) para la seguridad y administración después de la migración.
- [Procedimientos recomendados](./migrate-best-practices-costs.md) para la administración de costos después de la migración.
