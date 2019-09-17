---
title: 'Modelos de promoción: en un solo paso, provisional y por etapas'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Descripción del impacto de la promoción en las actividades de migración
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 88f8d847a1eac05a1e291c8908fd9a161904f626
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70836650"
---
# <a name="promotion-models---single-step-staged-or-flight"></a>Modelos de promoción: de paso único, preconfigurados o piloto

La migración de una carga de trabajo se suele tratar como una actividad única. En realidad, es un conjunto de actividades más pequeñas que facilitan el traslado de un recurso digital a la nube. Una de las últimas actividades de una migración es la promoción de un recurso a producción. La promoción es el punto en el que el sistema de producción cambia para los usuarios finales. A menudo, puede ser algo tan simple como cambiar el enrutamiento de red, redirigiendo a los usuarios finales al nuevo recurso en producción. La promoción es también el punto en el que las operaciones de TI o las operaciones en la nube cambian el foco de atención, pasando de los procesos de administración operativa del sistema de producción anterior a los nuevos sistemas de producción.

Hay varios modelos de promoción. En este artículo se describen tres de los más comunes que se usan en las migraciones a la nube. La elección de un modelo de promoción cambia las actividades que se pueden ver en los procesos de migración y optimización. Por ello, el modelo de promoción debe decidirse en una fase temprana del lanzamiento.

## <a name="impact-of-promotion-model-on-migrate-and-optimize-activities"></a>Impacto del modelo de promoción en las actividades de migración y optimización

En cada uno de los siguientes modelos de promoción, la herramienta de migración elegida replica y almacena en un entorno provisional los recursos que conforman una carga de trabajo. Después del entorno provisional, cada modelo trata el recurso de forma un poco diferente.

- **Promoción en un solo paso.** En un modelo de promoción *en un solo paso*, el entorno provisional se duplica como proceso de promoción. Una vez que todos los recursos están en el entorno provisional, el tráfico de los usuarios finales se vuelve a enrutar y el entorno provisional se convierte en entorno de producción. En este caso, la promoción forma parte del proceso de migración. Este es el modelo de migración más rápido. Sin embargo, este enfoque dificulta la integración de actividades sólidas de optimización y prueba. Además, en este tipo de modelo se da por hecho que el equipo de migración tiene acceso al entorno provisional y de producción, lo que pone en peligro la separación de los requisitos del servicio en algunos entornos.
  > [!NOTE]
  >La tabla de contenido de este sitio muestra la actividad de promoción como parte del proceso de optimización. En un modelo en un solo paso, la promoción se produce durante el proceso de migración. Al usar este modelo, los roles y las responsabilidades se deben actualizar para reflejar esto.
- **Provisional.** En un modelo de promoción *provisional*, la carga de trabajo se considera migrada cuando está en el entorno provisional pero aún no se ha promocionado. Antes de la promoción, la carga de trabajo migrada se somete a una serie de pruebas de rendimiento, pruebas empresariales y cambios de optimización. Después, se promociona en una fecha futura junto con un plan de pruebas empresariales. Este enfoque mejora el equilibrio entre el costo y el rendimiento, a la vez que facilita la obtención de validación empresarial.
- **Por etapas.** El modelo de promoción *por etapas* combina los modelos en un solo paso y provisional. En un modelo por etapas, los recursos de la carga de trabajo se tratan como recursos de producción después de ponerlos en el entorno provisional. Después de un período comprimido de pruebas automatizadas, el tráfico de producción se enruta a la carga de trabajo. Sin embargo, se trata de un subconjunto del tráfico. Ese tráfico actúa como la primera etapa de producción y pruebas. Si damos por hecho que la carga de trabajo se realiza desde una perspectiva de características y rendimiento, se migra tráfico adicional. Una vez que todo el tráfico de producción se ha trasladado a los nuevos recursos, la carga de trabajo se considera totalmente promocionada.

El modelo de promoción elegido afecta a la secuencia de actividades que se van a realizar. También afecta a los roles y responsabilidades del equipo de adopción de la nube. Incluso puede afectar a la composición de un sprint o de varios.

## <a name="single-step-promotion"></a>Promoción en un solo paso

