---
title: Escenarios y ejemplos de gobernanza de suscripciones
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Proporciona ejemplos de cómo implementar un sistema de gobernanza de suscripciones de Azure para escenarios comunes.
author: rdendtler
ms.author: rodend
ms.date: 01/03/2017
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: reference
ms.openlocfilehash: 208bab0093d8add065a8c8f5ad2b92d9ff012fe8
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032515"
---
# <a name="examples-of-implementing-azure-enterprise-scaffold"></a>Ejemplos de implementación de plantillas scaffold empresariales de Azure

> [!NOTE]
> Scaffolding empresarial de Azure se ha integrado con Microsoft Cloud Adoption Framework. El contenido de este artículo se representa ahora en la sección [Preparación](../ready/index.md) del nuevo marco. Este artículo estará en desuso a principios de 2020. Para empezar a usar el nuevo proceso, consulte [Introducción a la preparación](../ready/index.md), [Creación de la primera zona de aterrizaje](../ready/azure-readiness-guide/migration-landing-zone.md) o [Consideraciones sobre la zona de aterrizaje](../ready/considerations/index.md).

En este artículo se ofrecen ejemplos de cómo una empresa puede implementar las recomendaciones de un [scaffolding empresarial de Azure](./azure-scaffold.md). Se usa una compañía ficticia denominada "Contoso" con el objetivo de ilustrar las prácticas recomendadas para escenarios comunes.

## <a name="background"></a>Fondo

Contoso es una empresa con representación en todo el mundo que ofrece soluciones de cadena de suministro a sus clientes. Proporciona todos los elementos, desde un modelo de software como servicio a un modelo de empaquetado implementado de forma local. Desarrollan software en todo el mundo con centros de desarrollo importantes en India, Estados Unidos y Canadá.

La parte de ISV de la compañía está dividida en varias unidades de negocio independientes que administran productos con una importante actividad empresarial. Cada unidad de negocio tiene sus propios arquitectos, directores de producto y desarrolladores.

La unidad de negocio de servicios de tecnología empresariales (ETS) proporciona las funcionalidades de TI centralizadas y administra varios centros de datos donde las unidades de negocio hospedan sus aplicaciones. Además de la administración de los centros de datos, la organización ETS proporciona y administra la colaboración centralizada (por ejemplo, el correo electrónico y los sitios web) y los servicios de red y telefonía. También se encargan de las cargas de trabajo orientadas al cliente de las unidades de negocio más pequeñas que no disponen de personal de operaciones.

En este artículo se usan los siguientes roles:

- David, administrador de Azure en ETS
- Alicia, directora de desarrollo de Contoso en la unidad de negocio de la cadena de suministro

Contoso necesita compilar una aplicación de línea de negocio y una aplicación orientada al cliente. Ha decidido ejecutar las aplicaciones en Azure. David ha leído el artículo sobre [gobernanza prescriptiva de suscripciones](./azure-scaffold.md) y está listo para implementar las recomendaciones.

## <a name="scenario-1-line-of-business-application"></a>Escenario 1: aplicación de línea de negocio

Contoso está creando un sistema de administración de código fuente (BitBucket) para que puedan utilizarlo desarrolladores de todo el mundo. La aplicación utiliza la infraestructura como servicio (IaaS) para el hospedaje y consta de servidores web y un servidor de bases de datos. Los desarrolladores acceden a los servidores en sus entornos de desarrollo, pero no necesitan entrar en los servidores de Azure. La unidad ETS de Contoso desea permitir que tanto el equipo como el propietario de la aplicación puedan administrar la aplicación. Esta solo está disponible mientras lo esté la red corporativa de Contoso. David debe configurar la suscripción para esta aplicación. La suscripción también hospedará más adelante otro software relacionado con el desarrollador.

### <a name="naming-standards-and-resource-groups"></a>Estándares de nomenclatura y grupos de recursos

David crea una suscripción para admitir las herramientas de desarrollo que son comunes a todas las unidades de negocio. Dave necesita crear nombres descriptivos para la suscripción y los grupos de recursos (de la aplicación y las redes). Por tanto, genera la siguiente suscripción y estos grupos de recursos:

