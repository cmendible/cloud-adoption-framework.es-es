---
title: Primer proyecto de adopción de la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información sobre cómo implementar su primer proyecto de adopción de la nube.
author: BrianBlanchard
ms.author: brblanch
ms.date: 5/19/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.openlocfilehash: 590875a336b8af23723ab122e2af8f2290404ab3
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224137"
---
<!-- markdownlint-disable MD026 -->

# <a name="first-cloud-adoption-project"></a>Primer proyecto de adopción de la nube

El planeamiento de adopción de la nube conlleva una curva de aprendizaje y un compromiso de tiempo asociados. Incluso para los equipos experimentados, un planeamiento adecuado lleva tiempo: tiempo para alinear a las partes interesadas, tiempo para recopilar y analizar datos, tiempo para validar decisiones a largo plazo y tiempo para alinear a las personas, los procesos y la tecnología. En los esfuerzos de adopción más productivos, el planeamiento crece en paralelo con la adopción, mejorando con cada versión y con cada migración de la carga de trabajo a la nube. Es importante comprender la diferencia entre un plan de adopción de la nube y una estrategia de adopción de la nube. Se necesita una estrategia bien definida para facilitar y guiar la implementación de un plan de adopción de la nube.

En Cloud Adoption Framework para Azure se describen los procesos para la adopción de la nube y el funcionamiento de las cargas de trabajo hospedadas en la nube. Cada uno de los procesos de las fases de definición de la estrategia, planeamiento, preparación, adopción y operación requiere ampliar ligeramente los conocimientos técnicos, empresariales y operativos. Algunos de estos conocimientos pueden provenir de aprendizaje dirigido. No obstante, muchos de ellos se obtienen de forma más eficaz a través de la experiencia práctica.

Emprender un proceso de primera adopción en paralelo con el desarrollo del plan proporciona algunas ventajas:

- Establece una mentalidad de crecimiento que fomenta el aprendizaje y la exploración.
- Da al equipo la oportunidad de desarrollar los conocimientos necesarios.
- Crea situaciones que fomentan nuevos enfoques para la colaboración.
- Identifica carencias de conocimientos y posibles necesidades de asociación.
- Proporciona entradas tangibles al plan.

## <a name="first-project-criteria"></a>Criterios del primer proyecto

Su primer proyecto de adopción debe estar en línea con sus [motivaciones](./motivations.md) para la adopción de la nube. Siempre que sea posible, el primer proyecto también debe demostrar el progreso hacia un [resultado empresarial](./business-outcomes/business-outcome-template.md) definido.

## <a name="first-project-expectations"></a>Expectativas del primer proyecto

Lo más probable es que el proyecto de primera adopción del equipo dé lugar a una implementación de producción de algún tipo. Sin embargo, esto no siempre es así. Establezca las expectativas adecuadas cuanto antes. Estas son algunas de las expectativas que se recomienda establecer:

- Este proyecto es una fuente de aprendizaje.
- Este proyecto puede dar lugar a implementaciones de producción, pero probablemente requerirá un esfuerzo adicional antes.
- El resultado de este proyecto es un conjunto de requisitos claros para proporcionar una solución de producción a largo plazo.

## <a name="first-project-examples"></a>Ejemplos de primer proyecto

Para respaldar los criterios anteriores, esta lista proporciona un ejemplo de un primer proyecto para cada categoría de motivación:

- **Eventos empresariales críticos:** cuando un evento empresarial crítico es la motivación principal, la implementación de una herramienta como [Azure Site Recovery](../migrate/azure-migration-guide/migrate.md?tabs=Tools#azure-site-recovery) podría ser un buen primer proyecto. Durante la migración, puede usar esta herramienta para migrar rápidamente recursos de centros de datos. Sin embargo, durante el primer proyecto, podría usarla exclusivamente como herramienta de recuperación ante desastres, lo que reduce las dependencias de recursos de recuperación ante desastres en el centro de datos.

- **Motivaciones de migración:** cuando la migración es la motivación principal, es aconsejable empezar con la migración de una carga de trabajo no crítica. La [guía de preparación para Azure[ y la ](../migrate/azure-migration-guide/index.md)guía de migración a Azure](../ready/azure-readiness-guide/index.md) proporcionan instrucciones para la migración de la primera carga de trabajo.

- **Motivaciones de innovación:** cuando la innovación es la motivación principal, la creación de un entorno de desarrollo y pruebas de destino puede ser un excelente primer proyecto.

A continuación se incluyen otros ejemplos de proyectos de primera adopción:

- **Recuperación ante desastres y continuidad empresarial (DRBC):** además de Azure Site Recovery, puede implementar varias estrategias de recuperación ante desastres y continuidad empresarial como primer proyecto.
- **No producción:** implemente una instancia de no producción de una carga de trabajo.
- **Archivo:** el almacenamiento en frío puede suponer una carga excesiva para los recursos de los centros de datos. Trasladar los datos a la nube es una solución eficaz rápida.
- **Finalización del soporte técnico:** la migración de los recursos que han alcanzado la finalización del soporte técnico es otra ventaja rápida que genera conocimientos técnicos. También puede prevenir algunos costos de licencias o de contratos de soporte técnico costosos.
- **Interfaz de escritorio virtual (VDI):** la creación de escritorios virtuales para empleados remotos puede proporcionar una ventaja rápida. En algunos casos, este proyecto de primera adopción también podría reducir la dependencia de redes privadas costosas en favor de la conectividad de Internet público de los productos.
- **Desarrollo y pruebas:** quite operaciones de desarrollo y pruebas de entornos locales para ofrecer a los desarrolladores control, agilidad y capacidad de autoservicio.
- **Aplicaciones sencillas (menos de cinco):** modernice y migre una aplicación sencilla para obtener rápidamente experiencia de desarrollo y operaciones.
- **Laboratorios de rendimiento:** cuando necesite un rendimiento a gran escala en un entorno de laboratorio, utilice la nube para aprovisionar de forma rápida y rentable esos laboratorios durante un breve período de tiempo.
- **Plataforma de datos:** cree un lago de datos con proceso escalable para análisis, informes o cargas de trabajo de aprendizaje automático y migre a bases de datos administradas mediante los métodos dump/restore o los servicios de migración de datos.

## <a name="next-steps"></a>Pasos siguientes

Una vez iniciado el primer proyecto de adopción de la nube, el equipo de estrategia de la nube puede centrar su atención en el [plan de adopción de la nube](../plan/index.md) a largo plazo.

> [!div class="nextstepaction"]
> [Creación del plan de adopción de la nube](../plan/index.md)
