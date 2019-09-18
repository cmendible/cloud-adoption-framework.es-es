---
title: Alineación inicial de la organización
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Proporciona información general sobre la alineación inicial de la organización.
author: alexbuckgit
ms.author: abuck
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.custom: governance
ms.openlocfilehash: 5e425a61f6b9da7fed044d06ac9323306d728261
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71021985"
---
# <a name="initial-organization-alignment"></a>Alineación inicial de la organización

La **transformación digital** a la informática en la nube representa un cambio desde la operación en el entorno local hacia la operación en la nube. Este cambio incluye nuevas formas de hacer negocios; por ejemplo, la transformación digital cambia de inversiones en capital para software y hardware del centro de datos a gastos de operación por el uso de recursos en la nube. Veamos cómo empezar a usar la [Plataforma de adopción de la nube de Microsoft para Azure](../index.md).

## <a name="the-digital-transformation-process"></a>El proceso de transformación digital

Para tener éxito en la adopción de la informática en la nube, una empresa debe preparar su organización, personal y procesos para que estén listos para esta transformación digital. La estructura organizativa de cada empresa es diferente, por lo que no hay una aproximación única para estos preparativos de la empresa. Este documento describe los pasos más importantes que su empresa puede seguir para prepararse. La organización tendrá que dedicar un tiempo a desarrollar un plan detallado para realizar cada uno de los pasos que se indican.

El proceso general para la transformación digital es:

1. Crear un equipo de estrategia en la nube. Este equipo es responsable de dirigir la transformación digital. También es importante en esta fase formar un equipo de gobernanza y un equipo de seguridad para la transformación digital.
2. Los miembros del equipo de estrategia en la nube obtienen información sobre las novedades en tecnologías en la nube y sus diferencias.
3. El equipo de estrategia en la nube prepara la empresa mediante la creación del caso de negocio de la transformación digital: enumera todas las brechas actuales en la estrategia empresarial y determina las soluciones de alto nivel para eliminarlos.
4. Alinear las soluciones de alto nivel con los grupos de negocio. Identificar las partes interesadas en cada grupo de negocio para llevar el diseño e implementación de cada solución.
5. Adaptar los roles, habilidades y procesos existentes para incluir roles, habilidades y procesos en la nube.

<!--6. Develop processes for operating in the cloud to make solutions more robust in terms of availability, resiliency, and security.
1. Optimize solutions for performance, scalability, and cost efficiency.-->

## <a name="step-1-create-a-cloud-strategy-team"></a>Paso 1: Creación de un equipo de estrategia en la nube

El primer paso en la transformación digital de la empresa es incorporar a responsables empresariales de toda la organización para crear un equipo de estrategia en la nube (CST). Este equipo está formado por responsables empresariales de los grupos de finanzas, infraestructura de TI y aplicaciones. Estos equipos pueden ayudar en la fase de análisis y experimentación en la nube.

Por ejemplo, un equipo de estrategia en la nube podría estar a cargo del director de tecnología e incluir miembros del equipo de arquitectura empresarial, finanzas de TI, tecnólogos de distintos grupos de aplicaciones de TI (recursos humanos, finanzas, etc.) y responsables de los equipos de infraestructura, seguridad y redes.

También es importante formar otros dos equipos de alto nivel: un equipo de gobernanza y un equipo de seguridad. Estos equipos son responsables del diseño, la implementación y la auditoría regular de directivas de seguridad y gobernanza de la empresa. El equipo de gobernanza precisa de miembros que hayan trabajado con protección de recursos, administración de costos, directivas de grupo y temas relacionados. El equipo de seguridad requiere que sus miembros sean expertos en los estándares de seguridad actuales, así como en los requisitos de seguridad de la empresa.

![Equipo de estrategia de nube, con equipos de gobernanza y seguridad](../_images/ready/getting-started-overview-1.png)

El equipo de gobernanza es responsable de diseñar e implementar el modelo de gobernanza de la empresa en la nube, así como de implementar y mantener los recursos de infraestructura compartida que forman parte de la transformación digital. Estos recursos incluyen el hardware, el software y los recursos en la nube necesarios para conectar la red local a una red virtual en la nube.

