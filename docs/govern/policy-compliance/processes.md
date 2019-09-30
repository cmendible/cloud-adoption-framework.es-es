---
title: Establecimiento de procesos de adhesión a directivas
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Establezca procesos para garantizar el cumplimiento de las directivas corporativas.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: f6104a3b2f5f2e68016623029ac0e7b71a5e35f1
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222049"
---
<!-- markdownlint-disable MD026 -->

# <a name="establish-policy-adherence-processes"></a>Establecimiento de procesos de adhesión a directivas

Después de establecer las instrucciones de la directiva de la nube y redactar una guía de diseño, deberá crear una estrategia para garantizar que su implementación de la nube cumpla con los requisitos de la directiva. Esta estrategia debe abarcar los procesos de comunicación y revisión en curso del equipo de gobernanza de la nube, establecer criterios para cuando las infracciones de las directivas requieran medidas y definir los requisitos para los sistemas automatizados de supervisión y cumplimiento que van a detectar las infracciones y desencadenar las medidas correctoras.

Vea las secciones de directivas corporativas de las [guías prácticas de gobernanza](../guides/index.md) para obtener ejemplos de cómo el proceso de adhesión a las directivas encaja en un plan de gobernanza de la nube.

## <a name="prioritize-policy-adherence-processes"></a>Clasificación de los procesos de adhesión a las directivas

¿Cuánta inversión en el desarrollo de procesos se requiere para apoyar los objetivos de la directiva? Dependiendo del tamaño y la madurez de la implementación de la nube, el esfuerzo requerido para establecer procesos que admitan el cumplimiento, y los costos asociados con este esfuerzo, pueden variar ampliamente.

Para implementaciones pequeñas que consisten en recursos de desarrollo y de prueba, los requisitos de las directivas pueden ser simples y requerir pocos recursos dedicados para abordarlos. Por otro lado, una implementación en la nube madura y crítica con necesidades de seguridad y rendimiento de alta prioridad puede requerir un equipo de personal, amplios procesos internos y herramientas de supervisión personalizadas para respaldar los objetivos de las directivas.

Como primer paso para definir la estrategia de adherencia a la directiva, evalúe cómo los procesos que se discuten a continuación pueden respaldar los requisitos de la directiva. Determine cuánto esfuerzo vale la pena invertir en estos procesos y después utilice esta información para establecer un presupuesto realista y planes de personal para satisfacer estas necesidades.

## <a name="establish-cloud-governance-team-processes"></a>Establecimiento de procesos del equipo de gobernanza de la nube

Antes de definir los desencadenadores para la corrección del cumplimiento de las directivas, debe establecer los procesos generales que va a usar el equipo y cómo se va a compartir y escalar la información entre el personal de TI y el equipo de gobernanza de la nube.

### <a name="assign-cloud-governance-team-members"></a>Asignación de miembros al equipo de gobernanza de la nube

El equipo de gobernanza de la nube va a proporcionar orientación continua sobre el cumplimiento de las directivas y se va a ocupar de los problemas relacionados con estas que surjan durante la implementación y el funcionamiento de los recursos de la nube. Al crear este equipo, invite a personal de la organización con experiencia en áreas incluidas en las declaraciones de las directivas definidas y en los riesgos identificados.

Para las implementaciones de pruebas iniciales, esto puede limitarse a unos pocos administradores de sistemas responsables de establecer las bases de la gobernanza. A medida que maduren los procesos de gobernanza, revise regularmente los miembros del equipo de gobernanza de la nube para asegurarse de que puede abordar adecuadamente los posibles nuevos riesgos y los requisitos de las directivas. Identifique a los miembros del personal de TI y empresarial con experiencia de relevancia o interés en áreas específicas de gobernanza e inclúyalos en los equipos de forma permanente o ad hoc, según sea necesario.

### <a name="reviews-and-policy-iteration"></a>Revisiones e iteración de directivas

A medida que se implementan recursos y cargas de trabajo adicionales, el equipo de gobernanza de la nube debe asegurarse de que las nuevas cargas de trabajo o los recursos cumplan los requisitos de las directivas. Evalúe los nuevos requisitos de los equipos de desarrollo de cargas de trabajo para asegurarse de que sus implementaciones planeadas se alinean con las guías de diseño y actualice las directivas para admitir estos requisitos cuando sea necesario.

Planee la evaluación de nuevos riesgos potenciales y la actualización de las declaraciones de las directivas y las guías de diseño cuando sea necesario. Trabaje con el personal de TI y los equipos de cargas de trabajo para evaluar las nuevas características y los servicios de Azure de manera continua. Además, programe ciclos regulares de revisión de las cinco materias de gobernanza para asegurar que las directivas estén actualizadas y se cumplan.

