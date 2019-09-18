---
title: Procesos de cumplimiento de la directiva de la base de referencia de seguridad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Procesos de cumplimiento de la directiva de la base de referencia de seguridad
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6494f64b91a0a59f235efbc21030c65fa5e7ded8
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031953"
---
# <a name="security-baseline-policy-compliance-processes"></a>Procesos de cumplimiento de la directiva de la base de referencia de seguridad

En este artículo se describe un enfoque de los procesos de cumplimiento de directivas que rigen la directiva de la [base de referencia de seguridad](./index.md). La gobernanza efectiva de la seguridad de la nube comienza con procesos manuales periódicos diseñados para detectar vulnerabilidades e imponer directivas para remediar los riesgos para la seguridad. Esto requiere la participación regular del equipo de gobernanza de la nube y las partes interesadas de TI y de la empresa para revisar y actualizar la directiva y garantizar el cumplimiento de esta. Además, muchos procesos de aplicación y supervisión en curso se pueden automatizar o complementar con herramientas para reducir la sobrecarga de la gobernanza y permitir una respuesta más rápida a la desviación de directivas.

## <a name="planning-review-and-reporting-processes"></a>Procesos de planeación, revisión y generación de informes

Las mejores herramientas de la base de referencia de seguridad en la nube están limitadas a los procesos y directivas que admiten. El siguiente es un conjunto de procesos de ejemplo que normalmente están incluidos en la materia sobre la base de referencia de la seguridad. Use estos ejemplos como punto de partida al planear los procesos que le permitirán continuar actualizando la directiva de seguridad en función de los cambios que se produzcan en la empresa y los comentarios de los equipos de seguridad y TI cuya tarea es la activación de la guía de gobernanza.

**Planeamiento y evaluación inicial de los riesgos:** como parte de la adopción inicial de la materia sobre la base de referencia de la seguridad, identifique los principales riesgos empresariales y las tolerancias relacionadas con la seguridad de la nube. Esta información se usa para debatir sobre riesgos técnicos concretos con los miembros de los equipos de seguridad y de TI, y para desarrollar un conjunto de referencia de directivas de seguridad para mitigar dichos riesgos, con el fin de establecer la estrategia de gobernanza inicial.

**Planeación de la implementación:** antes de implementar cualquier carga de trabajo o recurso, realice una revisión de seguridad para identificar los nuevos riesgos y asegurarse de que se cumplen todos los requisitos de acceso y de la directiva de seguridad de datos.

**Pruebas de la implementación:** como parte del proceso de implementación de cualquier carga de trabajo o recurso, el equipo de gobernanza de la nube, en colaboración con los equipos de seguridad corporativa, será responsable de revisar la implementación para validar el cumplimiento de la directiva de seguridad.

**Planeación anual:** realice todos los años una revisión general de la estrategia de la base de referencia de la seguridad. Explore las futuras prioridades corporativas y las estrategias actualizadas de adopción de la nube para identificar un posible aumento del riesgo y otras necesidades de seguridad emergentes. También puede usar este tiempo para revisar los procedimientos recomendados de la base de referencia de seguridad más recientes e integrarlos en sus directivas y procesos de revisión.

**Planeamiento y revisión trimestrales:** realice una revisión trimestral de los datos de auditoría de seguridad y los informes de incidentes, con el fin de identificar los cambios necesarios en la directiva de seguridad. Como parte de este proceso, revise el panorama actual de ciberseguridad para anticiparse proactivamente a las amenazas emergentes y actualizar la directiva según corresponda. Una vez completada la revisión, alinee la guía de diseño con la directiva actualizada.

Este proceso de planeamiento también es un buen momento para evaluar a los miembros actuales del equipo de gobernanza de la nube, por si hay lagunas de conocimientos relacionadas con una directiva nueva o cambiante, y con los riesgos relacionados con la seguridad. Invite al personal de TI pertinente a participar en las revisiones y el planeamiento como asesores técnicos temporales o miembros permanentes del equipo.

**Educación y aprendizaje:** ofrezca sesiones de aprendizaje con carácter bimensual para asegurarse de que tanto los desarrolladores como el personal de TI están al día de los requisitos más recientes de las directivas de seguridad. Como parte de este proceso, revise y actualice cualquier documentación, guía u otros recursos de aprendizaje para asegurarse de que estén sincronizados con las declaraciones de directiva corporativa más recientes.

