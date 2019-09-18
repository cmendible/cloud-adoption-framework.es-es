---
title: Abordar la complejidad de migrar varias regiones geográficas
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Abordar la complejidad de migrar varias regiones geográficas.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 2d834b9e7c3e661561dc44b8d3104ef819f0c6af
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025483"
---
# <a name="multiple-geographic-regions"></a>Varias regiones geográficas

Cuando las empresas operan en varias regiones geográficas, los trabajos de migración a la nube pueden tener una mayor complejidad. Estas complejidades se manifiestan de tres formas: la distribución de los recursos, los perfiles de acceso de usuario y los requisitos de cumplimiento. Antes de abordar las complejidades relativas a la existencia de varias regiones, resulta importante entender el alcance de la complejidad potencial.

## <a name="general-scope-expansion"></a>Expansión del ámbito general

El enfoque siguiente puede ayudar a evaluar los desafíos posibles y a establecer una línea de acción general:

- Considere una implementación de disponibilidad y gobernanza más sólida.
- Realice un inventario de las geografías afectadas. Compile una lista de las regiones y los países a los que afecta la migración a la nube.
- Documente los requisitos de soberanía de datos: ¿Los países identificados tienen requisitos de cumplimiento que rigen la soberanía de datos?
- Documente la base de usuarios: ¿La migración a la nube afectará a los empleados, asociados o clientes del país identificado?
- Documente los centros de datos y los recursos: ¿En el país identificado hay recursos que se podrían incluir en el trabajo de migración?

Alinee los cambios en el proceso de migración para dirigir el inventario inicial.

### <a name="documenting-complexity"></a>Documentación de la complejidad

La tabla siguiente puede ayudar a documentar los resultados de los pasos anteriores:

|Region  |Country  |Empleados locales  |Usuarios externos locales  |Centros de datos o recursos locales |Requisitos de soberanía de datos  |
|---------|---------|---------|---------|---------|---------|
|Norteamérica     |EE. UU.         |Sí         |Asociados y clientes         |Sí         |Sin         |
|Norteamérica     |Canadá         |Sin         |Clientes         |Sí         |Sí         |
|Europa     |Alemania         |Sí         |Asociados y clientes         |No, solo red         |Sí         |
|Asia Pacífico     |Corea del Sur         |Sí         |Asociados         |Sí         |Sin         |

<!-- markdownlint-disable MD026 -->

### <a name="why-is-data-sovereignty-relevant"></a>¿Por qué es importante la soberanía de datos?

En todo el mundo, las organizaciones gubernamentales han empezado a establecer requisitos de soberanía de datos, como el Reglamento general de protección de datos (RGPD). Con frecuencia, los requisitos de cumplimiento de esta naturaleza requieren localización dentro de una región específica o, incluso, dentro de un país específico para proteger a sus ciudadanos. En algunos casos, los datos que pertenecen a clientes, empleados o asociados se deben almacenar en una plataforma en la nube dentro de la misma región en que se encuentra el usuario final.

Abordar este desafío ha sido una motivación importante para que las empresas que operan a escala global realicen la migración a la nube. Para mantener los requisitos de cumplimiento, algunas empresas han optado por implementar recursos de TI duplicados en los proveedores de nube dentro de la región. En la tabla de ejemplo anterior, Alemania sería un buen ejemplo de este escenario. En este ejemplo, hay clientes, asociados y empleados en Alemania, pero no recursos de TI existentes. Esta empresa puede optar por implementar algunos recursos en un centro de datos dentro del área del RGPD, posiblemente incluso usando los centros de datos de Azure Alemania. Entender cuáles son los datos a los que afectará el RGPD podría ayudar al equipo de adopción de la nube a comprender cuál es el mejor enfoque de migración en este caso.

### <a name="why-is-the-location-of-end-users-relevant"></a>¿Por qué es importante la ubicación de los usuarios finales?

Las empresas que admiten usuarios finales en varios países han desarrollado soluciones técnicas para abordar el tráfico de usuario final. En algunos casos, esto implica la localización de los recursos. En otros escenarios, la empresa puede optar entonces por implementar soluciones WAN globales para abordar diferentes bases de usuarios a través de soluciones centradas en la red. En cualquier caso, la estrategia de migración se podría ver afectada por los perfiles de uso de esos distintos usuarios finales.

