---
title: 'Guía de supervisión de la nube: alertas'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Decida cuándo usar Azure Monitor o System Center Operations Manager en Microsoft Azure.
author: MGoedtel
ms.author: magoedte
ms.date: 06/26/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 76fb8084aad799d3bbfdaf3bd2ef4330fd080ac0
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032094"
---
# <a name="cloud-monitoring-guide-alerting"></a>Guía sobre la supervisión en la nube: Alertas

Durante años, las organizaciones de TI se han esforzado por combatir la fatiga de alertas creada por las herramientas de supervisión implementadas en la empresa. Muchos sistemas generan un gran volumen de alertas que a menudo se consideran no significativas, mientras que otras son pertinentes pero se pasan por alto o se omiten. Como resultado, las operaciones de los responsables de TI y de los desarrolladores han tenido dificultades para satisfacer la calidad de nivel de servicio prometida a los clientes internos o externos. Para garantizar la confiabilidad, es fundamental comprender el estado de la infraestructura y de las aplicaciones. Es necesario identificar las causas rápidamente, para minimizar la degradación y la interrupción del servicio o para reducir el efecto de los incidentes o el número de estos.

## <a name="successful-alerting-strategy"></a>Estrategia de alertas correcta

*No se puede corregir lo que no se sabe que está dañado.*

Alertar sobre lo que importa es fundamental. Para ello, es necesario recopilar y medir las métricas y los registros correctos. También se necesita una herramienta de supervisión capaz de almacenar, agregar, visualizar, analizar e iniciar una respuesta automatizada cuando se cumplan las condiciones. La mejora de la observabilidad de los servicios y de las aplicaciones solo se puede lograr si se entiende totalmente su composición. A esa composición se le asigna una configuración de supervisión detallada que aplica la plataforma de supervisión. Esto incluye los estados de error predecibles (los síntomas, no la causa del error) que tienen sentido para la alerta.

Para determinar si un síntoma es un candidato adecuado de una alerta, tenga en cuenta los siguientes principios:

- **¿Importa?** ¿Es el problema síntoma de un problema real o de un problema que influye en el estado general de la aplicación? Por ejemplo, ¿le preocupa que el uso de CPU sea alto en el recurso? ¿o que una determinada consulta SQL que se ejecuta en una instancia de base de datos SQL en ese recurso haga un uso elevado de CPU durante un período prolongado? Dado que la condición de uso de CPU es un problema real, debe alertar sobre ella. Pero no es necesario notificarlo al equipo, ya que no es de ayuda señalar qué está causando la condición en primer lugar. Las alertas y notificaciones sobre el problema de utilización del proceso de consultas SQL son pertinentes y procesables.
- **¿Es urgente?** ¿El problema es real y requiere atención urgente? Si es así, se debe notificar inmediatamente al equipo responsable.
- **¿Se ven afectados los clientes?** ¿Los usuarios del servicio o de la aplicación resultan afectados a causa del problema?
- **¿Se ven afectados otros sistemas dependientes?** ¿Hay alertas de dependencias que están interrelacionadas y que, por lo tanto, se pueden correlacionar para evitar notificar a distintos equipos que trabajan con el mismo problema?

Formule estas preguntas al desarrollar inicialmente una configuración de supervisión. Pruebe y valide las suposiciones en un entorno que no sea de producción y, luego, implemente en producción. Las configuraciones de supervisión se derivan de modos de error conocidos, de resultados de pruebas de errores simulados y de la experiencia de los distintos miembros del equipo.

Después del lanzamiento de la configuración de supervisión, puede aprender mucho sobre lo que funciona y lo que no. Piense en los problemas con un alto volumen de alertas desapercibidos en la supervisión pero advertidos por los usuarios finales, y cuáles fueron las mejores acciones que se tomaron como parte de esta evaluación. Identifique los cambios que se deben implementar para mejorar la entrega del servicio, como parte de un proceso continuo de mejora de la supervisión. No consiste solo en evaluar el ruido de las alertas o la ausencia de ellas, sino también de la efectividad de la supervisión de la carga de trabajo. Consiste en la efectividad de las directivas de alerta, el proceso y la referencia cultural general para determinar las mejoras.

