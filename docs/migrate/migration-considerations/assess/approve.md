---
title: Aprobación de los cambios de arquitectura antes de la migración
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Descripción de la importancia de la aprobación antes de la migración
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 360565a9d42dadc25c5ddcce5e8f1b3941d9ee42
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70839102"
---
# <a name="approve-architecture-changes-before-migration"></a>Aprobación de los cambios de arquitectura antes de la migración

Durante el proceso de evaluación de la migración, cada carga de trabajo se evalúa, diseña y calcula para desarrollar un plan de estado a futuro para la carga de trabajo. Algunas cargas de trabajo se pueden migrar a la nube sin cambiar la arquitectura. Mantener la arquitectura y la configuración local puede disminuir el riesgo y optimizar el proceso de migración. Desafortunadamente, no todas las aplicaciones se pueden ejecutar en la nube sin realizar cambios en la arquitectura. Cuando se requieren cambios en la arquitectura, este artículo puede ayudarlo a clasificar el cambio y puede proporcionar alguna orientación sobre las actividades de aprobación adecuadas.

## <a name="business-impact-and-approval"></a>Impacto de negocio y aprobación

Durante la migración, es probable que algunas cosas cambien de maneras que afecten a la empresa. Aunque a veces no se pueden evitar los cambios, sí se deben evitar las sorpresas como resultado de los cambios no divulgados o no documentados. Para mantener el respaldo de las partes interesadas a lo largo del trabajo de migración, es importante evitar las sorpresas. Sorprender a los propietarios de aplicaciones o las partes interesadas puede ralentizar o detener un esfuerzo de adopción de la nube.

Antes de la migración, es importante preparar al propietario empresarial de la carga de trabajo para los cambios que podrían afectar a los procesos empresariales, como los cambios en:

- Contratos de nivel de servicio.
- Patrones de acceso o requisitos de seguridad que afectan al usuario final.
- Prácticas de retención de datos.
- Rendimiento de la aplicación principal.

Incluso cuando una carga de trabajo se puede migrar con ningún cambio, o muy pocos, podría haber un impacto en el negocio. Los procesos de replicación pueden ralentizar el rendimiento de los sistemas de producción. Los cambios en el entorno como preparación para la migración tienen la posibilidad de generar limitaciones en el rendimiento de la red o el enrutamiento. Hay muchos efectos adicionales que pueden derivarse de las actividades de replicación, almacenamiento provisional o promoción.

Las actividades de aprobación periódicas pueden ayudar a minimizar o evitar sorpresas como consecuencia de los cambios o de los impactos de negocio generados por el rendimiento. El equipo de adopción de la nube debe ejecutar un proceso de aprobación de cambios al final del proceso de evaluación, antes de comenzar el proceso de migración.

## <a name="existing-culture"></a>Referencia cultural existente

Es probable que los equipos de TI tengan mecanismos existentes para administrar los cambios que implican los recursos locales. Habitualmente, estos mecanismos se rigen por los procesos de administración de cambios basados en la biblioteca de infraestructuras de tecnologías de la información (basados en ITIL) tradicionales. En muchas migraciones de empresas, estos procesos implican a un Comité de evaluación de cambios (CAB) responsable de revisar, documentar y aprobar todas las solicitudes de cambios (RFC) relacionadas con TI.

Por lo general, el CAB incluye expertos de varios equipos de TI y empresariales, que ofrecen una amplia variedad de perspectivas y una revisión detallada de todos los cambios relacionados con TI. Un proceso de aprobación del CAB es una manera comprobada para reducir el riesgo y minimizar el impacto empresarial de los cambios que implican cargas de trabajo estables administradas por las operaciones de TI.

## <a name="technical-approval"></a>Aprobación técnica

La disponibilidad de la organización para la aprobación de los cambios técnicos se encuentra entre las causas más comunes de los errores del proceso de migración a la nube. Hay más proyectos detenidos por una serie de aprobaciones técnicas que cualquier déficit en una plataforma en la nube. Preparar la organización para la aprobación de los cambios técnicos es un requisito importante para que la migración se realice correctamente. A continuación, se indican algunos procedimientos recomendados para garantizar que la organización está lista para la aprobación técnica.

