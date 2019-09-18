---
title: Definición y clasificación por prioridades de las cargas de trabajo para un plan de adopción de la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Definición y clasificación por prioridades de las cargas de trabajo para un plan de adopción de la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: d77a17af60c8ed4540b2c40ddf8d75a4e4f6f306
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70839166"
---
# <a name="prioritize-and-define-workloads-for-a-cloud-adoption-plan"></a>Definición y clasificación por prioridades de las cargas de trabajo para un plan de adopción de la nube

El establecimiento de prioridades claras y accionables es uno de los secretos para la adopción correcta de la nube. La tentación natural es invertir tiempo en la definición de todas las cargas de trabajo que podrían verse afectadas durante la adopción de la nube. Pero eso es contraproducente, especialmente al principio del proceso de adopción.

En su lugar, se recomienda que el equipo se centre en clasificar por orden de prioridad y documentar las 10 primeras cargas de trabajo. Después de comenzar la implementación del plan de adopción, el equipo puede mantener una lista de las siguientes 10 cargas de trabajo de prioridad más alta. Este enfoque proporciona información suficiente para planear las siguientes iteraciones.

Limitar el plan a 10 cargas de trabajo fomenta la agilidad y la alineación de las prioridades a medida que cambian los criterios de negocio. Este enfoque también posibilita que el equipo de adopción de la nube aprenda y refine las estimaciones. Lo más importante es que elimina el planeamiento extensivo como una barrera para un cambio empresarial efectivo.

## <a name="what-is-a-workload"></a>¿Qué es una carga de trabajo?

En el contexto de una adopción de la nube, una carga de trabajo es una colección de recursos de TI (servidores, máquinas virtuales, aplicaciones, datos o dispositivos) que posibilitan colectivamente un proceso definido. Las cargas de trabajo pueden posibilitar más de un proceso. Las cargas de trabajo también pueden depender de otros activos compartidos o plataformas más grandes. Sin embargo, una carga de trabajo debe tener límites definidos con respecto a los recursos dependientes y los procesos que dependen de la carga de trabajo. A menudo, las cargas de trabajo se pueden visualizar mediante la supervisión del tráfico de red entre los recursos de TI.

## <a name="prerequisites"></a>Requisitos previos

Las entradas estratégicas de la lista de comprobación de requisitos previos hacen que las siguientes tareas sean mucho más fáciles de realizar. Para obtener ayuda con la recopilación de los datos que se describen en este artículo, consulte la [lista de comprobación de requisitos previos](./prerequisites.md).

## <a name="initial-workload-prioritization"></a>Clasificación por prioridades de la carga de trabajo inicial

Durante el proceso de [racionalización incremental](../digital-estate/rationalize.md), el equipo debe consensuar un enfoque de "potencia de 10", que consta de 10 cargas de trabajo prioritarias. Estas cargas de trabajo sirven como límite inicial para el planeamiento de la adopción.

Si decide que no se necesita una racionalización del patrimonio digital, se recomienda que los equipos de adopción y estrategia de la nube acuerden una lista de 10 aplicaciones que sirvan como foco inicial de la migración. Se recomienda que estas 10 cargas de trabajo contengan una combinación de cargas de trabajo sencillas (menos de 10 activos en una implementación autocontenida) y cargas de trabajo más complejas. Esas 10 cargas de trabajo iniciarán el proceso de clasificación por prioridades de las cargas de trabajo.

> [!NOTE]
> La potencia de 10 sirve como límite inicial para el planeamiento, para centrar la energía y la inversión en el análisis en una fase temprana. Sin embargo, es probable que el acto de analizar y definir las cargas de trabajo cause cambios en la lista de cargas de trabajo prioritarias.

## <a name="add-workloads-to-your-cloud-adoption-plan"></a>Adición de cargas de trabajo al plan de adopción de la nube

En el artículo anterior, [Plan de adopción de la nube y Azure DevOps](./template.md), creó un plan de adopción de la nube en Azure DevOps.

