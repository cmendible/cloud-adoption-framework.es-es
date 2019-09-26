---
title: Guía de decisiones sobre regiones
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Más información sobre la selección de regiones en la plataforma de nube.
author: doodlemania2
ms.author: dermar
ms.date: 09/19/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 041e1ccaf6ec0e928b6868f4e8c90849c8d4dea8
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224599"
---
# <a name="azure-regions"></a>Regiones de Azure

Azure se compone de muchas regiones repartidas por todo el mundo. Cada una de las [regiones de Azure](https://azure.microsoft.com/global-infrastructure/regions) tiene un conjunto específico de características que hacen que la elección de la región que se va a usar sea muy importante.

1. **Servicios disponibles:** los servicios que se implementan en cada región difieren en función de una serie de factores. Para implementar su carga de trabajo, tendrá que seleccionar una región en que incluya el servicio que desea. Para más información acerca de qué servicios están disponibles en cada región, consulte [Productos disponibles por región](https://azure.microsoft.com/global-infrastructure/services).
1. **Capacidad**: cada región tiene una capacidad máxima. Aunque esto normalmente pasa desapercibido al usuario final, puede afectar a qué tipos de suscripciones pueden implementar los distintos tipos de servicios y en qué circunstancias. Esto es diferente a las cuotas de suscripción. Si planea una migración masiva de centros de datos a Azure, puede que desee consultar con el equipo de campo local de Azure o con el administrador de cuentas para confirmar que puede realizar la implementación a la escala necesaria.
1. **Restricciones:** la implementación de servicios en determinadas regiones está sujeta a ciertas restricciones. Por ejemplo, algunas regiones solo están disponibles como destino de copia de seguridad o de conmutación por error. Otras restricciones que se deben tener en cuenta son los [requisitos de soberanía de los datos](https://azure.microsoft.com/global-infrastructure/geographies).
1. **Soberanía:** hay regiones específicas dedicadas a entidades soberanas concretas. Aunque todas ellas son regiones de Azure, estas regiones soberanas están completamente aisladas del resto de Azure, no necesariamente las administra Microsoft y pueden tener restricciones que dependen del cliente. Estas regiones soberanas son:
    1. [Azure en China](https://azure.microsoft.com/global-infrastructure/china)
    1. [Azure Alemania](https://azure.microsoft.com/global-infrastructure/germany); en desuso en favor de las regiones alemanas estándar de Azure (no soberanas)
    1. [Azure US Government](https://azure.microsoft.com/global-infrastructure/government)
    1. Nota: hay dos regiones en [Australia](https://azure.microsoft.com/global-infrastructure/australia) que administra Microsoft, pero que se proporcionan para el gobierno australiano y sus clientes y contratistas y, por tanto, tienen restricciones para el cliente similares a las del resto de nubes soberanas.

## <a name="operating-in-multiple-geographic-regions"></a>Funcionamiento en varias regiones geográficas

Cuando las empresas operan en varias regiones geográficas, lo cual es importante para mejorar la resistencia, se da una mayor complejidad. Esta complejidad se manifiesta de cuatro formas principales:

- Distribución de los recursos
- Perfiles de acceso de los usuarios
- Requisitos de cumplimiento
- Resistencia regional

A medida que profundicemos en estos puntos, empezará a comprender lo importante que es la selección de la región en la estrategia global de adopción de la nube. Empecemos por las consideraciones sobre la red.

## <a name="networking-considerations"></a>Consideraciones sobre redes

Cualquier implementación sólida en la nube requiere una red bien ponderada que tenga en cuenta las regiones de Azure. Después de reflexionar sobre las características anteriores acerca de en qué regiones realizar la implementación, se debe implementar la red. Aunque el análisis exhaustivo de las redes queda fuera del ámbito de este artículo, se deben tener en cuenta algunas consideraciones:

1. Las regiones de Azure se implementan por pares. Si se produce un error grave en una región, se designa otra región dentro del mismo límite geopolítico* como su región emparejada. La implementación en regiones emparejadas debe considerarse una estrategia de resistencia principal y secundaria. *Azure Brasil es una excepción importante cuya región emparejada es Centro y Sur de EE. UU. Para más información, [consulte aquí](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions).
    1. Azure Storage admite el [almacenamiento con redundancia geográfica (GRS)](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs), lo que implica que se almacenan tres copias de los datos en la región primaria y tres copias adicionales en la región emparejada. En el almacenamiento con redundancia geográfica no se puede cambiar el emparejamiento del almacenamiento.
    1. Los servicios que se basan en este tipo de almacenamiento de Azure Storage pueden sacar el máximo partido a esta funcionalidad de región emparejada. Para ello, se deben orientar las aplicaciones y la red para que admitan dicha funcionalidad.
    1. Si no tiene previsto aprovechar GRS para apoyar sus necesidades de resistencia regional, se recomienda que _NO_ utilice la región emparejada como secundaria. En caso de error regional, los recursos de la región emparejada estarán sometidos a una gran presión mientras se migran los recursos. Realizar la recuperación en un sitio alternativo evita esa presión y proporcionar más velocidad.
    > [!WARNING]
    > No intente utilizar el almacenamiento con redundancia geográfica de Azure para las copias de seguridad o la recuperación de máquinas virtuales. En vez de eso, utilice [Azure Backup](https://azure.microsoft.com/services/backup) y [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery), además de [Managed Disks](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview), para mejorar la resistencia de las cargas de trabajo de IaaS.
2. Azure Backup y Azure Site Recovery funcionan de forma conjunta con el diseño de la red para facilitar la resistencia regional para sus necesidades de IaaS y de copia de seguridad de datos. Asegúrese de que la red está optimizada para que las transferencias de datos permanezcan en la red troncal de Microsoft y utilicen el [emparejamiento de redes virtuales](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview) si es posible. En su lugar, algunas organizaciones de mayor tamaño con implementaciones globales pueden utilizar [ExpressRoute Premium](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) para enrutar el tráfico entre regiones, lo cual puede suponer un ahorro en los cargos de salida de la región.
3. Los grupos de recursos de Azure son construcciones específicas de cada región. Sin embargo, es normal que los recursos de un grupo de recursos abarquen varias regiones. Si es así, es importante tener en cuenta que, en caso de error en una región, las operaciones del plano de control en un grupo de recursos producirán un error en la región afectada, aunque los recursos de otras regiones (dentro de ese grupo de recursos) sigan funcionando. Esto puede afectar a la red y al diseño del grupo de recursos.
4. Muchos servicios de PaaS de Azure admiten [puntos de conexión de servicio](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) o [Private Link](https://docs.microsoft.com/azure/private-link/private-link-overview). Ambas soluciones afectan notablemente a aspectos como la resistencia, la migración y la gobernanza regionales.
5. Muchos servicios de PaaS se basan en sus propias soluciones de resistencia regional. Por ejemplo, Azure SQL Database le permite replicar fácilmente en N regiones adicionales, como también hace CosmosDB. Algunos servicios no incluyen ninguna dependencia de región como Azure DNS. A la hora de considerar qué servicios va a utilizar en el proceso de adopción, asegúrese de que comprende claramente las funcionalidades de conmutación por error y los pasos de recuperación que puede necesitar cada servicio de Azure.
6. Además de realizar la implementación en varias regiones para dar servicio a la recuperación ante desastres, muchas organizaciones deciden implementarse en un patrón activo-activo para que no sea necesaria ninguna conmutación por error. Esto tiene la ventaja adicional de proporcionar equilibrio de carga global, una mejora de la tolerancia a errores y mejor rendimiento de red. Para sacar el máximo partido a este patrón, las aplicaciones deben admitir la ejecución activa-activa en varias regiones.

> [!WARNING]
> Las regiones de Azure son construcciones de alta disponibilidad a las que se ha aplicado un Acuerdo de Nivel de Servicio a los servicios que se ejecutan en ellas. Sin embargo, nunca debe usar una única dependencia de región en aplicaciones críticas. Disponga siempre de algún plan ante errores regionales y practique medidas de recuperación y de mitigación.

Después de reflexionar sobre la topología de red que necesita para preservar constantemente el funcionamiento, necesitará documentación adicional y alinear los procesos. El enfoque siguiente puede ayudar a evaluar los desafíos posibles y a establecer una línea de acción general:

- Considere una implementación de disponibilidad y gobernanza más sólida.
- Realice un inventario de las geografías afectadas. Cree una lista de las regiones y los países afectados.
- Documente los requisitos de soberanía de datos: ¿Los países identificados tienen requisitos de cumplimiento que rigen la soberanía de datos?
- Documente la base de usuarios: ¿La migración a la nube afectará a los empleados, asociados o clientes del país identificado?
- Documente los centros de datos y los recursos: ¿En el país identificado hay recursos que se podrían incluir en el trabajo de migración?
- Documente los requisitos de disponibilidad y conmutación por error de la SKU regional.

Alinee los cambios en el proceso de migración para dirigir el inventario inicial.

## <a name="documenting-complexity"></a>Documentación de la complejidad

La tabla siguiente puede ayudar a documentar los resultados de los pasos anteriores:

|Region  |Country  |Empleados locales  |Usuarios externos locales  |Centros de datos o recursos locales |Requisitos de soberanía de datos  |
|---------|---------|---------|---------|---------|---------|
|Norteamérica     |EE. UU.         |Sí         |Asociados y clientes         |Sí         |Sin         |
|Norteamérica     |Canadá         |Sin         |Clientes         |Sí         |Sí         |
|Europa     |Alemania         |Sí         |Asociados y clientes         |No, solo red         |Sí         |
|Asia Pacífico     |Corea del Sur         |Sí         |Asociados         |Sí         |Sin         |

<!-- markdownlint-disable MD026 -->

## <a name="data-sovereignty-relevancy"></a>Importancia de la soberanía de datos

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

Cuando el ámbito de una migración incluye varias regiones, el equipo de adopción de la nube debe evaluar las consideraciones de disponibilidad siguientes:

- Es posible que la soberanía de datos requiera localizar algunos recursos, pero puede que esas restricciones de cumplimiento no rijan muchos de esos recursos. Aspectos como el registro, la creación de informes, el enrutamiento de red, la identidad y otros servicios centrales de TI pueden ser elegibles para hospedarlos como servicios compartidos en varias suscripciones o, incluso, en varias regiones. Se recomienda que el equipo de adopción de la nube evalúe un modelo de servicio de recurso compartido para esos servicios, tal como se describe en la [arquitectura de referencia para una topología radial con servicios compartidos](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services).
- Cuando se implementan varias instancias de entornos similares, un generador de entornos podría crear coherencia, mejorar la gobernanza y acelerar la implementación. El [recorrido de la gobernanza de las grandes empresas](../../govern/guides/complex/index.md) establece un enfoque que crea un entorno que se escala en varias regiones.

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
