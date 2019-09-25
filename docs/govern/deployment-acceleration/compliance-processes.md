---
title: Procesos de cumplimiento de directivas de aceleración de la implementación
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Procesos de cumplimiento de directivas de aceleración de la implementación
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: a393791aac072cb9a135c6fc11e08fc653817742
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222593"
---
# <a name="deployment-acceleration-policy-compliance-processes"></a>Procesos de cumplimiento de directivas de aceleración de la implementación

En este artículo se describe un enfoque de los procesos de cumplimiento de directivas que rigen la [aceleración de la implementación](./index.md). Una gobernanza efectiva de la configuración en la nube comienza con los procesos manuales periódicos diseñados para detectar problemas e imponer directivas para remediar los riesgos. Sin embargo, puede automatizar estos procesos y complementarlos con herramientas para reducir la sobrecarga de gobernanza y permitir una respuesta más rápida a las desviaciones.

## <a name="planning-review-and-reporting-processes"></a>Procesos de planificación, revisión e informes

Las mejores herramientas de aceleración de la implementación en la nube son solo tan buenas como los procesos y directivas que admiten. El siguiente es un conjunto de procesos de ejemplo que se utilizan normalmente como parte de la materia de aceleración de la implementación. Use estos ejemplos como punto de partida al planear los procesos que le permitirán continuar actualizando la directiva de implementación y configuración en función de los cambios del negocio y los comentarios de los equipos de seguridad y TI responsables de poner en práctica la guía de gobernanza.

**Planeamiento y evaluación inicial de los riesgos:** Como parte de la adopción inicial de la disciplina de aceleración de la implementación, identifique los riesgos y tolerancias principales del negocio, relacionados con la implementación de las aplicaciones empresariales. Use esta información para analizar los riesgos técnicos específicos con los miembros del equipo de operaciones de TI. Desarrolle una base de referencia de directivas de implementación y configuración para remediar estos riesgos y establecer la estrategia de gobernanza inicial.

**Planeación de la implementación:** antes de implementar cualquier recurso, realice una revisión de la seguridad y las operaciones para identificar nuevos riesgos y asegurarse de que se cumplen todos los requisitos de la directiva de implementación.

**Pruebas de la implementación:** como parte del proceso de implementación para cualquier recurso, el equipo de gobernanza de la nube, en colaboración con los equipos de operaciones de TI, es el responsable de revisar el cumplimiento de la directiva de implementación.

**Planeación anual:** Lleve a cabo una revisión anual de nivel superior de la estrategia de aceleración de la implementación. Explore las prioridades corporativas futuras y las estrategias de adopción de la nube actualizadas para identificar un posible aumento del riesgo y otras necesidades y oportunidades de configuración emergentes. También puede usar este tiempo para revisar los procedimientos recomendados de DevOps e integrarlos en sus directivas y procesos de revisión.

**Planeamiento y revisión trimestrales:** realice una revisión trimestral de los datos de auditoría de las operaciones y los informes de incidentes para identificar los cambios necesarios en la directiva de aceleración de la implementación. Como parte de este proceso, revise los procedimientos recomendados actuales de DevOps y DevTechOps y actualice la directiva según corresponda. Una vez completada la revisión, alinee la guía de diseño de sistemas y aplicaciones con la directiva actualizada.

Este proceso de planeamiento también es un buen momento para evaluar a los miembros actuales del equipo de gobernanza de la nube, por si hubiera carencias de conocimientos relacionadas con la directiva nueva o cambiante, y los riesgos relacionados con DevOps y la aceleración de la implementación. Invite al personal de TI pertinente a participar en las revisiones y el planeamiento como asesores técnicos temporales o miembros permanentes del equipo.

**Educación y aprendizaje:** ofrezca sesiones de aprendizaje con carácter bimensual para asegurarse de que los desarrolladores y el personal de TI están al día de los requisitos y la estrategia de aceleración de la implementación más reciente. Como parte de este proceso, revise y actualice cualquier documentación, guía u otros recursos de aprendizaje para asegurarse de que estén sincronizados con las declaraciones de directiva corporativa más recientes.