### <a name="itil-change-advisory-board-challenges"></a>Desafíos del Comité de evaluación de cambios de ITIL

Cada enfoque de administración de cambios tiene su propio conjunto de controles y procesos de aprobación. La migración es una serie de cambios continuos que comienzan con un alto grado de ambigüedad y desarrollan mayor claridad durante el curso de la ejecución. De ese modo, la migración se rige mejor por los enfoques de administración de cambios basados en Agile, con el equipo de estrategia en la nube que actúa como propietario del producto.

Sin embargo, la escala y la frecuencia de los cambios durante una migración a la nube no se ajustan bien a la naturaleza de los procesos de ITIL. Los requisitos de una aprobación del CAB pueden poner en peligro el éxito de una migración, lo que ralentiza o detiene el trabajo. Además, en las primeras fases de la migración, la ambigüedad es alta y la experiencia en la materia tiende a ser baja. En el caso de las primeras migraciones o liberaciones de varias cargas de trabajo, el equipo de adopción de la nube suele estar en modo de aprendizaje. De ese, podría ser difícil para el equipo proporcionar los tipos de datos necesarios para pasar una aprobación del CAB.

Los procedimientos recomendados siguientes pueden ayudar al CAB a mantener un grado de confort durante la migración sin convertirse en un obstáculo bloqueador complicado.

### <a name="standardize-change"></a>Estandarización de los cambios

Para un equipo de adopción de la nube resulta tentador considerar decisiones de diseño detalladas para cada carga de trabajo que se va a migrar a la nube. Es igualmente tentador usar la migración a la nube como catalizador para refactorizar las decisiones de diseño anteriores. En el caso de las organizaciones que están migrando cientos de máquinas virtuales o algunas docenas de cargas de trabajo, cualquiera de estos enfoques se puede administrar correctamente. Al migrar un centro de información que consta de 1000 o más recursos, cada uno de estos enfoques se considera un como un antipatrón de alto riesgo que disminuye considerablemente la probabilidad de éxito. Modernizar, refactorizar y rediseñar cada aplicación requiere diversos conjuntos de aptitudes y una gran variedad de cambios y estas tareas crean dependencias de los esfuerzos humanos a escala. Cada una de estas dependencias inserta riesgo en el esfuerzo de migración.

En el artículo sobre la [racionalización del patrimonio digital](../../../digital-estate/rationalize.md) se describe la agilidad y el impacto del ahorro de tiempo de las suposiciones básicas al racionalizar un patrimonio digital. El cambio estandarizado agrega una ventaja adicional. Al elegir un enfoque de racionalización predeterminado para regir el esfuerzo de migración, el Comité de evaluación de la nube o el propietario del producto puede revisar y aprobar la aplicación de un cambio a una larga lista de cargas de trabajo. Esto reduce la aprobación técnica de cada carga de trabajo a aquellas que requieren un cambio significativo en la arquitectura para ser compatible con la nube.

### <a name="clarify-expectations-and-roles-of-approvers"></a>Aclaración de las expectativas y los roles de los aprobadores

Antes de evaluar la primera carga de trabajo, el equipo de estrategia en la nube debe documentar y comunicar las expectativas de cualquier persona implicada en la aprobación de los cambios. Esta sencilla actividad puede evitar retrasos costosos cuando el equipo de adopción de la nube está totalmente comprometido.

### <a name="seek-approval-early"></a>Búsqueda anticipada de la aprobación

Cuando sea posible, el cambio técnico se debe detectar y documentar durante el proceso de evaluación. Independientemente de los procesos de aprobación, el equipo de adopción de la nube debe ponerse en contacto con los aprobadores al principio. Cuanto antes se pueda comenzar la aprobación de los cambios, menos probable será que un proceso de aprobación bloquee las actividades de migración.

## <a name="next-steps"></a>Pasos siguientes

Con la ayuda de estos procedimientos recomendados, debería ser más fácil integrar la aprobación adecuada y de bajo riesgo en los esfuerzos de migración. Una vez que se aprueban los cambios en la carga de trabajo, el equipo de adopción de la nube está listo para [migrar las cargas de trabajo](../migrate/index.md).

> [!div class="nextstepaction"]
> [Migración de cargas de trabajo](../migrate/index.md)
