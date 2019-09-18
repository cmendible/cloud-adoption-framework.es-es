---
title: Preparación de una aplicación migrada para la promoción de producción
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Proceso dentro de la migración a la nube que se centra en las tareas de migración de cargas de trabajo a la nube.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b7f526cbf2b7efba981058d5614b4378adc8c6f6
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022623"
---
# <a name="prepare-a-migrated-application-for-production-promotion"></a>Preparación de una aplicación migrada para la promoción de producción

Después de promocionar una carga de trabajo, el tráfico de usuario de producción se enruta a los recursos migrados. Las actividades de preparación proporcionan una oportunidad para preparar la carga de trabajo para ese tráfico. A continuación se muestran algunas consideraciones empresariales y tecnológicas que le ayudarán a guiar las actividades de preparación.

## <a name="validate-the-business-change-plan"></a>Validación del plan de cambio empresarial

La transformación se produce cuando los usuarios o clientes empresariales pueden beneficiarse de una solución técnica para ejecutar procesos que impulsan la empresa. La preparación es una buena oportunidad para validar el [plan de cambio empresarial](./business-change-plan.md) y de garantizar un entrenamiento adecuado para los equipos empresariales y técnicos implicados. En concreto, asegúrese de que se comunican correctamente los siguientes aspectos relacionados con la tecnología del plan de cambios:

- Se completó el entrenamiento del usuario final (o al menos se planeó).
- Se han comunicado y aprobado los períodos de interrupción.
- Los usuarios finales han sincronizado y validado los datos de producción.
- Valide la promoción y el tiempo de adopción, y asegúrese de que las escalas de tiempo y los cambios se han comunicado a los usuarios finales.

## <a name="final-technical-readiness-tests"></a>Pruebas finales de reparación técnica

La *preparación* es el último paso antes de la versión de producción. Esto significa que también es la última oportunidad de probar la carga de trabajo. A continuación se indican algunas pruebas que se sugieren durante esta fase:

- **Pruebas del aislamiento de red.** Pruebe y supervise el tráfico de red para garantizar el aislamiento adecuado y las vulnerabilidades de red inesperadas. Compruebe también que cualquier enrutamiento de red que se interrumpa durante la migración no esté experimentando tráfico inesperado.
- **Pruebas de dependencia.** Asegúrese de que todas las dependencias de la aplicación de carga de trabajo se han migrado y son accesibles desde los recursos migrados.
- **Pruebas de continuidad empresarial y recuperación ante desastres (BCDR).** Compruebe que se han establecido los SLA de copia de seguridad y recuperación. Si es posible, realice una recuperación completa de los recursos desde la solución BCDR.
- **Pruebas de enrutamiento de usuarios finales.** Valide los patrones de tráfico y el enrutamiento para el tráfico de usuarios finales. Asegúrese de que el rendimiento de la red se alinee con las expectativas.
- **Comprobación final de rendimiento.** Asegúrese de que las pruebas de rendimiento se han completado y aprobado por los usuarios finales. Ejecute las pruebas de rendimiento automatizadas.

## <a name="final-business-validation"></a>Validación final empresarial

Una vez validados el plan de cambio empresarial y la preparación técnica, los siguientes pasos finales pueden completar la validación empresarial:

- **Validación de costos (planeados frente a reales).** Es probable que las pruebas produzcan cambios en el tamaño y la arquitectura. Asegúrese de que los precios reales de implementación siguen alineados con el plan original.
- **Comunicación y ejecución del plan de migración.** Antes de la migración, comunique la migración y ejecútela en consecuencia.

## <a name="next-steps"></a>Pasos siguientes

Una vez completadas todas las actividades de preparación, es el momento de [promover la carga de trabajo](./promote.md).

> [!div class="nextstepaction"]
> [¿Qué se necesita para promover un recurso migrado a producción?](./promote.md)
