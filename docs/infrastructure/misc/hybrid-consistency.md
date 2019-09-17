---
title: Creación de coherencia en la nube híbrida
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Defina el enfoque para crear la coherencia de la nube híbrida.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/27/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 819d0c058acf48402296bbac8d4cb4837271259e
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70835446"
---
# <a name="create-hybrid-cloud-consistency"></a>Creación de coherencia en la nube híbrida

En este artículo le guiaremos a través de los enfoques de alto nivel para crear una coherencia en la nube híbrida.

Los modelos de implementación híbridos durante la migración pueden reducir el riesgo y contribuir a una transición sin problemas de la infraestructura. Las plataformas en la nube ofrecen el mayor nivel de flexibilidad cuando se trata de procesos de negocios. Muchas organizaciones no tienen claro si deberían trasladarse a la nube. Prefieren mantener el control absoluto sobre los datos más confidenciales. Desafortunadamente, los servidores locales no permiten la misma tasa de innovación que la nube. Las soluciones de nube híbrida ofrecen la velocidad de la innovación en la nube y el control de la administración local.

## <a name="integrate-hybrid-cloud-consistency"></a>Integrar la coherencia en la nube híbrida

El uso de una solución de nube híbrida permite a las organizaciones escalar los recursos informáticos. También elimina la necesidad de realizar grandes gastos de capital para administrar los picos de demanda a corto plazo. Los cambios en su empresa pueden impulsar la necesidad de liberar recursos locales para aplicaciones o datos más confidenciales. Es más fácil, rápido y menos costoso desaprovisionar recursos en la nube. Así, solo debe pagar por aquellos recursos que su organización usa temporalmente, en lugar de tener que comprar y mantener recursos adicionales. Este enfoque reduce la cantidad de equipo que podría permanecer inactivo durante largos períodos de tiempo. La informática en la nube híbrida ofrece todas las ventajas de la informática en la nube (flexibilidad, escalabilidad y rentabilidad) con el menor riesgo posible para los datos.

![Creación de coherencia de la nube híbrida entre identidades, administración, seguridad, datos, desarrollo y DevOps](../../_images/hybrid-consistency.png)
*Figura 1: Creación de coherencia de la nube híbrida entre identidades, administración, seguridad, datos, desarrollo y DevOps*.

Una verdadera solución de nube híbrida debe proporcionar cuatro componentes, cada uno de los cuales aporta ventajas significativas:

- **Identidad común para aplicaciones locales y en la nube**: este componente mejora la productividad del usuario al otorgarle un inicio de sesión único (SSO) para todas sus aplicaciones. También garantiza la coherencia a medida que las aplicaciones y los usuarios cruzan los límites de la red o la nube.
- **Administración y seguridad integradas en toda la nube híbrida**: este componente proporciona una manera coherente de supervisar, administrar y asegurar el entorno, permitiéndole obtener una mayor visibilidad y control.
- **Plataforma de datos coherente para el centro de datos y la nube:** este componente crea una portabilidad de datos y ofrece un acceso continuo a los servicios de datos locales y en la nube, para obtener una visión profunda de todos los orígenes de datos.
- **Desarrollo unificado y DevOps en la nube y centros de datos locales**: este componente permite trasladar las aplicaciones entre los dos entornos según sea necesario. La productividad de los desarrolladores mejora porque ambas ubicaciones tienen ahora el mismo entorno de desarrollo.

Estos son algunos ejemplos de estos componentes desde una perspectiva de Azure:

- Azure Active Directory (Azure AD) funciona con una instancia local de Active Directory para proporcionar una identidad común a todos los usuarios. El inicio de sesión único local y en la nube facilita a los usuarios el acceso seguro a las aplicaciones y a los activos que necesiten. Los administradores pueden administrar controles de seguridad y gobernanza, y también tienen la flexibilidad de ajustar los permisos sin que ello afecte a la experiencia del usuario.
- Azure proporciona servicios de administración y seguridad integrados para la infraestructura en la nube y en el entorno local. Estos servicios incluyen un conjunto integrado de herramientas que se usan para supervisar, configurar y proteger nubes híbridas. Este enfoque integral de administración aborda específicamente los desafíos del mundo real a los que deben enfrentarse las organizaciones que consideran tener una solución de nube híbrida.
- La nube híbrida de Azure proporciona herramientas comunes que garantizan el acceso seguro a todos los datos, de manera transparente y eficaz. Igualmente, los servicios de datos de Azure se combinan con Microsoft SQL Server para crear una plataforma de datos coherente. Un modelo de nube híbrida coherente permite a los usuarios trabajar con datos analíticos y operativos. Los mismos servicios se proporcionan de forma local y en la nube para el almacenamiento de datos, el análisis de datos y la visualización de datos.
- Los servicios en la nube de Azure, combinados con la instancia local de Azure Stack, proporcionan un desarrollo unificado y DevOps. La coherencia local y en la nube significa que su equipo de DevOps puede compilar aplicaciones que se ejecuten en cualquier entorno y que pueden implementarse fácilmente en la ubicación correcta. También puede reutilizar las plantillas en la solución híbrida, lo que puede simplificar aún más los procesos de DevOps.

## <a name="azure-stack-in-a-hybrid-cloud-environment"></a>Azure Stack en un entorno de nube híbrida

Azure Stack es una solución de nube híbrida que permite a las organizaciones ejecutar servicios de Azure coherentes en su centro de datos. Proporciona una experiencia simplificada de desarrollo, administración y seguridad coherente con los servicios en la nube pública de Azure. Azure Stack es una extensión de Azure. Puede usarlo para ejecutar servicios de Azure desde sus entornos locales y, después, pasar a la nube de Azure si es necesario.

