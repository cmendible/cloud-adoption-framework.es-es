---
title: Mejora de la materia sobre la base de referencia de la seguridad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Mejora de la materia sobre la base de referencia de la seguridad
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 8ad6b84a67bb81459fbd78ebe413a93c1a58e099
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031229"
---
# <a name="security-baseline-discipline-improvement"></a>Mejora de la materia sobre la base de referencia de la seguridad

La materia de base de referencia de la seguridad se centra en formas de establecer directivas que protegen la red, los recursos y, lo que es más importante, los datos que residirán en una solución del proveedor de nube. Dentro de las cinco materias de gobernanza de la nube, la base de referencia de la seguridad incluye la clasificación del patrimonio digital y los datos. También incluye documentación de estrategias de mitigación, tolerancia empresarial y riesgos que se asocian a la seguridad de los datos, los recursos y la red. Desde una perspectiva técnica, esto también incluye la participación en decisiones sobre el [cifrado](../../decision-guides/encryption/index.md), los [requisitos de red](../../decision-guides/software-defined-network/index.md), las [estrategias de identidad híbrida](../../decision-guides/identity/index.md) y los [procesos](./compliance-processes.md) utilizados para desarrollar las directivas de la base de referencia de la seguridad.

En este artículo se destacan algunas de las posibles tareas en las que su empresa puede participar para desarrollar y mejorar la materia sobre la base de referencia de la seguridad. Estas tareas se dividen en las fases de planeamiento, compilación, adopción y funcionamiento de la implementación de una solución de nube que, posteriormente, se iteran para permitir el desarrollo de un [enfoque incremental a la gobernanza de la nube](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Cuatro fases de adopción](../../_images/govern/adoption-phases.png)

*Figura 1: Fases de adopción del enfoque incremental para la gobernanza de la nube.*