**Auditoría mensual y revisiones de informes:** realice una auditoría mensual de todas las implementaciones de la nube para garantizar su alineación continuada con la directiva de seguridad. Revise las actividades relacionadas con la seguridad con el personal de TI e identifique los problemas de cumplimiento que aún no se han abordado como parte del proceso continuo de supervisión y cumplimiento. El resultado de esta revisión es un informe para el equipo de estrategia de la nube y cada equipo de adopción de la nube para comunicar la adhesión general a la directiva. El informe también se almacena con fines de auditoría y legales.

## <a name="ongoing-monitoring-processes"></a>Procesos de supervisión en curso

La determinación de si la estrategia de gobernanza de la seguridad es correcta depende de la visibilidad de los estados actual y pasado de la infraestructura en la nube. Sin la capacidad para analizar las métricas pertinentes y los datos del estado de seguridad y de la actividad de los recursos en la nube, no se pueden identificar cambios en los riesgos o detectar infracciones de las tolerancias al riesgo. Los procesos de gobernanza en curso explicados anteriormente requieren datos de calidad para asegurarse de que se puede modificar la directiva para proteger mejor la infraestructura contra los constantes cambios que se producen tanto en las amenazas como en los requisitos de seguridad.

Asegúrese de que los equipos de seguridad y de TI han implementado sistemas de supervisión automatizados para la infraestructura en la nube que capturen los datos pertinentes de los registros que necesita para evaluar el riesgo. Sea proactivo en la supervisión de estos sistemas para asegurar la pronta detección y mitigación de posibles infracciones de la directiva y que su estrategia de supervisión esté en línea con las necesidades de seguridad.

## <a name="violation-triggers-and-enforcement-actions"></a>Desencadenadores de infracción y acciones de cumplimiento

Dado que el incumplimiento de las directivas de seguridad puede dar lugar a riesgos de exposición de datos e interrupción de servicios críticos, el equipo de gobernanza de la nube debe tener visibilidad sobre las infracciones graves de la directiva. Asegúrese de que el personal de TI conoce a la perfección las rutas de escalado para notificar los problemas de seguridad a los miembros del equipo de gobernanza más adecuados para identificar y comprobar que se han mitigado los problemas de la directiva.

Cuando se detectan infracciones, debe realizar acciones para volver a alinearse con la directiva lo antes posible. El equipo de TI puede automatizar la mayoría de los desencadenadores de infracciones mediante las herramientas que se describen en [Security Baseline toolchain for Azure](./toolchain.md) (Cadena de herramientas de la base de referencia de seguridad para Azure).

Los siguientes desencadenadores y acciones de cumplimiento son ejemplos que puede consultar para planear cómo usar los datos de supervisión para resolver las infracciones de directivas:

- **Aumento de los ataques detectados.** Si el número de ataques de fuerza bruta o DDoS que recibe cualquier recurso aumenta un 25 %, hable con el personal de seguridad de TI y con el propietario de la carga de trabajo para determinar las posible soluciones. Realice un seguimiento del problema y actualice la guía si es preciso realizar una revisión de la directiva para evitar dichos incidentes en el futuro.
- **Se han detectado datos sin clasificar.** A todos los orígenes de datos que carezcan de una adecuada clasificación de privacidad, seguridad o impacto en la empresa se les denegará el acceso externo hasta que el propietario de los datos aplique la clasificación y el nivel adecuado de protección.
- **Se ha detectado un problema en el estado de la seguridad.** Deshabilite el acceso a las máquinas virtuales (VM) que se sepa que tienen acceso o que se haya identificado que tienen vulnerabilidades de malware hasta que se puedan instalar las revisiones apropiadas o software de seguridad. Actualice las instrucciones de directiva para que tenga en cuenta las amenazas detectadas recientemente.
- **Se ha detectado una vulnerabilidad en la red.** El acceso a cualquier recurso no permitido explícitamente por las directivas de acceso de red debe desencadenar una alerta para el personal de seguridad de TI y el propietario de la carga de trabajo pertinente. Realice un seguimiento del problema y actualice la guía si es preciso realizar una revisión de la directiva para mitigar dichos incidentes en el futuro.

## <a name="next-steps"></a>Pasos siguientes

Mediante la [plantilla de Cloud Management](./template.md), documente los procesos y desencadenadores que se alinean con el plan de adopción de la nube actual.

Para obtener instrucciones acerca de cómo ejecutar directivas de administración en la nube de conformidad con los planes de adopción, consulte el artículo sobre la mejora de la materia.

> [!div class="nextstepaction"]
> [Mejora de la materia sobre la base de referencia de la seguridad](./discipline-improvement.md)
