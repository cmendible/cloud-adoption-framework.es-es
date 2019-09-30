---
title: Métricas de aceleración de la implementación, indicadores y tolerancia al riesgo
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Métricas de aceleración de la implementación, indicadores y tolerancia al riesgo
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: d7a7965acb7b1ace74983c7d0e1e65c3d47b2cc5
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71220711"
---
# <a name="deployment-acceleration-metrics-indicators-and-risk-tolerance"></a>Métricas de aceleración de la implementación, indicadores y tolerancia al riesgo

Este artículo le ayudará a cuantificar la tolerancia al riesgo de la empresa en relación con la aceleración de la implementación. La definición de métricas e indicadores le ayudará a crear un caso de negocio de inversión en el desarrollo de la disciplina de aceleración de la implementación.

## <a name="metrics"></a>Métricas

La materia de aceleración de la implementación se centra en los riesgos relacionados con la configuración, implementación, actualización y mantenimiento de los recursos en la nube. La siguiente información es útil al adoptar esta disciplina de gobernanza en la nube:

- **Errores de implementación.** Porcentaje de implementaciones que generan errores o producen recursos mal configurados.
- **Tiempo de implementación.** La cantidad de tiempo que se necesita para implementar las actualizaciones en un sistema existente.
- **Recursos fuera de cumplimiento.** El número o porcentaje de recursos que no cumplen con las directivas definidas.

## <a name="risk-tolerance-indicators"></a>Indicadores de tolerancia al riesgo

Los riesgos relacionados con la aceleración de la implementación están, en gran medida, relacionados con el número y la complejidad de los sistemas basados en la nube implementados para la empresa. A medida que crece su entorno de nube, aumentará el número de sistemas implementados y la frecuencia de actualización de los recursos de nube. Las dependencias entre recursos aumentan la importancia de garantizar la correcta configuración de los recursos y el diseño de los sistemas para lograr resistencia si uno o varios recursos experimentan tiempos de inactividad inesperados.

<!-- "en-us" location is required for the URL below. -->

A menudo, las organizaciones de TI corporativas tradicionales han aislado las operaciones, la seguridad y los equipos de desarrollo que no suelen colaborar o que incluso se encuentran enfrentados. Reconocer estos desafíos al principio e integrar partes interesadas clave de cada uno de los equipos puede ayudar a garantizar la agilidad en la adopción de la nube, mientras permanecen protegidos y bien controlados. Por tanto, debería considerar la posibilidad de adoptar una cultura organizativa DevOps o [DevSecOps](https://www.microsoft.com/en-us/securityengineering/devsecops) al principio del proceso de adopción de la nube. 

Trabaje con el equipo de DevSecOps y las partes interesadas de la empresa para identificar los [riesgos del negocio](./business-risks.md) relacionados con la configuración, luego determine una línea de base aceptable para la tolerancia al riesgo de la configuración. En esta sección de la guía Cloud Adoption Framework se proporcionan ejemplos, pero los riesgos y las bases de referencia específicos de su empresa o sus implementaciones serán diferentes.

Una vez que tenga una base de referencia, establezca bancos de pruebas mínimos que representen un aumento inaceptable de los riesgos identificados. Estos bancos de pruebas actúan como desencadenadores cuando se necesita tomar medidas para corregir estos riesgos. En los siguientes ejemplos, se muestra cómo las métricas relacionadas con la configuración, como las descritas anteriormente, pueden justificar una mayor inversión en la disciplina de aceleración de la implementación.

- **Desencadenadores de desfase de configuración:** Una compañía que experimente cambios inesperados en la configuración de los componentes clave del sistema o errores en la implementación o las actualizaciones de sus sistemas, debe invertir en la disciplina de aceleración de la implementación para identificar las causas raíz y los pasos de corrección.
- **Desencadenadores de no cumplimiento:** Si el número de recursos fuera de cumplimiento supera un umbral definido (ya sea como un número total de recursos o un porcentaje del total de recursos), la compañía debe invertir en mejoras de la disciplina de aceleración de la implementación para asegurarse de que la configuración de cada recurso permanece en cumplimiento a lo largo del ciclo de vida de ese recurso.
- **Desencadenadores de programación de proyecto:** Si el tiempo para implementar los recursos y aplicaciones de la compañía suele superar un umbral definido, la compañía debe invertir en los procesos de aceleración de la implementación para introducir o mejorar la coherencia y previsibilidad de las implementaciones automatizadas. Los tiempos de implementación, medidos en días o incluso semanas, suelen indicar una estrategia de aceleración de la implementación poco óptima.

## <a name="next-steps"></a>Pasos siguientes

Use la [plantilla de administración de la nube](./template.md) para documentar las métricas y los indicadores de tolerancia que están en línea con el plan de adopción de la nube actual.

Revise las directivas de aceleración de la implementación como punto de partida para desarrollar directivas que aborden los riesgos empresariales específicos en línea con los planes de adopción de la nube.

> [!div class="nextstepaction"]
> [Revisión de las directivas de ejemplo](./policy-statements.md)
