---
title: Mejora de la materia de coherencia de recursos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Mejora de la materia de coherencia de recursos
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 84c7a45b52c541ad9efbec4594db022947b3ff40
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223011"
---
# <a name="resource-consistency-discipline-improvement"></a>Mejora de la materia de coherencia de recursos

Esta materia de coherencia de recursos se centra en formas de establecer directivas relacionadas con la administración operativa de un entorno, una aplicación o una carga de trabajo. Dentro de las cinco materias de gobernanza de la nube, la coherencia de los recursos incluye la supervisión del rendimiento de las aplicaciones, las cargas de trabajo y los recursos. También incluye las tareas necesarias para satisfacer las demandas de escala, corregir las infracciones del Acuerdo de Nivel de Servicio (SLA) de rendimiento y evitar de forma proactiva las infracciones del SLA a través de la corrección automatizada.

En este artículo se destacan algunas tareas potenciales en las que su empresa puede participar para desarrollar y mejorar la materia de coherencia de recursos. Estas tareas se dividen en las fases de planeamiento, compilación, adopción y funcionamiento de la implementación de una solución de nube que, posteriormente, se iteran para permitir el desarrollo de un [enfoque incremental a la gobernanza de la nube](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Cuatro fases de adopción](../../_images/govern/adoption-phases.png)

*Figura 1: Fases de adopción del enfoque incremental para la gobernanza de la nube.*

