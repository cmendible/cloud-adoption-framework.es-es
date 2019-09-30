---
title: Centro de excelencia de la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Describe la formación de un centro de excelencia de la nube (CCoE).
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: ac1fe4cac44d4a1f830be1faba7f2d50ddbd98f0
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224345"
---
# <a name="cloud-center-of-excellence"></a>Centro de excelencia de la nube

La agilidad técnica y empresarial son objetivos fundamentales para la mayoría de las organizaciones de TI. El centro de excelencia de la nube (CCoE) es una función que crea un equilibrio entre velocidad y estabilidad.

## <a name="function-structure"></a>Estructura de la función

CCoE requiere la colaboración entre cada una de las siguientes funcionalidades:

- Adopción de la nube (concretamente, los arquitectos de soluciones)
- Estrategia de la nube (concretamente, los jefes de proyectos y de programas)
- Gobernanza de la nube
- Plataforma de nube
- Automatización en la nube

## <a name="impact-and-cultural-change"></a>Impacto y cambio cultural

Si se admite esta función y se estructura correctamente, los participantes pueden acelerar los esfuerzos de innovación y migración a la vez que reducen el costo total de los cambios y aumentan la agilidad empresarial. Cuando se implementa correctamente, esta función puede reducir notablemente el tiempo de comercialización. A medida que los procedimientos del equipo se consolidan, los indicadores de calidad mejoran. Entre estos indicadores, se incluye la confiabilidad, el rendimiento, la seguridad, el mantenimiento y la satisfacción del cliente. Estas mejoras en eficacia, agilidad y calidad son especialmente importantes si la empresa tiene previsto implementar esfuerzos de migración a la nube a gran escala o desea emplear la nube para impulsar las innovaciones asociadas a la diferenciación de mercado.

Si se realiza correctamente, el modelo de CCoE supondrá un cambio cultural significativo en el equipo de TI. La premisa fundamental de un enfoque con un CCoE es que el departamento de TI actúa como un agente, asociado o representante para la empresa. Este modelo representa un cambio de paradigma que se aleja de la consideración tradicional de TI como una unidad de operaciones o un nivel de abstracción entre la empresa y los recursos de TI.

La imagen siguiente proporciona una analogía de este cambio cultural. En los enfoques sin CCoE, el equipo de TI tiende a centrarse en proporcionar control y responsabilidad central, actuando como los semáforos en un cruce. Si el modelo con CCoE es correcto, la atención se centra en la libertad y la responsabilidad delegada, lo cual se asemeja más a una rotonda.

![Analogía para un cambio de paradigma con un CCoE](../_images/ready/ccoe-paradigm-shift.png)

Ninguno de los enfoques que se ilustran en la analogía anterior es correcto o incorrecto, solo son puntos de vista alternativos de responsabilidad y administración. Si se desea establecer un modelo de autoservicio que permita a las unidades de negocio tomar sus propias decisiones siempre y cuando se adhieran a un conjunto de directrices y controles establecidos y repetibles, el modelo con un CCoE puede encajar en la estrategia tecnológica.

## <a name="key-responsibilities"></a>Principales responsabilidades

El deber principal del equipo del CCoE es acelerar la adopción de la nube mediante soluciones híbridas o nativas en la nube.

El objetivo del CCoE es:

- Ayudar a crear una organización de TI moderna a través de métodos ágiles para capturar e implementar requisitos empresariales.
- Emplear paquetes de implementación reutilizables que se adapten a las directivas de seguridad, cumplimiento y administración de servicios.
- Mantener una plataforma de Azure funcional en consonancia con los procedimientos operativos.
- Revisar y aprobar el uso de herramientas nativas en la nube.
- Con el tiempo, estandarizar y automatizar los componentes y soluciones de la plataforma que se necesitan normalmente.

## <a name="meeting-cadence"></a>Cadencia de las reuniones

El CCoE es una función dotada con personal de cuatro equipos con grandes exigencias. Es importante permitir la colaboración orgánica y realizar un seguimiento del crecimiento mediante un repositorio o catálogo de soluciones común. Maximice las interacciones naturales y reduzca al mínimo las reuniones. Una vez consolidada esta función, los equipos deben intentar limitar las reuniones específicas. La asistencia a reuniones periódicas, como las reuniones de lanzamiento que realiza el equipo de adopción de la nube, proporcionarán entradas de datos. Al mismo tiempo, una reunión después de compartir cada plan de lanzamiento puede servir de punto de contacto mínimo para este equipo.

## <a name="solutions-and-controls"></a>Soluciones y controles

A cada miembro del CCoE se le pide que comprenda las restricciones, riesgos y protecciones necesarios que condujeron al conjunto actual de controles de TI. Los esfuerzos colectivos del CCoE deben centrarse en soluciones nativas en la nube (o híbridas) o en controles que permitan los resultados empresariales de autoservicio que se desean. A medida que se crean las soluciones, estas se comparten con diversos equipos en forma de controles o automatizaciones que actúan como medidas de protección de los distintos esfuerzos. Estas medidas de protección ayudan a enrutar las actividades de libre circulación de los diversos equipos, al tiempo que permiten delegar responsabilidades en los participantes de los distintos esfuerzos de migración o innovación.

