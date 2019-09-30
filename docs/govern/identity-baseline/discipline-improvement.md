---
title: Mejora de la materia sobre la base de referencia de la identidad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Mejora de la materia sobre la base de referencia de la identidad
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 256242f90e45719994a12cdb209202a18bba830c
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71220491"
---
# <a name="identity-baseline-discipline-improvement"></a>Mejora de la materia sobre la base de referencia de la identidad

Esta materia sobre la base de referencia de la identidad se centra en las maneras de establecer directivas que garanticen la coherencia y continuidad de las identidades de usuario, independientemente del proveedor de servicios en la nube que hospede la aplicación o carga de trabajo. Dentro de las cinco materias de gobernanza de la nube, la base de referencia de la identidad incluye decisiones relacionadas con la [estrategia de identidad híbrida](../../decision-guides/identity/index.md), la evaluación y extensión de los repositorios de identidades, la implementación del inicio de sesión único (mismo inicio de sesión), la auditoría y la supervisión de usos no autorizados o la intervención de actores malintencionados. En algunos casos, también puede implicar decisiones para modernizar, consolidar o integrar varios proveedores de identidades.

En este artículo se destacan algunas tareas potenciales en las que su empresa puede participar para desarrollar y mejorar la materia sobre la base de referencia de la identidad. Estas tareas se dividen en las fases de planeamiento, compilación, adopción y funcionamiento de la implementación de una solución de nube que, posteriormente, se iteran para permitir el desarrollo de un [enfoque incremental a la gobernanza de la nube](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Cuatro fases de adopción](../../_images/govern/adoption-phases.png)

*Figura 1: Fases de adopción del enfoque incremental para la gobernanza de la nube.*