| item | NOMBRE | DESCRIPCIÓN |
| --- | --- | --- |
| Subscription |Contoso ETS DeveloperTools Production |Admite las herramientas de desarrollo comunes. |
| Resource group |bitbucket-prod-rg |Contiene el servidor de aplicaciones web y el de bases de datos. |
| Resource group |corenetworks-prod-rg |Contiene las redes virtuales y la conexión de puerta de enlace de sitio a sitio. |

### <a name="role-based-access-control"></a>Control de acceso basado en rol

Después de crear la suscripción, David quiere asegurarse de que los equipos y propietarios de aplicaciones adecuados pueden acceder a sus recursos. David identifica que cada equipo tiene requisitos diferentes. Por tanto, utiliza los grupos que se han sincronizado del servicio local de Active Directory de Contoso en Azure Active Directory y proporciona el nivel adecuado de acceso a los equipos.

David asigna los siguientes roles a la suscripción:

| Role | Asignado a | DESCRIPCIÓN |
| --- | --- | --- |
| [Propietario](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) |Identificador administrado de la instancia de Active Directory local de Contoso |Este identificador se controla con acceso Just-In-Time (JIT) mediante la herramienta de administración de identidades de Contoso y garantiza que se audite por completo el acceso del propietario de la suscripción |
| [Lector de seguridad](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#security-reader) |Departamento de administración de riesgos y seguridad |Este rol permite a los usuarios ver Azure Security Center y el estado de los recursos |
| [Colaborador de la red](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#network-contributor) |Equipo de red |Este rol permite al equipo de red de Contoso administrar la VPN de sitio a sitio y las redes virtuales |
| *Rol personalizado* |Propietario de la aplicación |David crea un rol que concede la capacidad de modificar recursos en el grupo de recursos. Para más información, consulte [Roles personalizados en RBAC de Azure](https://docs.microsoft.com/azure/role-based-access-control/custom-roles). |

### <a name="policies"></a>Directivas

David tiene los siguientes requisitos para administrar recursos de la suscripción:

- Dado que las herramientas de desarrollo pueden usarla desarrolladores de todo el mundo, no quiere impedir que los usuarios creen recursos en cualquier región. Sin embargo, debe saber dónde se crean los recursos.
- Además, le preocupan los costos. Por lo tanto, quiere impedir que los propietarios de la aplicación creen máquinas virtuales innecesariamente costosas.
- Como esta aplicación la utilizan desarrolladores de muchas unidades de negocio, quiere etiquetar cada recurso con el propietario de la aplicación y la unidad de negocio. Mediante el uso de estas etiquetas, la unidad ETS puede emitir las facturas a los equipos adecuados.

Además, crea las siguientes directivas mediante [Azure Policy](https://docs.microsoft.com/azure/azure-policy/azure-policy-introduction):

| Campo | Efecto | DESCRIPCIÓN |
| --- | --- | --- |
| location |audit |Audita la creación de los recursos en cualquier región. |
| Tipo |deny |Deniega la creación de máquinas virtuales de serie G. |
| etiquetas |deny |Exige la etiqueta de propietario de la aplicación. |
| etiquetas |deny |Exige la etiqueta de centro de costos. |
| etiquetas |append |Anexa el nombre de etiqueta **BusinessUnit** y el valor de etiqueta **ETS** a todos los recursos. |

### <a name="resource-tags"></a>Etiquetas del recurso

David es consciente de que debe tener información específica sobre facturación para identificar el centro de costos para la implementación de BitBucket. Además, quiere conocer todos los recursos que posee ETS.

Para ello, agrega las siguientes [etiquetas](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) a los grupos de recursos y recursos.

| Nombre de etiqueta | Valor de etiqueta |
| --- | --- |
| ApplicationOwner |El nombre de la persona que administra esta aplicación |
| CostCenter |El centro de costos del grupo que paga el consumo de Azure |
| BusinessUnit |**ETS** (la unidad de negocio asociada a la suscripción). |

### <a name="core-network"></a>Red principal

El equipo de administración de riesgos y de seguridad de información de la unidad ETS de Contoso revisa el plan que ha propuesto David para migrar la aplicación a Azure. Desean asegurarse de que no puede accederse a la aplicación a través de Internet. David también tiene aplicaciones de desarrollador que, más adelante, se migrarán a Azure. Estas aplicaciones requieren interfaces públicas. Para cumplir estos requisitos, proporciona redes virtuales externas e internas, y un grupo de seguridad de red para restringir el acceso.

Además, crea estos recursos:

| Tipo de recurso | NOMBRE | DESCRIPCIÓN |
| --- | --- | --- |
| Virtual Network |red virtual interna |Se utiliza con la aplicación de BitBucket y se conecta a través de ExpressRoute a la red corporativa de Contoso. Una subred (`bitbucket`) proporciona a la aplicación con un espacio de direcciones IP específico |
| Virtual Network |red virtual externa |Está disponible para las aplicaciones futuras que requieran puntos de conexión orientados al público |
| Grupo de seguridad de red (NSG) |bitbucket-nsg |Garantiza que se reduzca al máximo la superficie de ataque de esta carga de trabajo permitiendo conexiones solo en el puerto 443 para la subred donde se encuentra la aplicación (`bitbucket`) |

### <a name="resource-locks"></a>Bloqueos de recursos

David identifica que la conectividad de la red corporativa de Contoso a la red virtual interna debe protegerse de cualquier script "rebelde" o eliminación accidental.

Para ello, crea los siguientes [bloqueos de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources):

| Tipo de bloqueo | Recurso | DESCRIPCIÓN |
| --- | --- | --- |
| **CanNotDelete** |red virtual interna |Impide que los usuarios eliminen la red virtual o las subredes, pero no que se agreguen nuevas subredes |

### <a name="azure-automation"></a>Azure Automation

David no tiene que automatizar nada en esta aplicación. Aunque creó una cuenta de Azure Automation, por ahora, no la utilizará.

### <a name="azure-security-center"></a>Azure Security Center

El equipo de administración de servicios de TI de Contoso debe identificar y controlar rápidamente las amenazas. También quiere entender los problemas que existan.

Para cumplir estos requisitos, David habilita [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) y proporciona acceso al rol de administrador de seguridad.

## <a name="scenario-2-customer-facing-app"></a>Escenario 2: aplicación orientada al cliente

Los responsables de la unidad de negocio de la cadena de suministro han identificado diversas oportunidades para aumentar la interacción con los clientes de Contoso mediante el uso de una tarjeta de fidelización. El equipo de Alicia debe crear esta aplicación y decide que Azure aumenta su capacidad de satisfacer las necesidades del negocio. Alicia trabaja con David de la unidad ETS para configurar dos suscripciones con el objetivo de desarrollar y usar esta aplicación.

### <a name="azure-subscriptions"></a>Suscripciones de Azure

David inicia sesión en Azure Enterprise Portal y se percata de que el departamento de la cadena de suministro ya existe. Sin embargo, como este proyecto es el primero de desarrollo del equipo de la cadena de suministro en Azure, David identifica la necesidad de que el equipo de desarrollo de Alicia tenga una nueva cuenta. Por tanto, crea la cuenta I+D para su equipo y concede acceso a Alicia. Alicia inicia sesión mediante el portal de Azure y crea dos suscripciones: una para almacenar los servidores de desarrollo y otra donde se hospedarán los servidores de producción. Además, sigue las normas de nomenclaturas establecidas previamente al crear las siguientes suscripciones:

| Uso de la suscripción | NOMBRE |
| --- | --- |
| Desarrollo |Contoso SupplyChain ResearchDevelopment LoyaltyCard Development |
| Producción |Contoso SupplyChain Operations LoyaltyCard Production |

### <a name="policies"></a>Directivas

David y Alicia analizan la aplicación e identifican que solo la utilizan clientes de la región de Norteamérica. Alicia y su equipo planean utilizar Azure SQL y el entorno de servicios de aplicaciones de Azure para crear la aplicación. Deben crear máquinas virtuales durante el desarrollo. Alicia quiere asegurarse de que sus desarrolladores dispongan de los recursos que necesitan para explorar y examinar problemas sin perjudicar a la unidad ETS.

Para la **suscripción de desarrollo**, crean la siguiente directiva:

| Campo | Efecto | DESCRIPCIÓN |
| --- | --- | --- |
| location |audit |Audita la creación de los recursos en cualquier región. |

No limitan el tipo de SKU que puede crear un usuario durante el desarrollo y no requieren etiquetas para ningún recurso o grupo de recursos.

Para la **suscripción de producción**, crean las siguientes directivas:

| Campo | Efecto | DESCRIPCIÓN |
| --- | --- | --- |
| location |deny |Deniega la creación de cualquier recurso fuera de los centros de datos de Estados Unidos |
| etiquetas |deny |Exige la etiqueta de propietario de la aplicación. |
| etiquetas |deny |Exige la etiqueta de departamento |
| etiquetas |append |Anexa una etiqueta a cada grupo de recursos que indica el entorno de producción |

No limitan el tipo de SKU que puede crear un usuario durante la producción.

### <a name="resource-tags"></a>Etiquetas del recurso

David es consciente de que debe tener información específica con el objetivo de identificar los grupos de negocios adecuados para las tareas de facturación y propiedad. Por ello, define las etiquetas de recurso para los grupos de recursos y recursos.

| Nombre de etiqueta | Valor de etiqueta |
| --- | --- |
| ApplicationOwner |El nombre de la persona que administra esta aplicación |
| department |El centro de costos del grupo que paga el consumo de Azure |
| EnvironmentType |**Production** (aunque el nombre de la suscripción incluya **Production**, esta etiqueta permite facilitar su identificación al buscar recursos en el portal o en la factura) |

### <a name="core-networks"></a>Redes principales

El equipo de administración de riesgos y de seguridad de información de la unidad ETS de Contoso revisa el plan que ha propuesto David para migrar la aplicación a Azure. Quiere asegurarse de que la aplicación de tarjeta de fidelización está aislada y protegida en una red DMZ correctamente. Para cumplir este requisito, Alicia y David crean una red virtual externa y un grupo de seguridad de red para aislar la aplicación de tarjeta de fidelización de la red corporativa de Contoso.

Para la **suscripción de desarrollo**, crean los siguientes recursos:

| Tipo de recurso | NOMBRE | DESCRIPCIÓN |
| --- | --- | --- |
| Virtual Network |red virtual interna |Se utiliza con el entorno de desarrollo de la tarjeta de fidelización de Contoso y se conecta a través de ExpressRoute a la red corporativa de Contoso |

Para la **suscripción de producción**, crean los siguientes recursos:

| Tipo de recurso | NOMBRE | DESCRIPCIÓN |
| --- | --- | --- |
| Virtual Network |red virtual externa |Hospeda la aplicación de tarjeta de fidelización y no está conectada directamente a ExpressRoute de Contoso. El código se envía directamente a través de su sistema de código fuente a los servicios de PaaS. |
| Grupo de seguridad de red (NSG) |loyaltycard-nsg |Garantiza que se reduzca al máximo la superficie de ataque permitiendo solo las conexiones entrantes en el puerto TCP 443. Contoso también está investigando el uso de un firewall de aplicaciones web para agregar más protección. |

### <a name="resource-locks"></a>Bloqueos de recursos

David y Alicia se reúnen y deciden agregar bloqueos de recursos en algunos de los recursos claves del entorno para evitar la eliminación accidental durante una inserción de código malintencionado.

Para ello, crean el bloqueo siguiente:

| Tipo de bloqueo | Recurso | DESCRIPCIÓN |
| --- | --- | --- |
| **CanNotDelete** |red virtual externa |Se utiliza para evitar que los usuarios eliminen la red virtual o las subredes. El bloqueo no impide que se agreguen nuevas subredes |

### <a name="azure-automation"></a>Azure Automation

Alicia y su equipo de desarrollo tienen runbooks de gran tamaño para administrar el entorno de esta aplicación. Los runbooks permiten agregar o eliminar nodos en la aplicación, además de realizar otras tareas de DevOps.

Para usar estos runbooks, habilitan [Automation](https://docs.microsoft.com/azure/automation/automation-intro).

### <a name="azure-security-center"></a>Azure Security Center

El equipo de administración de servicios de TI de Contoso debe identificar y controlar rápidamente las amenazas. También quiere entender los problemas que existan.

Para cumplir estos requisitos, David habilita Azure Security Center. Se asegura de que Azure Security Center esté supervisando los recursos y proporciona acceso a los equipos de DevOps y seguridad.

## <a name="next-steps"></a>Pasos siguientes

- Para ver más recomendaciones sobre cómo crear plantillas de Resource Manager, consulte [Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) (Procedimientos recomendados para crear plantillas de Azure Resource Manager).
