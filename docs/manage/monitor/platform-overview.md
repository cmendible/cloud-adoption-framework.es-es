---
title: 'Guía de supervisión de la nube: introducción a las plataformas de supervisión'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Decida cuándo usar Azure Monitor o System Center Operations Manager en Microsoft Azure.
author: mgoedtel
ms.author: magoedte
ms.date: 07/31/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: operate
services: azure-monitor
ms.openlocfilehash: 33d9647a0804859a611d45e130c753cab89a6ef6
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031281"
---
# <a name="cloud-monitoring-guide-overview-of-our-monitoring-platforms"></a>Guía sobre la supervisión en la nube: introducción a nuestras plataformas de supervisión

Microsoft ofrece una gama de funcionalidades de supervisión en dos productos: System Center Operations Manager, diseñado para el entorno local y después ampliado a la nube, y Azure Monitor, diseñado para la nube, pero que también puede supervisar sistemas locales. Estas dos ofertas proporcionan servicios de supervisión principales, como alertas, seguimiento del tiempo de actividad del servicio, supervisión del estado de la aplicación y la infraestructura, diagnóstico y análisis.

Muchas organizaciones están adoptando las prácticas más recientes en agilidad de DevOps e innovaciones en la nube, con el fin de administrar sus entornos heterogéneos. Pero también les preocupa su capacidad para tomar decisiones adecuadas y responsables respecto a la forma de supervisar estas cargas de trabajo.

En este artículo se ofrece una introducción general sobre nuestras plataformas de supervisión, para ayudarle a entender cómo ambas proporcionan la funcionalidad de supervisión principal.

## <a name="story-of-system-center-operations-manager"></a>Historia de System Center Operations Manager

En 2000, nos adentramos en el campo de la gestión de operaciones con Microsoft Operations Manager (MOM) 2000. En 2007, presentamos una versión rediseñada del producto, denominada System Center Operations Manager. Pasó de realizar una simple supervisión de un servidor de Windows y se centró en una supervisión sólida y completa de aplicaciones y servicios, incluidas las plataformas heterogéneas, los dispositivos de red y otras dependencias de aplicaciones o servicios. Ahora es una reconocida plataforma de supervisión de nivel empresarial para entornos locales, del mismo tipo que IBM Tivoli o HP Operations Manager en el sector. Ha crecido para admitir la supervisión de recursos de proceso y plataforma que se ejecutan en Azure, Amazon Web Services (AWS) y otros proveedores de nube.

## <a name="story-of-azure-monitor"></a>Historia de Azure Monitor

Cuando se lanzó Azure en 2010, la supervisión de los servicios en la nube se proporcionaba con el agente de Azure Diagnostics, que ofrecía una manera de recopilar datos de diagnóstico de los recursos de Azure. Esta funcionalidad se consideraba una herramienta de supervisión general y no una plataforma de supervisión de clase empresarial.  

Se presentó Application Insights para adaptarse a los cambios en un sector donde aumentaban los dispositivos en la nube, móviles e IoT y comenzaban las prácticas de DevOps. Pasó de ser Supervisión de rendimiento de aplicaciones en Operations Manager a un servicio de Azure, donde ofrece sofisticadas funciones de supervisión de las aplicaciones web escritas en diversos lenguajes. En 2015 se anunció la versión preliminar de Application Insights para Visual Studio, que más adelante pasó a conocerse simplemente como Application Insights. Recopila detalles sobre el rendimiento de las aplicaciones, las solicitudes y las excepciones, y los seguimientos.

En 2015, Azure Operational Insights empezó a estar disponible de forma general. Incluía el servicio de análisis Log Analytics, que recopilaba y buscaba datos de máquinas en Azure, en entornos locales o en otros entornos en la nube, conectadas a System Center Operations Manager. Se ofrecían Intelligence Packs que ofrecían diferentes configuraciones de administración y supervisión empaquetadas con una recopilación de lógica de consulta y analítica, visualizaciones y reglas de recopilación de datos para escenarios como la auditoría de seguridad, las evaluaciones de estado y la administración de alertas.  Más adelante, Azure Operational Insights pasó a conocerse como Log Analytics.  

En 2016 se anunció Ignite, la versión preliminar de Azure Monitor. Proporcionó un marco común para recopilar métricas de plataformas, registros de diagnóstico de recursos y eventos de registro de actividades en el nivel de suscripción de cualquier servicio de Azure iniciado desde el marco. Anteriormente, cada servicio de Azure tenía su propio método de supervisión.

En la conferencia de Microsoft Ignite de 2018 se anunció que la marca Azure Monitor se ampliaba para incluir varios servicios diferentes, originalmente desarrollados con funcionalidad independiente:

- La funcionalidad original de **Azure Monitor** de recopilación de métricas de plataforma, registros de diagnóstico de recursos y registros de actividad solo para recursos de la plataforma Azure.
- **Application Insights** para la supervisión de aplicaciones.
- **Log Analytics** como ubicación principal para la recopilación y el análisis de los datos de registro.
- Un nuevo **servicio unificado de alertas** que reunía los mecanismos de alerta de cada uno de los servicios mencionados anteriormente.  
- **Azure Network Watcher** para supervisar, diagnosticar y ver las métricas de los recursos en una red virtual de Azure.

## <a name="the-story-of-operations-management-suite-oms"></a>Historia de Operations Management Suite (OMS)

Entre 2015 y abril de 2018, Operations Management Suite (OMS) fue la unión de los siguientes servicios de administración de Azure para facilitar su licencia:

- Application Insights
- Azure Automation
- Azure Backup
- Operational Insights (nombre cambiado más adelante a Log Analytics)
- Site Recovery

La funcionalidad de los servicios que formaban parte de OMS no cambió cuando se interrumpió OMS, sino que se volvieron a combinar bajo Azure Monitor.

## <a name="infrastructure-requirements"></a>Requisitos de infraestructura

### <a name="operations-manager"></a>Operations Manager

Operations Manager requiere una infraestructura y un mantenimiento importantes para admitir un grupo de administración, que es una unidad básica de funcionalidad. Como mínimo, un grupo de administración consta de uno o varios servidores de administración, una instancia de SQL Server —que hospeda la base de datos de almacenamiento de datos operativos y de informes— y agentes. La complejidad del diseño de un grupo de administración depende de una serie de factores, como el ámbito de las cargas de trabajo que se van a supervisar y el número de dispositivos o equipos que admiten las cargas de trabajo. Si necesita alta disponibilidad y resistencia de los sitios, como suele suceder en las plataformas de supervisión empresarial, los requisitos de infraestructura y el mantenimiento asociado pueden aumentar drásticamente.

![Diagrama del grupo de administración de Operations Manager](./media/monitoring-management-guidance-cloud-and-on-premises/operations-manager-management-group-optimized.svg)

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor es un servicio SaaS, en el que toda la infraestructura subyacente se ejecuta en Azure y es administrada por Microsoft. Se ha diseñado para realizar la supervisión, el análisis y el diagnóstico a escala, y está disponible en todas las nubes nacionales. Microsoft mantiene las partes principales de la infraestructura (recopiladores, almacén de métricas y registros, y análisis) necesarias para la compatibilidad con Azure Monitor.  

![Diagrama de Azure Monitor](./media/monitoring-management-guidance-cloud-and-on-premises/azure-monitor-greyed-optimized.svg)

## <a name="data-collection"></a>Colección de datos

### <a name="operations-manager"></a>Operations Manager

#### <a name="agents"></a>Agentes