Este modelo utiliza herramientas de automatización de la migración para replicar recursos, enviarlos al entorno provisional y promoverlos. Los recursos se replican en un entorno de ensayo contenido que la herramienta de migración controla. Una vez que se han replicado todos los recursos, la herramienta puede ejecutar un proceso automatizado para promocionarlos a la suscripción elegida en un solo paso. Mientras se encuentran en el entorno de ensayo, la herramienta continúa replicando los recursos para minimizar la pérdida de datos entre los dos entornos. Una vez que se promociona un recurso, se rompe la vinculación entre el sistema de origen y el sistema replicado. En este enfoque, si se producen cambios adicionales en los sistemas de origen iniciales, se perderán los cambios.

**Ventajas.** Las ventajas de este enfoque incluyen:

- Este modelo introduce menos cambios en los sistemas de destino.
- La replicación continua minimiza la pérdida de datos.
- Si se produce un error en un proceso del entorno provisional, este puede eliminarse y repetirse rápidamente.
- La replicación y las pruebas de ensayo repetidas habilitan un proceso de scripting y pruebas incremental.

**Inconvenientes.** Entre los aspectos negativos de este enfoque se incluyen:

- Los recursos que se encuentran provisionalmente en el espacio aislado de las herramientas no permiten modelos de prueba complejos.
- Durante la replicación, la herramienta de migración consume ancho de banda en el centro de datos local. Mantener en un entorno provisional un gran volumen de recursos durante mucho tiempo tiene un impacto exponencial en el ancho de banda disponible, lo que perjudica al proceso de migración y puede afectar al rendimiento de las cargas de trabajo de producción en el entorno local.

## <a name="staged-promotion"></a>Promoción provisional

En este modelo, el espacio aislado de ensayo administrado por la herramienta de migración se usa para realizar un número limitado de pruebas. Los recursos replicados se implementan después en el entorno en la nube, que actúa como un entorno de ensayo extendido. Los recursos migrados se ejecutan en la nube, mientras que los recursos adicionales se replican, se envían al entorno provisional y se migran. Cuando hay cargas de trabajo completas disponibles, se inicia un conjunto de pruebas enriquecidas. Cuando se han migrado todos los recursos asociados a una suscripción, la suscripción y todas las cargas de trabajo hospedadas se promocionan a producción. En este escenario, no se produce ningún cambio en las cargas de trabajo durante el proceso de promoción. En vez de eso, los cambios tienden a producirse en las capas de red y de identidad, los usuarios se enrutan al nuevo entorno y se revoca el acceso del equipo de adopción de la nube.

**Ventajas.** Las ventajas de este enfoque incluyen:

- Este modelo ofrece la posibilidad de realizar pruebas empresariales más precisas.
- La carga de trabajo se puede estudiar más detenidamente para optimizar mejor el rendimiento y el costo de los recursos.
- Se puede replicar un mayor número de recursos en un límite de tiempo y de ancho de banda similar.

**Inconvenientes.** Entre los aspectos negativos de este enfoque se incluyen:

- La herramienta de migración elegida no puede facilitar la replicación en curso después de la migración.
- Se requiere un medio secundario de replicación de datos para sincronizar las plataformas de datos durante el período provisional.

## <a name="flight-promotion"></a>Promoción por etapas

Este modelo es similar al modelo de promoción provisional. Sin embargo, hay una diferencia fundamental. Cuando la suscripción está lista para su promoción, el enrutamiento del usuario final se produce en fases o etapas. En cada etapa se vuelve a enrutar a más usuarios a los sistemas de producción.

**Ventajas.** Las ventajas de este enfoque incluyen:

- Este modelo mitiga los riesgos asociados a una gran actividad de migración o promoción. Los errores de la solución migrada se pueden identificar con un menor impacto en los procesos empresariales.
- Permite supervisar las demandas de rendimiento de la carga de trabajo en el entorno en la nube durante un período prolongado, lo que aumenta la precisión de las decisiones sobre el tamaño de los recursos.
- Se puede replicar un mayor número de recursos en un límite de tiempo y de ancho de banda similar.

**Inconvenientes.** Entre los aspectos negativos de este enfoque se incluyen:

- La herramienta de migración elegida no puede facilitar la replicación en curso después de la migración.
- Se requiere un medio secundario de replicación de datos para sincronizar las plataformas de datos durante el período provisional.

## <a name="next-steps"></a>Pasos siguientes

Una vez que el equipo de adopción de la nube define y acepta un modelo de promoción, se puede iniciar la [corrección de los recursos](./remediate.md).

> [!div class="nextstepaction"]
> [Corrección de los recursos antes de la migración](./remediate.md)
