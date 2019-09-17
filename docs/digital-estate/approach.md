---
title: Enfoques de planeamiento del patrimonio digital
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información sobre los distintos enfoques del planeamiento del patrimonio digital.
author: BrianBlanchard
ms.author: brblanch
ms.date: 12/10/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.custom: governance
ms.openlocfilehash: d4f420274b27646e94c64c2e5347bff50124c9dd
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70837814"
---
# <a name="approaches-to-digital-estate-planning"></a>Enfoques de planeamiento del patrimonio digital

El planeamiento del patrimonio digital puede adoptar varias formas, según los resultados deseados y el tamaño del patrimonio existente. Hay varios enfoques que se pueden adoptar. Es importante establecer expectativas respecto al enfoque al principio de los ciclos de planeamiento. Unas expectativas poco claras suelen dar lugar a retrasos asociados con ejercicios adicionales de recopilación de inventario. En este artículo se describen tres enfoques de análisis.

## <a name="workload-driven-approach"></a>Enfoque basado en la carga de trabajo

El enfoque de evaluación de arriba a abajo evalúa aspectos de seguridad. La seguridad incluye requisitos de clasificación de los datos (impacto empresarial alto, medio o bajo), cumplimiento, soberanía y riesgo de seguridad. Este enfoque evalúa la complejidad general de la arquitectura. Evalúa aspectos como la autenticación, la estructura de datos, los requisitos de latencia, las dependencias y la esperanza de vida de las aplicaciones.

El enfoque de arriba a abajo también mide los requisitos operativos de la aplicación, como los niveles de servicio, la integración, las ventanas de mantenimiento, la supervisión y la información. Cuando todos estos aspectos se han analizado y tenido en cuenta, el resultado es una puntuación que refleja la dificultad relativa de migrar esta aplicación a cada una de las plataformas en la nube: IaaS, PaaS y SaaS.

Además, la valoración de arriba a abajo evalúa las ventajas financieras de la aplicación, como las eficiencias operativas, el TCO, la rentabilidad de la inversión y otras métricas financieras adecuadas. La valoración también examina la estacionalidad de la aplicación (por ejemplo, si existen picos de demanda en algunos momentos del año) y la carga de proceso general.

Además, examina los tipos de usuarios que admite (ocasional/experto, conectado siempre/ocasionalmente) y la escalabilidad y elasticidad necesarias. Por último, la valoración examina los requisitos de continuidad empresarial y resistencia, así como las dependencias para ejecutarla en caso de que se produzca una interrupción del servicio.

> [!TIP]
> Para llevar a cabo este enfoque se requieren entrevistas y comentarios anecdóticos de las partes interesadas empresariales y técnicas. El principal riesgo para el tiempo es la disponibilidad de los individuos clave. La naturaleza anecdótica de los orígenes de datos hace que sea más difícil realizar estimaciones precisas de costo y tiempo. Planee de antemano el calendario y valide todos los datos recopilados.

## <a name="asset-driven-approach"></a>Enfoque basado en los recursos

El enfoque basado en los recursos proporciona un plan basado en los recursos que admiten una aplicación que se va a migrar. En este enfoque, se extraen datos de uso estadísticos de una base de datos de administración de configuración (CMDB) u otras herramientas de valoración de la infraestructura.

Normalmente, en este enfoque se da por hecho un modelo IaaS de implementación como base de referencia. En este proceso, el análisis evalúa los atributos de cada recurso: memoria, número de procesadores (núcleos de CPU), espacio de almacenamiento del sistema operativo, unidades de datos, tarjetas de interfaz de red (NIC), IPv6, equilibrio de carga de red, agrupación en clústeres, versión del sistema operativo, versión de la base de datos (si fuese necesario), dominios admitidos y componentes o paquetes de software de terceros, entre otros. Los recursos inventariados en este enfoque luego se alinean con las cargas de trabajo o las aplicaciones con fines de agrupación y asignación de dependencias.

> [!TIP]
> Para llevar a cabo este enfoque se requiere un origen abundante de datos de uso estadísticos. El tiempo necesario para examinar el inventario y recopilar datos es el principal riesgo para el cumplimiento de los plazos. Los orígenes de datos de bajo nivel pueden perder las dependencias entre recursos o aplicaciones. Planee el examen del inventario durante un mes por lo menos. Valide las dependencias antes de la implementación.

## <a name="incremental-approach"></a>Enfoque incremental

Se recomienda encarecidamente un enfoque incremental, como para muchos procesos del Marco de adopción de la nube. En el caso del planeamiento del patrimonio digital, eso equivale a un proceso de varias fases:

- **Análisis de costos inicial:** si se requiere validación financiera, comience con un enfoque basado en los recursos, descrito anteriormente, a fin de obtener un cálculo de costos inicial de todo el patrimonio digital, sin racionalización. Esto establece una referencia de escenario del peor caso.

- **Planear la migración:** una vez formado un equipo de estrategia de la nube, cree un trabajo pendiente de migración inicial mediante un enfoque basado en la carga de trabajo que se base en su conocimiento colectivo y algunas entrevistas con las partes interesadas. Este enfoque crea rápidamente una valoración de la carga de trabajo ligera para fomentar la colaboración.

- **Planeamiento de versiones:** en cada versión, el trabajo pendiente de migración se elimina y se vuelve a clasificar por orden de prioridad para centrarse en el impacto empresarial más relevante. Durante este proceso, se seleccionan entre cinco y diez de las cargas de trabajo siguientes como versiones con prioridad. En este punto, el equipo de estrategia de la nube dedica tiempo a realizar un enfoque exhaustivo basado en la carga de trabajo. El hecho de retrasar esta valoración hasta que haya una versión alineada respeta mejor el tiempo de las partes interesadas. También retrasa la inversión en un análisis completo hasta que la empresa comience a ver resultados de los esfuerzos anteriores.

- **Análisis de ejecución:** antes de migrar, modernizar o replicar cualquier recurso, evalúelo de forma individual y como parte de una versión colectiva. En este momento, se pueden escrutar los datos del enfoque anterior basado en los recursos para garantizar el tamaño preciso y las restricciones operacionales.

> [!TIP]
> Este enfoque incremental permite un planeamiento simplificado y unos resultados acelerados. Es importante que todas las partes implicadas entiendan el enfoque de toma de decisiones diferida. Es igualmente importante que se documenten los supuestos realizados en cada fase para evitar la pérdida de detalles.

## <a name="next-steps"></a>Pasos siguientes

Una vez seleccionado un enfoque, se puede recopilar el inventario.

> [!div class="nextstepaction"]
> [Recopilación de datos de inventario](inventory.md)