El equipo de seguridad es responsable de diseñar e implementar las directivas de seguridad de la empresa en la nube, trabajando estrechamente con el equipo de gobernanza. El equipo de seguridad lleva la extensión del límite de seguridad de la red local para que incluya una red virtual en la nube. Esto puede adoptar la forma de propietario y mantenedor de los firewalls de entrada y salida a la red virtual en la nube, así como el papel de garantizar que las herramientas y las directivas impiden la implementación de recursos no autorizados.

## <a name="step-2-learn-whats-new-in-the-cloud"></a>Paso 2: Obtención de información sobre las novedades en tecnologías en la nube

El siguiente paso en la transformación digital de la empresa consiste en que los miembros del equipo de estrategia en la nube obtengan información sobre cómo las tecnologías en la nube cambiarán la forma en la que empresa hace negocios. Se trata de preparar y planear los cambios en la empresa, el personal y las tecnologías. Es importante que los miembros del equipo de estrategia en la nube comprendan qué es nuevo y diferente en la nube en comparación con un entorno local.

![Los equipos de estrategia, gobernanza y seguridad en la nube aprenden los procedimientos recomendados para trabajar en la nube.](../_images/ready/getting-started-overview-2.png)

El punto de partida para comprender la nube consiste en aprender [cómo funciona Azure](../getting-started/what-is-azure.md) de un modo general. A continuación, se trata de obtener información sobre los conceptos básicos de [gobernanza en Azure](../govern/resource-consistency/what-is-governance.md) como preparación para [comprender la administración del acceso a los recurso](../govern/resource-consistency/resource-access-management.md).

Para un aprendizaje avanzado, el equipo de gobernanza debería revisar los conceptos y las guías de diseño de la sección de gobernanza de la tabla de contenido. Las secciones de infraestructura y cargas de trabajo son útiles para comprender las arquitecturas y las cargas de trabajo típicas en la nube.

## <a name="step-3-identify-gaps-in-business-strategy"></a>Paso 3: Identificación de brechas en la estrategia empresarial

El paso siguiente consiste en que el equipo de estrategia en la nube enumere los problemas empresariales que requieren una solución de transformación digital. Por ejemplo, una empresa puede tener un centro de datos local con hardware que está al final de su ciclo de vida y que es necesario sustituir. En otro ejemplo, una empresa podría experimentar dificultades con el tiempo de comercialización de nuevas características y servicios y situarse por detrás de la competencia. Estas brechas representan los _objetivos_ de la transformación digital de la empresa.

Las brechas en la estrategia empresarial se pueden clasificar en las categorías siguientes:

| Categoría | DESCRIPCIÓN |
| --- | --- |
| Administración de costos | Representa una brecha en el modo en el que la empresa paga por la tecnología. |
| Gobernanza | Representa una brecha en los procesos utilizados por la empresa para proteger los recursos de un uso inadecuado que podría dar lugar a excesos de costo, problemas de seguridad o problemas de cumplimiento. |
| Cumplimiento normativo | Representa una brecha en la manera en la que la empresa cumple sus propios procesos y directivas internos, así como leyes, reglamentos y estándares externos. |
| Seguridad | Representa una brecha en la manera en la que la empresa protege su tecnología y recursos de datos frente a amenazas externas. |
| Gobernanza de datos | Representa una brecha en la manera en la que una empresa administra sus datos, especialmente los datos de los clientes. Por ejemplo, el nuevo Reglamento general de protección de datos (RGPD) de la Unión Europea tiene requisitos estrictos para la protección de los datos de los clientes que podrían requerir hardware y software nuevo. |

Una vez que la empresa ha clasificado todas las brechas de la estrategia empresarial en estas categorías, el siguiente paso es determinar una solución de alto nivel para cada problema.

En la tabla siguiente se muestran varios ejemplos:

|Brecha de la estrategia empresarial|Categoría &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|Solución &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
|-----|-----|-----|
| Los servicios hospedados actualmente en el entorno local experimentan problemas con la disponibilidad, la resistencia y la escalabilidad durante el tiempo de máxima demanda, que es aproximadamente un 10 por ciento del uso. Los servidores del centro de datos local están al final del ciclo de vida. El departamento de TI empresarial recomienda adquirir nuevo hardware local para el centro de datos con las especificaciones necesarias para controlar los momentos de máxima demanda.| Administración de costos | Migrar las cargas de trabajo locales existentes afectadas a recursos escalables en la nube y pagar solo por el uso. |
| Las normativas y regulaciones externas de administración de datos exigen que la empresa cumpla un conjunto de controles estándares que requieren el cifrado de datos en reposo, lo que a su vez hace necesario nuevo hardware y software. | Gobernanza de datos | Trasladar los datos al cifrado del servicio de Azure Storage para datos en reposo. |
| Los servicios hospedados en centros de datos locales han experimentado ataques por denegación de servicio distribuido (DDoS) en los servicios orientados al público. Los ataques son difíciles de mitigar y requieren nuevo hardware, software y personal de seguridad para controlarlos de forma eficaz. | Seguridad | Migrar los servicios a Azure y aprovechar las ventajas de Azure DDoS Protection.|

Cuando se han enumerado todas las brechas en la estrategia empresarial y se han determinado las soluciones de alto nivel, se debe asignar prioridades a la lista. Se puede asignar prioridades a la lista mediante la alineación de las brechas de la estrategia empresarial con los objetivos a corto y a largo plazo de la empresa en cada categoría. Por ejemplo, si la empresa tiene como objetivo a corto plazo reducir el gasto en TI en los dos próximos trimestres fiscales, las brechas de negocio de la categoría de *administración de costos* se pueden priorizar en función del ahorro en costos previsto de cada una.

El resultado de este proceso es una lista ordenada de soluciones de alto nivel alineadas con categorías de empresas.

## <a name="step-4-align-high-level-solutions-with-business-groups-to-design-solutions"></a>Paso 4: Alineación de las soluciones de alto nivel con los grupos de negocio para diseñar soluciones

Ahora que se han enumerado y priorizado los objetivos de la transformación digital y se han propuesto soluciones de alto nivel, el paso siguiente consiste en que el equipo de estrategia en la nube alinee cada una de las soluciones de alto nivel con equipos de diseño e implementación de cada uno de los grupos de negocio.

Los equipos reciben las listas con prioridades y trabajan en cada solución de alto nivel para diseñar cada solución. El proceso de diseño implica la especificación de nueva infraestructura y nuevas cargas de trabajo. También puede haber cambios en los roles de las personas y los procesos que siguen. También es muy importante en esta fase que cada uno de los equipos de diseño incluya a los equipos de gobernanza y de seguridad para que revisen cada diseño. Cada diseño debe cumplir las directivas y procedimientos definidos por los equipos de gobernanza y seguridad y estos equipos se deben incluir en la aprobación final de cada diseño.

![El equipo de estrategia en la nube entrega soluciones generales a los equipos de diseño e implementación.](../_images/ready/getting-started-overview-3.png)

El diseño de cada solución no es una tarea trivial. A medida que se crean diseños, deben tenerse en cuenta en el contexto de otros diseños de soluciones de otros equipos. Por ejemplo, si varios de los diseños provocan una migración de servicios y aplicaciones locales existentes a la nube, puede ser más eficaz agruparlos y diseñar una estrategia de migración general. En otro ejemplo, podría no resultar posible migrar algunas aplicaciones y servicios locales existentes y la solución puede ser reemplazarlos por un nuevo desarrollo o servicios de terceros. En este caso, puede resultar más eficaz agruparlos y determinar la superposición entre ellos para decidir si se puede usar un servicio de terceros para más de una solución.

Una vez completado el diseño de la solución, el equipo pasa a la fase de implementación de cada diseño. La fase de implementación de cada diseño de solución se puede llevar a cabo mediante el uso de los procesos de administración de proyectos estándar.

## <a name="step-5-adapt-existing-roles-skills-and-process-for-the-cloud"></a>Paso 5: Adaptación de los roles, las habilidades y los procesos existentes a la nube

En cada fase de la historia del sector de TI, los cambios más importantes del sector vienen a menudo marcados por cambios en los roles del personal. Durante la transición de los sistemas mainframe al modelo cliente/servidor, el rol del operador de equipo en gran medida desapareció, reemplazado por el administrador del sistema. Cuando llegó la era de la virtualización, disminuye el número de personas que trabajan con servidores físicos, reemplazado por una necesidad de especialistas en virtualización. De forma similar, a medida que las instituciones se desplacen a la informática en la nube, los roles probablemente cambiarán de nuevo. Por ejemplo, los especialistas en centros de datos podrían reemplazarse por analistas financieros de la nube. Aunque los nombres de los puestos de trabajo de TI no hayan cambiado, los roles de los trabajos diarios han cambiado significativamente.

