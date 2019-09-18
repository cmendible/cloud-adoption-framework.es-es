---
title: Funcionalidades de gobernanza de la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Se describe la formación de funcionalidades de gobernanza de la nube.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: bb40dc63fcf125548e2734cc18edf36adacb2570
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031474"
---
# <a name="cloud-governance-capabilities"></a>Funcionalidades de gobernanza de la nube

Cualquier tipo de cambio genera nuevos riesgos. Las funcionalidades de gobernanza de la nube garantizan una evaluación y administración correctas de los riesgos y la tolerancia a ellos. Esta funcionalidad garantiza la identificación adecuada de los riesgos que no puede tolerar la empresa. Las personas que proporcionan esta funcionalidad pueden convertir los riesgos en directivas corporativas de gobernanza. Las directivas de gobernanza se ejecutan mediante materias definidas que ejecutan los miembros del personal, quienes proporcionan funcionalidades de gobernanza de la nube.

## <a name="possible-sources-for-this-capability"></a>Posibles orígenes de esta funcionalidad

Según los resultados empresariales deseados, las aptitudes necesarias para proporcionar funcionalidades completas de gobernanza de la nube se podrían facilitar por los siguientes medios:

- Gobernanza de TI
- Arquitectura empresarial
- Operaciones de TI
- Infraestructura de TI
- Redes
- Identidad
- Virtualización
- Continuidad empresarial/recuperación ante desastres
- Propietarios de aplicaciones dentro de TI

La funcionalidad de gobernanza de la nube identifica los riesgos relacionados con las versiones actuales y futuras. Esta funcionalidad se puede percibir en los trabajos para evaluar el riesgo, comprender los posibles impactos y tomar decisiones respecto a la tolerancia a los riesgos. De esta forma, los planes se pueden actualizar rápidamente para reflejar las necesidades cambiantes de la [funcionalidad de adopción de la nube](./cloud-adoption.md).

## <a name="key-responsibilities"></a>Principales responsabilidades

El deber principal de cualquier funcionalidad de gobernanza de la nube es equilibrar las fuerzas rivales de transformación y mitigación de los riesgos. Además, la gobernanza de la nube garantiza que la [adopción de la nube](./cloud-adoption.md) está al tanto de las directrices de arquitectura y clasificación de los recursos y los datos que regulan todos los enfoques de adopción. También, el equipo trabajará con el [Centro de excelencia en la nube](./cloud-center-of-excellence.md) para aplicar enfoques automatizados a los entornos de gobernanza de la nube.

La funcionalidad de gobernanza de la nube ejecuta normalmente estas tareas cada mes.

**Tareas de planeamiento iniciales:**

- Comprender los [riesgos empresariales](../govern/policy-compliance/risk-tolerance.md) introducidos por el plan
- Representar la [tolerancia de la empresa a los riesgos](../govern/policy-compliance/risk-tolerance.md)
- Ayudar a la creación de un [producto viable mínimo de gobernanza](../govern/guides/index.md)

**Tareas mensuales continuadas:**

- Comprender los [riesgos empresariales](../govern/policy-compliance/risk-tolerance.md) introducidos en cada versión
- Representar la [tolerancia de la empresa a los riesgos](../govern/policy-compliance/risk-tolerance.md)
- Ayudar a la mejora incremental de los [requisitos de cumplimiento y directivas](../govern/policy-compliance/index.md)

## <a name="meeting-cadence"></a>Cadencia de las reuniones

El equipo de trabajo suele proporcionar normalmente la funcionalidad de gobernanza de la nube. El compromiso de tiempo de cada miembro del equipo representará un gran porcentaje de sus programaciones diarias. Las contribuciones no se limitarán a reuniones y ciclos de comentarios.

## <a name="additional-participants"></a>Participantes adicionales

A continuación se representan los participantes que colaborarán con frecuencia en las actividades de gobernanza de la nube:

- Los líderes de la administración media y los colaboradores directos en puestos destacados designado para representar a la empresa ayudarán a evaluar la tolerancia al riesgo.
- Las funcionalidades de gobernanza de la nube se ofrecen como una extensión de la [funcionalidad de estrategia de la nube](./cloud-strategy.md). Igual que se espera que el director de sistemas (CIO) y los líderes empresariales participen en las funcionalidades de la estrategia de la nube, se espera que sus subordinados directos participen en las actividades de gobernanza de la nube.
- Los empleados de la empresa que son miembros de la unidad de negocio que trabajan estrechamente con la dirección de la línea de negocio deben estar capacitados para tomar decisiones relacionadas con el riesgo técnico y corporativo.
- Los empleados de tecnologías de la información (TI) y seguridad de la información (IS) que comprenden los aspectos técnicos de la transformación hacia nube pueden servir de capacidad rotativa en lugar de como proveedor constante de funcionalidades de gobernanza de la nube.

## <a name="maturation-of-cloud-governance-capability"></a>Madurez de la funcionalidad de gobernanza de la nube

Algunas organizaciones de gran tamaño cuentan ya con equipos dedicados que se centran en la gobernanza de TI. Estos equipos se especializan en la administración de riesgos en la cartera de TI mediante metodologías como ITIL o ITSM. Cuando se tienen estos equipos, los siguientes modelos de madurez se pueden acelerar rápidamente. Sin embargo, se recomienda que el equipo de gobernanza de TI revise el modelo de gobernanza de la nube para comprender cómo la gobernanza cambia ligeramente en la nube. Los artículos principales son [Ampliación de la directiva corporativa a la nube](../govern/corporate-policy.md) y [Cinco materias sobre la gobernanza de la nube](../govern/governance-disciplines.md).

**Sin gobernanza:** no es raro que las organizaciones se muevan a la nube sin planes claros de gobernanza. Enseguida, los problemas relacionadas con la seguridad, el costo, la escala y las operaciones comienzan a desencadenar conversaciones sobre la necesidad de un modelo de gobernanza y la dotación de personal para llevar a cabo los procesos asociados con ese modelo. Iniciar esas conversaciones antes de que se conviertan en problemas es siempre un buen primer paso para superar el antipatrón de "sin gobernanza". La sección sobre la [definición de la directiva corporativa](../govern/corporate-policy.md) puede ayudar a facilitar esas conversaciones.

**Gobernanza bloqueada:** cuando los problemas entono a la seguridad, el costo, la escala y las operaciones quedan sin respuesta, los proyectos y los objetivos empresariales tienden a bloquearse. La falta de una gobernanza adecuada genera temor, incertidumbre y dudas entre las partes interesadas y los ingenieros. Tome medidas lo antes posible para impedir que esta situación avance. Las dos guías de gobernanza definidas en Cloud Adoption Framework pueden ayudarle a comenzar poco a poco, a establecer directivas inicialmente limitadoras para reducir la incertidumbre y a desarrollar la gobernanza con el tiempo. Elija entre la [guía de empresa compleja](../govern/guides/complex/index.md) o la [guía de empresa estándar](../govern/guides/standard/index.md).

**Gobernanza voluntaria:** En todas las empresas siempre hay algunos valientes. Personas que están dispuestas a lanzarse y ayudar al equipo a aprender de sus errores. A menudo así es como comienza la gobernanza, en especial en empresas pequeñas. Estos valientes se ofrece como voluntarios para resolver algunos problemas y empujar a los equipos de adopción de la nube hacia un conjunto de procedimientos recomendados coherentes y bien administrados.

Los esfuerzos de estas personas son mucho mejores que los escenarios "sin gobernanza" o "gobernanza bloqueada". Aunque estos esfuerzos son dignos de elogio, este enfoque no debe confundirse con la gobernanza. Una gobernanza adecuada requiere algo más que ayuda esporádica para impulsar la coherencia, que es el objetivo de cualquier buen enfoque de gobernanza. La guía de las [cinco materias de gobernanza de la nube](../govern/governance-disciplines.md) puede ayudar a desarrollar esta materia.

**Custodio de la nube:** este apodo se ha convertido en una insignia de honor para muchos arquitectos de la nube que se especializan en la gobernanza en su fase temprana. La primera vez que se emprenden las prácticas de gobernanza, los resultados parecen similares a los de los voluntarios de la gobernanza. Sin embargo, hay una diferencia fundamental. Un custodio de la nube tiene un plan en mente. En esta fase de madurez, el equipo dedica tiempo a limpiar el desorden realizado por los arquitectos de la nube que llegaron antes que ellos. Sin embargo, el custodio de la nube alinea ese esfuerzo con [directivas corporativas](../govern/corporate-policy.md) bien estructuradas. También usan herramientas de automatización de la gobernanza, como las que se describen en el [producto viable mínimo de gobernanza](../govern/guides/complex/index.md).