Es imposible recopilar en un solo documento los requisitos de todas las empresas. Por lo tanto, en este artículo se detallan ejemplos de actividades mínimas y potenciales sugeridas para cada fase del proceso de desarrollo de la gobernanza. El objetivo inicial de estas actividades es ayudarle a crear un [producto viable mínimo de directiva](../guides/index.md#an-incremental-approach-to-cloud-governance) y establecer un marco para la mejora incremental de las directivas. El equipo de gobernanza de la nube deberá decidir cuánto se invertirá en estas actividades para mejorar las funcionalidades de gobernanza de coherencia de los recursos.

> [!CAUTION]
> Ni las actividades mínimas ni las posibles que se describen en este artículo están en línea con directivas corporativas específicas ni con requisitos de cumplimiento de terceros. Esta guía está diseñada como ayuda para facilitar las conversaciones que darán lugar a la alineación de los requisitos con un modelo de gobernanza de la nube.

## <a name="planning-and-readiness"></a>Planeamiento y preparación

Esta fase del desarrollo de la gobernanza permite salvar las diferencias entre los resultados empresariales y unas estrategias accionables. Durante este proceso, el equipo directivo define métricas específicas, las asigna al patrimonio digital y empieza a planear el esfuerzo global de migración.

**Actividades mínimas sugeridas:**

- evalúe sus opciones de la [cadena de herramientas de coherencia de recursos](./toolchain.md).
- Conozca los requisitos de licencia para su estrategia en la nube.
- Desarrolle un borrador de las directrices de arquitectura y distribúyalo a las partes interesadas clave.
- Familiarícese con el administrador de recursos que use para implementar, administrar y supervisar todos los recursos para su solución como grupo.
- Eduque e implique a las personas y equipos afectados por el desarrollo de las directrices de arquitectura.
- Agregue tareas de implementación de recursos priorizadas a su trabajo pendiente de migración.

**Posible actividades:**

- trabaje con las partes interesadas de la empresa o con su equipo de estrategia de la nube para conocer el enfoque de cuentas de nube deseado y las prácticas de contabilidad de costos dentro de sus unidades de negocio y su organización como un todo.
- Defina sus requisitos de [supervisión y aplicación de directivas](./compliance-processes.md).
- Examine el valor empresarial y el costo de interrupción para definir los requisitos del Acuerdo de Nivel de Servicio y la directiva de corrección.
- Determine si aplicará una estrategia de gobernanza de [carga de trabajo sencilla](./governance-simple-workload.md) o [varios equipos](./governance-multiple-teams.md) para sus recursos.
- Determine los requisitos de escalabilidad para sus cargas de trabajo planeadas.

## <a name="build-and-predeployment"></a>Compilación y fase anterior a la implementación

Se necesitan varios requisitos técnicos y no técnicos para migrar correctamente un entorno. Este proceso se centra en las decisiones, la preparación y la infraestructura principal que precede a una migración.

**Actividades mínimas sugeridas:**

- Para implementar su [cadena de herramientas de coherencia de los recursos](./toolchain.md), agréguela en una fase anterior a la implementación.
- Actualice el documento de directrices de arquitectura y distribúyalo a las principales partes interesadas.
- Implemente tareas de implementación de recursos en su trabajo pendiente de migración priorizado.
- Desarrolle materiales y documentación educativos, comunicaciones de reconocimiento, incentivos y otros programas para ayudar a impulsar la adopción del usuario.

**Actividades potenciales:**

- decida sobre una [estrategia de diseño de la suscripción](../../decision-guides/subscriptions/index.md), eligiendo los patrones de suscripción que mejor se adapten a las necesidades de su organización y carga de trabajo.
- Use una estrategia de [coherencia de recursos](../../decision-guides/resource-consistency/index.md) para aplicar las instrucciones de arquitectura con el tiempo.
- Implemente los [estándares de nomenclatura y etiquetado de recursos](../../decision-guides/resource-tagging/index.md) para que sus recursos se adecuen a sus requisitos organizativos y de contabilidad.
- Para crear una gobernanza activa en un momento específico, use plantillas de implementación y automatización para aplicar configuraciones habituales y una estructura de agrupación coherente al implementar recursos y grupos de recursos.
- Establezca un modelo de permisos de privilegios mínimos, en el cual los usuarios no poseen permisos de forma predeterminada.
- Determine quién de su organización posee cada carga de trabajo y cuenta, y quién deberá tener acceso para mantener o modificar estos recursos. Defina roles y responsabilidades en la nube que coincidan con estas necesidades y use estos roles como base para el control de acceso.
- Defina las dependencias entre recursos.
- Implemente el escalado de recursos automatizado para adecuarse a los requisitos definidos en la fase Plan.
- Gestione el rendimiento de acceso para medir la calidad de los servicios recibidos.
- Considere la posibilidad de implementar la [directiva](https://docs.microsoft.com/azure/governance/policy/overview) para administrar la aplicación del Acuerdo de Nivel de Servicio mediante reglas de creación de recursos y valores de configuración.

## <a name="adopt-and-migrate"></a>Adoptar y migrar

La migración es un proceso incremental que se centra en el traslado, las pruebas y la adopción de las aplicaciones o cargas de trabajo de un patrimonio digital existente.

**Actividades mínimas sugeridas:**

- migre su [cadena de herramientas de coherencia de los recursos](./toolchain.md) desde la fase anterior a la implementación a la de producción.
- Actualice el documento de directrices de arquitectura y distribúyalo a las principales partes interesadas.
- Desarrolle materiales y documentación educativos, comunicaciones de reconocimiento, incentivos y otros programas para ayudar a impulsar la adopción del usuario.
- Migre las herramientas o scripts de corrección automatizados existentes para admitir los requisitos del Acuerdo de Nivel de Servicio definidos.

**Posible actividades:**

- Complete y pruebe los datos de supervisión y generación de informes con el entorno local, la puerta de enlace en la nube o la solución híbrida que elija.
- Determine si los cambios deben aplicarse a la directiva de administración o Acuerdo de Nivel de Servicio para los recursos.
- Mejore las tareas de operaciones implementando funcionalidades de consulta para buscar recursos con eficacia en todo su patrimonio en la nube.
- Alinee los recursos para cambiar las necesidades empresariales y los requisitos de gobernanza.
- Asegúrese de que sus máquinas virtuales, redes virtuales y cuentas de almacenamiento reflejan necesidades de acceso a los recursos reales durante cada lanzamiento y realice los ajustes que sean necesarios.
- Compruebe que el escalado automatizado de recursos cumple los requisitos de acceso.
- Revise el acceso del usuario a los recursos, los grupos de recursos y las suscripciones de Azure, y ajuste los controles de acceso según sea necesario.
- Supervise los cambios en los planes de acceso a los recursos y valide con las partes interesadas si son necesarias aprobaciones adicionales.
- Actualice los cambios en el documento de las directrices de arquitectura para reflejar los costos reales.
- Determine si su organización requiere una alineación financiera más clara con P&Ls para las unidades de negocio.
- Para las organizaciones globales, implemente sus requisitos de soberanía o cumplimiento del Acuerdo de Nivel de Servicio.
- Para la agregación de la nube, implemente una solución de puerta de enlace en un proveedor de nube.
- Para las herramientas que no permiten opciones de puerta de enlace o híbridas, asocie estrechamente la supervisión con una herramienta de supervisión operativa que abarque todos los centros de datos y nubes.

## <a name="operate-and-post-implementation"></a>Funcionamiento y fase posterior a la implementación

Una vez completada la transformación, la gobernanza y las operaciones deben estar disponibles durante el ciclo de vida natural de una aplicación o carga de trabajo. Esta fase de desarrollo de la gobernanza se centra en las actividades que surgen habitualmente cuando la solución ya está implementada y el ciclo de transformación comienza a estabilizarse.

**Actividades mínimas sugeridas:**

- personalice su [cadena de herramientas de coherencia de recursos](./toolchain.md) en función de las actualizaciones a las necesidades de Cost Management en constante cambio de su organización.
- Considere la posibilidad de automatizar cualquier notificación e informe para reflejar el uso de recursos real.
- Refine las directrices de arquitectura para guiar los procesos de adopción futuros.
- Ofrezca cursos a los equipos afectados de forma periódica para garantizar la adhesión en curso a las directrices de arquitectura.

**Actividades potenciales:**

- ajuste los planes trimestralmente para reflejar los cambios en los recursos reales.
- Aplique automáticamente los requisitos de gobernanza durante las implementaciones futuras.
- Evalúe los recursos infrautilizados y determine si merece la pena continuar con ellos.
- Detecte desajustes y anomalías entre el uso de recursos planeado y el real.
- Ayude a los equipos de adopción y estrategia de la nube a conocer y resolver estas anomalías.
- Determine si deben realizarse cambios en la coherencia de recursos para la facturación y los Acuerdos de Nivel de Servicio.
- Evalúe las herramientas de registro y supervisión para determinar si su entorno local, su puerta de enlace en la nube o su solución híbrida debe ajustarse.
- Para las unidades de negocio y los grupos distribuidos geográficamente, determine si su organización debe considerar la posibilidad de usar características de administración en la nube adicionales (por ejemplo, [grupos de administración de Azure](https://docs.microsoft.com/azure/governance/management-groups)) para aplicar mejor la directiva centralizada y cumplir los requisitos del Acuerdo de Nivel de Servicio.

## <a name="next-steps"></a>Pasos siguientes

Ahora que comprende el concepto de gobernanza de recursos en la nube, puede obtener información acerca de [cómo se administra el acceso a los recursos](./resource-access-management.md) en Azure como preparación para aprender a diseñar un modelo de gobernanza para una [carga de trabajo sencilla](./governance-simple-workload.md) o para [varios equipos](./governance-multiple-teams.md).

> [!div class="nextstepaction"]
> [Más información sobre la administración del acceso a los recursos en Azure](./resource-access-management.md)
> [Más información sobre los Acuerdos de Nivel de Servicio de Azure](https://azure.microsoft.com/support/legal/sla)
> [Más información sobre registros, informes y supervisión](../../decision-guides/logging-and-reporting/index.md)
