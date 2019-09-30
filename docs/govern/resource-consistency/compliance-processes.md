---
title: Procesos de cumplimiento de directivas de coherencia de recursos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Procesos de cumplimiento de directivas de coherencia de recursos
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: fd44ae6fcdc84efd42ea3f79719475a32ead3111
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223706"
---
# <a name="resource-consistency-policy-compliance-processes"></a>Procesos de cumplimiento de directivas de coherencia de recursos

En este artículo se describe un enfoque de los procesos de cumplimiento de directivas que rigen la directiva de la [coherencia de recursos](./index.md). Una gobernanza eficaz de la coherencia de recursos en la nube comienza con procesos manuales periódicos diseñados para identificar la falta de eficiencia operativa, mejorar la administración de los recursos implementados y garantizar que las cargas de trabajo críticas tengan interrupciones mínimas. Estos procesos manuales se complementan con supervisión, automatización y herramientas para ayudar a reducir la sobrecarga de gobernanza y permitir una respuesta más rápida ante una desviación de la directiva.

## <a name="planning-review-and-reporting-processes"></a>Procesos de planeamiento, revisión y generación de informes

Las plataformas en la nube proporcionan una matriz de características y herramientas de administración que se pueden utilizar para organizar, aprovisionar, escalar y minimizar el tiempo de inactividad. El uso de estas herramientas para estructurar y administrar de forma eficaz las implementaciones en la nube de formas que corrijan los riesgos potenciales requiere directivas y procesos bien meditados, además de una cooperación estrecha con los equipos de operaciones de TI y las partes interesadas del negocio.

A continuación, se presenta un conjunto de procesos de ejemplo que normalmente están implicados en la materia de la coherencia de recursos. Use estos ejemplos como punto de partida al planear los procesos que le permitirán continuar actualizando la directiva de coherencia de recursos en función de los cambios que se produzcan en la empresa y los comentarios de los equipos de seguridad y TI cuya tarea es poner en práctica las instrucciones.

**Evaluación de riesgos y planeamiento iniciales:** como parte de su adopción inicial de la materia de coherencia de recursos, identifique sus principales riesgos empresariales y tolerancias relacionadas con las operaciones y la administración de TI. Esta información se usa para hablar de riesgos técnicos concretos con los miembros de los equipos de TI y los propietarios de cargas de trabajo a fin de desarrollar un conjunto de referencia de directivas de coherencia de recursos diseñado para corregir dichos riesgos, con el establecimiento de la estrategia de gobernanza inicial.

**Planeación de la implementación:** antes de implementar cualquier recurso, realice una revisión para identificar los nuevos riesgos operativos. Establezca requisitos de recursos y los patrones de demanda esperada e identifique las necesidades de escalabilidad y posibles oportunidades de optimización del uso. Asegúrese también de que existan planes de copia de seguridad y recuperación.

**Pruebas de la implementación:** como parte de la implementación, el equipo de gobernanza de la nube, en colaboración con los equipos de operaciones en la nube, se encarga de revisar la implementación a fin de validar el cumplimiento de las directivas de coherencia de recursos.

**Planeación anual:** realice todos los años una revisión de alto nivel de la estrategia de coherencia de recursos. Explore las prioridades o los planes de expansión corporativa futuros y actualice las estrategias de adopción de la nube para identificar un posible aumento del riesgo u otras necesidades emergentes relativas a la coherencia de recursos. Use también este tiempo para revisar los procedimientos recomendados de coherencia de recursos en la nube más recientes e integrarlos en sus directivas y procesos de revisión.

**Planeamiento y revisión trimestrales:** realice una revisión trimestral de los datos operativos y los informes de incidentes, con el fin de identificar los cambios necesarios en la directiva de coherencia de recursos. Como parte de este proceso, revise los cambios de rendimiento y uso de recursos para identificar los recursos que requieren aumentar o reducir la asignación de recursos y, además, identifique todas las cargas de trabajo o los recursos que se pueden retirar.

Este proceso de planeamiento también es un buen momento para evaluar a los miembros actuales del equipo de gobernanza de la nube, por si hay lagunas de conocimientos relacionadas con las directivas nuevas o en modificación y con los riesgos relacionados con la materia de coherencia de recursos. Invite al personal de TI pertinente a participar en las revisiones y el planeamiento como asesores técnicos temporales o miembros permanentes del equipo.

**Educación y aprendizaje:** ofrezca sesiones de aprendizaje con carácter bimensual para asegurarse de que los desarrolladores y el personal de TI están al tanto de las instrucciones y los requisitos más recientes de las directivas de coherencia de recursos. Como parte de este proceso, revise y actualice cualquier documentación u otros recursos de aprendizaje para asegurarse de que estén sincronizados con las declaraciones de directiva corporativa más recientes.