Operations Manager solo recopila datos directamente de los agentes instalados en [equipos Windows](https://docs.microsoft.com//system-center/scom/plan-planning-agent-deployment?view=sc-om-1807#windows-agent). Puede aceptar datos del SDK de Operations Manager, pero esta opción es habitualmente utilizada por los asociados que amplían el producto con aplicaciones personalizadas, no para recopilar datos de supervisión. Puede recopilar datos de otros orígenes, como [equipos Linux](https://docs.microsoft.com/system-center/scom/plan-planning-agent-deployment?view=sc-om-1807#linuxunix-agent) y dispositivos de red, mediante el uso de módulos especiales que se ejecutan en el agente de Windows que acceden de forma remota a estos otros dispositivos.

![Diagrama del agente de Operations Manager](./media/monitoring-management-guidance-cloud-and-on-premises/data-collection-opsman-agents-optimized.svg)

El agente de Operations Manager puede recopilar de varios orígenes de datos en el equipo local, como el registro de eventos, registros personalizados y contadores de rendimiento. También puede ejecutar scripts, que pueden recopilar datos del equipo local o de orígenes externos. Se pueden escribir scripts personalizados para recopilar datos que no se pueden recopilar por otros medios, o desde una variedad de dispositivos remotos que de otro modo no se podrían supervisar.

#### <a name="management-packs"></a>Módulos de administración

Operations Manager realiza toda la supervisión con flujos de trabajo (reglas, monitores y detecciones de objetos). Estos elementos se empaquetan en un [módulo de administración](https://docs.microsoft.com/system-center/scom/manage-overview-management-pack?view=sc-om-2019) y se implementan en agentes. Hay módulos de administración disponibles para una variedad de productos y servicios que incluyen reglas y monitores predefinidos. También se pueden crear módulos de administración para aplicaciones propias y escenarios personalizados.

#### <a name="monitoring-configuration"></a>Configuración de supervisión

Los módulos de administración pueden contener cientos de reglas, monitores y reglas de detección de objetos. Un agente ejecuta toda la configuración de supervisión de todos los módulos de administración correspondientes, determinados mediante reglas de detección. Cada instancia de cada configuración de supervisión se ejecuta de forma independiente y actúa inmediatamente en los datos que recopila. Así es como Operations Manager puede lograr alertas casi en tiempo real y el estado de mantenimiento actual de los recursos supervisados.

Por ejemplo, un monitor podría tomar una muestra de un contador de rendimiento cada pocos minutos. Si ese contador supera un umbral, establece inmediatamente el estado de mantenimiento de su objeto de destino, lo que desencadena también inmediatamente una alerta en el grupo de administración. Una regla programada puede inspeccionar la creación de un evento determinado y activar al instante una alerta cuando se crea ese evento en el registro de eventos local.

Dado que las configuraciones de supervisión están aisladas entre sí y funcionan desde los orígenes individuales de datos, Operations Manager tiene dificultades para correlacionar los datos entre varios orígenes. También le resulta difícil reaccionar a los datos después de que se hayan recopilado. Se pueden ejecutar flujos de trabajo que accedan a la base de datos de Operations Manager, pero este escenario no es habitual y se usa normalmente para un número limitado de flujos de trabajo de uso especial.

![Diagrama del grupo de administración de Operations Manager](./media/monitoring-management-guidance-cloud-and-on-premises/operations-manager-management-group-optimized.svg)

### <a name="azure-monitor"></a>Azure Monitor

#### <a name="data-sources"></a>Orígenes de datos

Azure Monitor recopila datos de diversos orígenes, incluidos los recursos de la infraestructura y la plataforma de Azure, los agentes en los equipos Windows y Linux, y la supervisión de datos recopilados en Azure Storage. Cualquier cliente de REST puede escribir datos de registro en Azure Monitor mediante una API, y se pueden definir métricas personalizadas para las aplicaciones web. Algunos datos de métricas se pueden enrutar a ubicaciones diferentes, en función de su uso. Por ejemplo, puede usar los datos para las alertas "tan rápidas como sea posible" o para el análisis de tendencias a largo plazo que se busca junto con otros datos de registro.

#### <a name="monitoring-solutions-and-insights"></a>Soluciones de supervisión e información

Las soluciones de supervisión usan la plataforma de registros en Azure Monitor para proporcionar supervisión para una aplicación o un servicio determinados. Normalmente definen la recopilación de datos a partir de los agentes o de los servicios de Azure y proporcionan consultas y vistas de registros para analizar los datos. No suelen incluir reglas de alerta, lo que significa que debe definir sus propios criterios de alerta en función de los datos recopilados.

Las soluciones de información, como Azure Monitor para contenedores y Azure Monitor para VM, usan la plataforma de registros y métricas de Azure Monitor para proporcionar una experiencia de supervisión personalizada de una aplicación o un servicio en Azure Portal. Pueden proporcionar supervisión del estado y condiciones de alerta, además del análisis personalizado de los datos recopilados.

#### <a name="monitoring-configuration"></a>Configuración de supervisión

Azure Monitor separa la recopilación de datos de las acciones realizadas en ellos, lo que aporta compatibilidad con microservicios distribuidos en un entorno en la nube. Consolida los datos de varios orígenes en una plataforma de datos común y proporciona funcionalidad de análisis, visualización y alerta basadas en los datos recopilados.

Todos los datos recopilados por Azure Monitor se almacenan como registros o como métricas, y las distintas características de Monitor se basan en ambos. Las métricas contienen valores numéricos en una serie temporal que resultan adecuados para alertas casi en tiempo real y la detección rápida de problemas. Los registros contienen texto o datos numéricos, y son compatibles con un potente lenguaje de consulta que los hace especialmente útiles para realizar análisis complejos.

Dado que Monitor separa la recopilación de datos de las acciones en ellos, es posible que no pueda proporcionar alertas casi en tiempo real en muchos casos. Para generar alertar sobre los datos del registro, se ejecutan consultas según una programación periódica definida en la alerta. Este comportamiento permite a Azure Monitor correlacionar fácilmente los datos de todos los orígenes supervisados, lo que a su vez permite analizar interactivamente los datos de diversas maneras. Esto resulta especialmente útil para realizar análisis de la causa principal e identificar en qué otras circunstancias puede producirse un problema.

## <a name="health-monitoring"></a>Supervisión del estado

### <a name="operations-manager"></a>Operations Manager

Los módulos de administración de Operations Manager incluyen un modelo de servicio que describe los componentes de la aplicación que se está supervisando y su relación. Los monitores identifican el estado de mantenimiento actual de cada componente en función de los datos y los scripts del agente. Los estados de mantenimiento se acumulan para que se pueda ver rápidamente el estado de mantenimiento resumido de los equipos y las aplicaciones supervisados.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor no ofrece un método definible por el usuario para implementar un modelo de servicio ni monitores que indiquen el estado de mantenimiento actual de los componentes del servicio. Dado que las soluciones de supervisión se basan en las características estándar de Azure Monitor, no proporcionan supervisión de estado. Las siguientes características de Azure Monitor pueden resultar útiles:

- **Application Insights** crea un mapa compuesto de la aplicación web y proporciona el estado de mantenimiento de cada componente o dependencia de la aplicación. Esto incluye el estado de las alertas y la exploración en profundidad de diagnósticos más detallados de la aplicación.

- **Azure Monitor para VM** ofrece una experiencia de supervisión de estado para las máquinas virtuales invitadas de Azure, similar a Operations Manager, al supervisar máquinas virtuales Windows y Linux. Evalúa el estado de componentes clave del sistema operativo desde la perspectiva de la disponibilidad y el rendimiento, para determinar el estado de mantenimiento actual. Cuando determina que la máquina virtual invitada está experimentando problemas de uso sostenido de los recursos, capacidad de espacio en disco o relacionados con la funcionalidad básica del sistema operativo, genera una alerta para llamar la atención sobre este estado.

- **Azure Monitor para contenedores** supervisa el rendimiento y el estado de instancias de Azure Kubernetes Services o Azure Container Instances. Dicha característica recopila métricas del procesador y de la memoria procedentes de los controladores, los nodos y los contenedores disponibles en Kubernetes mediante Metrics API. También recopila los registros de contenedor y los datos de inventario sobre los contenedores y sus imágenes. Los criterios de mantenimiento predefinidos basados en los datos de rendimiento recopilados ayudan a identificar si hay un problema de capacidad o un cuello de botella en los recursos. También se puede comprender el rendimiento global o el rendimiento de un tipo de objeto Kubernetes específico (pod, nodo, controlador o contenedor).

## <a name="analyzing-data"></a>Análisis de datos

### <a name="operations-manager"></a>Operations Manager

Operations Manager proporciona cuatro formas básicas de analizar los datos después de su recopilación.

- El **Explorador de estado** permite averiguar qué monitores identifican un problema de estado de mantenimiento y revisar la información acerca del monitor y las posibles causas de las acciones relacionadas con él.

- Las **vistas** son visualizaciones predefinidas de los datos recopilados como, por ejemplo, un gráfico de datos de rendimiento o una lista de los componentes supervisados y su estado de mantenimiento actual. Las vistas de diagrama presentan visualmente el modelo de servicio de una aplicación.

- Los **informes** permiten resumir los datos históricos guardados en el almacenamiento de datos de Operations Manager. Se pueden personalizar los datos en los que se basan las vistas y los informes. Sin embargo, no hay ninguna característica que permita el análisis complejo o interactivo de los datos recopilados.

- El **shell de comandos de Operations Manager**, que amplía Windows PowerShell con un conjunto adicional de cmdlets, puede consultar y visualizar los datos recopilados. Esto incluye gráficos y otras visualizaciones, de forma nativa con PowerShell o mediante la consola web basada en HTML de Operations Manager.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor cuenta con un potente motor de análisis que permite trabajar de forma interactiva con los datos de registro y combinarlos con otros datos de supervisión para el análisis de tendencias y otros análisis de datos. Las vistas y los paneles permiten visualizar los datos de consulta de maneras diferentes desde Azure Portal e importarlos en Power BI. Las soluciones de supervisión incluyen consultas y vistas para presentar los datos que recopilan. Las soluciones de información como Application Insights, Azure Monitor para VM y Azure Monitor para contenedores incluyen visualizaciones personalizadas para admitir escenarios de supervisión interactivos.

## <a name="alerting"></a>Alertas

### <a name="operations-manager"></a>Operations Manager

Operations Manager crea alertas como respuesta a eventos predefinidos, cuando se alcanza un umbral de rendimiento y cuando cambia el estado de mantenimiento de un componente supervisado. Incluye la administración completa de las alertas, lo que permite establecer su resolución y asignarlas a distintos operadores o ingenieros del sistema. Se pueden establecer reglas de notificación que especifiquen qué alertas enviarán notificaciones proactivas.

Los módulos de administración incluyen varias reglas de alertas predefinidas para distintas condiciones críticas en la aplicación que se supervisa. Puede ajustar estas reglas o crear reglas personalizadas para los requisitos específicos de su entorno.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor permite crear alertas basadas en una métrica que supera un umbral o en función del resultado de una consulta programada. Las alertas basadas en métricas pueden lograr resultados casi en tiempo real, mientras que las consultas programadas tienen un tiempo de respuesta más largo, en función de la velocidad de ingesta e indexación de los datos. En lugar de limitarse a un agente específico, las alertas de consulta de registro en Azure Monitor permiten realizar análisis con todos los datos almacenados en varias áreas de trabajo. Estas alertas también incluyen datos de una aplicación de Application Insights específica mediante una consulta entre áreas de trabajo.

Aunque las soluciones de supervisión pueden incluir reglas de alerta, normalmente se crean en función de los propios requisitos.

## <a name="workflows"></a>Workflows

### <a name="operations-manager"></a>Operations Manager

Los módulos de administración de Operations Manager contienen cientos de flujos de trabajo individuales y determinan tanto los datos que se van a recopilar como la acción que se debe realizar con ellos. Por ejemplo, una regla podría tomar una muestra de un contador de rendimiento cada pocos minutos y almacenar los resultados para su análisis. Un monitor podría tomar una muestra del mismo contador de rendimiento y comparar su valor con un umbral para determinar el estado de mantenimiento de un objeto supervisado. Otra regla podría ejecutar un script para recopilar y analizar algunos datos en el equipo de un agente, y activar una alerta si devuelve un valor determinado.

Los flujos de trabajo de Operations Manager son independientes entre sí, por lo que resulta difícil realizar un análisis en varios objetos supervisados. Estos escenarios de supervisión deben basarse en los datos después de su recopilación, lo que es posible pero puede ser difícil, y no es habitual.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor separa la recopilación de datos de las acciones y los análisis efectuados a partir de estos datos. Los agentes y otros orígenes de datos escriben datos de registro en un área de trabajo de Log Analytics y datos de métricas en la base de datos de métricas, sin ningún análisis de esos datos ni conocimientos de cómo podrían usarse. El monitor genera las alertas y realizar otras acciones a partir de los datos almacenados, lo que permite realizar análisis con datos de todos los orígenes.

## <a name="extending-base-platform"></a>Ampliación de la plataforma base

### <a name="operations-manager"></a>Operations Manager

Operations Manager implementa toda la lógica de supervisión en un módulo de administración, que puede crear usted mismo o bien obtener de nosotros o de un asociado. Al instalar un módulo de administración, se detectan automáticamente los componentes de la aplicación o el servicio en agentes diferentes, y se implementan las reglas y los monitores adecuados. El módulo de administración contiene definiciones de estado, reglas de alertas, reglas de rendimiento y recopilación de eventos, y vistas, para proporcionar una supervisión completa que admita la aplicación o el servicio de la infraestructura.

El SDK de Operations Manager permite que Operations Manager se integre con plataformas de supervisión de terceros o software ITSM. Algunos asociados utilizan el SDK en los módulos de administración para admitir la supervisión de dispositivos de red y ofrecer experiencias de presentación personalizadas, como el panel de HTML5 de Squared Up o la integración con Microsoft Office Visio.

### <a name="azure-monitor"></a>Azure Monitor

Azure Monitor recopila las métricas y los registros de los recursos de Azure, con poca o ninguna configuración. Las soluciones de supervisión agregan lógica para la supervisión de una aplicación o un servicio, pero siguen funcionando en las consultas y vistas de registro estándar en Monitor. Las soluciones de información, como Application Insights y Azure Monitor para VM, usan la plataforma de Monitor para la recopilación y el procesamiento de datos, y también proporcionan herramientas adicionales para visualizar y analizar los datos. Puede combinar los datos recopilados por las soluciones de información con otros datos, mediante el uso de características de Monitor principales, como las alertas y las consultas de registro.

Monitor admite varios métodos de recopilación de datos de supervisión o administración desde recursos externos o de Azure. Después, se pueden extraer y reenviar los datos desde los almacenes de métricas o de registro a las herramientas de ITSM o supervisión, o bien se pueden realizar tareas administrativas mediante la API REST de Azure Monitor.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Supervisión de los modelos de implementación en la nube](./cloud-models-monitor-overview.md)
