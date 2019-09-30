---
title: Descripción del riesgo empresarial durante la migración a la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Descripción del riesgo empresarial durante la migración a la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 078ba561384c07cee6ce3a174d1663f7590e228c
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71220403"
---
<!-- markdownlint-disable MD026 -->

# <a name="understand-business-risk-during-cloud-migration"></a>Descripción del riesgo empresarial durante la migración a la nube

Comprender el riesgo empresarial es uno de los elementos más importantes de cualquier transformación en la nube. El riesgo impulsa las directivas e influye en los requisitos de supervisión y aplicación. El riesgo influye en gran medida en nuestra forma de administrar el patrimonio digital, ya sea en el entorno local o en la nube.

<!-- markdownlint-enable MD026 -->

## <a name="relativity-of-risk"></a>Relatividad del riesgo

El riesgo es relativo. Una pequeña empresa con pocos recursos de TI y en un edificio cerrado tiene poco riesgo. Si se agregan usuarios y una conexión a Internet con acceso a esos recursos, el riesgo se intensifica. Cuando esa pequeña empresa crece hasta pertenecer a Fortune 500, los riesgos son exponencialmente mayores. A medida que se acumulan los ingresos, los procesos de negocio, los recuentos de empleados y los recursos de TI, los riesgos aumentan y se fusionan. Los recursos de TI que ayudan a generar ingresos corren el riesgo tangible de detener ese flujo de ingresos en caso de que se produzca una interrupción del servicio. Cada momento de inactividad equivale a pérdidas. Asimismo, a medida que se acumulan los datos, aumenta el riesgo de perjudicar a los clientes.

En el entorno local tradicional, los equipos de gobernanza de TI se centran en evaluar riesgos, crear procesos para administrar esos riesgos e implementar sistemas para garantizar que las medidas de corrección se implementen correctamente. Estos esfuerzos equilibran los riesgos necesarios para operar en un entorno empresarial conectado y moderno.

## <a name="understand-business-risks-in-the-cloud"></a>Descripción de los riesgos empresariales en la nube

Durante una transformación, se presentan los mismos riesgos relativos.

- Durante la experimentación temprana, se implementan algunos recursos con poca o ninguna información relevante. El riesgo es pequeño.
- Cuando se implementa la primera carga de trabajo, el riesgo aumenta un poco. Este riesgo se corrige fácilmente al elegir una aplicación intrínsecamente de bajo riesgo con una pequeña base de usuarios.
- A medida que se conectan más cargas de trabajo, los riesgos cambian en cada versión. Nuevas aplicaciones se ponen en marcha y los riesgos cambian.
- Cuando una empresa lanza las primeras 10 a 20 aplicaciones en línea, el perfil de riesgo es muy diferente al de cuando las 1000 aplicaciones entran en producción en la nube.

Los recursos que se han acumulado en el patrimonio local tradicional probablemente lo han hecho a lo largo del tiempo. La madurez de los equipos de negocio y de TI probablemente estaba creciendo de manera similar. Este crecimiento paralelo puede tender a crear un bagaje de directivas innecesario.

Durante una transformación de la nube, tanto el equipo de negocio como el de TI tienen la oportunidad de restablecer esas directivas y crear nuevas con una mentalidad madura.

<!-- markdownlint-disable MD026 -->

## <a name="what-is-a-business-risk-mvp"></a>¿Qué es un producto mínimo viable de riesgo empresarial?

Un **producto mínimo viable** se usa normalmente para definir la unidad más pequeña de algo que puede producir valor tangible. En un producto mínimo viable de riesgo empresarial, el equipo de gobernanza de la nube parte del supuesto de que algunos recursos se van a implementar en un entorno de nube en algún momento. Se desconoce lo que esos recursos son en ese momento y es posible que el equipo no esté seguro de qué tipos de datos se van a almacenar en esos recursos.

