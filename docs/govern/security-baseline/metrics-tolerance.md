---
title: Métricas, indicadores y tolerancia al riesgo de la base de referencia de seguridad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Métricas, indicadores y tolerancia al riesgo de la base de referencia de seguridad
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: b8171839b79ffbe9e3849cf303180d1f1ee049f2
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71222838"
---
# <a name="security-baseline-metrics-indicators-and-risk-tolerance"></a>Métricas, indicadores y tolerancia al riesgo de la base de referencia de seguridad

Este artículo le ayudará a cuantificar la tolerancia al riesgo de la empresa en relación con la línea de base de Seguridad. La definición de métricas e indicadores le ayudará a crear un caso de negocio de inversión en la madurez de la materia de la base de referencia de seguridad.

## <a name="metrics"></a>Métricas

La base de referencia de seguridad, por lo general, se centra en identificar posibles vulnerabilidades en sus implementaciones en la nube. Como parte del análisis de riesgos, querrá recopilar datos relacionados con el entorno de seguridad para determinar cuánto riesgo enfrenta, y cuán importante es la inversión en la gobernanza de la base de referencia de seguridad para las implementaciones en la nube planeadas.

Cada organización tiene distintos entornos y requisitos de seguridad y diferentes orígenes potenciales de datos de seguridad. A continuación encontrará varios ejemplos de métricas útiles que debe recopilar, ya que le ayudarán a evaluar la tolerancia al riesgo en la materia sobre la base de referencia de la seguridad:

- **Clasificación de datos**: Número de servicios y datos almacenados en la nube que no están clasificados según las normas de privacidad, cumplimiento o impacto empresarial de su organización.
- **Número de almacenes de datos confidenciales**: Número de puntos de conexión de almacenamiento o bases de datos que contienen información confidencial y que deben protegerse.
- **Número de almacenes de datos sin cifrar**: Número de almacenes de datos confidenciales que no están cifrados.
- **Superficie expuesta a ataques**: Cuántos orígenes de datos, servicios y aplicaciones en total se hospedarán en la nube. ¿Qué porcentaje de estos orígenes de datos se clasifican como confidenciales? ¿Qué porcentaje de estas aplicaciones y servicios es crítico?
- **Estándares cubiertos**: Número de estándares de seguridad definidos por el equipo de seguridad.
- **Recursos cubiertos**: Recursos implementados que están cubiertos por los estándares de seguridad.
- **Cumplimiento general de estándares**: Tasa de cumplimiento de los estándares de seguridad.
- **Ataques por gravedad**: ¿Cuántos intentos de interrupción de los servicios hospedados en la nube, por ejemplo, mediante ataques de denegación de servicio distribuido (DDoS), experimenta su infraestructura? ¿Cuál es el tamaño y la gravedad de estos ataques?
- **Protección contra malware**: Porcentaje de máquinas virtuales implementadas que tienen todo el software antimalware, firewall u otro software de seguridad instalado.
- **Latencia de revisiones**: El tiempo que hace desde que se aplicaron las últimas revisiones de software y del sistema operativo a las máquinas virtuales.
- **Recomendaciones sobre estado de seguridad**: Número de recomendaciones de software de seguridad para resolver los estándares de mantenimiento para los recursos implementados, organizados por gravedad.

## <a name="risk-tolerance-indicators"></a>Indicadores de tolerancia al riesgo

Las plataformas en la nube proporcionan un conjunto básico de características que permiten a los equipos de implementaciones pequeñas configurar las opciones básicas de seguridad sin un planeamiento adicional amplio. Como resultado, las primeras cargas de trabajo experimentales o de desarrollo/pruebas pequeñas que no incluyen información confidencial representan un nivel de riesgo relativamente bajo, y probablemente no necesitarán demasiado en relación con la directiva formal de la base de referencia de seguridad. Sin embargo, en cuanto los datos importantes o la funcionalidad crítica se transfieren a la nube, los riesgos de seguridad aumentan, mientras que la tolerancia a dichos riesgos se reduce rápidamente. Cuantos más datos y funcionalidades se implementen en la nube, más deberá invertir en la materia de la base de referencia de seguridad.