Es imposible recopilar en un solo documento los requisitos de todas las empresas. Por lo tanto, en este artículo se detallan ejemplos de actividades mínimas y potenciales sugeridas para cada fase del proceso de desarrollo de la gobernanza. El objetivo inicial de estas actividades es ayudarle a crear un [producto viable mínimo de directiva](../guides/index.md#an-incremental-approach-to-cloud-governance) y establecer un marco para la mejora incremental de las directivas. El equipo de gobernanza de la nube deberá decidir cuánto invertir en estas actividades para mejorar las funcionalidades de gobernanza de la base de referencia de identidad.

> [!CAUTION]
> Ni las actividades mínimas ni las posibles que se describen en este artículo están en línea con directivas corporativas específicas ni con requisitos de cumplimiento de terceros. Esta guía está diseñada como ayuda para facilitar las conversaciones que darán lugar a la alineación de los requisitos con un modelo de gobernanza de la nube.

## <a name="planning-and-readiness"></a>Planeamiento y preparación

Esta fase del desarrollo de la gobernanza permite salvar las diferencias entre los resultados empresariales y unas estrategias accionables. Durante este proceso, el equipo directivo define métricas específicas, las asigna al patrimonio digital y empieza a planear el esfuerzo global de migración.

**Actividades mínimas sugeridas:**

- Evalúe las opciones de su [cadena de herramientas de identidad](./toolchain.md) e implemente una estrategia híbrida que sea adecuada para su organización.
- Desarrolle un borrador de las directrices de arquitectura y distribúyalo a las partes interesadas clave.
- Eduque e implique a las personas y equipos afectados por el desarrollo de las directrices de arquitectura.

**Actividades potenciales:**

- Defina los roles y asignaciones que gobernarán la administración de la identidad y el acceso en la nube.
- Defina los grupos locales y asígnelos a los roles correspondientes basados en la nube.
- Proveedores de identidades de inventario (incluidas las identidades controladas por bases de datos que utilizan las aplicaciones personalizadas).
- Consolide e integre a los proveedores de identidades en los que existe una duplicación para simplificar la solución global de identidad y reducir el riesgo.
- Evalúe la compatibilidad híbrida de los proveedores de identidades existentes.
- Para aquellos proveedores de identidades que no presentan esta compatibilidad, evalúe las opciones de consolidación o reemplazo.

## <a name="build-and-predeployment"></a>Compilación y fase anterior a la implementación

Se necesitan varios requisitos técnicos y no técnicos para migrar correctamente un entorno. Este proceso se centra en las decisiones, la preparación y la infraestructura principal que precede a una migración.

**Actividades mínimas sugeridas:**

- Considere la posibilidad de realizar una prueba piloto antes de implementar la [cadena de herramientas de identidad](./toolchain.md), para asegurarse de que esta simplifica la experiencia del usuario al máximo.
- Aplique la información obtenida de estas pruebas piloto en la fase anterior a la implementación. Repita las pruebas hasta que los resultados sean aceptables.
- Actualice el documento de directrices de arquitectura para que incluya los planes de implementación y adopción por parte del usuario, y distribúyalo a las partes interesadas clave.
- Evalúe la posibilidad de establecer un programa para usuarios pioneros y extiéndalo a un número limitado de usuarios.
- A continuación, eduque a los usuarios y equipos a los que más afecten las directrices de la arquitectura.

**Actividades potenciales:**

- Evalúe la arquitectura lógica y física y determine una [estrategia de identidad híbrida](../../decision-guides/identity/index.md).
- Asigne directivas de administración de acceso de las identidades como, por ejemplo, asignaciones de id. de inicio de sesión, y elija el método de autenticación adecuado para Azure AD.
  - Si es federado, habilite restricciones de inquilino para las cuentas administrativas.
- Integre los directorios locales y en la nube.
- Considere el uso de los siguientes modelos de acceso:
  - Modelo de [acceso con privilegios mínimos](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models).
  - Modelo de acceso de [base de referencia de identidad con privilegios](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure).
- Complete todos los detalles previos a la integración y repase los [procedimientos recomendados de identidad](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices).
  - Habilite una sola identidad, un inicio de sesión único (SSO) o un SSO de conexión directa.
  - Configure la autenticación multifactor para los administradores
  - Consolide o integre los proveedores de identidades, cuando sea necesario.
  - Implemente las herramientas necesarias para centralizar la administración de identidades.
  - Habilite el acceso Just-In-Time (JIT) y las alertas de cambio de rol.
  - Realice un análisis de riesgos de las actividades de administración principales para la asignación a roles integrados.
  - Considere la posibilidad de realizar un lanzamiento actualizado de una autenticación más segura para todos los usuarios.
  - Habilite Privileged Identity Management (PIM) para JIT (mediante una activación limitada en el tiempo) para los roles administrativos adicionales.
  - Separe las cuentas de usuarios de las cuentas de Administrador global (para asegurarse de que los administradores no abren de forma involuntaria correos electrónicos ni ejecutan programas asociados a sus cuentas de Administrador global).

## <a name="adopt-and-migrate"></a>Adopción y migración

La migración es un proceso incremental que se centra en el traslado, las pruebas y la adopción de las aplicaciones o cargas de trabajo de un patrimonio digital existente.

**Actividades mínimas sugeridas:**

- Migre la [cadena de herramientas de identidad](./toolchain.md) desde el entorno de desarrollo al de producción.
- Actualice el documento de las directrices de arquitectura y distribúyalo a las partes interesadas clave.
- Desarrolle materiales y documentación educativos, comunicaciones de reconocimiento, incentivos y otros programas para ayudar a impulsar la adopción del usuario.

**Posible actividades:**

- Compruebe que los procedimientos recomendados que se definieron durante las fases anteriores a la implementación de la compilación se ejecutan correctamente.
- Compruebe y refine la [estrategia de identidad híbrida](../../decision-guides/identity/index.md).
- Cerciórese de que todas las aplicaciones o cargas de trabajo siguen alineadas con la estrategia de identidad antes de la publicación.
- Compruebe que el inicio de sesión único (SSO) y el SSO de conexión directa funcionan según lo previsto en las aplicaciones.
- Reduzca el número de almacenes de identidades alternativos o elimine algunos de ellos.
- Examine la necesidad de almacenes de identidades en aplicaciones o en bases de datos. Las identidades que se encuentran fuera de un proveedor de identidades adecuado (propias o de terceros) pueden suponer un riesgo para la aplicación y para los usuarios.
- Habilite el acceso condicional para las [aplicaciones federadas locales](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup).
- Distribuya la identidad entre las regiones globales en varios centros con sincronización entre regiones.
- Establezca la federación central del control de acceso basado en rol (RBAC).

## <a name="operate-and-post-implementation"></a>Funcionamiento y fase posterior a la implementación

Una vez completada la transformación, la gobernanza y las operaciones deben estar disponibles durante el ciclo de vida natural de una aplicación o carga de trabajo. Esta fase de desarrollo de la gobernanza se centra en las actividades que surgen habitualmente cuando la solución ya está implementada y el ciclo de transformación comienza a estabilizarse.

**Actividades mínimas sugeridas:**

- Personalice la [cadena de herramientas de la base de referencia de identidad](./toolchain.md) según los cambios en las necesidades de identidades de la organización.
- Automatice notificaciones e informes para que le avisen de posibles amenazas malintencionadas.
- Supervise e informe sobre el uso del sistema y el progreso del proceso de adopción por parte del usuario.
- Informe sobre las métricas posteriores a la implementación y distribuya a las partes interesadas.
- Refine las directrices de arquitectura para guiar los procesos de adopción futuros.
- Comunique y eduque constantemente a los equipos implicados de forma periódica para garantizar el cumplimiento continuo de las directrices de arquitectura.

**Actividades potenciales:**

- Realice auditorías periódicas de las directivas de identidad y de los procedimientos de cumplimiento.
- Asegúrese de que las cuentas de usuario confidenciales (CEO, CFO, VP, etc.) estén siempre habilitadas para la autenticación multifactor y la detección de inicios de sesión anómalos.
- Examine en busca de actores malintencionados y vulneraciones de seguridad de los datos de forma periódica, especialmente aquellas relacionadas con los fraudes de identidad como, por ejemplo, posibles apropiaciones de cuentas de administrador.
- Configure una herramienta de supervisión e informes.
- Considere la posibilidad de una integración más estrecha con los sistemas de seguridad y prevención de fraudes.
- Revise con regularidad los derechos de acceso para los usuarios o roles con privilegios elevados.
  - Identifique a todos aquellos usuarios que sean aptos para activar sus privilegios administrativos.
- Revise los procesos de incorporación, baja y actualización de credenciales.
- Investigue la posibilidad de aumentar los niveles de automatización y comunicación entre los módulos de administración de identidad y acceso (IAM).
- Considere la posibilidad de implementar un enfoque de desarrollo, seguridad y operaciones (DevSecOps).
- Lleve a cabo un análisis de impacto para medir los resultados de costos, seguridad y adopción por parte del usuario.
- Genere periódicamente un informe de impacto que muestre los cambios en las métricas que crea el sistema y haga una estimación del impacto empresarial de la [estrategia de identidad híbrida](../../decision-guides/identity/index.md).
- Establezca la supervisión integrada que recomienda [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro).

## <a name="next-steps"></a>Pasos siguientes

Ahora que conoce el concepto de gobernanza de identidades en la nube, examine la [cadena de herramientas de la base de referencia de identidad](./toolchain.md) para identificar las herramientas y características de Azure que necesitará al desarrollar la materia sobre la base de referencia de la identidad en la plataforma Azure.

> [!div class="nextstepaction"]
> [Cadena de herramientas de la línea de base de identidad para Azure](./toolchain.md)
