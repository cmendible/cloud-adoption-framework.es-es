---
title: Corrección de los recursos antes de la migración
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Corrección de los recursos incompatibles antes de la migración
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 54621d366f0ae0a3e2e3504532ace183bc7f49c4
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70839078"
---
# <a name="remediate-assets-prior-to-migration"></a>Corrección de los recursos antes de la migración

Durante el proceso de evaluación de la migración, el equipo intenta identificar cualquier configuración que pueda hacer que un recurso sea incompatible con el proveedor de nube elegido. La *corrección* es un punto de control en el proceso de migración para asegurarse de que se han resuelto esas incompatibilidades. En este artículo se describen algunas tareas de corrección habituales a modo de referencia. También se establece un proceso estructural para decidir si la corrección es una inversión razonable.

## <a name="common-remediation-tasks"></a>Tareas de corrección habituales

En cualquier entorno corporativo, existe una deuda técnica. En cierto modo, esto es algo correcto y previsible. Puede que las decisiones con respecto a la arquitectura resultaran adecuadas para un entorno local pero no completamente apropiadas para una plataforma de nube. En cualquier caso, es posible que se requieran tareas habituales de corrección para preparar los recursos para la migración. Estos son algunos ejemplos:

- **Actualizaciones de host secundarias.** En ocasiones, un host obsoleto debe actualizarse antes de la replicación.
- **Actualizaciones secundarias del sistema operativo invitado.** Es más probable que sea necesario actualizar o aplicar revisiones al sistema operativo antes de la replicación.
- **Modificaciones en el acuerdo de nivel de servicio.** Las operaciones de copia de seguridad y recuperación cambian significativamente en una plataforma en la nube. Es probable que los recursos necesiten modificaciones menores en sus procesos de copia de seguridad para garantizar que seguirán funcionando en la nube.
- **Migración de PaaS.** En algunos casos, puede ser necesaria una implementación de PaaS de una estructura de datos o una aplicación para acelerar la implementación. Puede que se necesiten modificaciones menores para preparar la solución para la implementación de PaaS.
- **Cambios de código para PaaS.** No es infrecuente que las aplicaciones personalizadas requieran modificaciones menores de código para estar preparadas para PaaS. Entre los ejemplos cabe incluir los métodos que escriben en un disco local o que usan el estado de sesión en memoria.
- **Cambios de configuración de la aplicación.** Las aplicaciones migradas pueden requerir cambios en las variables como, por ejemplo, las rutas de acceso de red a recursos dependientes, cambios en la cuenta de servicio o actualizaciones de direcciones IP dependientes.
- **Cambios menores en las rutas de acceso de red.** Es posible que sea necesario modificar los patrones de enrutamiento para enrutar correctamente el tráfico de los usuarios a los nuevos recursos.
    > [!NOTE]
    > Este no es el enrutamiento definitivo de producción a los nuevos recursos, sino la configuración que permite el enrutamiento correcto a los recursos en general.

## <a name="large-scale-remediation-tasks"></a>Tareas de corrección a gran escala

Cuando un centro de recursos se mantiene, revisa y actualiza correctamente, es probable que se necesite poca corrección. Los entornos en los que hay una gran necesidad de corrección tienden a ser habituales en grandes empresas, organizaciones que han experimentado una gran reducción del departamento de TI, algunos entornos de servicios administrados heredados y entornos con muchas adquisiciones. En cada uno de estos tipos de entornos, la corrección puede suponer una gran parte del esfuerzo de migración. Si las siguientes tareas de corrección aparecen con frecuencia y afectan negativamente a la velocidad o coherencia de la migración, puede que sea conveniente dividir estas tareas de corrección en trabajos y equipos paralelos (de forma parecida a como funcionan los procesos de adopción y de gobernanza de la nube).

- **Actualizaciones de host frecuentes.** Si se debe actualizar un gran número de hosts para completar la migración de una carga de trabajo, es probable que el equipo de migración sufra retrasos. Es aconsejable dividir las aplicaciones afectadas y afrontar las tareas de corrección antes de incluir esas aplicaciones en las versiones planeadas.
- **Actualización frecuente del sistema operativo invitado.** Las grandes empresas suelen tener servidores que se ejecutan en versiones obsoletas de Linux o Windows. Además del riesgo de seguridad evidente que supone el uso de un sistema operativo obsoleto, también hay problemas de incompatibilidad que impiden la migración de las cargas de trabajo afectadas. Si un gran número de máquinas virtuales requiere la corrección del sistema operativo, puede que sea conveniente dividir esta tarea en trabajos paralelos.
- **Cambios principales de código.** Las aplicaciones personalizadas más antiguas pueden requerir un número significativamente más elevado de modificaciones para prepararlas para la implementación de PaaS. En este caso, puede que sea aconsejable eliminarlas por completo del trabajo pendiente de la migración y administrarlas en un programa totalmente independiente.

## <a name="decision-framework"></a>Marco de decisión

La corrección de las cargas de trabajo más pequeñas es sencilla. Este es uno de los motivos por los que se recomienda elegir una carga de trabajo más pequeña para la migración inicial. Sin embargo, a medida que los esfuerzos de migración evolucionan y se empieza a tratar con cargas de trabajo de mayor tamaño, la corrección puede ser un proceso lento y costoso. Por ejemplo, los esfuerzos de corrección para una migración de Windows Server 2003 que incluye un conjunto de recursos de más de 5000 máquinas virtuales puede retrasar una migración varios meses. Cuando se requiere este tipo de corrección a gran escala, las siguientes preguntas pueden servir de orientación para tomar decisiones:

- ¿Se han identificado todas las cargas de trabajo afectadas por la corrección y se han anotado en el trabajo pendiente de migración?
- En el caso de las cargas de trabajo que no se ven afectadas, ¿una migración puede producir una rentabilidad de la inversión parecida?
- ¿Se pueden corregir los recursos afectados dentro de la escala de tiempo original de la migración? ¿Qué impacto tendrían los cambios de la escala de tiempo en la rentabilidad de la inversión?
- ¿Es económicamente factible corregir los recursos en paralelo a los trabajos de migración?
- ¿Hay suficiente ancho de banda para efectuar la corrección y la migración? ¿Debe participar un asociado para ejecutar una o ambas tareas?

Si estas preguntas no tienen una respuesta favorable, puede que sea conveniente considerar la posibilidad de utilizar otros enfoques que vayan más allá de una simple estrategia de rehospedaje de IaaS:

- **Creación de contenedores.** Algunos recursos se pueden hospedar en un entorno con contenedores sin corrección. Esto podría generar un rendimiento inferior al deseable y no resuelve los problemas de seguridad o de cumplimiento.
- **Automatización.** Según los requisitos de la carga de trabajo y de la corrección, puede que sea más beneficioso crear un script para la implementación en nuevos recursos utilizando un enfoque de DevOps.
- **Recompilación.** Cuando los costos de la corrección son muy altos y el valor empresarial es igualmente alto, una carga de trabajo puede ser una buena candidata para la recompilación o el rediseño de su arquitectura.

## <a name="next-steps"></a>Pasos siguientes

Una vez finalizado el proceso de corrección, las [actividades de replicación](./replicate.md) están listas.

> [!div class="nextstepaction"]
> [Replicación de recursos](./replicate.md)