Los miembros del personal de TI pueden sentirse preocupados por sus roles y puestos a medida que se dan cuenta de que se necesita un conjunto diferente de habilidades para el trabajo con soluciones en la nube. Pero los empleados ágiles que exploran y aprenden las nuevas tecnologías en la nube no tienen por qué preocuparse. Pueden dirigir la adopción de los servicios en la nube y ayudar a la organización a comprender y adoptar los cambios asociados.

### <a name="capturing-concerns"></a>Registro de preocupaciones

Durante la transformación digital, cada equipo debe capturar cualquier preocupación del personal que surja. Al capturar las preocupaciones, identifique lo siguiente:

- **Tipo de preocupación.** Por ejemplo, los trabajadores pueden ser reacios a los cambios en las tareas del trabajo que acompañan a la transformación digital.
- **El impacto de la preocupación si no se soluciona.** Por ejemplo, la resistencia a la transformación digital puede provocar que los trabajadores sean lentos al ejecutar los cambios necesarios.
- **El área preparada para solucionar el problema.** Por ejemplo, si los empleados del departamento de TI son reacios a adquirir nuevas habilidades, el área de responsables de TI está mejor preparada para solucionar este problema. La identificación del área puede no estar clara para algunas preocupaciones y, en estos casos, es posible que se deban escalar a un responsable ejecutivo.

### <a name="identify-gaps"></a>Identificación de brechas

Otro aspecto que aparece al repasar los problemas de la transformación digital de la empresa es la identificación de las **brechas**. Una brecha es un rol, habilidad o proceso necesario para la transformación digital que no existe actualmente en la empresa.

Comience por enumerar las responsabilidades nuevas que acompañan a la transformación digital, con énfasis en las nuevas responsabilidades y las responsabilidades actuales que se retirarán. Identifique el área que se alinea con cada responsabilidad. Para las nuevas responsabilidades, determine el grado de alineación con el área. Algunas responsabilidades pueden abarcar varias áreas y esto representa una oportunidad para mejorar la alineación que se debería registrar como una preocupación. En el caso de que ningún área se pueda identificar como responsable, regístrelo como una brecha.

A continuación, identifique las habilidades necesarias para posibilitar la responsabilidad. Determine si la empresa tiene recursos existentes con estas habilidades. Si no hay ningún recurso existente disponible, determine los programas de entrenamiento o la adquisición de talentos necesarios. Determine el período de tiempo que debe estar lista la responsabilidad para mantener la transformación digital por un camino controlado.

Por último, identifique los roles que ejecutarán estas habilidades. Algunos de los trabajadores existentes asumirán partes del rol y en otros casos puede ser necesario un rol completamente nuevo.

### <a name="partner-across-teams"></a>Trabajo entre equipos

Las habilidades necesarias para llenar las brechas de la transformación digital de la organización normalmente no estarán limitadas a un solo rol o incluso un único departamento. Las habilidades tendrán relaciones y dependencias que pueden abarcar un único rol o varios y esos roles pueden estar en varios departamentos. Por ejemplo, un propietario de la carga de trabajo puede requerir una persona de un rol de TI para aprovisionar recursos básicos como las suscripciones y los grupos de recursos.

Estas dependencias representan nuevos procesos que la organización implementa para administrar el flujo de trabajo entre los roles. En el ejemplo anterior, hay varios tipos diferentes de proceso que puede admitir la relación entre el propietario de la carga de trabajo y el rol de TI. Por ejemplo, se puede crear una herramienta de flujos de trabajo para administrar el proceso o se puede usar una simple plantilla de correo electrónico.

Realice un seguimiento de estas dependencias y tome nota de los procesos que las posibilitarán y si el proceso existe actualmente o no. Para aquellos procesos que precisen de herramientas, asegúrese de que la escala de tiempo para la implementación de las herramientas se alinea con la programación de la transformación digital en general.

## <a name="next-steps"></a>Pasos siguientes

La transformación digital es un proceso iterativo y con cada iteración los equipos implicados serán más eficaces.

> [!div class="nextstepaction"]
> [Funcionamiento de Azure](../getting-started/what-is-azure.md)