En las primeras fases de adopción de la nube, trabaje con el equipo de seguridad de TI y las partes interesadas de la empresa para identificar [riesgos de negocio](./business-risks.md) relacionados con la seguridad y, luego, determine una línea de base aceptable para la tolerancia al riesgo de seguridad. En esta sección del marco de adopción de la nube se proporcionan ejemplos, pero los riesgos detallados y las bases de referencia para su empresa o sus implementaciones pueden ser diferentes.

Una vez que tenga una base de referencia, establezca bancos de pruebas mínimos que representen un aumento inaceptable de los riesgos identificados. Estos bancos de pruebas actúan como desencadenadores cuando necesita tomar medidas para poner remedio a estos riesgos. En los siguientes ejemplos, se muestra cómo las métricas relacionadas con la seguridad, como las descritas anteriormente, pueden justificar una mayor inversión en la materia de la base de referencia de seguridad.

- **Desencadenador de cargas de trabajo críticas**. Una empresa que implementa cargas de trabajo críticas en la nube debe invertir en la materia de la base de referencia de seguridad para evitar posibles interrupciones del servicio o la exposición de información confidencial.
- **Desencadenador de datos protegidos**. Una empresa que hospeda datos en la nube que se pueden clasificar como confidenciales, privados o sujetos a otras cuestiones legales. Necesitan una materia de base de referencia de seguridad para garantizar que estos datos no corran el peligro de pérdida, exposición o robo.
- **Desencadenador de ataques externos**. Una empresa que experimenta graves ataques contra su infraestructura _x_ veces al mes podría beneficiarse de la materia de la base de referencia de seguridad.
- **Desencadenador de cumplimiento de estándares**. Una empresa con más de un _x%_ de recursos que no cumplen los estándares de seguridad debe invertir en la materia de la base de referencia de seguridad para garantizar la aplicación coherente de los estándares en toda la infraestructura de TI.
- **Desencadenador de tamaño para recursos en la nube**. Una empresa que hospeda más de un número _x_ de aplicaciones, servicios u orígenes de datos. Las implementaciones grandes en la nube pueden beneficiarse de la inversión en la materia de la base de referencia de seguridad para garantizar que su superficie expuesta a ataques total esté bien protegida frente a accesos no autorizados u otras amenazas externas.
- **Desencadenador de cumplimiento de software de seguridad**. Una empresa en la que menos de un _x%_ de las máquinas virtuales implementadas tienen todo el software de seguridad necesario instalado. Se puede usar una materia de base de referencia de seguridad para garantizar que el software está instalado de forma coherente en todo el software.
- **Desencadenador de aplicación de revisiones**. Una empresa en la que a las máquinas virtuales o los servicios implementados no se les han aplicado revisiones de software o del sistema operativo durante los últimos _x_ días. Se puede usar una materia de base de referencia de seguridad para garantizar que la aplicación de revisiones esté actualizada dentro de una programación necesaria.
- **Centrado en la seguridad**. Algunas empresas tendrán estrictos requisitos de seguridad y confidencialidad de datos incluso para las cargas de trabajo de pruebas y experimentales. Estas empresas deberán invertir en la materia de la base de referencia de seguridad antes de iniciar las implementaciones.

Las métricas y desencadenadores exactos que use para medir la tolerancia al riesgo y el nivel de inversión en la materia de base de referencia de seguridad serán específicos para su organización, pero los ejemplos anteriores deberían servir como base útil para las conversaciones con su equipo de gobernanza en la nube.

## <a name="next-steps"></a>Pasos siguientes

Use la [plantilla de administración de la nube](./template.md) para documentar las métricas y los indicadores de tolerancia que están en línea con el plan de adopción de la nube actual.

Revise las directivas de línea de base de seguridad como punto de partida para desarrollar directivas que aborden riesgos de negocio específicos que se alineen con los planes de adopción de la nube.

> [!div class="nextstepaction"]
> [Revisión de las directivas de ejemplo](./policy-statements.md)