Ejemplos de esta transición:

| Escenario | Solución anterior al CCoE | Solución posterior al CCoE |
|---------|---------|---------|
| Aprovisionamiento de un servidor de SQL Server de producción | Los equipos de las plataformas de redes, TI y datos aprovisionan diversos componentes durante días e incluso semanas. | El equipo que requiere el servidor implementa una instancia de PaaS de Azure SQL Database. Como alternativa, se podría usar una plantilla previamente aprobada para implementar todos los recursos de IaaS en la nube en cuestión de horas. |
| Aprovisionamiento de un entorno de desarrollo | Los equipos de redes, TI, desarrollo y DevOps acuerdan las especificaciones e implementan un entorno. | El equipo de desarrollo define sus propias especificaciones e implementa un entorno basado en el presupuesto asignado. |
| Actualización de los requisitos de seguridad para mejorar la protección de datos | Los equipos de redes, TI y seguridad actualizan diversas máquinas virtuales y dispositivos de red en varios entornos para agregar protecciones. | Se utilizan herramientas de gobernanza de la nube para actualizar las directivas, las cuales se pueden aplicar inmediatamente a todos los recursos de todos los entornos en la nube. |

## <a name="negotiations"></a>Negociaciones

En la raíz de cualquier esfuerzo del CCoE se encuentra un proceso de negociación continuo. El equipo del CCoE negocia las funciones de TI existentes para reducir el control central. Las ventajas de esta negociación para la empresa son: mayor libertad, agilidad y velocidad. El valor de estas ventajas para los equipos de TI existentes se traduce en nuevas soluciones. Las nuevas soluciones proporcionan al equipo de TI existente una o varias de las siguientes ventajas:

- Capacidad de automatizar problemas habituales.
- Mejoras en la coherencia (con la consiguiente reducción de las frustraciones diarias).
- Oportunidad para aprender e implementar nuevas soluciones técnicas.
- Reducción de los incidentes graves (menos correcciones y más rápidas, y menor uso de localizadores o necesidad de respuesta a altas horas de la madrugada).
- Capacidad para ampliar su ámbito técnico lo que les permite abordar temas más amplios.
- Participación en soluciones empresariales de nivel superior que abordan el impacto de la tecnología.
- Reducción de las tareas de mantenimiento de poca importancia.
- Aumento de las estrategias tecnológicas y la automatización.

Como contrapartida a estas ventajas, el equipo de TI existente puede experimentar una reducción, real o percibida, de los siguientes valores:

- Sensación de control procedente de los procesos de aprobación manual.
- Sensación de estabilidad originada por el control de cambios.
- Sensación de seguridad del trabajo gracias a la finalización de tareas necesarias aunque repetitivas.
- Sensación de coherencia que procede de la adhesión a los proveedores de soluciones de TI existentes.

En las mejores empresas pioneras en la implementación de la nube, este proceso de negociación es un diálogo dinámico entre colegas y los equipos de TI asociados. Los detalles técnicos pueden ser complejos, pero son fáciles de controlar cuando el equipo de TI comprende su finalidad y apoya los esfuerzos del CCoE. Si el equipo de TI no se muestra tan favorable a estos, la sección siguiente sobre cómo conseguir el éxito del CCoE puede ayudar a superar los bloqueos culturales.

## <a name="enabling-ccoe-success"></a>Consecución del éxito del CCoE

Antes de continuar con este modelo, es importante comprobar la tolerancia de la empresa a una mentalidad de crecimiento y la comodidad del equipo de TI a la hora de delegar responsabilidades centrales. Como se mencionó anteriormente, el propósito de un CCoE es intercambiar control por agilidad y rapidez.

Este tipo de cambio lleva tiempo, experimentación y negociación. Se producirán obstáculos y retrocesos durante este proceso de consolidación. Sin embargo, si el equipo persevera y no se desanima durante la fase de experimentación, hay una alta probabilidad de éxito en la mejora de la agilidad, la velocidad y la confiabilidad. Uno de los factores más importantes que determinan el éxito o fracaso de un CCoE es el respaldo por parte del equipo directivo y las principales partes interesadas.

### <a name="key-stakeholders"></a>Principales partes interesadas

El equipo de dirección de TI es la primera y más evidente. Los jefes de TI desempeñan un papel importante. Sin embargo, durante este proceso se necesita el respaldo del jefe de información y de otros directores ejecutivos de TI.

Menos evidente es la necesidad para las partes interesadas de la empresa. La agilidad empresarial y el tiempo de comercialización son motivaciones clave para la formación de un CCoE. Por tanto, las partes interesadas clave deben tener un interés particular en estas áreas. Entre los ejemplos de partes interesadas de la empresa se incluyen los responsables de la línea de negocio, directivos financieros, directivos de operaciones y propietarios de productos empresariales.

