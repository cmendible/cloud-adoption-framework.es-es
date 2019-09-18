---
title: Mejora de la disciplina de aceleración de la implementación
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Mejora de la disciplina de aceleración de la implementación
author: alexbuckgit
ms.author: abuck
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 7cff2c0cbf8fea06ea7ebdfaaade1c8538802639
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032085"
---
# <a name="deployment-acceleration-discipline-improvement"></a>Mejora de la disciplina de aceleración de la implementación

La disciplina de aceleración de la implementación se centra en establecer directivas que aseguren que los recursos se implementen y configuren de manera coherente y repetitiva, y que puedan cumplir los requisitos establecidos durante todo su ciclo de vida. Dentro de las cinco disciplinas de la gobernanza de la nube, la aceleración de la implementación incluye decisiones relacionadas con la automatización de implementaciones, los artefactos de implementación que controlan el origen, la supervisión de los recursos implementados para mantener el estado establecido y la auditoría de cualquier problema de cumplimiento.

En este artículo se destacan algunas tareas potenciales en las que su empresa puede participar para desarrollar y mejorar la materia sobre la aceleración de la implementación. Estas tareas se dividen en las fases de planeamiento, compilación, adopción y funcionamiento de la implementación de una solución de nube que, posteriormente, se iteran para permitir el desarrollo de un [enfoque incremental a la gobernanza de la nube](../guides/index.md#an-incremental-approach-to-cloud-governance).

![Cuatro fases de adopción](../../_images/govern/adoption-phases.png)

*Figura 1: Fases de adopción del enfoque incremental para la gobernanza de la nube.*

Es imposible recopilar en un solo documento los requisitos de todas las empresas. Por lo tanto, en este artículo se detallan ejemplos de actividades mínimas y potenciales sugeridas para cada fase del proceso de desarrollo de la gobernanza. El objetivo inicial de estas actividades es ayudarle a crear un [producto viable mínimo de directiva](../guides/index.md#an-incremental-approach-to-cloud-governance) y establecer un marco para la mejora incremental de las directivas. El equipo de gobernanza de la nube deberá decidir cuánto invertir en estas actividades para mejorar las funcionalidades de gobernanza de la base de referencia de identidad.

> [!CAUTION]
> Ni las actividades mínimas ni las posibles que se describen en este artículo están en línea con directivas corporativas específicas ni con requisitos de cumplimiento de terceros. Esta guía está diseñada como ayuda para facilitar las conversaciones que darán lugar a la alineación de los requisitos con un modelo de gobernanza de la nube.

## <a name="planning-and-readiness"></a>Planeamiento y preparación

Esta fase del desarrollo de la gobernanza permite salvar las diferencias entre los resultados empresariales y unas estrategias accionables. Durante este proceso, el equipo directivo define métricas específicas, las asigna al patrimonio digital y empieza a planear el esfuerzo global de migración.

**Actividades mínimas sugeridas:**

- Evalúe las opciones de su [cadena de herramientas de aceleración de la implementación](./toolchain.md), e implemente una estrategia híbrida que sea adecuada para su organización.
- Desarrolle un borrador con las directrices de arquitectura y distribúyalo a las partes interesadas clave.
- Eduque e implique a las personas y equipos que se vean afectados por el desarrollo de las directrices de arquitectura.
- Entrene a los equipos de desarrollo y al personal de TI para que comprendan los principios y estrategias de DevSecOps y la importancia de las implementaciones totalmente automatizadas de la Disciplina de aceleración de la implementación.

**Actividades potenciales:**

- Defina los roles y asignaciones que regirán la aceleración de la implementación en la nube.

## <a name="build-and-predeployment"></a>Compilación y fase anterior a la implementación

**Actividades mínimas sugeridas:**

- Para las nuevas aplicaciones basadas en la nube, introduzca implementaciones totalmente automatizadas al principio del proceso de desarrollo. Esta inversión mejorará la confiabilidad de sus procesos de prueba y garantizará la coherencia en sus entornos de desarrollo, el control de calidad y la producción.
- Almacene todos los artefactos de implementación, como las plantillas de implementación o los scripts de configuración, mediante una plataforma de control de origen como GitHub o Azure DevOps.
- Considere la posibilidad de realizar una prueba piloto antes de implementar su [cadena de herramientas para la aceleración de la implementación](./toolchain.md); así se asegurará de que se optimizan sus implementaciones tanto como sea posible. Aplique los comentarios de las pruebas piloto durante la fase previa a la implementación, repitiendo el proceso según sea necesario.
- Evalúe la arquitectura lógica y física de sus aplicaciones e identifique las oportunidades para automatizar la implementación de los recursos de la aplicación o mejorar partes de la arquitectura con otros recursos basados en la nube.
- Actualice el documento de directrices de arquitectura para que incluya los planes de implementación y adopción por parte del usuario, y distribúyalo a las partes interesadas clave.
- A continuación, eduque a los usuarios y equipos a los que más afecten las directrices de la arquitectura.

**Actividades potenciales:**

- Defina una canalización de integración e implementación continua (CI/CD) para administrar completamente las actualizaciones de versión de la aplicación a través de los entornos de desarrollo, el control de calidad y la producción.

## <a name="adopt-and-migrate"></a>Adoptar y migrar

La migración es un proceso incremental que se centra en el traslado, las pruebas y la adopción de las aplicaciones o cargas de trabajo de un patrimonio digital existente.

**Actividades mínimas sugeridas:**

- Migre la [cadena de herramientas para la aceleración de la implementación](./toolchain.md) desde el entorno de desarrollo al de producción.
- Actualice el documento de las directrices de arquitectura y distribúyalo a las partes interesadas clave.
- Desarrolle materiales y documentación educativos, comunicaciones de reconocimiento, incentivos y otros programas para ayudar a impulsar la adopción de TI y a los desarrolladores.

**Posible actividades:**

- Compruebe que los procedimientos recomendados que se definieron durante las fases de compilación y anterior a la implementación se ejecutan correctamente.
- Cerciórese de que todas las aplicaciones o cargas de trabajo siguen alineadas con la estrategia de aceleración de la implementación antes de la publicación.

## <a name="operate-and-post-implementation"></a>Funcionamiento y fase posterior a la implementación

Una vez completada la transformación, la gobernanza y las operaciones deben estar disponibles durante el ciclo de vida natural de una aplicación o carga de trabajo. Esta fase de desarrollo de la gobernanza se centra en las actividades que surgen habitualmente cuando la solución ya está implementada y el ciclo de transformación comienza a estabilizarse.

**Actividades mínimas sugeridas:**

- Personalice la [cadena de herramientas para la aceleración de la implementación](./toolchain.md) según los cambios en las necesidades de identidades de la organización.
- Automatice notificaciones e informes para que le avisen de posibles amenazas malintencionadas o problemas con la configuración.
- Supervise y envíe notificaciones sobre el uso de los recursos y la aplicación.
- Informe sobre las métricas posteriores a la implementación y distribúyalas a las partes interesadas.
- Revise las directrices de arquitectura para guiar los procesos de adopción futuros.
- Continue comunicándose y capacitando a las personas y equipos afectados de manera regular para garantizar el cumplimiento continuo de las Pautas de Arquitectura.

**Actividades potenciales:**

- Configure una herramienta de supervisión e información de la configuración de estado que quiera establecer.
- Revise periódicamente las herramientas de configuración y los scripts para mejorar los procesos e identificar problemas comunes.
- Trabaje con los equipos de desarrollo, operaciones y seguridad para mejorar las prácticas de DevSecOps y ordenar la maraña organizativa que conduce a ineficiencias.

## <a name="next-steps"></a>Pasos siguientes

Ahora que conoce el concepto de gobernanza de identidades en la nube, examine la [cadena de herramientas de la base de referencia de identidad](./toolchain.md) para identificar las herramientas y características de Azure que necesitará al desarrollar la materia sobre la base de referencia de la identidad en la plataforma Azure.

> [!div class="nextstepaction"]
> [Cadena de herramientas de la línea de base de identidad para Azure](./toolchain.md)
