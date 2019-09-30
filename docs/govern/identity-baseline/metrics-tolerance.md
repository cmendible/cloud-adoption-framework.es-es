---
title: Métricas, indicadores y tolerancia al riesgo de la línea de base de identidad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Métricas, indicadores y tolerancia al riesgo de la línea de base de identidad
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: bf929fe5f1addbb27da77b865dfbdc71253c62a3
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71220438"
---
# <a name="identity-baseline-metrics-indicators-and-risk-tolerance"></a>Métricas, indicadores y tolerancia al riesgo de la línea de base de identidad

Este artículo le ayudará a cuantificar la tolerancia al riesgo de la empresa en relación con la línea de base de identidad. La definición de métricas e indicadores le ayudará a crear un caso de negocio de inversión en la madurez de la materia de línea de base de identidad.

## <a name="metrics"></a>Métricas

La línea de base de identidad se centra en la identificación, autenticación y autorización de usuarios, grupos de usuarios o procesos automatizados, y proporcionarles acceso adecuado a los recursos en las implementaciones de nube. Como parte del análisis de riesgos, querrá recopilar datos de análisis relacionados con los servicios de identidad para determinar cuánto riesgo enfrenta, y cuán importante es la inversión en la gobernanza de la línea de base de identidad para las implementaciones en la nube planeadas.

Los siguientes son ejemplos de métricas útiles que debe reunir para ayudar a evaluar la tolerancia al riesgo en la materia de la línea de base de identidad:

- **Tamaño de los sistemas de identidad.** Número total de usuarios, grupos u otros objetos administrados a través de sus sistemas de identidad.
- **Tamaño general de la infraestructura de servicios de directorio.** Número de bosques de directorio, dominios e inquilinos usados por la organización.
- **Dependencia de los mecanismos de autenticación heredados o locales.** Número de cargas de trabajo que dependen de los mecanismos de autenticación heredados o servicios de autenticación multifactor de terceros.
- **Extensión de los servicios de directorio implementados en la nube.** Número de bosques de directorio, dominios e inquilinos implementados en la nube.
- **Servidores de Active Directory implementados en la nube.** Número de servidores de Active Directory implementados en la nube.
- **Unidades organizativas implementadas en la nube.** Número de unidades organizativas de Active Directory implementadas en la nube.
- **Extensión de la federación.** Número de sistemas de línea de base de identidad federados con sistemas de la organización.
- **Usuarios con privilegios.** Número de cuentas de usuario con acceso con privilegios elevados a recursos o herramientas de administración.
- **Uso del control de acceso basado en rol.** Número de suscripciones, grupos de recursos o recursos individuales que no se administran mediante el control de acceso basado en rol (RBAC) a través de los grupos.
- **Notificaciones de autenticación.** Número de intentos de autenticación de usuario correctos e incorrectos.
- **Notificaciones de autorización.** Número de intentos correctos e incorrectos de los usuarios por acceder a los recursos.
- **Cuentas en peligro.** Número de cuentas de usuario que podrían estar en peligro.

## <a name="risk-tolerance-indicators"></a>Indicadores de tolerancia al riesgo

Los riesgos relacionados con la línea de base de identidad se relacionan en gran medida con la complejidad de la infraestructura de identidades de su organización. Si todos los usuarios y grupos se administran mediante un único directorio o proveedor de identidad nativo en la nube con una integración mínima con otros servicios, el nivel de riesgo probablemente sea pequeño. Sin embargo, a medida que aumenten las necesidades empresariales, puede que los sistemas de línea de base de identidad deban admitir escenarios más complicados, como varios directorios para admitir su organización interna o la federación con proveedores de identidades externos. A medida que esos sistemas se vuelven más complejos, aumenta el riesgo.

En las primeras fases de adopción de la nube, trabaje con el equipo de seguridad de TI y las partes interesadas de la empresa para identificar [riesgos de negocio](./business-risks.md) relacionados con la identidad y, luego, determine una línea de base aceptable para la tolerancia al riesgo de identidad. En esta sección de Cloud Adoption Framework se proporcionan ejemplos, pero los riesgos y las bases de referencia específicos de su empresa o sus implementaciones pueden ser diferentes.

