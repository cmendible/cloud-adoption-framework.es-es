---
title: ¿Qué se necesita para promover un recurso migrado a producción?
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Un proceso dentro de la migración a la nube que se centra en las tareas de migración de cargas de trabajo a la nube.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: eb025eacb7743f470b15e2714ed65a05c21034a1
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70836622"
---
<!-- markdownlint-disable MD026 -->

# <a name="what-is-required-to-promote-a-migrated-resource-to-production"></a>¿Qué se necesita para promover un recurso migrado a producción?

La promoción a producción marca la finalización de la migración de una carga de trabajo a la nube. Después de promocionar el recurso y todas sus dependencias, se vuelve a enrutar el tráfico de producción. El redireccionamiento del tráfico hace que los recursos locales sean obsoletos, lo que permite su retirada.

El proceso de promoción varía según la arquitectura de la carga de trabajo. Sin embargo, hay varios requisitos previos coherentes y algunas tareas comunes. En este artículo se describen cada una de ellas y sirve como un tipo de lista de comprobación de promoción previa.

## <a name="prerequisite-processes"></a>Procesos de requisitos previos

Cada uno de los siguientes procesos debe ejecutarse, documentarse y validarse antes de la implementación de producción:

- **[Evaluación](../assess/index.md):** La carga de trabajo se ha evaluado para la compatibilidad con la nube.
- **[Diseño](../assess/architect.md):** La estructura de la carga de trabajo se ha diseñado correctamente para alinearse con el proveedor de nube elegido.
- **[Replicación](../migrate/replicate.md):** Los recursos se han replicado en el entorno de nube.
- **[Preparación por fases](../migrate/stage.md):** Los recursos replicados se han restaurado en una instancia por fases del entorno de nube.
- **[Pruebas empresariales](./business-test.md):** Los usuarios empresariales han probado y validado completamente la carga de trabajo.
- **[Plan de cambio empresarial](./business-change-plan.md):** La empresa ha compartido un plan para que los cambios se realicen de acuerdo con la promoción de producción. Esto debe incluir un plan de adopción de usuarios, cambios en los procesos empresariales, usuarios que requieren entrenamiento y escalas de tiempo para diversas actividades.
- **[Listo](./ready.md):** Por lo general, se deben realizar una serie de cambios técnicos antes de la promoción.

## <a name="best-practices-to-execute-prior-to-promotion"></a>Prácticas recomendadas para ejecutar antes de la promoción

Los siguientes cambios técnicos probablemente tendrán que completarse y documentarse como parte del proceso de promoción:

- **Alineación del dominio.** Algunas directivas corporativas requieren dominios independientes para el almacenamiento provisional y la producción. Asegúrese de que todos los recursos se unen al dominio adecuado.
- **Enrutamiento de usuarios.** Valide que los usuarios tengan acceso a la carga de trabajo mediante las rutas de red adecuadas; compruebe las expectativas de rendimiento coherentes.
- **Alineación de identidad.** Compruebe que los usuarios que se redirigen a la aplicación tienen los permisos adecuados en el dominio para hospedar la aplicación.
- **Rendimiento.** Realice una validación final del rendimiento de la carga de trabajo para minimizar las sorpresas.
- **Validación de la continuidad empresarial y recuperación ante desastres.** Compruebe que los procesos de copia de seguridad y recuperación adecuados funcionan según lo previsto.
- **Clasificación de datos.** Compruebe la clasificación de datos para asegurarse de que se han implementado las directivas y protecciones adecuadas.
- **Verificación del director de seguridad de la Información.** Compruebe que el responsable de seguridad de la información ha revisado la carga de trabajo, los riesgos empresariales, la tolerancia a riesgos y las estrategias de mitigación.

## <a name="final-step-promote"></a>Paso final: Promoción

Las cargas de trabajo requerirán niveles variables de procesos detallados de revisión y promoción. Sin embargo, la realineación de red sirve como el paso final común para todas las versiones de promoción. Cuando todo lo demás esté listo, actualice los registros DNS o las direcciones IP para enrutar el tráfico a la carga de trabajo migrada.

## <a name="next-steps"></a>Pasos siguientes

La promoción de una carga de trabajo indica la finalización de una versión. Sin embargo, en paralelo con la migración, los recursos retirados debe [darse de baja](./decommission.md) del servicio.

> [!div class="nextstepaction"]
> [Baja de recursos retirados](./decommission.md)
