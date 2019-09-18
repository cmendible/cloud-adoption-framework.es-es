---
title: Procesos de cumplimiento de la directiva de la base de referencia de identidad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Procesos de cumplimiento de la directiva de la base de referencia de identidad
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: f391f8233aa425ccf0ff61e625a2575fb9450b88
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031892"
---
# <a name="identity-baseline-policy-compliance-processes"></a>Procesos de cumplimiento de la directiva de la base de referencia de identidad

En este artículo se describe un enfoque de los procesos de cumplimiento de directivas que rigen la directiva de la [base de referencia de identidad](./index.md). La gobernanza eficaz de la identidad empieza con procesos manuales periódicos que guían la adopción y las revisiones de la directiva de identidad. Esto requiere la participación regular del equipo de gobernanza de la nube y las partes interesadas de TI y de la empresa para revisar y actualizar la directiva y garantizar el cumplimiento de esta. Además, muchos procesos de aplicación y supervisión en curso se pueden automatizar o complementar con herramientas para reducir la sobrecarga de la gobernanza y permitir una respuesta más rápida a la desviación de directivas.

## <a name="planning-review-and-reporting-processes"></a>Procesos de planeación, revisión y generación de informes

Las herramientas de administración de identidades ofrecen funcionalidades y características que facilitan en gran medida la administración de usuarios y el control de acceso en una implementación en la nube. No obstante, también se requieren procesos y directivas bien diseñados y planeados para apoyar los objetivos de la organización. El siguiente es un conjunto de procesos de ejemplo que normalmente están incluidos en la materia sobre la base de referencia de la identidad. Use estos ejemplos como punto de partida al planear los procesos que le permitirán continuar actualizando la directiva de identidad en función de los cambios que se produzcan en la empresa y los comentarios de los equipos de TI cuya tarea es la activación de la guía de gobernanza.

**Planeamiento y evaluación inicial de los riesgos:** como parte de la adopción inicial de la materia sobre la base de referencia de la identidad, identifique los principales riesgos empresariales y las tolerancias relacionadas con la administración de identidades en la nube. Esta información se usa para analizar riesgos técnicos concretos con los miembros de los equipos de TI responsables de la administración de los servicios de identidad, y para desarrollar un conjunto de referencia de directivas de seguridad para mitigar esos riesgos, con el fin de establecer la estrategia de gobernanza inicial.

**Planeación de la implementación:** Antes de realizar cualquier implementación, revise las necesidades de acceso de todas las cargas de trabajo y desarrolle una estrategia de control de acceso que se adapte a la directiva de identidad corporativa establecida. Documente cualquier desajuste entre las necesidades y la directiva actual para determinar si se requieren actualizaciones de la directiva y modifíquela si es necesario.

**Pruebas de la implementación:** como parte del proceso de implementación, el equipo de gobernanza de la nube en colaboración con los equipos de TI encargados de los servicios de identidad son responsables de revisar la implementación para validar el cumplimiento de la directiva de seguridad.

**Planeación anual:** realice todos los años una revisión de alto nivel de la estrategia de administración de identidades. Explore los cambios planeados para el entorno de servicios de identidad y las estrategias actualizadas de adopción de la nube para identificar un posible aumento del riesgo o la necesidad de modificar los patrones actuales de la infraestructura de identidades. También puede usar este tiempo para revisar los procedimientos recomendados de administración de identidades más recientes e integrarlos en sus directivas y procesos de revisión.

**Planeación trimestral:** de forma trimestral, efectúe una revisión general de los datos de auditoría de identidades y de control de acceso, y reúnase con los equipos de adopción de la nube para identificar nuevos riesgos o requisitos operativos que requieran actualizar la directiva de identidad o cambiar la estrategia de control de acceso.

Este proceso de planeamiento también es un buen momento para evaluar a los miembros actuales del equipo de gobernanza de la nube, por si hubiera carencias de conocimientos relacionadas con una directiva nueva o cambiante, y con los riesgos relacionados con la identidad. Invite al personal de TI pertinente a participar en las revisiones y el planeamiento como asesores técnicos temporales o miembros permanentes del equipo.