Una vez que tenga una base de referencia, establezca bancos de pruebas mínimos que representen un aumento inaceptable de los riesgos identificados. Estos bancos de pruebas actúan como desencadenadores cuando necesite tomar medidas para abordar estos riesgos. En los siguientes ejemplos, se muestra cómo las métricas relacionadas con la identidad, como las descritas anteriormente, pueden justificar una mayor inversión en la materia de línea de base de identidad.

- **Desencadenador de número de cuentas de usuario.** Una empresa con más de _x_ usuarios, grupos u otros objetos administrados en sus sistemas de identidad puede beneficiarse de la inversión en la materia de la línea de base de identidad para asegurarse una gobernanza eficaz en un gran número de cuentas.
- **Desencadenador de dependencia de identidades locales.** Una empresa que planea migrar cargas de trabajo a la nube y requiere funcionalidades de autenticación heredadas o autenticación multifactor de terceros debe invertir en la materia de línea de base de identidad para reducir los riesgos relacionados con la refactorización o la implementación de infraestructura de nube adicional.
- **Desencadenador de complejidad de servicios de directorio.** Una empresa que mantiene más de _x_ bosques, dominios o inquilinos de directorio individuales debe invertir en la materia de línea de base de identidad para reducir los riesgos relacionados con la administración de cuentas y los problemas de eficiencia relacionados con varias credenciales de usuario repartidas entre varios sistemas.
- **Desencadenador de servicios de directorio hospedados en la nube.** Una empresa que hospeda _x_ máquinas virtuales en servidores Active Directory hospedadas en la nube, o tiene _x_ unidades organizativas administradas en estos servidores basados en la nube, puede beneficiarse de la inversión en la materia de línea de base de identidad para optimizar la integración con cualquier servicio de identidad local o externo.
- **Desencadenador de federación.** Una empresa que implementa la federación de identidades con _x_ sistemas de línea de base de identidad externos puede beneficiarse de la inversión en la materia de línea de base de identidad para garantizar una directiva de la organización coherente entre los miembros de la federación.
- **Desencadenador de acceso con privilegios elevados.** Una empresa con más del _x %_ de los usuarios con permisos elevados administrar herramientas y recursos debería plantearse invertir en la materia de línea de base de identidad para minimizar el riesgo de sobreaprovisionamiento involuntario del acceso a los usuarios.
- **Desencadenador de RBAC.** Una empresa con menos del _x %_ de los recursos con métodos de control de acceso basado en roles debería plantearse invertir en la materia de línea de base de identidad para identificar maneras optimizadas de asignar el acceso de los usuarios a los recursos.
- **Desencadenador de errores de autenticación.** Una empresa donde los errores de autenticación representan más del _x %_ de los intentos debe invertir en la materia de línea de base de identidad para asegurarse de que los métodos de autenticación no estén bajo un ataque externo, y de que los usuarios puedan usar los métodos de autenticación correctamente.
- **Desencadenador de errores de autorización.** Una empresa donde los intentos de acceso se rechazan más del _x %_ de las veces debe invertir en la materia de línea de base de identidad para mejorar la aplicación y la actualización de los controles de acceso, e identificar intentos de acceso potencialmente malintencionados.
- **Desencadenador de cuentas en peligro.** Una empresa con más de 1 cuenta en peligro debe invertir en la materia de línea de base de identidad para mejorar la eficacia y la seguridad de los mecanismos de autenticación, y mejorar los mecanismos para remediar los riesgos relacionados con las cuentas en peligro.

Las métricas y desencadenadores exactos que use para medir la tolerancia al riesgo y el nivel de inversión en la materia de línea de base de identidad serán específicos para su organización, pero los ejemplos anteriores deberían servir como base útil para las conversaciones con su equipo de gobernanza de la nube.

## <a name="next-steps"></a>Pasos siguientes

Use la [plantilla de administración de la nube](./template.md) para documentar las métricas y los indicadores de tolerancia que están en línea con el plan de adopción de la nube actual.

Revise las directivas de línea de base de identidad como punto de partida para desarrollar directivas que aborden los riesgos empresariales específicos en línea con los planes de adopción de la nube.

> [!div class="nextstepaction"]
> [Revisión de las directivas de ejemplo](./policy-statements.md)