### <a name="business-stakeholder-support"></a>Respaldo de las partes interesadas de la empresa

Los esfuerzos del CCoE se pueden acelerar con el respaldo de las partes interesadas de la empresa. El principal objetivo de los esfuerzos del CCoE se centra en la realización de mejoras a largo plazo en la agilidad y velocidad empresarial. Definir el impacto de los modelos operativos actuales y el valor de las mejoras es útil como guía y herramienta de negociación para el CCoE. Se recomienda documentar los siguientes elementos para definir el respaldo del CCoE:

- Establezca el conjunto de resultados y objetivos empresariales que se pretende conseguir como resultado de la agilidad y velocidad empresarial.
- Defina claramente los puntos débiles que generan los procesos de TI actuales (como la velocidad, la agilidad, la estabilidad y los costos).
- Defina claramente el impacto histórico de esos puntos débiles (como, por ejemplo, la pérdida de cuota de mercado, los logros de la competencia en características y funciones, malas experiencias de los clientes y aumentos presupuestarios).
- Defina las oportunidades de mejora empresarial que están bloqueadas por los actuales puntos débiles y modelos operativos.
- Establezca escalas de tiempo y métricas relacionadas con esas oportunidades.

Estos puntos de datos no son un ataque contra el equipo de TI. En vez de eso, ayudan al CCoE a aprender del pasado y a establecer una serie de trabajos pendientes y un plan de mejora realistas.

**Respaldo e implicación continuos:** Los equipos del CCoE pueden generar beneficios rápidos en algunas áreas. Sin embargo, los objetivos de nivel superior, como la agilidad empresarial y el tiempo de comercialización, pueden tardar mucho más. Durante el proceso de consolidación, existe un riesgo elevado de que el CCoE pierda la motivación o que se le pida que se centre en otros esfuerzos de TI.

Durante los primeros seis a nueve meses de trabajo del CCoE, se recomienda que las partes interesadas de la empresa dediquen un tiempo para reunirse mensualmente con la dirección de TI y el CCoE. No es necesario que estas reuniones sean excesivamente formales. Simplemente recordar a los miembros del CCoE y a la dirección la importancia de este programa puede suponer un impulso para el éxito del CCoE.

Además, se recomienda que las partes interesadas de la empresa permanezcan informadas del progreso y de los bloqueos que experimente el equipo del CCoE. Muchos de los esfuerzos de este equipo parecerán minucias técnicas. Sin embargo, es importante que las partes interesadas de la empresa conozcan el progreso del plan, de modo que puedan implicarse si el equipo pierde la motivación o se distrae en otras prioridades.

### <a name="it-stakeholder-support"></a>Respaldo de las partes interesadas de TI

**Apoyo de la visión:** Un trabajo de CCoE satisfactorio requiere una gran cantidad de negociación con los miembros del equipo de TI existentes. Si se hace bien, todo el equipo de TI contribuye a la solución y se siente cómodo con el cambio. En caso contrario, puede que algunos miembros del equipo de TI existente quieran aferrarse a los mecanismos de control por diversas razones. El respaldo de las partes interesadas del departamento de TI será crucial para lograr el éxito del CCoE si estas situaciones se producen. El estímulo y el refuerzo de los objetivos generales del CCoE es importante para resolver los bloqueos para lograr una negociación adecuada. En raras ocasiones, es posible que las partes interesadas de TI tengan incluso que intervenir para resolver un bloqueo o una votación empatada para mantener el progreso del CCoE.

**Mantener el foco de atención:** Un CCoE puede suponer un compromiso importante para cualquier equipo de TI con recursos limitados. Quitar profesionales competentes de los proyectos a corto plazo para centrarse en objetivos a largo plazo puede provocar dificultades para los miembros del equipo que no forman parte del CCoE. Es importante que la dirección y las partes interesadas de TI se centren en los objetivos del CCoE. El apoyo de la dirección y de las partes interesadas de TI es necesario para reducir la prioridad de las interrupciones de las operaciones diarias en favor de las obligaciones del CCoE.

**Crear un espacio reservado:** El equipo del CCoE experimentará nuevos enfoques. Algunos de estos enfoques no se adaptarán bien a las restricciones técnicas u operativas ya existentes. Existe un riesgo real de que el CCoE experimente la presión o crítica de otros equipos si se produce un error en los experimentos. Es importante motivar y preservar al equipo de las consecuencias de las oportunidades de aprendizaje de "error rápido". Es igualmente importante hacer que el equipo se comprometa con una mentalidad de crecimiento, asegurándose de que aprenden de esos experimentos y de que encuentran soluciones mejores.

## <a name="next-steps"></a>Pasos siguientes

Un centro de excelencia de la nube requiere [funcionalidades de plataforma en la nube](./cloud-platform.md) y [funcionalidades de automatización de la nube](./cloud-automation.md). El siguiente paso consiste en alinear esas [funcionalidades de plataforma en la nube](./cloud-platform.md).

> [!div class="nextstepaction"]
> [Alineación de las funcionalidades de una plataforma en la nube](./cloud-platform.md)