Al planear para el riesgo empresarial, el equipo de gobernanza de la nube podría crear para el escenario más desfavorable y asignar todas las directivas posibles a la nube. Pero la identificación de todos los posibles riesgos empresariales para todos los escenarios de uso de la nube puede conllevar un tiempo y un esfuerzo considerables, lo que podría retrasar la implementación de la gobernanza en las cargas de trabajo en la nube. Esto no es aconsejable, pero es una opción.

Por el contrario, un enfoque de producto mínimo viable puede permitir al equipo definir un punto de partida inicial y un conjunto de supuestos que serían válidos para la mayoría o todos los recursos. Este producto mínimo viable de riesgo empresarial admite implementaciones iniciales en la nube de prueba o de pequeña escala y luego se usa como base para identificar y corregir gradualmente nuevos riesgos a medida que surgen necesidades empresariales o se agregan cargas de trabajo adicionales al entorno de nube. Este proceso permite aplicar la gobernanza a lo largo del proceso de adopción de la nube.

A continuación se muestran algunos ejemplos básicos de riesgos empresariales que pueden existir como parte de un producto mínimo viable:

- Todos los recursos corren el riesgo de ser eliminados (por error o mantenimiento).
- Todos los recursos corren el riesgo de generar demasiados gastos.
- Todos los recursos podrían verse comprometidos por contraseñas débiles o una configuración poco segura.
- Cualquier recurso con los puertos abiertos expuestos en Internet corre el riesgo de verse comprometido.

Los ejemplos anteriores tienen por objeto establecer los riesgos empresariales de producto mínimo viable como una teoría. La lista real será única para cada entorno.
Una vez establecido el producto mínimo viable de riesgo empresarial, se pueden convertir en [directivas](./index.md) para corregir cada riesgo.

<!-- markdownlint-enable MD026 -->

## <a name="incremental-risk-mitigation"></a>Mitigación de riesgos incrementales

A medida que la organización implementa más cargas de trabajo en la nube, los equipos de desarrollo usan una cantidad creciente de recursos en la nube. En cada iteración, se crean y se almacenan provisionalmente nuevos recursos. En cada versión, las cargas de trabajo se preparan para la promoción de la producción. Cada uno de estos ciclos tiene el potencial de incorporar riesgos empresariales no identificados previamente.

Si se supone que un producto mínimo viable de riesgo empresarial es el punto de partida de los esfuerzos iniciales de adopción de la nube, la gobernanza puede madurar en paralelo con el creciente uso de recursos en la nube. Cuando el equipo de gobernanza de la nube opera en paralelo con los equipos de adopción de la nube, el aumento de los riesgos empresariales se puede abordar a medida que se identifican, lo que proporciona un modelo continuo estable para desarrollar la madurez de la gobernanza.

Cada recurso preconfigurado se puede clasificar fácilmente en función del riesgo. Los documentos de clasificación de datos pueden generarse o crearse en paralelo a los ciclos de almacenamiento provisional. El perfil de riesgo y los puntos de exposición también pueden documentarse. Con el paso del tiempo, una visión extremadamente clara del riesgo empresarial se hace patente en toda la organización.

Con cada iteración, el equipo de gobernanza de la nube puede trabajar con el equipo de estrategia de la nube para comunicar rápidamente nuevos riesgos, estrategias de mitigación, compensaciones y costos potenciales. Esto permite a los participantes empresariales y a los responsables de TI tomar decisiones maduras y bien informadas. Estas decisiones influyen en la madurez de las directivas. Cuando es necesario, los cambios de directiva producen nuevos elementos de trabajo para la madurez de los sistemas de infraestructura básicos. Cuando se requieren cambios en los sistemas preconfigurados, los equipos de adopción de la nube tienen tiempo suficiente para hacer cambios, mientras que el negocio prueba los sistemas preconfigurados y desarrolla un plan de adopción de usuarios.

Este enfoque minimiza los riesgos, a la vez que capacita al equipo para actuar con rapidez. También garantiza que los riesgos se abordan y resuelven rápidamente antes de la implementación.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información sobre cómo evaluar la tolerancia a los riesgos durante la adopción de la nube.

> [!div class="nextstepaction"]
> [Evaluación de la tolerancia al riesgo](./risk-tolerance.md)
