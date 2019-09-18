---
title: Pruebas comparativas y ajuste del tamaño de los recursos de la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Pruebas comparativas y ajuste del tamaño de los recursos de la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 5/19/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 13a18db6a074f73b962d29f4d5963571a49869d4
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022643"
---
# <a name="benchmark-and-resize-cloud-assets"></a>Pruebas comparativas y ajuste del tamaño de los recursos de la nube

La supervisión del uso y el gasto es muy importante para las infraestructuras en la nube. Las organizaciones pagan por los recursos que consumen a lo largo del tiempo. Cuando el uso supera los umbrales del contrato, pueden acumularse gastos inesperados rápidamente. Los informes de Cost Management ayudan a supervisar los gastos para analizar y realizar un seguimiento del uso de la nube, los costos y las tendencias. Los informes de uso a lo largo del tiempo permiten detectar anomalías que difieren de las tendencias normales. Los informes de optimización también permiten detectar las deficiencias en la implementación de la nube. Observe las deficiencias en los informes de análisis de costos.

En los modelos locales tradicionales de TI, la solicitud de sistemas de TI es costosa y lenta. Los procesos requieren a menudo ciclos de revisión de inversiones prolongados e incluso pueden requerir un proceso de planeamiento anual. Como tal, es una práctica habitual comprar más de lo necesario. También es habitual que los administradores de TI sobreaprovisionen los recursos para anticiparse a demandas futuras.

En la nube, los modelos de contabilidad y aprovisionamiento eliminan los retrasos de tiempo que conducen a la adquisición excesiva. Si un recurso necesita recursos adicionales, se puede escalar vertical u horizontalmente de forma casi instantánea. Esto significa que los activos se pueden reducir de forma segura para minimizar el número de recursos y los costes consumidos. Durante las pruebas comparativas y la optimización, el equipo de adopción de la nube trata de encontrar el equilibrio entre el rendimiento y los costos, aprovisionando los recursos para que tengan justo el tamaño adecuado para satisfacer las demandas de producción.

<!-- markdownlint-disable MD026 -->

## <a name="should-assets-be-optimized-during-or-after-the-migration"></a>¿Se deben optimizar los recursos durante la migración o después de esta?

¿Cuando se debería optimizar un recurso? ¿Durante la migración o después de esta? La respuesta simple sería: en *ambos* casos. Sin embargo, eso no es totalmente correcto. Para explicarlo, eche un vistazo a dos escenarios básicos de optimización del tamaño de los recursos:

- **Cambio de tamaño planeado.** Frecuentemente, hay recursos claramente sobredimensionados e infrautilizados a los que se debería cambiar el tamaño durante la implementación. La determinación de si se ha cambiado el tamaño de un recurso correctamente en este caso requiere pruebas de aceptación de usuario después de la migración. Si un usuario avanzado no experimenta pérdidas de rendimiento o funcionalidad durante las pruebas, puede deducir que el tamaño del recurso se ha ajustado correctamente.
- **Optimización.** En los casos en los que la necesidad de optimización no es clara, los equipos de TI deben usar un enfoque basado en datos con respecto a la administración del tamaño de los recursos. Mediante el uso de pruebas comparativas del rendimiento del recurso, un equipo de TI puede tomar decisiones fundamentadas con respecto al tamaño, los servicios, la escala y la arquitectura de una solución más adecuados. Posteriormente, pueden cambiar el tamaño y probar las teorías de rendimiento después de la migración.

Durante la migración, utilice conjeturas razonadas y experimente con el cambio de tamaño. Sin embargo, la verdadera optimización de los recursos requiere datos basados en el rendimiento real de un entorno en la nube. Para que se produzca una verdadera optimización, el equipo de TI debe implementar primero métodos para supervisar el rendimiento y la utilización de recursos.

## <a name="benchmark-and-optimize-with-azure-cost-management"></a>Pruebas comparativas y optimización con Azure Cost Management

[Azure cost Management](https://docs.microsoft.com/azure/cost-management/overview) con licencia de Cloudyn, una subsidiaria de Microsoft, administra el gasto en la nube con transparencia y precisión. Este servicio supervisa, realiza pruebas comparativas, asigna y optimiza los costos de la nube.

Los datos históricos pueden ayudar a administrar los costos mediante el análisis del uso y los gastos a lo largo del tiempo para identificar tendencias, que a continuación se usan para pronosticar gastos futuros. Administración de costos también incluye informes útiles de costos previstos. La asignación de costos administra los costos mediante el análisis basado en las directivas de etiquetado. Use la asignación de costos para el proceso de visualización completa de los gastos y contracargo, y para mostrar el uso de recursos y los costos asociados para influir en los comportamientos de consumo o cobrar a los clientes del inquilino. El control de acceso ayuda a administrar los costos al garantizar que los equipos y los usuarios solo tienen acceso a los datos de Cost Management que necesitan. Las alertas ayudan a administrar los costos mediante la notificación automática cuando se producen gastos adicionales o inusuales. También pueden notificar automáticamente a otras partes interesadas sobre anomalías de gastos y riesgos de gastos adicionales. Existen varios informes que admiten alertas en función de los umbrales de costo y presupuesto.

## <a name="improve-efficiency"></a>Mejorar la eficiencia

Determine el uso óptimo de las máquinas virtuales e identifique o elimine aquellas que están inactivas, y detecte discos sin conexión con Cost Management. Con la información de los informes acerca de la optimización de tamaño y las deficiencias puede crear un plan para reducir o eliminar las máquinas virtuales inactivas.

## <a name="next-steps"></a>Pasos siguientes

Después de probar y optimizar una carga de trabajo, es el momento de [preparar la carga de trabajo para la promoción](./ready.md).

> [!div class="nextstepaction"]
> [Preparación de una carga de trabajo migrada para la promoción a producción](./ready.md)
