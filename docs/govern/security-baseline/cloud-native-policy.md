---
title: Directivas de línea de base de seguridad nativas en la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Directiva de base de referencia de seguridad nativa para la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: aef22e31d632a585e59dd946c5c0ef71c13d46de
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032006"
---
# <a name="cloud-native-security-baseline-policy"></a>Directivas de línea de base de seguridad nativas en la nube

La [base de referencia de seguridad](./index.md) es una de las [cinco materias de gobernanza en la nube](../governance-disciplines.md). Esta materia se centra en temas de seguridad generales que incluyen la protección de la red, los recursos digitales, los datos, etc. Como se ha indicado en la [guía de revisión de directivas](../policy-compliance/cloud-policy-review.md), el Marco de adopción de la nube incluye tres niveles de **directivas de ejemplo**: nativa en la nube, enterprise y conforme con los principios de diseño de la nube para cada una de las materias. En este artículo se trata la directiva de ejemplo nativa en la nube para la materia de línea de base de seguridad.

> [!NOTE]
> Microsoft no es quien debe dictar las directivas corporativas o de TI. Este artículo está pensado para ayudarle a prepararse para una revisión de directivas interna. Se supone que este ejemplo de directiva se ampliará, validará y probará con sus directivas corporativas antes de intentar utilizarla. El uso de este ejemplo de directiva tal y como está, no es recomendable.

## <a name="policy-alignment"></a>Alineación de la directiva

Esta directiva de ejemplo resume un escenario nativo en la nube, lo cual significa que las herramientas y plataformas que proporciona Azure son suficientes para administrar los riesgos empresariales que conlleva una implementación. En tal escenario, se supone que una configuración sencilla de los servicios predeterminados de Azure ofrece suficiente protección a los recursos.

## <a name="cloud-security-and-compliance"></a>Seguridad en la nube y cumplimiento

La seguridad está integrada en todos los aspectos de Azure y le ofrece unas ventajas exclusivas que se derivan de una inteligencia global de seguridad, unos sofisticados controles orientados al cliente y una infraestructura segura reforzada. Esta potente combinación le ayuda a proteger sus datos y aplicaciones, viene en ayuda de sus esfuerzos en cumplimiento normativo y proporciona una seguridad rentable para organizaciones de todos los tamaños. Este enfoque permite crear un sólido punto de partida para cualquier directiva de seguridad, pero no invalida la necesidad de seguir unos procedimientos de seguridad igualmente potentes en relación con los servicios de seguridad que se usan.

### <a name="built-in-security-controls"></a>Controles de seguridad integrados

Es difícil de mantener una infraestructura de alta seguridad cuando los controles de seguridad no son intuitivos y deben configurarse por separado. Azure incluye controles de seguridad integrados en una variedad de servicios que le ayuda a proteger datos y cargas de trabajo de manera rápida, y a administrar el riesgo en los entornos híbridos. Las soluciones de asociados integradas permiten también trasladar fácilmente a la nube los elementos de protección existentes.

### <a name="cloud-native-identity-policies"></a>Directivas de identidad nativas en la nube

La identidad se está convirtiendo en el nuevo plano de control límite de la seguridad, asumiendo ese papel desde la perspectiva tradicional centrada en la red. Los perímetros de red se han vuelto cada vez más porosos y la defensa del perímetro ya no es tan eficaz como lo era antes de la aparición de las características BYOD y las aplicaciones en la nube. La administración de identidades y el control de acceso de Azure permiten un acceso seguro e ininterrumpido a todas las aplicaciones.

Una directiva de ejemplo nativa en la nube para la identidad en directorios en la nube y locales podría incluir requisitos como los siguientes:

- Acceso autorizado a recursos con control de acceso basado en rol (RBAC), autenticación multifactor e inicio de sesión único (SSO).
- Mitigación rápida de identidades de usuario sospechosas.
- Acceso Just-In-Time (JIT) suficiente que se concede tarea por tarea para limitar la exposición de credenciales de administrador con demasiados privilegios.
- Identidad de usuario extendida y acceso a las directivas en varios entornos mediante Azure Active Directory.

Aunque es importante comprender la [base de referencia de identidad](../identity-baseline/index.md) en el contexto de la base de referencia de seguridad, las [cinco materias sobre la gobernanza de la nube](../index.md) consideran la [base de referencia de la identidad](../identity-baseline/index.md) como una materia propia, independiente de la base de referencia de la seguridad.

### <a name="network-access-policies"></a>Directivas de acceso de red

El control de las redes incluye la configuración, administración y protección de los elementos de la red como, por ejemplo, las redes virtuales, el equilibrio de carga, los DNS y las puertas de enlace. Los controles proporcionan a los servicios un medio para comunicarse e interoperar. Azure incluye una sólida y segura infraestructura de red que respalda sus requisitos de conectividad de aplicaciones y servicios. La conectividad de red es posible entre recursos ubicados en Azure, entre recursos locales y hospedados en Azure y entre Internet y Azure.

Una directiva nativa en la nube para los controles de red puede incluir requisitos como los siguientes:

- Las conexiones híbridas a recursos locales (aunque técnicamente posibles en Azure) podrían no estar permitidas en una directiva nativa en la nube. Si se comprueba la necesidad de una conexión híbrida, puede que un ejemplo de directiva de seguridad Enterprise más sólida resulte más adecuada.
- Los usuarios pueden establecer conexiones seguras con Azure y dentro de este mediante redes virtuales y grupos de seguridad de red.
- Windows Azure Firewall nativo protege los hosts de tráfico malintencionado limitando el acceso a los puertos. Un buen ejemplo de esta directiva es un requisito de bloquear (o no habilitar) el tráfico directo a una máquina virtual a través del puerto 3389 de RDP - TCP/UDP.
- Servicios como el firewall de aplicaciones web (WAF) Azure Application Gateway y Azure DDoS Protection protegen las aplicaciones y garantizan la disponibilidad de las máquinas virtuales que se ejecutan en Azure. No se deberían deshabilitar estas características ni realizar un uso indebido de ellas.

### <a name="data-protection"></a>Protección de datos

Uno de los elementos clave para la protección de datos en la nube consiste en tener en cuenta los posibles estados en que se pueden producir datos y qué controles hay disponibles para cada estado. Como parte de los procedimientos recomendados de cifrado y seguridad de datos en Azure, se ofrecen recomendaciones centradas en los estados de datos siguientes:

- Los controles de cifrado de datos están integrados en los servicios, desde Virtual Machines a Storage y SQL Database.
- A medida que se trasladan los datos entre nubes y clientes, estos se pueden proteger mediante protocolos de cifrado estándar.
- Azure Key Vault permite a los usuarios proteger y controlar claves criptográficas y otros secretos usados por aplicaciones y servicios en la nube.
- Azure Information Protection le ayudará a clasificar, etiquetar y proteger la información confidencial en las aplicaciones.

Aunque estas características están integradas en Azure, cada una de ellas requiere configuración y esto podría aumentar los costos. Se recomienda la alineación de cada característica nativa en la nube con una [estrategia de clasificación de datos](../policy-compliance/data-classification.md).

### <a name="security-monitoring"></a>Supervisión de la seguridad

La supervisión de seguridad es una estrategia proactiva que audita los recursos a fin de identificar los sistemas que no cumplen con los estándares o los procedimientos recomendados de la organización. Azure Security Center proporciona una base de referencia unificada de la seguridad y protección avanzada contra amenazas para cargas de trabajo en la nube híbrida. Con Security Center, puede aplicar directivas de seguridad en las cargas de trabajo, limitar la exposición a amenazas y detectar y responder a los ataques. Esto incluye lo siguiente:

- Vista unificada de la seguridad en todas las cargas de trabajo locales y en la nube con Azure Security Center.
- Evaluaciones de seguridad y supervisión continuas para garantizar el cumplimiento y corregir las vulnerabilidades.
- Herramientas interactivas e inteligencia de amenazas contextual para una investigación optimizada.
- Registro completo e integración con la información de seguridad existente.

### <a name="extending-cloud-native-policies"></a>Extensión de las directivas nativas en la nube

El uso de la nube puede reducir en parte la carga de seguridad. Microsoft proporciona seguridad física para los centros de datos de Azure y ayuda a proteger la plataforma de nube frente a amenazas como un ataque de denegación de servicio distribuido. Dado que Microsoft tiene miles de especialistas en ciberseguridad que trabajan en ella a diario, los recursos para detectar, evitar o mitigar los ciberataques son considerables. De hecho, aunque en el pasado las organizaciones han estado preocupadas por la seguridad de la nube, la mayoría ahora comprende que el nivel de inversión en personal e infraestructura especializada realizado por proveedores como Microsoft convierte a la nube en un entorno más seguro que la mayoría de los centros de datos locales.

Pero incluso con esta inversión en una línea de base de seguridad nativa en la nube, se recomienda que cualquier directiva de línea de base de seguridad se extienda a las directivas nativas en la nube predeterminadas. Los siguientes son ejemplos de directivas extendidas que se deben tener en cuenta incluso en un entorno nativo en la nube:

- **Proteger las máquinas virtuales.** La seguridad debería ser la prioridad principal de todas las organizaciones, y lograr que esta sea eficaz requiere varias cosas. Debe evaluar el estado de la seguridad, protegerse contra amenazas de seguridad y, posteriormente, detectar y responder rápidamente a las amenazas que ya se están produciendo.
- **Proteger los contenidos de las máquinas virtuales.** La configuración de copias de seguridad automatizadas regulares es fundamental para protegerse frente a errores del usuario. Sin embargo, esto no es suficiente. También hay que asegurarse de que las copias de seguridad están protegidas frente a ciberataques y que están disponibles para cuando las necesita.
- **Supervisar las máquinas virtuales y las aplicaciones.** Este patrón abarca varias tareas, entre las que se incluye la obtención de información sobre el estado de las máquinas virtuales, la descripción de las interacciones entre ellas y el establecimiento de maneras de supervisar las aplicaciones que estas máquinas virtuales ejecutan. Todas estas tareas son fundamentales para mantener sus aplicaciones en ejecución ininterrumpidamente.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha revisado las directivas de ejemplo de línea de base de seguridad para soluciones nativas en la nube, vuelva a la [guía de revisión de directivas](../policy-compliance/cloud-policy-review.md) y empiece a trabajar en este ejemplo para crear sus propias directivas de adopción de la nube.

> [!div class="nextstepaction"]
> [Cree sus propias directivas mediante la guía de revisión de directivas](../policy-compliance/cloud-policy-review.md)