Tanto System Center Operations Manager como Azure Monitor admiten alertas basadas en umbrales estáticos o incluso dinámicos y acciones configuradas sobre ellos. Algunos ejemplos son las alertas de correo electrónico, SMS y llamadas de voz para notificaciones simples. Ambos servicios también admiten la integración de ITSM para automatizar la creación de registros de incidentes y escalarlos al equipo de soporte técnico correcto, o cualquier otro sistema de administración de alertas que use un webhook.

Cuando sea posible, puede usar cualquiera de los diversos servicios para automatizar las acciones de recuperación. Por ejemplo, System Center Orchestrator, Azure Automation, Azure Logic Apps o la escalabilidad automática en caso de cargas de trabajo elásticas. Aunque la acción más normal de alerta es notificar a los equipos responsables, también podría ser adecuado automatizar las acciones correctivas. Esto puede ayudar a simplificar todo el proceso de administración de incidentes. La automatización de estas tareas de recuperación también puede reducir el riesgo de errores humanos.

## <a name="azure-monitor-alerting"></a>Alertas de Azure Monitor

Si usa Azure Monitor exclusivamente, se aplica la siguiente guía. Siga estas instrucciones a la hora de considerar la velocidad, el costo y el volumen de almacenamiento de Azure Monitor.

Hay seis repositorios que almacenan los datos de supervisión, en función de la característica y la configuración que use.

- **Base de datos de métricas de Azure Monitor** Una base de datos de serie temporal usada principalmente para las métricas de la plataforma de Azure Monitor, pero también tiene los datos de métricas de Application Insights reflejados en ella. La información que entra en esta base de datos tiene los tiempos de alerta más rápidos.

- **Almacén de registros de Application Insights.** Una base de datos que almacena la mayor parte de la telemetría de Application Insights en forma de registros.

- **Almacén de registros de Azure Monitor.** El almacén principal de los datos de registro de Azure. Otras herramientas pueden enrutar los datos a él y se pueden analizar en registros de Azure Monitor. Las consultas de alertas de registro tienen una latencia mayor debido a la ingesta y la indexación. Esta latencia suele ser de entre 5 y 10 minutos, aunque puede ser mayor en determinadas circunstancias.

- **Almacén del registro de actividad.** Se usa en todos los eventos de estado del servicio y registro de actividad. Es posible crear alertas dedicadas. Contiene los eventos de nivel de suscripción que se producen en objetos de la suscripción, tal como se ha ve desde fuera de esos objetos. Por ejemplo, cuando se establece una directiva o se accede a un recurso o se elimina.

- **Azure Storage.** Almacenamiento de uso general respaldado por Azure Diagnostics y otras herramientas de supervisión. Se trata de una opción de bajo costo para la retención de la telemetría de supervisión a largo plazo. No se admiten las alertas de datos almacenados en este servicio.

- **Event Hubs.** Se suele usar para transmitir datos al entorno local o a otras herramientas de supervisión e ITSM de los asociados.

Hay cuatro tipos de alertas en Azure Monitor, que están vinculadas en cierto modo al repositorio en el que se almacenan los datos.

- [Alerta de métrica](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric). Alertas sobre los datos de la base de datos de métricas de Azure Monitor. Las alertas se producen cuando un valor supervisado cruza un umbral definido por el usuario y, después, vuelve al estado "normal".

- [Alerta de consulta de registro](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log-query). Disponible para las alertas sobre el contenido de los almacenes de registros de Application Insights o de Azure. También puede generar alertas basadas en consultas entre áreas de trabajo.

- [Alerta de registro de actividad](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log). Alertas sobre los elementos del almacén de registro de actividad, a excepción de los datos de Service Health.

- [Alerta de Service Health](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log-service-notifications?toc=%2fazure%2fservice-health%2ftoc.json). Un tipo especial de alerta, solo para problemas de Service Health procedentes del almacén de registro de actividad.

### <a name="alerting-through-partner-tools"></a>Alertas a través de herramientas de asociados