**Auditoría mensual y revisiones de informes:** realice una auditoría mensual de todas las implementaciones de la nube para garantizar su alineación continuada con la directiva de coherencia de recursos. Revise las actividades relacionadas con el personal de TI e identifique los problemas de cumplimiento que aún no se han abordado como parte del proceso continuo de supervisión y cumplimiento. El resultado de esta revisión es un informe para el equipo de estrategia de la nube y cada equipo de adopción de la nube para comunicar la adhesión general a la directiva y su cumplimiento. El informe también se almacena con fines de auditoría y legales.

## <a name="ongoing-monitoring-processes"></a>Procesos de supervisión en curso

La determinación de si la estrategia de gobernanza de coherencia de recursos es correcta depende de la visibilidad del estado actual y pasado de la infraestructura en la nube. Sin la capacidad para analizar las métricas pertinentes y los datos del estado y la actividad del entorno en la nube, no se pueden identificar cambios en los riesgos o detectar infracciones de las tolerancias al riesgo. Los procesos de gobernanza mencionados anteriormente requieren datos de calidad para garantizar que la directiva se pueda modificar a fin de optimizar el uso de los recursos en la nube y mejorar el rendimiento general de las cargas de trabajo hospedadas en la nube.

Asegúrese de que los equipos de TI han implementado sistemas de supervisión automatizados para la infraestructura en la nube que capturen los datos pertinentes de los registros que necesita para evaluar los riesgos. Sea proactivo en la supervisión de estos sistemas para asegurar la pronta detección y mitigación de posibles infracciones de la directiva y que su estrategia de supervisión esté en línea con las necesidades operativas.

## <a name="violation-triggers-and-enforcement-actions"></a>Desencadenadores de infracción y acciones de cumplimiento

Como el cumplimiento de las directivas de coherencia de recursos puede provocar interrupciones de servicio críticas o riesgos importantes de sobrecostos, el equipo de gobernanza de la nube debe tener visibilidad sobre los incidentes de incumplimiento. Asegúrese de que el personal de TI tiene rutas de escalado claras para notificar estos problemas a los miembros del equipo de gobernanza más adecuados para identificar y comprobar que se han corregido los problemas de directivas una vez detectados.

Cuando se detectan infracciones, debe realizar acciones para volver a alinearse con la directiva lo antes posible. El equipo de TI puede automatizar la mayoría de los desencadenadores de infracción con las herramientas descritas en [Resource Consistency toolchain for Azure](./toolchain.md) (Cadena de herramientas de coherencia de recursos para Azure).

Los siguientes desencadenadores y acciones de cumplimiento son ejemplos que puede consultar para planear cómo usar los datos de supervisión para resolver las infracciones de directivas:

- **Recurso sobreaprovisionado detectado.** cuando se detectan recursos que utilizan menos del 60 % de CPU o de capacidad de memoria, estos se deben reducir verticalmente o desaprovisionar automáticamente para reducir costos.
- **Recurso infraaprovisionado detectado.** cuando se detectan recursos que utilizan más del 80 % de CPU o de capacidad de memoria, es necesario escalar verticalmente o aprovisionar automáticamente recursos adicionales para proporcionar más capacidad.
- **Creación de recursos sin etiquetas.** todas las solicitudes para crear un recurso sin las etiquetas META necesarias se rechazarán automáticamente.
- **Interrupción de recursos crítica detectada.** el personal de TI recibe una notificación de todas las interrupciones críticas detectadas. Si la interrupción no se puede resolver inmediatamente, el personal escala el problema e informa a los propietarios de las cargas de trabajo y al equipo de gobernanza de la nube. El equipo de gobernanza de la nube realiza un seguimiento del problema hasta la resolución y actualiza las instrucciones si se necesita la revisión de las directivas para prevenir futuros incidentes.
- **Desfase de configuración.** Los recursos detectados que no se ajustan a las líneas de base establecidas deben desencadenar alertas y corregirse automáticamente mediante herramientas de administración de configuración como Azure Automation, Chef, Puppet, Ansible, etc.

## <a name="next-steps"></a>Pasos siguientes

Mediante la [plantilla de Cloud Management](./template.md), documente los procesos y desencadenadores que se alinean con el plan de adopción de la nube actual.

Para obtener instrucciones sobre cómo ejecutar directivas de administración en la nube de conformidad con los planes de adopción, consulte el artículo sobre la mejora de la materia.

> [!div class="nextstepaction"]
> [Mejora de la materia de coherencia de recursos](./discipline-improvement.md)
