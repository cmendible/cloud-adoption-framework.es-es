---
title: Motivaciones y riesgos empresariales de la base de referencia de la identidad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Motivaciones y riesgos empresariales de la base de referencia de la identidad
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 9c838063c77b02af4ec86187854a15d93b2998ef
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031396"
---
# <a name="identity-baseline-motivations-and-business-risks"></a>Motivaciones y riesgos empresariales de la base de referencia de la identidad

En este artículo se describen las razones por las que los clientes normalmente adoptan una materia sobre la base de referencia de la identidad dentro de una estrategia de gobernanza de la nube. También se proporcionan algunos ejemplos de riesgos empresariales que impulsan las declaraciones de directivas.

<!-- markdownlint-disable MD026 -->

## <a name="is-identity-baseline-relevant"></a>¿Es pertinente una base de referencia de la identidad?

Los directorios locales tradicionales están diseñados para permitir a las empresas controlar estrictamente los permisos y directivas de usuarios, grupos y roles dentro de sus redes internas y centros de datos. Normalmente, esto está pensado para facilitar implementaciones de un solo inquilino, con servicios aplicables únicamente en el entorno local.

Los servicios de identidad de la nube están pensados para expandir las funcionalidades de autenticación y control de acceso de una organización a Internet. Admiten la existencia de varios inquilinos y se pueden usar para administrar usuarios y la directiva de acceso en todas las aplicaciones en la nube y las implementaciones. Las plataformas de nube pública disponen de una clase de servicios de identidad nativos para la nube que admiten tareas de administración e implementación, y que son capaces de [variar los niveles de integración](../../decision-guides/identity/index.md) con las soluciones de identidad locales existentes. Puede que todas estas características den lugar a que la directiva de identidad de la nube sea más compleja de lo que requieren sus soluciones locales tradicionales.

La importancia de la materia sobre la base de referencia de la identidad para su implementación de la nube dependerá del tamaño de su equipo y de la necesidad de integrar la solución de identidad basada en la nube con un servicio de identidad local existente. Puede que las implementaciones de prueba iniciales no requieran mucho de organización o administración por parte del usuario pero, a medida que el patrimonio de la nube evoluciona, necesitará probablemente dar cabida a una integración organizativa y administración centralizada más complejas.

## <a name="business-risk"></a>Riesgo empresarial

La materia sobre la base de referencia de la identidad intenta dar respuesta a los principales riesgos empresariales relacionados con los servicios de identidad y el control de acceso. Trabaje con su empresa para identificar estos riesgos y supervise cada uno de ellos para determinar su pertinencia a medida que planee y aplique sus implementaciones en la nube.

Los riesgos variarán según la organización, pero los siguientes pueden servir como ejemplos de riesgos habituales relacionados con la identidad que puede usar como punto de partida para su análisis en el seno de su equipo de gobernanza de la nube:

- **Acceso no autorizado.** El acceso de usuarios no autorizados a información y recursos confidenciales puede provocar pérdidas de datos o interrupciones del servicio, infracciones del perímetro de seguridad de la organización y poner en riesgo responsabilidades empresariales o legales.
- **Ineficacia debida a la existencia de varias soluciones de identidad.** Las organizaciones con varios inquilinos de servicios de identidad pueden requerir varias cuentas para los usuarios. Esto puede provocar ineficacias para los usuarios, ya que tienen que recordar varios juegos de credenciales, y para TI a la hora de administrar las cuentas en varios sistemas. Si no se actualizan las asignaciones de acceso de los usuarios en todas las soluciones de identidad a medida que cambia el personal, los equipos y los objetivos empresariales, los recursos en la nube serán susceptibles de un acceso no autorizado o los usuarios no podrán acceder a determinados recursos necesarios.
- **Imposibilidad de compartir recursos con asociados externos.** Las dificultades para agregar asociados comerciales externos a las soluciones de identidad existentes pueden impedir un uso compartido de los recursos y una comunicación empresarial eficaces.
- **Dependencias de identidad locales.** Puede que los mecanismos de autenticación heredados o la autenticación multifactor de terceros no esté disponible en la nube, lo cual hará que sea necesario adaptar la migración de las cargas de trabajo o que se deban implementar servicios de identidad adicionales en la nube. Cualquiera de estos requisitos podría retrasar o incluso impedir la migración, con el consiguiente aumento de los costos.

## <a name="next-steps"></a>Pasos siguientes

Utilice la [plantilla de administración de la nube](./template.md) para documentar los riesgos empresariales que probablemente se presentarán en el plan de adopción de la nube actual.

Una vez que se consigue una comprensión realista de los riesgos empresariales, el siguiente paso es documentar la tolerancia al riesgo de la empresa y los indicadores y métricas clave para supervisar esa tolerancia.

> [!div class="nextstepaction"]
> [Descripción de indicadores, métricas y tolerancia al riesgo](./metrics-tolerance.md)