**Educación y aprendizaje:** ofrezca sesiones de aprendizaje con carácter bimensual para asegurarse de que tanto los desarrolladores como el personal de TI están al día de los requisitos más recientes de las directivas de identidad. Como parte de este proceso, revise y actualice cualquier documentación, guía u otros recursos de aprendizaje para asegurarse de que estén sincronizados con las declaraciones de directiva corporativa más recientes.

**Auditoría mensual y revisiones de informes:** realice una auditoría mensual de todas las implementaciones de la nube para garantizar su alineación continuada con la directiva de identidad. Use este proceso de revisión para comprobar el acceso de los usuarios en relación con los cambios en la empresa para asegurarse de que los usuarios tienen el acceso correcto a los recursos en la nube, y para asegurarse de que las estrategias de acceso, como RBAC, se siguen de forma coherente. Identifique todas las cuentas con privilegios elevados y documente su finalidad. El resultado de este proceso de revisión es un informe para el equipo de estrategia de la nube y para cada equipo de adopción de la nube en el que se detalla la adhesión general a la directiva. El informe también se almacena con fines de auditoría y legales.

## <a name="ongoing-monitoring-processes"></a>Procesos de supervisión en curso

La determinación de si la estrategia de gobernanza de la identidad es correcta depende de la visibilidad de los estados actual y pasado de los sistemas de identidades. Sin la capacidad para analizar las métricas pertinentes de la implementación de la nube y los datos relacionados, no se pueden identificar cambios en los riesgos ni detectar infracciones de las tolerancias al riesgo. Los procesos de gobernanza en curso que se analizaron anteriormente requieren datos de calidad para asegurarse de que se puede modificar la directiva para adaptarse a las necesidades cambiantes de su negocio.

Asegúrese de que los equipos de TI han implementado sistemas de supervisión automatizados para los servicios de identidad que capturan los registros y la información de auditoría que necesita para evaluar los riesgos. Sea proactivo en la supervisión de estos sistemas para asegurar la pronta detección y mitigación de posibles infracciones de la directiva, y cerciórese de que cualquier cambio en la infraestructura de identidad queda reflejado en su estrategia de supervisión.

## <a name="violation-triggers-and-enforcement-actions"></a>Desencadenadores de infracción y acciones de cumplimiento

Las infracciones de la directiva de identidad pueden provocar accesos no autorizados a información confidencial y producir daños importantes en servicios y aplicaciones críticos. Cuando se detectan infracciones, debe realizar acciones para volver a alinearse con la directiva lo antes posible. El equipo de TI puede automatizar la mayoría de los desencadenadores de infracciones mediante las herramientas que se describen en la [cadena de herramientas sobre la base de referencia de la identidad](./toolchain.md).

Los siguientes desencadenadores y acciones de cumplimiento son ejemplos que puede consultar para planear cómo usar los datos de supervisión para resolver las infracciones de directivas:

- **Se ha detectado una actividad sospechosa:** los inicios de sesión de usuarios desde direcciones IP de proxy anónimo, ubicaciones desconocidas o los inicios de sesión desde ubicaciones sorprendentemente distantes pueden indicar una posible vulneración de la cuenta o un intento de acceso malintencionado. El inicio de sesión se bloqueará hasta que se pueda verificar la identidad del usuario y restablecer la contraseña.
- **Se han filtrado credenciales de usuario:** Las cuentas cuyo nombre de usuario y contraseña se filtren a Internet se deshabilitarán hasta que se pueda verificar la identidad del usuario y restablecer la contraseña.
- **Se han detectado controles de acceso insuficientes:** Aquellos recursos protegidos en los que las restricciones de acceso no reúnen los requisitos de seguridad tendrán bloqueado el acceso hasta que lo sí hagan.

## <a name="next-steps"></a>Pasos siguientes

Mediante la [plantilla de Cloud Management](./template.md), documente los procesos y desencadenadores que se alinean con el plan de adopción de la nube actual.

Para obtener instrucciones acerca de cómo ejecutar directivas de administración en la nube de conformidad con los planes de adopción, consulte el artículo sobre la mejora de la materia.

> [!div class="nextstepaction"]
> [Mejora de la materia sobre la base de referencia de la identidad](./discipline-improvement.md)