Es imposible recopilar en un solo documento los requisitos de todas las empresas. Por lo tanto, en este artículo se detallan ejemplos de actividades mínimas y potenciales sugeridas para cada fase del proceso de desarrollo de la gobernanza. El objetivo inicial de estas actividades es ayudarle a crear un [producto viable mínimo de directiva](../guides/index.md#an-incremental-approach-to-cloud-governance) y establecer un marco para la mejora incremental de las directivas. El equipo de gobernanza de la nube deberá decidir cuánto invertir en estas actividades para mejorar las funcionalidades de gobernanza de la base de referencia de la seguridad.

> [!CAUTION]
> Ni las actividades mínimas ni las posibles que se describen en este artículo están en línea con directivas corporativas específicas ni con requisitos de cumplimiento de terceros. Esta guía está diseñada como ayuda para facilitar las conversaciones que darán lugar a la alineación de los requisitos con un modelo de gobernanza de la nube.

## <a name="planning-and-readiness"></a>Planeamiento y preparación

Esta fase del desarrollo de la gobernanza permite salvar las diferencias entre los resultados empresariales y unas estrategias accionables. Durante este proceso, el equipo directivo define métricas específicas, las asigna al patrimonio digital y empieza a planear el esfuerzo global de migración.

**Actividades mínimas sugeridas:**

- Evalúe las opciones que tiene para la [cadena de herramientas de la base de referencia de la seguridad](./toolchain.md).
- Elabore un borrador con las directrices de arquitectura y distribúyalo a las principales partes interesadas.
- Eduque e implique a las personas y equipos a los que afectará el desarrollo de las directrices de arquitectura.
- Agregue tareas de seguridad priorizadas a su trabajo pendiente de migración.

**Posible actividades:**

- Defina un esquema de clasificación de los datos.
- Realice un proceso de planeamiento del patrimonio digital para inventariar los recursos de TI actuales que dan servicio a los procesos empresariales y respaldan las operaciones.
- Lleve a cabo una [revisión de la directiva](../../govern/policy-compliance/cloud-policy-review.md) para comenzar el proceso de modernización de las directivas de seguridad de TI corporativas existentes, y defina las directivas de producto mínimo viable para abordar los riesgos conocidos.
- Revise las directrices de seguridad de la plataforma de nube. En el caso de Azure, se encuentran en la [plataforma de confianza de servicios de Microsoft](https://www.microsoft.com/trustcenter/stp/default.aspx).
- Determine si la directiva de base de referencia de la seguridad incluye un [ciclo de vida de desarrollo de la seguridad](https://www.microsoft.com/securityengineering/sdl).
- Evalúe la red, los datos y los riesgos empresariales relacionadas con los recursos, utilizando para ello de una a tres de las próximas versiones, y evalúe la tolerancia de su organización a esos riesgos.
- Revise el informe de Microsoft sobre las [principales tendencias en ciberseguridad](https://www.microsoft.com/security/operations/security-intelligence-report) para obtener información general sobre el panorama actual de la seguridad.
- Considere la posibilidad de incorporar un rol de [DevOps de seguridad](https://www.microsoft.com/en-us/securityengineering/devsecops) en su organización.

<!-- "en-us" location is required for the URL above. -->

## <a name="build-and-predeployment"></a>Compilación y fase anterior a la implementación

Se necesitan varios requisitos técnicos y no técnicos para migrar correctamente un entorno. Este proceso se centra en las decisiones, la preparación y la infraestructura principal que precede a una migración.

**Actividades mínimas sugeridas:**

- Implemente su [cadena de herramientas de la base de referencia de la seguridad](./toolchain.md) agregándola en una fase anterior a la implementación.
- Actualice el documento de directrices de arquitectura y distribúyalo a las principales partes interesadas.
- Implemente tareas de seguridad en su trabajo pendiente de migración priorizado.
- Desarrolle materiales y documentación educativos, comunicaciones de concienciación, incentivos y otros programas para ayudar a impulsar la adopción por parte de los usuarios.

**Posible actividades:**

- Determine la estrategia de [cifrado](../../decision-guides/encryption/index.md) de la organización para los datos hospedados en la nube.
- Evalúe la estrategia de [identidad](../../decision-guides/identity/index.md) de la implementación en la nube. Determine cómo la solución de identidad basada en la nube coexistirá o se integrará con los proveedores de identidades del entorno local.
- Determine las directivas de límites de red para el diseño de sus [redes definidas por software (SDN)](../../decision-guides/software-defined-network/index.md), para poder garantizar funcionalidades de red virtualizada seguras.
- Evalúe las directivas de [acceso con privilegios mínimos](https://docs.microsoft.com/azure/active-directory/users-groups-roles/roles-delegate-by-task) de su organización y use roles basados en tareas para proporcionar acceso a recursos específicos.
- Aplique mecanismos de seguridad y supervisión a todos los servicios y máquinas virtuales en la nube.
- Automatice las [directivas de seguridad](../../decision-guides/policy-enforcement/index.md) siempre que sea posible.
- Revise su directiva de base de referencia de la seguridad y determine si necesita modificar los planes de acuerdo con la guía de procedimientos recomendados, por ejemplo, los descritos en [Ciclo de vida de desarrollo de seguridad](https://www.microsoft.com/securityengineering/sdl).

## <a name="adopt-and-migrate"></a>Adopción y migración

La migración es un proceso incremental que se centra en el traslado, las pruebas y la adopción de las aplicaciones o cargas de trabajo de un patrimonio digital existente.

**Actividades mínimas sugeridas:**

- Migre la [cadena de herramientas de su base de referencia de la seguridad](./toolchain.md) de la fase anterior a la implementación a la fase de producción.
- Actualice el documento de directrices de arquitectura y distribúyalo a las principales partes interesadas.
- Desarrolle materiales y documentación educativos, comunicaciones de reconocimiento, incentivos y otros programas para ayudar a impulsar la adopción del usuario.

**Posible actividades:**

- Revise la información más reciente sobre amenazas y la base de referencia de la seguridad para identificar nuevos riesgos empresariales.
- Calibre qué tolerancia tiene su organización para controlar los nuevos riesgos para la seguridad que pudieran surgir.
- Identifique las desviaciones de la directiva y aplique correcciones.
- Ajuste la automatización del control de acceso y la seguridad para garantizar el máximo cumplimiento de la directiva.
- Compruebe que los procedimientos recomendados que se definieron durante las fases de compilación y anterior a la implementación se ejecutan correctamente.
- Revise las directivas de acceso con privilegios mínimos y ajuste los controles de acceso para maximizar la seguridad.
- Pruebe la cadena de herramientas de su base de referencia de la seguridad con sus cargas de trabajo para identificar y resolver las vulnerabilidades.

## <a name="operate-and-post-implementation"></a>Funcionamiento y fase posterior a la implementación

Una vez completada la transformación, la gobernanza y las operaciones deben estar disponibles durante el ciclo de vida natural de una aplicación o carga de trabajo. Esta fase de desarrollo de la gobernanza se centra en las actividades que surgen habitualmente cuando la solución ya está implementada y el ciclo de transformación comienza a estabilizarse.

**Actividades mínimas sugeridas:**

- Valide y ajuste la [cadena de herramientas de su base de referencia de la seguridad](./toolchain.md).
- Personalice las notificaciones y los informes para que le avisen de posibles problemas para la seguridad.
- Refine las directrices de arquitectura para guiar los procesos de adopción futuros.
- Informe a los equipos afectados y ofrézcales cursos de forma periódica para garantizar el cumplimiento de las directrices de la arquitectura.

**Posible actividades:**

- Identifique los patrones y el comportamientos de sus cargas de trabajo y configure herramientas de supervisión e informes para que identifiquen y le notifiquen de actividades, accesos o uso de recursos anómalos.
- Actualice continuamente las directivas de supervisión e informes para detectar los ataques y las vulnerabilidades más recientes.
- Ponga en marcha procedimientos para detener rápidamente el acceso no autorizado y deshabilitar los recursos que un atacante haya podido poner en riesgo.
- Revise con regularidad los procedimientos recomendados de seguridad más recientes y aplique las recomendaciones a su directiva de seguridad y a sus funcionalidades de automatización y supervisión siempre que sea posible.

## <a name="next-steps"></a>Pasos siguientes

Ahora que comprende el concepto de gobernanza de la seguridad en la nube, vamos a ver [qué procedimientos recomendados y guías para la seguridad ofrece Microsoft](./azure-security-guidance.md) para Azure.

> [!div class="nextstepaction"]
> [Más información sobre las guías de seguridad para Azure](./azure-security-guidance.md)
> [Introducción a la seguridad de Azure](https://docs.microsoft.com/azure/security/azure-security)
> [Más información sobre registro, informes y supervisión](../../decision-guides/logging-and-reporting/index.md)