**Auditoría mensual y revisiones de informes:** Realice una auditoría mensual en todas las implementaciones de nube para garantizar su alineación continuada con la directiva de configuración. Revise las actividades relacionadas con la implementación con el personal de TI e identifique los problemas de cumplimiento que aún no se han abordado como parte del proceso continuo de supervisión y cumplimiento. El resultado de esta revisión es un informe para el equipo de estrategia de la nube y cada equipo de adopción de la nube para comunicar la adhesión general a la directiva. El informe también se almacena con fines de auditoría y legales.

## <a name="ongoing-monitoring-processes"></a>Procesos de supervisión en curso

La determinación de si la estrategia de gobernanza de aceleración de la implementación es correcta depende de la visibilidad del estado actual y pasado de la infraestructura en la nube. Sin la capacidad para analizar las métricas pertinentes y los datos del estado de las operaciones y la actividad de los recursos en la nube, no se pueden identificar cambios en los riesgos ni detectar infracciones de las tolerancias al riesgo. Los procesos de gobernanza en curso explicados anteriormente requieren datos de calidad para asegurarse de que se puede modificar la directiva para proteger la infraestructura contra amenazas y riesgos cambiantes de recursos mal configurados.

Asegúrese de que los equipos de operaciones de TI han implementado sistemas de supervisión automatizados para la infraestructura en la nube que capturen los datos pertinentes de los registros que necesita para evaluar los riesgos. Sea proactivo en la supervisión de estos sistemas para asegurar la pronta detección y mitigación de posibles infracciones de la directiva de supervisión y que su estrategia de supervisión esté en línea con las necesidades de implementación y configuración.

## <a name="violation-triggers-and-enforcement-actions"></a>Desencadenadores de infracción y acciones de cumplimiento

Dado que el incumplimiento de las directivas de configuración puede dar lugar a riesgos de interrupción de los servicios críticos, el equipo de gobernanza de la nube debe tener visibilidad sobre las infracciones graves de la directiva. Asegúrese de que el personal de TI tiene rutas de escalación claras para notificar problemas de cumplimiento de la configuración a los miembros del equipo de gobernanza más adecuados para identificar y comprobar que se han mitigado los problemas de la directiva una vez detectados.

Cuando se detectan infracciones, debe realizar acciones para volver a alinearse con la directiva lo antes posible. El equipo de TI puede automatizar la mayoría de los desencadenadores de infracción con las herramientas descritas en [Deployment Acceleration toolchain for Azure](./toolchain.md) (Cadena de herramientas de aceleración de la implementación para Azure).

Los siguientes desencadenadores y acciones de cumplimiento son ejemplos que puede usar al analizar cómo usar los datos de supervisión para resolver las infracciones de directivas:

- **Se han detectado cambios inesperados en la configuración.** Si la configuración de un recurso cambia de forma inesperada, trabaje con los propietarios de la carga de trabajo y el personal de TI para identificar la causa raíz y desarrollar un plan de corrección.
- **La configuración de nuevos recursos no se adhiere a la directiva.** Trabaje con los equipos de DevOps y los propietarios de la carga de trabajo para revisar las directivas de aceleración de la implementación durante el inicio del proyecto para que todos los implicados entiendan los requisitos correspondientes de la directiva.
- **Los errores de implementación o problemas de configuración provocan retrasos en las programaciones del proyecto.** Trabaje con los equipos de desarrollo y los propietarios de la carga de trabajo para asegurarse de que el equipo entienda cómo automatizar la implementación de recursos basados en la nube para lograr coherencia y capacidad de repetición. Se deben requerir las implementaciones completamente automatizadas al principio del ciclo de desarrollo. Si se hace más tarde durante el ciclo de desarrollo, normalmente da lugar a problemas y retrasos inesperados.

## <a name="next-steps"></a>Pasos siguientes

Mediante la [plantilla de Cloud Management](./template.md), documente los procesos y desencadenadores que se alinean con el plan de adopción de la nube actual.

Para obtener instrucciones sobre cómo ejecutar directivas de administración en la nube de conformidad con los planes de adopción, consulte el artículo sobre la mejora de la disciplina.

> [!div class="nextstepaction"]
> [Mejora de la disciplina de aceleración de la implementación](./discipline-improvement.md)