Otra diferencia fundamental entre un custodio de la nube y un voluntario de la gobernanza es el apoyo de la dirección. El voluntario invierte horas adicionales y sobrepasa las expectativas normales por su afán de aprender y hacer. El custodio de la nube obtiene el respaldo de la dirección para reducir sus deberes diarios y garantizar que se pueden invertir las asignaciones normales de tiempo en la mejora de la gobernanza de la nube.

**Guardián de la nube:** a medida que se consolidan los procedimientos de gobernanza y los equipos de adopción de la nube las aceptan, el rol de los arquitectos de la nube especializados en la gobernanza cambia un poco, al igual que el del equipo de gobernanza de la nube. Por lo general, los procedimientos más madurados se ganan la atención de los expertos en la materia, quienes pueden ayudar a reforzar las protecciones que proporcionan las implementaciones de la gobernanza.

Aunque la diferencia es sutil, esta es una distinción importante al crear una cultura de TI centrada en la gobernanza. Un administrador en la nube se encarga de solucionar los problemas que crean los arquitectos en la nube con sus innovaciones, así que se puede decir que estos dos roles tienen objetivos encontrados. Un administrador en la nube ayuda a mantener la nube segura, para que los arquitectos en la nube puedan moverse rápidamente y crear menos problemas.

Los guardianes de la nube comienzan con enfoques de gobernanza avanzados a fin de acelerar la implementación de la plataforma y ayudar a los equipos a ser autosuficientes en cuanto a sus necesidades ambientales, de modo que puedan avanzar más rápido. Ejemplos de estas funciones más avanzadas se ven en las mejoras incrementales del producto viable mínimo de gobernanza, como la [mejora de la base de referencia de la seguridad](../govern/guides/complex/security-baseline-improvement.md).

**Aceleradores de la nube:** los guardianes de la nube y los custodios de la nube recopilan de forma natural scripts y automatizaciones que aceleran la implementación de entornos, plataformas o incluso componentes de varias aplicaciones. Conservar y compartir estos scripts, además de las responsabilidades de gobernanza centralizadas, desarrolla un alto grado de respeto por estos arquitectos en todo el ámbito de TI.

Aquellos profesionales de gobernanza que compartan de forma abierta sus scripts conservados ayudarán a ofrecer proyectos tecnológicos con mayor rapidez y a incorporar la gobernanza en la arquitectura de las cargas de trabajo. Esta influencia de la carga de trabajo y el respaldo de unos buenos patrones de diseño elevan los aceleradores de la nube a una categoría mayor de especialista en gobernanza.

**Gobernanza global:** cuando las organizaciones dependen de necesidades de TI distribuidas globalmente, puede haber desviaciones importantes en las operaciones y la gobernanza de diversas zonas geográficas. Las demandas de las unidades de negocio e incluso los requisitos de soberanía de los datos locales pueden hacer que los procedimientos recomendados de gobernanza interfieran con las operaciones necesarias. En estos casos, un modelo de gobernanza por niveles permite una coherencia mínimamente viable y una gobernanza localizada. En el artículo sobre [varios niveles de gobernanza](../govern/guides/complex/multiple-layers-of-governance.md) se proporciona más información sobre el alcance de este nivel de madurez.

Cada empresa es única y, por lo tanto, también lo son sus necesidades de gobernanza. Elija el nivel de madurez que mejor se adapte a su organización y use Cloud Adoption Framework para que guíe las prácticas, los procesos y las herramientas que le ayuden a conseguirlo.

## <a name="next-steps"></a>Pasos siguientes

A medida que la gobernanza de la nube madura, los equipos estarán capacitados para adoptar la nube a un ritmo cada vez mayor. Los continuos esfuerzos de adopción de la nube tienden a desencadenar la madurez en las operaciones de TI. Este madurez puede requerir también el desarrollo de [funcionalidades de operaciones de la nube](./cloud-operations.md).

> [!div class="nextstepaction"]
> [Desarrollo de funcionalidades de operaciones de la nube](./cloud-operations.md)