Ahora puede representar las cargas de trabajo en la lista de potencia de 10 en el plan de adopción de la nube. La forma más fácil de hacerlo es mediante la edición en masa en Microsoft Excel. Para preparar la estación de trabajo para la edición en masa, consulte [Adición o modificación en masa de elementos de trabajo con Excel](/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

En el paso 5 de este artículo se indica cómo seleccionar la **Lista de entradas**. En su lugar, seleccione **Lista de consultas**. A continuación, en la lista desplegable **Seleccionar una consulta**, seleccione la consulta **Plantilla de carga de trabajo**. Dicha consulta carga todos los trabajos relacionados con la migración de una sola carga de trabajo en la hoja de cálculo.

Una vez cargados los elementos de trabajo de la plantilla de carga de trabajo, siga estos pasos para empezar a agregar nuevas cargas de trabajo:

1. Copie todos los elementos que tengan la etiqueta **Plantilla de carga de trabajo** en la columna situada más a la derecha.
2. Pegue las filas copiadas debajo del último elemento de línea de la tabla.
3. Cambie la celda de título de la nueva característica de **Plantilla de carga de trabajo** al nombre de la nueva carga de trabajo.
4. Pegue la nueva celda del nombre de la carga de trabajo en la columna de etiqueta para todas las filas situadas debajo de la nueva característica. Tenga cuidado de no cambiar las etiquetas o el nombre de las filas relacionadas con la característica **Plantilla de carga de trabajo** real. Necesitará esos elementos de trabajo cuando agregue la siguiente carga de trabajo al plan de adopción de la nube.
5. Vaya al paso 8 de las instrucciones de edición por lotes para publicar la hoja de cálculo. En este paso se crean todos los elementos de trabajo necesarios para migrar la carga de trabajo.

Repita los pasos del 1 al 5 para cada una de las cargas de trabajo de la lista Potencia de 10.

## <a name="define-workloads"></a>Definición de cargas de trabajo

Una vez que se han definido las prioridades iniciales y se han agregado cargas de trabajo al plan, se puede definir cada una de las cargas de trabajo mediante un análisis cualitativo más profundo. Antes de incluir cualquier carga de trabajo en el plan de adopción de la nube, intente proporcionar los siguientes puntos de datos para cada carga de trabajo.

### <a name="business-inputs"></a>Entradas de negocio

| Punto de datos | DESCRIPCIÓN | Entrada |
|---|---|---|
| Nombre de la carga de trabajo | ¿Cómo se llama esta carga de trabajo? |         |
| Descripción de la carga de trabajo | En una sola frase, ¿qué hace esta carga de trabajo? |         |
| Motivaciones para la adopción | ¿Cuáles de las motivaciones para la adopción de la nube se ven afectadas por esta carga de trabajo? |         |
| Patrocinador principal | De las partes interesadas afectadas, ¿quién es el patrocinador principal que solicita las motivaciones anteriores? |         |
| Unidad de negocio | ¿Qué unidad de negocio es responsable del costo de esta carga de trabajo? |         |
| Procesos empresariales | ¿Qué procesos empresariales se verán afectados por los cambios en la carga de trabajo? |         |
| Equipos empresariales | ¿Qué equipos empresariales se verán afectados por los cambios? |         |
| Partes interesadas del negocio | ¿Hay algún ejecutivo cuyo negocio se verá afectado por los cambios? |         |
| Resultados empresariales | ¿Cómo medirá el negocio el éxito de este trabajo? |         |
| Métricas | ¿Qué métricas se usarán para realizar un seguimiento del éxito? |         |
| Cumplimiento normativo | ¿Hay algún requisito de cumplimiento de terceros para esta carga de trabajo? |         |
| Propietarios de la aplicación | ¿Quién es responsable del impacto empresarial de las aplicaciones asociadas a esta carga de trabajo? |         |
| Períodos de inmovilización empresarial | ¿Hay algún momento en el que la empresa no permita el cambio? |         |
| Zonas geográficas | ¿Hay zonas geográficas que se ven afectadas por esta carga de trabajo? |         |

### <a name="technical-inputs"></a>Entradas técnicas

| Punto de datos | DESCRIPCIÓN | Entrada |
|---|---|---|
| Enfoque de la adopción | ¿Esta adopción es candidata para la migración o la innovación? |         |
| Responsable de operaciones de la aplicación | Enumere las partes responsables del rendimiento y la disponibilidad de esta carga de trabajo. |         |
| SLA | Enumere los contratos de nivel de servicio (requisitos de RTO y RPO). |         |
| Grado de importancia | Enumere la importancia crítica actual de la aplicación. |         |
| Clasificación de los datos | Enumere la clasificación de la confidencialidad de los datos. |         |
| Zonas geográficas en funcionamiento | Enumere las zonas geográficas en las que la carga de trabajo está o debe hospedarse. |         |
| APLICACIONES | Especifique una lista o un recuento inicial de las aplicaciones incluidas en esta carga de trabajo. |         |
| Máquinas virtuales | Especifique una lista o un recuento inicial de las máquinas virtuales o servidores incluidos en la carga de trabajo. |         |
| Orígenes de datos | Especifique una lista o un recuento inicial de los orígenes de datos incluidos en la carga de trabajo. |         |
| Dependencias | Enumere las dependencias de recursos no incluidas en la carga de trabajo. |         |
| Zonas geográficas de tráfico de usuario | Enumere las zonas geográficas que tienen una colección significativa de tráfico de usuario. |         |

## <a name="confirm-priorities"></a>Confirmación de prioridades

En función de los datos recopilados, el equipo de estrategia de la nube y el equipo de adopción de la nube deben reunirse para volver a evaluar las prioridades. La clarificación de los puntos de datos empresariales podría llevar a cambios en las prioridades. La complejidad técnica o las dependencias pueden dar lugar a cambios relacionados con las asignaciones de personal, las escalas de tiempo o la secuenciación de los trabajos técnicos.

Después de una revisión, ambos equipos deberían estar de acuerdo con la confirmación de las prioridades resultantes. Este conjunto de prioridades documentadas, validadas y confirmadas es el trabajo pendiente de adopción de la nube con prioridades.

## <a name="next-steps"></a>Pasos siguientes

El equipo ahora está listo para [alinear los recursos](./assets.md) de cualquier carga de trabajo del trabajo pendiente de adopción de la nube con prioridades.

> [!div class="nextstepaction"]
> [Alineación de recursos para cargas de trabajo prioritarias](./assets.md)
