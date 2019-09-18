---
title: Metodología de gobernanza de la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Establezca un reconocimiento básico de la metodología que promueve la gobernanza en la nube dentro de Cloud Adoption Framework.
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/04/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: cc4567495d60f76be760d532dc16a66274834396
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031595"
---
# <a name="cloud-governance-methodology"></a>Metodología de gobernanza de la nube

Adoptar la nube es un recorrido, no un destino. En el camino, hay hitos claros y ventajas empresariales tangibles. Sin embargo, el estado final de la adopción de la nube es desconocido cuando una compañía comienza el recorrido. La gobernanza de la nube crea barreras de seguridad que mantienen a la compañía en una ruta segura a lo largo del recorrido.

Cloud Adoption Framework ofrece las guías de gobernanza que describen las experiencias de compañías ficticias basadas en experiencias de clientes reales. Cada guía sigue al cliente a través de los aspectos de gobernanza de la adopción de la nube.

## <a name="envision-an-end-state"></a>Previsión de un estado final

Un recorrido sin un destino objetivo no es más que una deambulación. Es importante establecer una visión aproximada del estado final antes de dar el primer paso. La infografía siguiente proporciona un marco de referencia del estado final. No es el punto de partida, sino que muestra el destino posible.

![Infografía del modelo de gobernanza del marco de adopción en la nube](../_images/operational-transformation-govern-highres.png)

El modelo de gobernanza del marco de adopción en la nube identifica las principales áreas de importancia del recorrido. Cada área se relaciona con diferentes tipos de riesgos que la compañía debe resolver al adoptar más servicios en la nube. En este marco, la guía de gobernanza identifica las acciones necesarias para el equipo de gobernanza en la nube. En el camino, cada entidad de seguridad del modelo de gobernanza del marco de adopción en la nube se describe con más detalle. En líneas generales, se incluyen las siguientes:

**Directivas corporativas:** Las directivas corporativas rigen la gobernanza de la nube. La guía de gobernanza se centra en aspectos específicos de las directivas corporativas:

- **Riesgos empresariales:** identificación y reconocimiento de los riesgos corporativos.
- **Directiva y cumplimiento:** conversión de los riesgos en instrucciones de directiva que admitan los requisitos de cumplimiento.
- **Procesos:** garantía del cumplimiento de las directivas indicadas.

**Cinco disciplinas de la gobernanza de la nube:** Estas disciplinas admiten las directivas corporativas. Cada disciplina protege a la compañía de posibles dificultades:

- Administración de costos
- Línea de base de seguridad
- Coherencia de recursos
- Línea de base de identidad
- Aceleración de la implementación

Básicamente, las directivas corporativas sirven como sistema de advertencia anticipada para detectar posibles problemas. Las disciplinas ayudan a la compañía a mitigar los riesgos y crear barreras de seguridad.

## <a name="grow-to-the-end-state"></a>Alcanzar el estado final

Dado que los requisitos de gobernanza cambiarán a lo largo del recorrido de adopción de la nube, se requiere un enfoque diferente para la gobernanza. Las compañías ya no pueden esperar a que un equipo pequeño cree las barreras de seguridad y los mapas de ruta de cada trayectoria *antes de dar el primer paso*. Se esperan resultados empresariales más rápidamente y sin problemas. La gobernanza de TI también debe avanzar rápidamente y mantener el ritmo de las demandas empresariales para conservar su relevancia durante la adopción de la nube y evitar "shadow IT".

Un enfoque de **gobernanza incremental** fortalece estos rasgos. La gobernanza incremental se basa en un pequeño conjunto de directivas corporativas, procesos y herramientas para establecer una base para la adopción y la gobernanza. Esta base se denomina **producto viable mínimo (MVP)** . Un MVP permite al equipo de gobernanza incorporar con rapidez la gobernanza en las implementaciones a lo largo del ciclo de vida de la adopción. Se puede establecer un MVP en cualquier punto durante el proceso de adopción de la nube. Sin embargo, es recomendable adoptar un MVP tan pronto como sea posible.

La capacidad de responder rápidamente a los riesgos cambiantes faculta al equipo de gobernanza en la nube para desarrollar nuevos métodos. El equipo de gobernanza en la nube puede unirse al equipo de estrategia de la nube con una función de explorador, moviéndose por delante de los equipos de adopción de la nube, trazando rutas y estableciendo rápidamente barreras de seguridad para administrar los riesgos asociados con los planes de adopción. Estos niveles de gobernanza just-in-time se conocen como **iteraciones de gobernanza**. Con este enfoque, la estrategia de gobernanza avanza un paso por delante de los equipos de adopción de la nube.

En el siguiente diagrama se muestra un MVP de gobernanza simple y tres iteraciones de gobernanza. Durante las iteraciones, se definen directivas corporativas adicionales para corregir los nuevos riesgos. Luego la disciplina de aceleración de la implementación aplica dichos cambios en cada implementación.

![Ejemplo de mejora de gobernanza incremental](../_images/govern/incremental-governance-example.png)

> [!NOTE]
> La gobernanza no sustituye a las funciones clave como la seguridad, las redes, la identidad, las finanzas, DevOps o las operaciones. En el camino, surgirán interacciones y dependencias con los miembros de cada función. Estos miembros deben incluirse en el equipo de gobernanza en la nube para acelerar las decisiones y las acciones.

## <a name="next-steps"></a>Pasos siguientes

Use la [herramienta de pruebas comparativas de gobernanza](https://cafbaseline.com) de Cloud Adoption Framework para evaluar su recorrido de transformación e identificar carencias en su organización en seis dominios clave, tal y como se define en el marco.

> [!div class="nextstepaction"]
> [Evaluación del recorrido de transformación](./benchmark.md)