Con Azure Stack, puede implementar y usar tanto IaaS como PaaS mediante las mismas herramientas; además, ofrece la misma experiencia que la nube pública de Azure. La administración de Azure Stack, ya sea a través del portal de la interfaz de usuario web o a través de PowerShell, tiene una apariencia coherente con Azure tanto para los administradores de TI como para los usuarios finales.

Azure y Azure Stack abren nuevos casos de uso híbridos para aplicaciones de línea de negocio que están orientadas al cliente e internas:

- **Soluciones perimetrales y desconectadas**. Para abordar los requisitos de latencia y conectividad, los clientes pueden procesar los datos localmente en Azure Stack y, después, agregarlos a Azure para realizar análisis adicionales. Pueden usar la lógica de aplicación común en ambos. Muchos clientes están interesados en este escenario de vanguardia de diferentes maneras, como pisos de fábricas, cruceros y minas.
- **Aplicaciones en la nube que cumplen diversas regulaciones**. Los clientes pueden desarrollar e implementar aplicaciones en Azure, ya que cuentan con total flexibilidad de implementación en el entorno local de Azure Stack para satisfacer sus requisitos de cumplimiento normativo o de directivas. No es necesario realizar ningún cambio de código. Algunos ejemplos de aplicación son la auditoría global, los informes financieros, las operaciones de cambio de divisas, los juegos en línea y los informes de gastos. A veces los clientes buscan implementar diferentes instancias de la misma aplicación en Azure o Azure Stack, en función de los requisitos empresariales y técnicos. Si bien Azure cumple con la mayoría de los requisitos, Azure Stack complementa el enfoque de implementación allí donde es necesario.
- **Modelo de aplicación en la nube en el entorno local**. Los clientes pueden usar las arquitecturas de servicios web, contenedores, sin servidor y microservicio de Azure para actualizar y ampliar las aplicaciones existentes o crear otras nuevas. Puede usar un proceso de DevOps coherente a través de Azure en la nube, y mediante Azure Stack en un entorno local. Existe un creciente interés en la modernización de aplicaciones, incluso para las aplicaciones críticas fundamentales.

Azure Stack se ofrece a través de dos opciones de implementación:

- **Sistemas integrados de Azure Stack**: los sistemas integrados de Azure Stack se ofrecen a través de Microsoft y asociados de hardware para crear una solución que proporciona una oportunidad de innovación dirigida a la nube y que a su vez está equilibrada con una administración sencilla. Como Azure Stack se suministra como un sistema integrado de hardware y software, se consigue flexibilidad y control, al mismo tiempo que se adopta la innovación de la nube. Los sistemas integrados de Azure Stack tienen un tamaño de entre 4 y 12 nodos. Son compatibles conjuntamente con el asociado de hardware y Microsoft. Use los sistemas integrados de Azure Stack para permitir nuevos escenarios para las cargas de trabajo de producción.
- **Kit de desarrollo de Azure Stack**: El Kit de desarrollo de Microsoft Azure Stack es una implementación de un único nodo de Azure Stack. Puede usarlo para evaluar y obtener información sobre Azure Stack. También puede usar el kit como entorno de desarrollo, donde puede desarrollar elementos mediante las API y las herramientas que sean coherentes con Azure. El Kit de desarrollo de Azure Stack no está pensado para usarlo como entorno de producción.

## <a name="azure-stack-one-cloud-ecosystem"></a>Ecosistema de Azure Stack One Cloud

Puede acelerar las iniciativas de Azure Stack si usa el ecosistema de Azure al completo:

- Azure garantiza que la mayoría de las aplicaciones y servicios certificados para Azure funcionarán en Azure Stack. Varios fabricantes de software independientes están extendiendo sus soluciones a Azure Stack. Algunos de estos fabricantes son Bitnami, Docker, Kemp Technologies, Pivotal Cloud Foundry, Red Hat Enterprise Linux y SUSE Linux.
- Puede configurar Azure Stack para que funcione como un servicio totalmente administrado. Varios asociados tendrán ofertas de servicios administrados en Azure y Azure Stack en breve. Entre estos asociados se incluyen Tieto, Yourhosting, Revera, Pulsant, y NTT. Estos asociados ofrecen servicios administrados para Azure a través del programa de Proveedor de soluciones en la nube (CSP). Están ampliando sus ofertas para incluir soluciones híbridas.
- Un ejemplo de solución de nube híbrida completa y totalmente administrada es Avanade, con una oferta todo en uno. Incluye servicios de transformación en la nube, software, infraestructura, instalación y configuración y servicios administrados en curso. De esta forma, los clientes pueden consumir Azure Stack igual que hacen con Azure en la actualidad.
- Con los proveedores, es más fácil acelerar las iniciativas de modernización de aplicaciones mediante la creación de soluciones integrales de Azure para los clientes. Estos le ofrecen una serie detallada de habilidades de Azure, el dominio y conocimiento del sector y la experiencia en procesos (por ejemplo, DevOps). Cada nube de Azure Stack es una oportunidad para que un proveedor diseñe la solución y pueda influir en la implementación del sistema. También puede personalizar las capacidades incluidas y ofrecer actividades operativas. Algunos ejemplos de proveedores son Avanade, DXC, Dell EMC Services, InFront Consulting Group, HPE Pointnext y PwC (anteriormente PricewaterhouseCoopers).
