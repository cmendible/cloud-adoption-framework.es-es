---
title: Implementación del plan de adopción de la nube en Azure DevOps
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Implementación de la plantilla del plan de adopción de la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 07/01/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: plan
ms.openlocfilehash: f7634f15735c68296a96d997d3bf8e915d03e6b7
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022308"
---
# <a name="cloud-adoption-plan-and-azure-devops"></a>Plan de adopción de la nube y Azure DevOps

Azure DevOps es el conjunto de herramientas basadas en la nube para los clientes de Azure que administran proyectos iterativos. También incluye herramientas para administrar canalizaciones de implementación y otros aspectos importantes de DevOps. 

En este artículo aprenderá a implementar rápidamente un trabajo pendiente en Azure DevOps mediante una plantilla del plan de adopción de la nube. Esta plantilla alinea los trabajos de adopción de la nube con un proceso normalizado según la guía de Cloud Adoption Framework.

## <a name="create-your-cloud-adoption-plan"></a>Creación del plan de adopción de la nube

Para implementar el plan de adopción de la nube, abra el [Generador de demostraciones de Azure DevOps](https://aka.ms/adopt/plan/generator). Esta herramienta implementará la plantilla en el inquilino de Azure DevOps. El uso de la herramienta requiere los pasos siguientes:

1. Compruebe que el campo **Plantilla seleccionada** está establecido en **Plan de adopción de la nube**. Si no es así, seleccione **Elegir plantilla** para elegir la plantilla correcta.
2. Seleccione la organización de Azure DevOps en el cuadro de lista desplegable **Seleccionar organización**.
3. Escriba un nombre para el nuevo proyecto. El plan de adopción de la nube tendrá este nombre cuando se implemente en el inquilino de Azure DevOps.
4. Seleccione **Crear proyecto** para crear un nuevo proyecto en el inquilino basado en la plantilla del plan. Una barra de progreso muestra el progreso hacia la implementación del proyecto.
5. Una vez finalizada la implementación, seleccione **Ir al proyecto** para ver el nuevo proyecto.

Una vez creado el proyecto, continúe con esta serie de artículos para ver cómo puede modificar la plantilla para alinearla con el plan de adopción de la nube.

Para más información sobre soporte técnico e instrucciones de esta herramienta,consulte [Generador de demostraciones de Azure DevOps Services](https://docs.microsoft.com/azure/devops/demo-gen/?toc=%2Fazure%2Fdevops%2Fdemo-gen%2Ftoc.json&bc=%2Fazure%2Fdevops%2Fdemo-gen%2Fbreadcrumb%2Ftoc.json&view=azure-devops).

## <a name="bulk-edit-the-cloud-adoption-plan"></a>Edición en masa del plan de adopción de la nube

Una vez implementado el proyecto del plan, puede usar Microsoft Excel para modificarlo. Es mucho más fácil crear nuevas cargas de trabajo o recursos en el plan mediante el uso de Excel que con la experiencia del explorador de Azure DevOps.

Para preparar la estación de trabajo para la edición en masa, consulte [Adición o modificación en masa de elementos de trabajo con Excel](https://docs.microsoft.com/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel?view=azure-devops).

## <a name="use-the-cloud-adoption-plan"></a>Uso del plan de adopción de la nube

El plan de adopción de la nube organiza las actividades por tipo de actividad:

- **Epopeyas**: una *epopeya* representa una fase general del ciclo de vida de la adopción de la nube.
- **Características**: las características se usan para organizar objetivos específicos dentro de cada fase. Por ejemplo, la migración de una carga de trabajo específica sería una característica.
- **Casos de usuario**: los casos de usuario agrupan el trabajo en colecciones lógicas de actividades en función de un objetivo específico.
- **Tareas**: las tareas son el trabajo real que se va a realizar.

En cada nivel, las actividades se ordenan en función de las dependencias. Las actividades se vinculan a los artículos de Cloud Adoption Framework para aclarar el objetivo o la tarea.

La vista más clara del plan de adopción de la nube procede de la vista de trabajos pendientes de **Epopeyas**. Para obtener ayuda con el cambio a la vista de trabajos pendientes de **Epopeyas**, consulte el artículo [Visualización de un trabajo pendiente](https://docs.microsoft.com/azure/devops/boards/backlogs/define-features-epics?view=azure-devops#view-a-backlog-or-portfolio-backlog). Desde esta vista, es fácil planear y administrar el trabajo necesario para completar la fase actual del ciclo de vida de la adopción.

> [!NOTE]
> El estado actual del plan de adopción de la nube se centra principalmente en los trabajos de migración. Las tareas relacionadas con la gobernanza, la innovación o las operaciones se deben rellenar manualmente.

## <a name="align-the-cloud-adoption-plan"></a>Alineación del plan de adopción de la nube

Las páginas de información general de las fases de estrategia y planeamiento del ciclo de vida de la adopción de la nube hacen referencia a la [Plantilla de estrategia y planeamiento de Cloud Adoption Framework](https://archcenter.blob.core.windows.net/cdn/fusion/readiness/Microsoft-Cloud-Adoption-Framework-Strategy-and-Plan-Template.docx). Esa plantilla organiza las decisiones y los puntos de datos que alinearán la plantilla del plan de adopción de la nube con los planes específicos para la adopción. Si aún no lo ha hecho, es posible que desee completar los ejercicios relacionados con la [estrategia](../strategy/index.md) y el [planeamiento](../plan/index.md) antes de alinear el nuevo proyecto.

En los artículos siguientes se trata la alineación del plan de adopción de la nube:

- [Cargas de trabajo](./workloads.md): alinee las características de la epopeya de la migración a nube para capturar cada carga de trabajo que se va a migrar o modernizar. Agregue y modifique esas características para capturar el trabajo necesario para migrar las 10 cargas de trabajo principales.
- [Recursos](./assets.md): cada recurso (máquina virtual, aplicación o datos) se representa mediante los casos de usuario de cada carga de trabajo. Agregue y modifique los casos de usuario para alinearlos con el patrimonio digital.
- [Racionalización](./review-rationalization.md): a medida que se define cada carga de trabajo, puede significar un desafío para las suposiciones iniciales sobre esa carga de trabajo. Esto puede dar lugar a cambios en las tareas de cada recurso.
- [Creación de planes de versiones](./iteration-paths.md): las rutas de iteración establecen planes de versiones mediante la alineación de los trabajos con las distintas versiones e iteraciones.
- [Establecimiento de escalas de tiempo](./timelines.md): la definición de las fechas de inicio y finalización de cada iteración crea una escala de tiempo para administrar el proyecto global.

Estos cinco artículos le ayudarán con cada una de las tareas de alineación necesarias para empezar a administrar los trabajos de adopción. El siguiente paso le ayuda a iniciarse en el ejercicio de la alineación.

## <a name="next-steps"></a>Pasos siguientes

Empiece a alinear el proyecto del plan mediante la [definición y clasificación por prioridades de las cargas de trabajo](./workloads.md).

> [!div class="nextstepaction"]
> [Definición y clasificación por prioridades de las cargas de trabajo](./workloads.md)