Como la empresa admite empleados, asociados y clientes en Alemania pero actualmente no hay centros de datos ene se país, es probable que esta empresa haya implementado algún tipo de solución de línea alquilada para enrutar ese tráfico a los centros de datos de otros países. Este enrutamiento existente presenta un riesgo importante al rendimiento percibido de las aplicaciones migradas. Insertar saltos adicionales en una WAN global establecida y ajustada puede crear la percepción de que las aplicaciones bajan su rendimiento después de la migración. Buscar y corregir estos problemas puede agregar retrasos importantes a un proyecto. En cada uno de los procesos siguientes, se incluyen instrucciones para abordar esta complejidad respecto de los requisitos previos, los recursos, la migración y los procesos de optimización. Comprender los perfiles de usuario de cada país resulta crítico para administrar correctamente esta complejidad.

### <a name="why-is-the-location-of-datacenters-relevant"></a>¿Por qué es importante la ubicación de los centros de datos?

La ubicación de los centros de datos existentes puede afectar a una estrategia de migración. A continuación, se muestran algunos de los impactos más comunes:

**Decisiones sobre la arquitectura:** la ubicación o región de destino es uno de los primeros pasos que se establecen en el diseño de la estrategia de migración. Suele verse afectado por la ubicación de los recursos existentes. Además, la disponibilidad de los servicios en la nube y el costo unitario de esos servicios puede variar de una región a otra. Por lo tanto, entender la ubicación actual y futura de los recursos afecta las decisiones sobre la arquitectura y también puede afectar los cálculos de presupuesto.

**Dependencias de los centros de datos:** según los datos de la tabla anterior, es probable que existan dependencias entre los distintos centros de datos de todo el mundo. En muchas organizaciones que operan en este tipo de escala, es posible que esas dependencias no estén documentadas o que no se comprendan bien. Los enfoques que se usan para evaluar los perfiles de usuario ayudarán a identificar algunas de estas dependencias. Sin embargo, se sugieren pasos adicionales durante el proceso de evaluación para mitigar los riesgos asociados con esta complejidad.

## <a name="implementing-the-general-approach"></a>Implementación del enfoque general

Este enfoque lo controla la información cuantificable. De ese modo, el enfoque siguiente seguirá un modelo controlado por datos para abordar las complejidades de la migración global.

## <a name="suggested-prerequisites"></a>Requisitos previos sugeridos

Se sugiere que el equipo de adopción de la nube empiece con la migración de una carga de trabajo sencilla con la [Guía de migración a Azure](../azure-migration-guide/index.md) antes de intentar una migración a escala global. De este modo, se garantizará que el equipo esté familiarizado con el proceso general de la migración a la nube antes de intentar un escenario de migración más complejo.

Cuando el ámbito de una migración incluye varias regiones, el equipo de adopción de la nube debe evaluar las consideraciones de disponibilidad siguientes:

- Es posible que la soberanía de datos requiera localizar algunos recursos, pero puede que esas restricciones de cumplimiento no rijan muchos de esos recursos. Aspectos como el registro, la creación de informes, el enrutamiento de red, la identidad y otros servicios centrales de TI pueden ser elegibles para hospedarlos como servicios compartidos en varias suscripciones o, incluso, en varias regiones. Se recomienda que el equipo de adopción de la nube evalúe un modelo de servicio de recurso compartido para esos servicios, tal como se describe en la [arquitectura de referencia para una topología radial con servicios compartidos](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services).
- Cuando se implementan varias instancias de entornos similares, un generador de entornos podría crear coherencia, mejorar la gobernanza y acelerar la implementación. El [recorrido de gobernanza de las grandes empresas](../../govern/guides/complex/index.md) establece un enfoque que crea un generador de entornos que escala en varias regiones.

Una vez que el equipo esté familiarizado con el enfoque de línea de base y que la disponibilidad está alineada, es necesario considerar algunos requisitos previos controlados por datos:

- **Detección general:** complete la tabla [Documentación de la complejidad](#documenting-complexity) anterior.
- **Realice un análisis de los perfiles de usuario en cada país afectado:** es importante entender el enrutamiento del usuario final general en una etapa temprana del proceso de migración. Cambiar las líneas alquiladas globales y agregar conexiones como ExpressRoute a un centro de datos en la nube pueden requerir meses de retrasos en la red. Aborde esta complejidad tan pronto como sea posible en el proceso.
- **Racionalización del patrimonio digital inicial:** cada vez que se introduce una complejidad en una estrategia de migración, se debe realizar una racionalización del patrimonio digital inicial. Consulte las instrucciones sobre [racionalización del patrimonio digital](../../digital-estate/index.md) para obtener ayuda.
  - **Requisitos adicionales del patrimonio digital:** establezca directivas de etiquetado para identificar todas las cargas de trabajo afectadas por los requisitos de soberanía de datos. Las etiquetas necesarias deben empezar en la racionalización del patrimonio digital y pasar a los recursos migrados.
- **Evaluación de un modelo radial:** a menudo, los sistemas distribuidos comparten dependencias comunes. Por lo general, esas dependencias se pueden abordar mediante la implementación de un modelo radial. Si bien ese tipo de modelo está fuera del ámbito del proceso de migración, se debe marcar para considerarlo durante las iteraciones futuras de los [procesos de preparación](../../ready/index.md).
- **Asignación de prioridades de los trabajos pendientes de migración:** cuando se requieren cambios en la red para admitir la implementación en producción de una carga de trabajo que admite varias regiones, es importante que el equipo de estrategia en la nube haga un seguimiento de las escalaciones y las administre con respecto a esos cambios en la red. Un mayor nivel de apoyo ejecutivo ayudará a acelerar los cambios. Sin embargo, el impacto más importante es que proporciona al equipo de estrategia la capacidad de cambiar la prioridad de los trabajos pendientes para garantizar que los cambios en la red no bloqueen las cargas de trabajo globales. La prioridad de dichas cargas de trabajo solo se debe establecer una vez que se completen los cambios en la red.

Estos requisitos previos ayudarán a establecer procesos que puedan abordar esta complejidad durante la ejecución de la estrategia de migración.

## <a name="assess-process-changes"></a>Evaluación de los cambios del proceso

Cuando se trata con las complejidades de las bases de usuarios y los recursos globales, hay algunas actividades clave que se deben agregar a la evaluación de todo candidato a la migración. Cada uno de estos cambios aportará claridad al impacto sobre los recursos y los usuarios globales a través de un enfoque controlado por datos.

### <a name="suggested-action-during-the-assess-process"></a>Acción sugerida durante el proceso de evaluación

**Evaluación de las dependencias entre centros de datos:** Las [herramientas de visualización de dependencias de Azure Migrate](https://docs.microsoft.com/azure/migrate/concepts-dependency-visualization) pueden ayudar a identificar las dependencias. El uso de este conjunto de herramientas antes de la migración es un excelente procedimiento recomendado general. Sin embargo, cuando se trabaja con una complejidad global, se vuelve un paso necesario para el proceso de evaluación. A través de una [agrupación de dependencias](https://docs.microsoft.com/azure/migrate/how-to-create-group-machine-dependencies), la visualización puede ayudar a identificar los puertos y las direcciones IP de cualquiera de los recursos que se necesitan para admitir la carga de trabajo.

> [!IMPORTANT]
> Dos notas importantes: en primer lugar, se requiere que un experto en la materia que entienda los esquemas de dirección IP y la ubicación de los recursos identifique los recursos que residen en un centro de datos secundario. En segundo lugar, es importante evaluar tanto las dependencias de nivel inferior y clientes en el objeto visual para comprender las dependencias bidireccionales.

**Identificación del impacto en el usuario global:** las salidas del análisis de perfiles de usuario de requisito previo deben identificar las cargas de trabajo afectadas por los perfiles de usuario globales. Cuando un candidato a la migración se encuentra en la lista de cargas de trabajo afectadas, el arquitecto que prepara la migración debe consultar a los expertos en redes y operaciones para validar las expectativas de rendimiento y enrutamiento de la red. Como mínimo, la arquitectura debería incluir una conexión de ExpressRoute entre el centro de operaciones de red (NOC) más cercano y Azure. La [arquitectura de referencia para las conexiones de ExpressRoute](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/expressroute) pueden ayudar a configurar la conexión necesaria.

**Diseño para el cumplimiento:** las salidas del análisis de perfiles de usuario de requisito previo deben identificar las cargas de trabajo afectadas por los requisitos de soberanía de datos. Durante las actividades de arquitectura del proceso de evaluación, el arquitecto asignado debe consultar a expertos en cumplimiento para comprender los requisitos de migración o implementación en varias regiones. Esos requisitos afectarán considerablemente las estrategias de diseño. Las arquitecturas de referencia para las [aplicaciones web de varias regiones](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) y las [aplicaciones de n niveles de varias regiones](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server) pueden ayudar en el diseño.

> [!WARNING]
> Al usar cualquiera de las arquitecturas de referencia anteriores, puede ser necesario excluir elementos de datos específicos de los procesos de replicación para cumplir con los requisitos de soberanía de datos. Esto agregará un paso adicional al proceso de promoción.

## <a name="migrate-process-changes"></a>Cambios en el proceso de migración

Al migrar una aplicación que se debe implementar en varias regiones, el equipo de adopción de la nube debe considerar algunos aspectos. Estas consideraciones constan del diseño del almacén de Azure Site Recovery, el diseño del servidor de configuración/proceso, los diseños del ancho de banda de la red y la sincronización de datos.

### <a name="suggested-action-during-the-migrate-process"></a>Acción sugerida durante el proceso de migración

**Diseño del almacén de Azure Site Recovery:** Azure Site Recovery es la herramienta sugerida para la replicación nativa de la nube y la sincronización de recursos digitales en Azure. Site Recovery replica los datos sobre el recurso en un almacén de Site Recovery, que está enlazado a una suscripción específica en un centro de datos de Azure y una región específicos. Cuando se replican recursos en una segunda región, es posible que se necesite un segundo almacén de Site Recovery.

**Diseño del servidor de configuración y proceso:** Site Recovery funciona con una instancia local de un servidor de configuración y proceso, que está enlazado a un almacén de Site Recovery único. Esto significa que es posible que sea necesario instalar una segunda instancia de estos servidores en el centro de datos de origen para facilitar la replicación.

**Diseño del ancho de banda de la red:** durante la replicación y la sincronización en curso, los datos binarios se mueven a través de la red, desde el centro de datos de origen al almacén de Site Recovery en el centro de datos de Azure de destino. Este proceso consume ancho de banda. La duplicación de la carga de trabajo en una segunda región doblará la cantidad de ancho de banda consumido. Cuando el ancho de banda es limitado o una carga de trabajo implica una gran cantidad de configuración o la desviación de los datos, puede interferir con el tiempo que se necesita para completar la migración. Lo que es más importante, podría afectar la experiencia de los usuarios o las aplicaciones que siguen dependiendo del ancho de banda del centro de datos de origen.

**Sincronización de datos:** a menudo, el mayor consumo de ancho de banda se origina en la sincronización de la plataforma de datos. Tal como se define en las arquitecturas de referencia de las [aplicaciones web de varias regiones](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) y las [aplicaciones de n niveles de varias regiones](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server), a menudo se requiere la sincronización de datos para mantener alineadas las aplicaciones. Si este es el estado operativo deseado de la aplicación, puede ser aconsejable completar una sincronización entre la plataforma de datos de origen y cada una de las plataformas en la nube antes de migrar los recursos de la aplicación y del nivel intermedio.
**Sincronización de datos:** a menudo, el mayor consumo de ancho de banda se origina en la sincronización de la plataforma de datos. Tal como se define en las arquitecturas de referencia de las [aplicaciones web de varias regiones](https://docs.microsoft.com/azure/architecture/reference-architectures/app-service-web-app/multi-region) y las [aplicaciones de n niveles de varias regiones](https://docs.microsoft.com/azure/architecture/reference-architectures/n-tier/multi-region-sql-server), a menudo se requiere la sincronización de datos para mantener alineadas las aplicaciones. Si este es el estado operativo deseado de la aplicación, puede ser aconsejable completar una sincronización entre la plataforma de datos de origen y cada una de las plataformas en la nube antes de migrar los recursos de la aplicación y del nivel intermedio.

**Recuperación ante desastres de Azure a Azure:** existe una opción alternativa que puede reducir aún más la complejidad. Si los enfoques de sincronización de datos y las escalas de tiempo se enfocan en una implementación en dos pasos, una solución aceptable podría ser la [recuperación ante desastres de Azure a Azure](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-architecture). En este escenario, la carga de trabajo se migra al primer centro de datos de Azure con un almacén de Site Recovery único y un diseño de proceso de configuración o proceso. Una vez que se prueba la carga de trabajo, se puede recuperar en un segundo centro de datos de Azure desde los recursos migrados. Este enfoque reduce el impacto en los recursos del centro de datos de origen y usa las velocidades de transferencia más rápidas y los límites altos de ancho de banda disponibles entre los centros de datos de Azure.

> [!NOTE]
> Este enfoque puede aumentar el costo de la migración a corto plazo, porque podría generar cargos adicionales por el ancho de banda de salida.

## <a name="optimize-and-promote-process-changes"></a>Cambios en los procesos de optimización y promoción

Abordar la complejidad global durante la optimización y promoción podría requerir trabajos duplicados en cada una de las regiones adicionales. Cuando es aceptable una implementación única, puede que todavía se requiera la duplicación de las pruebas empresariales y de los planes de cambios empresariales.

### <a name="suggested-action-during-the-optimize-and-promote-process"></a>Acción sugerida durante el proceso de optimización y promoción

**Prueba preliminar de optimización:** una prueba de automatización inicial puede identificar posibles oportunidades de optimización, como con cualquier trabajo de migración. En el caso de las cargas de trabajo globales, es importante probar la carga de trabajo en cada región de manera independiente, porque cambios menores en la configuración de la red o del centro de datos de Azure de destino podrían afectar el rendimiento.

**Planes de cambios empresariales:** en cualquier escenario de migración complejo, se recomienda crear un plan de cambios empresarial para garantizar la comunicación clara respecto de cualquier cambio que se haga en los procesos empresariales, las experiencias de usuario y el momento de los esfuerzos que se requieren para integrar los cambios. En el caso de los trabajos de migración global, el plan debe incluir las consideraciones para los usuarios finales de cada geografía afectada.

**Pruebas empresariales:** junto con el plan de cambios empresarial, en cada región se pueden requerir pruebas empresariales para garantizar el rendimiento adecuado y el cumplimiento de los patrones de enrutamiento de red modificados.

**Pilotos de promoción:** a menudo, la promoción se realiza como una actividad única, reenrutando el tráfico de producción a las cargas de trabajo migradas. En el caso de los esfuerzos de liberación global, se recomienda que la promoción se realice en pilotos (o colecciones predefinidas de usuarios). Esto permite que el equipo de estrategia de la nube y el equipo de adopción de la nube observen un mejor rendimiento y mejoren el respaldo de los usuarios de cada región. Por lo general, los pilotos de promoción se controlan en el nivel de red al cambiar el enrutamiento de intervalos IP específicos desde los recursos de carga de trabajo de origen a los recursos migrados recientemente. Una vez que se migra una colección especificada de usuarios finales, es posible volver a enrutar el grupo siguiente.

**Optimización de pilotos:** una de las ventajas de los pilotos de promoción es que permiten observaciones más profundas y la optimización adicional de los recursos implementados. Después de un período breve de uso de producción por parte del primer piloto, se sugiere perfeccionar más los recursos migrados cuando así lo permitan los procedimientos de operaciones de TI.

## <a name="next-steps"></a>Pasos siguientes

Otro punto de complejidad, a menudo relacionado con varias regiones, es la necesidad de preparar la migración de [varios centros de datos](./multiple-datacenters.md). Aunque de naturaleza similar, esta complejidad tiene que ver con el volumen de los recursos que se van a migrar cuando se trasladan varios centros de datos a la nube.

> [!div class="nextstepaction"]
> [Migración de varios centros de datos](./multiple-datacenters.md)