### <a name="education"></a>Educación

El cumplimiento de las directivas requiere que el personal de TI y los desarrolladores comprendan los requisitos de las directivas que afectan a sus áreas de responsabilidad. Planee dedicar recursos a documentar las decisiones y los requisitos, y eduque a todos los equipos pertinentes sobre las guías de diseño que respaldan los requisitos de la directiva.

A medida que cambien las directivas, actualice regularmente la documentación y los materiales de aprendizaje, y asegúrese de que los esfuerzos educativos comuniquen los requisitos actualizados y la guía al personal de TI pertinente.

En varias fases del recorrido en la nube, es posible que le resulte más conveniente consultar con asociados y programas de aprendizaje profesional para mejorar la formación de su equipo, técnica y procedimentalmente. Además, muchos consideran los certificados formales como una valiosa adición a la cartera de formación que se debe tener en cuenta.

### <a name="establish-escalation-paths"></a>Establecimiento de las rutas de escalado

Si un recurso no cumple con las normas, ¿a quién se le notifica? Si el personal de TI detecta un problema de cumplimiento de directivas, ¿con quién se ponen en contacto? Asegúrese de que el proceso de escalado al equipo de gobernanza de la nube está claramente definido. Asegúrese de que estos canales de comunicación se mantengan actualizados para reflejar los cambios del personal y de la organización.

## <a name="violation-triggers-and-actions"></a>Desencadenadores y acciones de infracciones

Después de definir el equipo de gobernanza de la nube y sus procesos, debe definir explícitamente lo que se consideran infracciones de cumplimiento que desencadenan acciones, y cuáles deben ser esas acciones.

### <a name="define-triggers"></a>Definición de desencadenadores

Para cada una de sus declaraciones de directiva, revise los requisitos para determinar qué constituye una infracción de la directiva. Genere los desencadenadores con la información que ya ha establecido como parte del proceso de definición de directivas.

- **Tolerancia a riesgos:** cree desencadenadores de infracción basados en las métricas y los indicadores de riesgo establecidos como parte del [análisis de tolerancia al riesgo](./risk-tolerance.md).
- **Requisitos de directivas definidos:** las declaraciones de directivas pueden proporcionar requisitos de contrato de nivel de servicio (SLA), continuidad empresarial y recuperación ante desastres (BRCD) o rendimiento que deben usarse como base para los desencadenadores de cumplimiento.

### <a name="define-actions"></a>Definición de acciones

Cada desencadenador de infracción debe tener una acción correspondiente. Las acciones desencadenadas siempre deben informar a un miembro del personal de TI o del equipo de gobernanza de la nube cuando se produce una infracción. Esta notificación puede llevar a una revisión manual del problema de cumplimiento o iniciar un proceso de corrección preestablecido, en función del tipo y la gravedad de la infracción detectada.

Algunos ejemplos de desencadenadores y acciones de infracciones:

| Materia de gobernanza en la nube | Desencadenador de ejemplo | Acción de ejemplo |
|-----------------------------|----------------|---------------|
| Administración de costos | El gasto mensual en la nube es más de un 20 % mayor de lo esperado. | Notifique al responsable de la unidad de facturación quién comenzará una revisión de la utilización de los recursos. |
| Línea de base de seguridad | Detecte actividad sospechosa de inicio de sesión de usuario. | Notifique al equipo de seguridad de TI y deshabilite la cuenta de usuario sospechosa. |
| Coherencia de recursos | La utilización de la CPU para la carga de trabajo es superior al 90 %. | Notifique al equipo de operaciones de TI y amplíe los recursos adicionales para manejar la carga. |

## <a name="monitoring-and-compliance-automation"></a>Automatización de la supervisión y cumplimiento

Después de haber definido los desencadenadores y las acciones de las infracciones de cumplimiento, puede empezar a planear la mejor manera de utilizar las herramientas de registro y generación de informes y otras funciones de la plataforma de nube para ayudar a automatizar la estrategia de supervisión y cumplimiento de directivas.

Vea el tema [Guía de decisiones sobre registros e informes](../../decision-guides/logging-and-reporting/index.md) del Marco de adopción de la nube para obtener orientación a fin de elegir el mejor patrón de supervisión para la implementación.

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre el cumplimiento normativo en la nube.

> [!div class="nextstepaction"]
> [Cumplimiento normativo](./regulatory-compliance.md)