Si usa una solución de alertas externa, enrútelas lo más posible por Azure Event Hubs, ya que es la ruta más rápida de Azure Monitor. Tendrá que pagar por la ingesta en Event Hubs. Si el costo es un problema y la velocidad no, puede usar Azure Storage como alternativa más económica. Solo tiene que asegurarse de que las herramientas de supervisión o ITSM puedan leer Azure Storage para extraer los datos.

Azure Monitor incluye compatibilidad con la integración con otras plataformas de supervisión, y software ITSM, como ServiceNow. Puede usar alertas de Azure y seguir desencadenando acciones fuera de Azure, según lo requiera el proceso de administración de incidentes o DevOps. Si quiere generar alertas en Azure Monitor y automatizar la respuesta, puede iniciar acciones automatizadas mediante Azure Functions, Azure Logic Apps o Azure Automation, según el escenario y los requisitos.

### <a name="specialized-azure-monitoring-offerings"></a>Ofertas especializadas de supervisión de Azure

Las [soluciones de administración](https://docs.microsoft.com/azure/azure-monitor/insights/solutions-inventory) generalmente almacenan sus datos en el almacén de registros de Azure. Las dos excepciones son Azure Monitor para VM y Azure Monitor para contenedores. En la tabla siguiente se describe la experiencia de alerta basada en el tipo de datos concreto y el lugar donde se almacena.

Solución| Tipo de datos | Comportamiento de alerta
:---|:---|:---
Azure Monitor para contenedores | Los datos de rendimiento medio calculados de nodos y pods se escriben en el almacén de métricas. | Cree alertas de métricas si quiere recibir alertas en función de la variación del rendimiento de uso medido, acumulado durante un período de tiempo.
|| Los datos de rendimiento calculados que usan percentiles de nodos, controladores, contenedores y pods se escriben en el almacén de registros. Los registros de contenedor y la información de inventario también se escriben en el almacén de registros. | Cree alertas de consulta de registro si quiere recibir alertas en función de la variación del uso medido de clústeres y contenedores. Las alertas de consulta de registro también se pueden configurar en función de los recuentos de fase de pod y el número de nodos de estado.
Azure Monitor para máquinas virtuales | Los criterios de mantenimiento son métricas que se escriben en el almacén de métricas. | Se generan alertas cuando el estado de mantenimiento cambia de una condición de correcto a incorrecto. Solo admite grupos de acciones configurados para enviar notificaciones por correo electrónico o SMS.
|| Los datos de registro de rendimiento de asignación y del sistema operativo invitado se escriben en el almacén de registros. | Cree alertas de consulta de registros.

### <a name="fastest-speed-driven-by-cost"></a>Velocidad más rápida controlada por el costo

La latencia es una de las decisiones más importantes que determinan las alertas y la resolución rápida de problemas que afectan a su servicio. Si necesita alertas casi en tiempo real en menos de cinco minutos, evalúe primero si tiene o puede obtener alertas sobre la telemetría donde se almacena de forma predeterminada. En general, esta estrategia es también la opción más económica porque la herramienta que usa ya está enviando los datos a esa ubicación.

Dicho esto, hay algunas notas al pie importantes para esta regla.

La **telemetría del sistema operativo invitado** tiene una serie de rutas de acceso para entrar en el sistema.

- La forma más rápida de alertar sobre estos datos es importarlos como métricas personalizadas. Para ello, use la extensión de Azure Diagnostics y, luego, utilice una alerta de métrica. Sin embargo, las métricas personalizadas se encuentran actualmente en versión preliminar y son [más caras que otras opciones](https://azure.microsoft.com/pricing/details/monitor/).

- El método más económico pero más lento es enviarlas al almacén de Kusto de registros de Azure. Ejecutar el agente Log Analytics en la máquina virtual es la mejor manera de obtener todos los datos de registro y métricas del sistema operativo invitado de este almacén.

- Puede enviar a ambos almacenes mediante la ejecución de la extensión y del agente en la misma máquina virtual. Después, puede generar alertas rápidamente, pero también usar los datos del sistema operativo invitado como parte de búsquedas más complejas cuando se combinan con otros datos de telemetría.

**Importar los datos del entorno local.** Si intenta consultar y supervisar datos en máquinas que se ejecutan en Azure y en el entorno local, puede usar el agente de Log Analytics para recopilar datos del sistema operativo invitado. Después, puede usar una característica denominada [registros en métricas](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-metric-logs) para simplificar esas métricas en el almacén de métricas. Este método omite parte del proceso de ingesta en el almacén de registros de Azure y, por tanto, está disponible antes en la base de datos de métricas.

### <a name="minimize-alerts"></a>Minimizar las alertas

Si usa una solución como Azure Monitor para VM y encuentra los criterios de mantenimiento predeterminados que supervisan el uso de rendimiento aceptable, no cree alertas de métricas o de consulta de registro superpuestas basadas en los mismos contadores de rendimiento.

Si no usa Azure Monitor para VM, explore las siguientes características para facilitar el trabajo de creación de alertas y administración de notificaciones:  

> [!NOTE]
> Estas características solo se aplican a alertas de métricas; es decir, las alertas basadas en los datos que se envían a la base de datos de métricas de Azure Monitor. No se aplican a los otros tipos de alertas. Como se mencionó anteriormente, el objetivo principal de las alertas de métricas es la velocidad. Si recibir una alerta en menos de 5 minutos no es la principal preocupación, puede usar en su lugar una alerta de consulta de registro.

- [Umbrales dinámicos](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-dynamic-thresholds). Los umbrales dinámicos examinan la actividad del recurso durante un período de tiempo y crean umbrales de "comportamiento normal" superiores e inferiores. Cuando la métrica que se supervisa está fuera de estos umbrales, recibe una alerta.

- [Alertas de varias señales](https://azure.microsoft.com/blog/monitor-at-scale-in-azure-monitor-with-multi-resource-metric-alerts/). Puede crear una alerta de métrica que use la combinación de dos entradas diferentes de dos tipos de recursos diferentes. Por ejemplo, si quiere activar una alerta cuando la CPU de una máquina virtual supere el 90 por ciento y el número de mensajes en una determinada cola de Azure Service Bus que alimenta esa máquina virtual supera una cantidad determinada, puede hacerlo sin crear una consulta de registro. Esta situación solo funciona con dos señales. Si tiene una consulta más compleja, suministre los datos de métricas al almacén de registros de Azure Monitor y use una consulta de registro.

- [Alertas de varios recursos](https://azure.microsoft.com/blog/monitor-at-scale-in-azure-monitor-with-multi-resource-metric-alerts/). Azure Monitor permite una única regla de alertas de métricas que se aplica a todos los recursos de máquina virtual. Esta característica puede ahorrar tiempo, ya que no es necesario crear alertas individuales para cada máquina virtual. Los precios de este tipo de alerta son los mismos. Lo mismo cuesta crear 50 alertas para supervisar el uso de CPU de 50 máquinas virtuales que 1 alerta para supervisar el uso de CPU de las 50 máquinas virtuales. También puede usar estos tipos de alertas en combinación con umbrales dinámicos.

En conjunto, estas características pueden ahorrar tiempo al minimizar las notificaciones de alerta y la administración de las alertas subyacentes.

### <a name="alerts-limitations"></a>Limitaciones de alertas

Asegúrese de tener en cuenta las [limitaciones](https://docs.microsoft.com/azure/azure-subscription-service-limits#azure-monitor-limits) de la cantidad de alertas que se pueden crear. Algunos límites (pero no todos) se pueden aumentar mediante una llamada a soporte técnico.

### <a name="best-query-experience"></a>Mejor experiencia de consulta

Si busca tendencias en todos los datos, tiene sentido importar todos los datos en los registros de Azure, a menos que ya estén en Application Insights. Puede crear consultas en ambas áreas de trabajo, por lo que no es necesario mover los datos entre ellas. También puede importar los datos del registro de actividad y de Service Health en el área de trabajo de Log Analytics. Se paga por esta ingesta y almacenamiento, pero se obtienen todos los datos en un solo lugar para su análisis y consulta. Esto también le ofrece la posibilidad de crear condiciones de consulta complejas y alertar sobre ellas.
