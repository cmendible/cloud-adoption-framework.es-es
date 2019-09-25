---
title: Escalado de una migración en Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información acerca de cómo Contoso administra una migración con escala a Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/08/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: azure-migrate
ms.openlocfilehash: fbb1e57d1073286d9b92db96dbf923eb28612f49
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224085"
---
# <a name="scale-a-migration-to-azure"></a>Escalado de una migración en Azure

En este artículo se muestra cómo la empresa ficticia Contoso realiza una migración a escala en Azure. Consideran cómo planear y realizar una migración de más de 3000 cargas de trabajo, 8000 bases de datos y más de 10 000 máquinas virtuales.

## <a name="business-drivers"></a>Impulsores del negocio

El equipo directivo de TI ha trabajado estrechamente con sus socios comerciales para comprender lo quieren lograr con esta migración:

- **Abordar el crecimiento del negocio.** Contoso está creciendo y, como resultado, sus sistemas locales e infraestructura están bajo presión.
- **Aumentar la eficacia.** Contoso debe quitar procedimientos innecesarios y optimizar los procesos para sus desarrolladores y usuarios. La empresa necesita que el departamento de TI sea rápido y no malgaste tiempo ni dinero a fin de satisfacer más rápidamente los requisitos del cliente.
- **Aumentar la agilidad.** el equipo de TI de Contoso necesita más capacidad de respuesta a las necesidades de la empresa. Debe poder reaccionar con más rapidez que los cambios del mercado para facilitar el éxito en una economía global. No se debe interponer en el camino ni bloquear el negocio.
- **Escala.** A medida que el negocio crece satisfactoriamente, el equipo de TI de Contoso debe facilitar sistemas que puedan crecer al mismo ritmo.
- **Mejorar los modelos de costos.** Contoso desea reducir los requisitos de capital del presupuesto de TI. Asimismo, desea utilizar las capacidades de la nube para escalar y reducir la necesidad de hardware demasiado caro.
- **Reducir los costos de licencias.** Contoso quiere minimizar los costos de la nube.

## <a name="migration-goals"></a>Objetivos de la migración

El equipo de la nube de Contoso ha establecido los objetivos de esta migración. Estos objetivos se usaron para determinar el mejor método de migración.

**Requisitos** | **Detalles**
--- | ---
**Pasar rápidamente a Azure** | Contoso desea comenzar a mover máquinas virtuales y aplicaciones a Azure tan pronto como sea posible.
**Crear un inventario completo** | Contoso desea un inventario completo de todas las aplicaciones, las bases de datos y las máquinas virtuales de la organización.
**Evaluar y clasificar las aplicaciones** | Contoso quiere aprovechar al máximo la nube. De forma predeterminada, Contoso supone que todos los servicios se ejecutarán como PaaS. Sin embargo, IaaS se usará cuando no sea adecuado usar PaaS.
**Formarse y pasar a DevOps** | Contoso desea pasar a un modelo DevOps. Para ello, proporcionará formación de Azure y DevOps, y reorganizará los equipos según sea necesario.

Después de precisar los objetivos y requisitos, Contoso revisa la huella de TI e identifica el proceso de migración.

## <a name="current-deployment"></a>Implementación actual

Después de planear y configurar una [infraestructura de Azure](./contoso-migration-infrastructure.md), y probar diferentes combinaciones de migración de prueba de concepto (POC), tal como se detalla en la tabla anterior, Contoso está listo para embarcarse en una migración completa a Azure a escala. Esto es lo que Contoso desea migrar.

<!--markdownlint-disable MD033 -->

**Elemento** | **Volumen** | **Detalles**
--- | --- | ---
**Cargas de trabajo** | Más de 3000 aplicaciones | Las aplicaciones se ejecutan en máquinas virtuales.<br/><br/>  Las aplicaciones son de Windows, de OSS LAMP o están basadas en SQL.
**Bases de datos** | Alrededor de 8500 | Las bases de datos incluyen SQL Server, MySQL, PostgreSQL.
**VM** | Más de 35 000 | Las máquinas virtuales se ejecutan en hosts de VMware y las administran servidores vCenter.

<!--markdownlint-enable MD033 -->

## <a name="migration-process"></a>Proceso de migración

Ahora que Contoso ha precisado las claves del negocio y los objetivos de la migración, determina un enfoque con cuatro puntos para el proceso de migración:

- **Fase 1. Evaluación:** detectar los activos actuales y averiguar si son adecuados para la migración a Azure.
- **Fase 2. Migración:** mover los recursos a Azure. La manera de mover las aplicaciones y objetos a Azure dependerá de la aplicación, y de lo que se quiere conseguir.
- **Fase 3. Optimización:** después de mover los recursos a Azure, Contoso debe mejorarlos y simplificarlos para obtener el máximo rendimiento y eficacia.
- **Fase 4. Protección y administración:** con todo ya preparado, Contoso usa los recursos de administración y seguridad de Azure para controlar, proteger y supervisar sus aplicaciones en la nube en Azure.

Estas fases no son consecutivas en toda la organización. Cada parte del proyecto de migración de Contoso estará en una fase diferente del proceso de evaluación y migración. La optimización, la seguridad y la administración serán continuas a lo largo del tiempo.

## <a name="phase-1-assess"></a>Fase 1: Evaluación

Contoso inicia el proceso con la detección y evaluación de las aplicaciones, la infraestructura y los datos locales. Esto es lo que Contoso hará:

- Contoso debe detectar las aplicaciones, asignar las dependencias entre aplicaciones y decidir la prioridad y el orden de la migración.
- A medida que Contoso realiza esta evaluación, se creará un inventario detallado de las aplicaciones y recursos. Junto con el nuevo inventario, Contoso usará y actualizará la Base de datos de administración de configuración (CMDB) y el catálogo de servicios.
  - La CMDB contiene la configuración técnica de las aplicaciones de Contoso.
  - El catálogo de servicios documenta los detalles operativos de las aplicaciones, incluidos los socios comerciales asociados y los Acuerdos de Nivel de Servicio (SLA)

### <a name="discover-apps"></a>Descubrir aplicaciones

Contoso ejecuta miles de aplicaciones a través de una amplia gama de servidores. Además de la CMDB y el catálogo de servicios, Contoso necesita herramientas de detección y evaluación.

- Las herramientas deben proporcionar un mecanismo que introduzca datos de evaluación en el proceso de migración.
- Las herramientas de evaluación deben proporcionar datos que ayuden a crear un inventario inteligente de los recursos físicos y virtuales de Contoso. Estos datos deben incluir información de perfil y métricas de rendimiento.
- Una vez completada la detección, Contoso debería disponer de un inventario completo de los recursos y los metadatos asociados con estos. Este inventario se usará para definir el plan de migración.

### <a name="identify-classifications"></a>Identificar las clasificaciones

Contoso identifica algunas categorías comunes para clasificar los recursos en el inventario. Estas clasificaciones son fundamentales para la toma de decisiones de Contoso para la migración. La lista de clasificación ayuda a establecer prioridades en la migración e identificar problemas complejos.

**Categoría** | **Valor asignado** | **Detalles**
--- | --- | ---
Grupo de negocios | Lista de nombres de grupos de negocios | ¿Qué grupo es responsable del artículo del inventario?
Candidato POC | S/N | ¿Puede usarse la aplicación como POC o usuario pionero para la migración a la nube?
Deuda técnica | Ninguna/Alguna/Grave | ¿El artículo del inventario se está ejecutando o está utilizando un producto, plataforma o sistema operativo que no es compatible?
Implicaciones de Firewall | S/N | ¿La aplicación se comunica con tráfico externo/Internet?  ¿Se integra con un firewall?
Problemas de seguridad | S/N | ¿Se conoce algún problema de seguridad en la aplicación?  ¿La aplicación usa datos sin cifrar o plataformas obsoletas?

### <a name="discover-app-dependencies"></a>Detectar dependencias de la aplicación

Como parte del proceso de evaluación, Contoso debe identificar dónde se ejecutan las aplicaciones y averiguar las dependencias y las conexiones entre los servidores de aplicaciones. Contoso asigna el entorno en diferentes pasos.

1. Como primer paso, Contoso detecta cómo los servidores y los equipos se asignan a aplicaciones individuales, ubicaciones de red y grupos.
2. Con esta información, Contoso puede identificar claramente las aplicaciones que tienen pocas dependencias y que, por tanto, son adecuadas para una migración rápida.
3. Contoso puede usar la asignación para identificar las dependencias y las comunicaciones más complejas entre servidores de aplicaciones. A continuación, Contoso podrá agrupar los servidores lógicamente para representar las aplicaciones y planear una estrategia de migración en función de estos grupos.

Una vez concluida la asignación, Contoso puede garantizar que todos los componentes de la aplicación se identifican y se tienen en cuenta al crear el plan de migración.

![Mapa de dependencia](./media/contoso-migration-scale/dependency-map.png)

### <a name="evaluate-apps"></a>Evaluación de aplicaciones

Como último paso en el proceso de detección y evaluación, Contoso puede evaluar los resultados de la evaluación y de la asignación para averiguar cómo migrar cada aplicación al Catálogo de servicios.

Para capturar este proceso de evaluación, se agregan un par de clasificaciones adicionales al inventario.

**Categoría** | **Valor asignado** | **Detalles**
--- | --- | ---
Grupo de negocios | Lista de nombres de grupos de negocios | ¿Qué grupo es responsable del artículo del inventario?
Candidato POC | S/N | ¿Puede usarse la aplicación como POC o usuario pionero para la migración a la nube?
Deuda técnica | Ninguna/Alguna/Grave | ¿El artículo del inventario se está ejecutando o está utilizando un producto, plataforma o sistema operativo que no es compatible?
Implicaciones de Firewall | S/N | ¿La aplicación se comunica con tráfico externo/Internet?  ¿Se integra con un firewall?
Problemas de seguridad | S/N | ¿Se conoce algún problema de seguridad en la aplicación?  ¿La aplicación usa datos sin cifrar o plataformas obsoletas?
Estrategia de migración | Rehospedar, refactorizar, rediseñar y recompilar | ¿Qué tipo de migración necesita la aplicación? ¿Cómo se implementará la aplicación en Azure? [Más información](./contoso-migration-overview.md#migration-patterns).
Complejidad técnica | 1-5 | ¿Cuál es el nivel de complejidad de la migración? Este valor debe definirlo Contoso DevOps y sus asociados relevantes.
Crucial para la empresa | 1-5 | ¿Qué importancia tiene la aplicación para la empresa? Por ejemplo, a una aplicación de un grupo de trabajo pequeño podría asignársele una puntuación de 1, mientras que a una aplicación fundamental que use toda la organización se le asignaría una puntuación de 5. Esta puntuación afectará al nivel de prioridad de la migración.
Prioridad de la migración | 1/2/3 | ¿Cuál es la prioridad de migración de la aplicación?
Riesgo de migración | 1-5 | ¿Cuál es el nivel de riesgo de migrar la aplicación? Este valor deben definirlo Contoso DevOps y sus asociados relevantes.

### <a name="figure-out-costs"></a>Averiguar los costos

Para averiguar los costos y el ahorro potencial de la migración a Azure, Contoso puede usar la [calculadora del costo total de propiedad (TCO)](https://azure.microsoft.com/pricing/tco/calculator) para calcular y comparar el TCO de Azure con una implementación local comparable.

### <a name="identify-assessment-tools"></a>Identificar las herramientas de valoración

Contoso decide qué herramienta se usará para detectar, evaluar y crear el inventario. Contoso identifica diferentes herramientas y servicios de Azure, scripts y herramientas de la aplicación, y herramientas de asociados. En concreto, Contoso está interesado en cómo Azure Migrate puede usarse para evaluar a escala.

#### <a name="azure-migrate"></a>Azure Migrate

El servicio Azure Migrate le ayuda a detectar y evaluar VM de VMware locales que se están preparando para la migración a Azure. Esto es lo que hace Azure Migrate:

1. Descubrir: detecta las máquinas virtuales locales de VMware.
    - Azure Migrate admite la detección de varios servidores vCenter (en serie) y puede ejecutar detecciones en diferentes proyectos de Azure Migrate.
    - Azure Migrate realiza la detección por medio de una VM de VMware ejecutando Migrate Collector. El mismo recopilador puede detectar máquinas virtuales en diferentes servidores vCenter y enviar datos a diferentes proyectos.
2. Evaluación de la preparación: evalúe si las máquinas locales son apropiadas para ejecutarse en Azure. La evaluación incluye:
    - Recomendaciones de tamaño: averigüe el tamaño recomendado de las máquinas virtuales de Azure en función del historial de rendimiento de las máquinas virtuales locales.
    - Coste mensual estimado: calcule el costo estimado de la ejecución de máquinas locales en Azure.
3. Identificar las dependencias: visualice las dependencias de las máquinas locales, para crear grupos de máquinas óptimos para la migración y la evaluación.

![Azure Migrate](./media/contoso-migration-scale/azure-migrate.png)

##### <a name="migrate-at-scale"></a>Migrar a escala

Contoso necesita usar Azure Migrate correctamente para determinar la escala de esta migración.

- Contoso hará una evaluación de aplicación por aplicación con Azure Migrate. Esto garantiza que Azure Migrate devolverá los datos oportunamente a Azure Portal.
- Los administradores de Contoso leen acerca de la [implementación de Azure Migrate a escala](https://docs.microsoft.com/azure/migrate/how-to-scale-assessment)
- Contoso anota un resumen de los límites de Azure Migrate en la tabla siguiente.

**Acción** | **Límite**
--- | ---
Crear un proyecto de Azure Migrate | 10 000 máquinas virtuales
Detección | 10 000 máquinas virtuales
Evaluación | 10 000 máquinas virtuales

Contoso usará Azure Migrate como se indica a continuación:

- En vCenter, Contoso va a organizar las máquinas virtuales en carpetas. Esto les permitirá concentrarse fácilmente al realizar una evaluación con respecto a las máquinas virtuales en una carpeta específica.
- Azure Migrate usa Azure Service Map para evaluar las dependencias entre los equipos. Esto requiere la instalación de agentes en las máquinas virtuales que deben evaluarse.
  - Contoso usará scripts automatizados para instalar los agentes necesarios de Windows o Linux.
  - Mediante scripts, Contoso puede realizar la instalación en las VM desde una carpeta vCenter.

#### <a name="database-tools"></a>Herramientas de base de datos

Además de Azure Migrate, Contoso usará herramientas específicas para la evaluación de la base de datos. Herramientas como [Data Migration Assistant](/sql/dma/dma-overview?view=sql-server-2017) ayudarán a evaluar las bases de datos de SQL Server para la migración.

Data Migration Assistant (DMA) puede ayudar a Contoso para averiguar si las bases de datos locales son compatibles con las diferentes soluciones de bases de datos de Azure, como Azure SQL Database, SQL Server en ejecución en una máquina virtual de Azure IaaS e Instancia administrada de Azure SQL Database.

Además de DMS, Contoso tiene algunos otros scripts que usan para detectar y documentar las bases de datos de SQL Server. Estos se encuentran en el repositorio de GitHub.

#### <a name="partner-assessment-tools"></a>Herramientas de evaluación de asociados

Hay otras herramientas de asociados que pueden ayudar a Contoso a evaluar el entorno local para la migración a Azure. [Obtenga más información](https://azure.microsoft.com/migration/partners) acerca de los asociados de migración de Azure.

## <a name="phase-2-migrate"></a>Fase 2: Migrar

Una vez concluida la evaluación, Contoso debe identificar herramientas para mover sus aplicaciones, datos e infraestructura a Azure.

### <a name="migration-strategies"></a>Estrategias de migración

Hay cuatro estrategias de migración generales que Contoso puede considerar.

<!--markdownlint-disable MD033 -->

**Estrategia** | **Detalles** | **Uso**
--- | --- | ---
**Rehospedaje** | Esta opción sin necesidad de escribir código, que a menudo se denomina "migración mediante lift and shift", permite migrar las aplicaciones actuales a Azure con rapidez.<br/><br/> Una aplicación se migra tal cual, con las ventajas que ofrece la nube, sin correr el riesgo ni incurrir en los costos asociados con los cambios de código. | Contoso puede rehospedar aplicaciones menos estratégicas, que no requieren ningún cambio de código.
**Refactorización** | También conocida como "reempaquetado", esta estrategia requiere una mínima cantidad de cambios en el código de la aplicación o en la configuración para conectar la aplicación a Azure PaaS, y aprovechar mejor las capacidades de la nube. | Contoso puede refactorizar aplicaciones estratégicas para conservar la misma funcionalidad básica, pero moverlas para que se ejecuten en una plataforma Azure como Azure App Service.<br/><br/> Esta acción requiere cambios mínimos en el código.<br/><br/> Por otro lado, Contoso deberá mantener una plataforma de máquina virtual, ya que esta ya no la administrara Microsoft.
**Rediseño** | Esta estrategia modifica o amplía una base de código de aplicación para optimizar la arquitectura de la aplicación para las capacidades y la escala de la nube.<br/><br/> Moderniza una aplicación para que tenga una arquitectura resistente y muy escalable que se puede implementar de forma independiente.<br/><br/> Los servicios de Azure permiten agilizar el proceso, escalar aplicaciones con confianza y administrar las aplicaciones con facilidad.
**Recompilación** | Esta estrategia recompila una aplicación desde cero con tecnologías nativas de la nube.<br/><br/> La plataforma como servicio (PaaS) de Azure ofrece un entorno de desarrollo e implementación completo en la nube. Así mismo, elimina algunos gastos y la complejidad de las licencias de software, así como la necesidad de una infraestructura de aplicaciones subyacente, middleware y otros recursos. | Contoso puede volver a escribir aplicaciones críticas desde cero, para aprovechar las ventajas de las tecnologías de la nube, como los ordenadores sin servidor o los microservicios.<br/><br/> Contoso administrará la aplicación y los servicios que desarrolla, y Azure administrará todo lo demás.

<!--markdownlint-enable MD033 -->

También hay que tener en cuenta los datos, especialmente con el volumen de bases de datos que tiene Contoso. De manera predeterminada, Contoso usa los servicios PaaS, como Azure SQL Database, para aprovechar al máximo las características de la nube. Al cambiar a un servicio PaaS para bases de datos, Contoso solo tendrá que mantener los datos, dejando que Microsoft se encargue de la plataforma subyacente.

### <a name="evaluate-migration-tools"></a>Evaluación de las herramientas de migración

Contoso usa principalmente un par de servicios y herramientas de Azure para la migración:

- [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview): herramienta que coordina la recuperación ante desastres y migra las máquinas virtuales locales a Azure.
- [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview): herramienta que migra las bases de datos locales como SQL Server, MySQL y Oracle a Azure.

#### <a name="azure-site-recovery"></a>Azure Site Recovery

Azure Site Recovery es el servicio principal de Azure para orquestar la recuperación ante desastres y la migración desde Azure y desde sitios locales a Azure.

1. Site Recovery permite y organiza la replicación de los sitios locales a Azure.
2. Cuando se configura y ejecuta la replicación, los equipos locales pueden conmutar por error a Azure, completando la migración.

Contoso ya [completó una prueba de concepto](./contoso-migration-rehost-vm.md) para ver cómo puede ayudarles Site Recovery a migrar a la nube.

##### <a name="using-site-recovery-at-scale"></a>Uso de Site Recovery en la escala

Contoso planea realizar múltiples migraciones mediante "lift-and-shift". Para asegurarse de que esto funciona, Site Recovery replicará lotes de aproximadamente 100 máquinas virtuales a la vez. Para averiguar cómo funcionará esto, Contoso necesita planear la capacidad para la migración de Site Recovery propuesta.

- Contoso necesita recopilar información acerca de sus volúmenes de tráfico. En particular:
  - Contoso necesita determinar la frecuencia de cambio para las máquinas virtuales que quiere replicar.
  - Contoso también debe tener en cuenta la conectividad de red desde el sitio local a Azure.
- En respuesta a los requisitos de capacidad y volumen, Contoso deberá asignar un ancho de banda suficiente basado en la frecuencia de cambio diaria de las máquinas virtuales necesarias, para así cumplir con el objetivo del punto de recuperación (RPO).
- Por último, debe calcularse cuántos servidores se necesitan para ejecutar los componentes de Site Recovery que se necesitan para la implementación.

###### <a name="gather-on-premises-information"></a>Recopilación de información local

Contoso puede usar la herramienta [Site Recovery Deployment Planner](https://docs.microsoft.com/azure/site-recovery/site-recovery-deployment-planner) para completar estos pasos:

- Contoso puede usar la herramienta para generar un perfil de máquinas virtuales de forma remota sin un impacto en el entorno de producción. Esto ayuda a identificar los requisitos de ancho de banda y almacenamiento para la replicación y la conmutación por error.
- Contoso puede ejecutar la herramienta sin que sea preciso instalar localmente ningún componente de Site Recovery.
- La herramienta recopila información sobre máquinas virtuales compatibles e incompatibles, discos por máquina virtual y la actividad de datos por disco. También identifica los requisitos de ancho de banda de red y de la infraestructura de Azure necesaria para una replicación y conmutación por error correctas.
- A continuación, Contoso debe asegurarse de que se ejecute la herramienta de planeación en una máquina de Windows Server que coincida con los requisitos mínimos del servidor de configuración de Site Recovery. El servidor de configuración es una máquina de Site Recovery necesaria para poder replicar máquinas virtuales de VMware locales.

###### <a name="identify-site-recovery-requirements"></a>Identificación de los requisitos de Site Recovery

Además de las máquinas virtuales que se replican, Site Recovery requiere una serie de componentes para la migración de VMware.

<!--markdownlint-disable MD033 -->

**Componente** | **Detalles**
--- | ---
**Servidor de configuración** | Normalmente, una máquina virtual de VMware se configura con una plantilla de OVF.<br/><br/> El componente servidor de configuración coordina las comunicaciones entre el entorno local y Azure y administra la replicación de datos.
**Servidor de proceso** | Se instala de forma predeterminada en el servidor de configuración.<br/><br/> El componente del servidor de procesos recibe los datos de la replicación; los optimiza mediante almacenamiento en caché, compresión y cifrado, y los envía a Azure Storage.<br/><br/> El servidor de procesos también instala Azure Site Recovery Mobility Service en las máquinas virtuales que se van a replicar y realiza la detección automática de las máquinas locales.<br/><br/> Las implementaciones de escalado necesitan servidores de procesos independientes y adicionales para controlar grandes volúmenes de tráfico de replicación.
**Mobility Service** | El agente de Mobility Service se instala en cada una de las máquinas virtuales de VMware que se va a migrar con Site Recovery.

<!--markdownlint-enable MD033 -->

Contoso necesita averiguar cómo implementar estos componentes, en función de las consideraciones de capacidad.

<!--markdownlint-disable MD033 -->

**Componente** | **Requisitos de capacidad**
--- | ---
**Frecuencia de cambio de datos diaria máx.** | Un servidor de un solo proceso puede administrar una frecuencia de cambio diaria de hasta 2 TB. Puesto que una máquina virtual solo puede usar un servidor de procesos, la frecuencia de cambio de datos diaria máxima que se admite para una máquina virtual replicada es de 2 TB.
**Rendimiento máximo** | Una cuenta de almacenamiento de Azure estándar puede controlar un máximo de 20 000 solicitudes por segundo y las operaciones de entrada/salida por segundo (IOPS) en una máquina virtual de replicación no deben superar este límite. Por ejemplo, si una máquina virtual tiene 5 discos y cada disco genera 120 E/S por segundo (8 K de tamaño) en la máquina virtual, se encontrará dentro del límite de 500 de Azure por E/S por segundo por disco.<br/><br/> Tenga en cuenta que el número de cuentas de almacenamiento necesario es igual al IOPS de máquina de origen total dividido por 20 000. Una máquina replicada solo puede pertenecer a una cuenta de almacenamiento en Azure.
**Servidor de configuración** | Según la estimación de Contoso de replicar 100-200 máquinas virtuales a la vez, y los [requisitos de configuración del tamaño de servidor](https://docs.microsoft.com/azure/site-recovery/site-recovery-plan-capacity-vmware#size-recommendations-for-the-configuration-server-and-inbuilt-process-server), Contoso calcula que necesita una máquina de servidor de configuración con las siguientes especificaciones:<br/><br/> CPU: 16 vCPUs (2 sockets * 8 núcleos @ 2,5 GHz)<br/><br/> Memoria: 32 GB<br/><br/> Disco de caché: 1 TB<br/><br/> Frecuencia de cambio de datos: 1 TB a 2 TB.<br/><br/> Además de los requisitos de tamaño, Contoso deberá asegurarse de que el servidor de configuración está ubicado de forma óptima, en la misma red y segmento LAN que las máquinas virtuales que se van a migrar.
**Servidor de proceso** | Contoso implementará un servidor de procesos dedicado e independiente con capacidad para replicar entre 100 y 200 máquinas virtuales:<br/><br/> CPU: 16 vCPUs (2 sockets * 8 núcleos @ 2,5 GHz)<br/><br/> Memoria: 32 GB<br/><br/> Disco de caché: 1 TB<br/><br/> Frecuencia de cambio de datos: 1 TB a 2 TB.<br/><br/> El servidor de procesos trabajará duro y como tal debe estar ubicado en un host ESXi que pueda manejar la E/S del disco, el tráfico de red y la CPU requeridos para la replicación. Contoso se planteará la posibilidad de contar con un host dedicado para este fin.
**Redes** | Contoso ha revisado la infraestructura VPN de sitio a sitio actual y decidió implementar Azure ExpressRoute. La implementación es fundamental porque reducirá la latencia y mejorará el ancho de banda en la región principal Este de EE. UU. 2 de Azure de Contoso.<br/><br/> **Supervisión:** Contoso deberá supervisar cuidadosamente los datos que fluyen desde el servidor de procesos. Si los datos sobrecargan el ancho de banda, Contoso considerará [limitar el ancho de banda del servidor de procesos](https://docs.microsoft.com/azure/site-recovery/site-recovery-plan-capacity-vmware#control-network-bandwidth).
**Almacenamiento de Azure** | Para la migración, Contoso debe identificar el tipo y el número correctos de cuentas de Azure Storage de destino. Site Recovery replica los datos de máquina virtual en Azure Storage.<br/><br/> Site Recovery puede replicar en cuentas de almacenamiento estándar o premium (SSD).<br/><br/> Para decidir sobre el almacenamiento, Contoso debe revisar [los límites de almacenamiento](https://docs.microsoft.com/azure/virtual-machines/windows/disks-types) y tener en cuenta el crecimiento esperado y el aumento del uso a lo largo del tiempo. Dada la velocidad y la prioridad de las migraciones, Contoso ha decidido usar discos SSD Premium.<br/><br/>
Contoso ha tomado la decisión de usar discos administrados para todas las máquinas virtuales que se implementan en Azure. El número de IOPS necesario determinará si los discos serán HDD estándar, SSD estándar o Premium (SSD).<br/><br/>

<!--markdownlint-enable MD033 -->

#### <a name="azure-database-migration-service"></a>Azure Database Migration Service

Azure Database Migration Service es un servicio totalmente administrado que permite migraciones completas desde varios orígenes de base de datos hasta las plataformas de datos de Azure con un tiempo de inactividad mínimo.

- DMS integra la funcionalidad de las herramientas y servicios existentes. Así mismo, usa Data Migration Assistant (DMA) para generar informes de evaluación que identifiquen las recomendaciones sobre la compatibilidad de las bases de datos y las modificaciones necesarias.
- DMS usa un proceso de migración sencillo y autoguiado, con una evaluación inteligente que ayuda a abordar los posibles problemas antes de la migración.
- DMS puede llevar a cabo una migración a escala desde varios orígenes a su base de datos de destino de Azure.
- DMS es compatible desde SQL Server 2005 hasta SQL Server 2017.

DMS no es la única herramienta de migración de base de datos de Microsoft. Consulta una [comparación de herramientas y servicios](https://blogs.msdn.microsoft.com/datamigration/2017/10/13/differentiating-microsofts-database-migration-tools-and-services).

##### <a name="using-dms-at-scale"></a>Uso de DMS a escala

Contoso usará DMS al migrar desde SQL Server.

- Al aprovisionar DMS, Contoso tiene que cambiar el tamaño correctamente y configurarlo para optimizar el rendimiento de las migraciones de datos. Contoso seleccionará la opción "nivel crítico para la empresa con 4 núcleos virtuales", lo que permite que el servicio pueda aprovechar varias vCPU para la paralelización y una transferencia de datos más rápida.

    ![Escalado de DMS](./media/contoso-migration-scale/dms.png)

- Otra táctica de escalado de Contoso es escalar verticalmente y de manera temporal la instancia de destino de Azure SQL o MySQL al SKU de nivel Premium durante la migración de datos. Esto minimiza la limitación de base de datos que puede afectar a las actividades de transferencia de datos al usar las SKU de nivel inferior.

##### <a name="using-other-tools"></a>Uso de otras herramientas

Además de DMS, Contoso puede usar otras herramientas y servicios para identificar la información de la máquina virtual.

- Cuentan con los scripts para ayudarle con las migraciones manuales. Estos se encuentran disponibles en el repositorio de GitHub.
- También hay diferentes [herramientas de asociados](https://azure.microsoft.com/migration/partners) que pueden usarse para la migración.

## <a name="phase-3-optimize"></a>Fase 3: Optimizar

Una vez que Contoso traslada los recursos a Azure, necesita agilizarlos para mejorar el rendimiento y maximizar el ROI con herramientas de administración de costos. Dado que Azure es un servicio de pago por uso, es fundamental que Contoso comprenda cómo funcionan los sistemas y se asegure de que cuentan con el tamaño correcto.

### <a name="azure-cost-management"></a>Azure Cost Management

Para aprovechar al máximo su inversión en la nube, Contoso aprovechará la herramienta gratuita Azure Cost Management.

- Esta solución con licencia creada por Cloudyn, una subsidiaria de Microsoft, permite a Contoso administrar los gastos en la nube con transparencia y precisión. Proporciona herramientas para supervisar, asignar y reducir los costos en la nube.
- Azure Cost Management proporciona informes de panel sencillos para ayudar con la asignación de costos, los contracargos y la visibilidad de los gastos.
- Cost Management permite optimizar los gastos en la nube mediante la identificación de los recursos que Contoso no está aprovechando para que pueda administrarlos y ajustarlos.
- [Más información](https://docs.microsoft.com/azure/cost-management/overview) sobre Azure Cost Management.

![Administración de costos](./media/contoso-migration-scale/cost-management.png)

### <a name="native-tools"></a>Herramientas nativas

Contoso también usará scripts para localizar los recursos no utilizados.

- Durante las migraciones de gran tamaño, a menudo hay piezas de datos sobrantes, como unidades de disco duro virtuales (VHD), que conllevan un costo, pero no proporcionan ningún valor para la empresa. Los scripts se encuentran disponibles en el repositorio de GitHub.
- Contoso aprovechará el trabajo realizado por el departamento de TI de Microsoft y considerará la posibilidad de implementar el kit de herramientas de Azure Resource Optimization (ARO).
- Contoso puede implementar una cuenta de Azure Automation con runbooks preconfigurados, programar sus suscripciones y empezar a ahorrar dinero. La optimización de recursos de Azure se realiza automáticamente en una suscripción al crear o habilitar una programación, incluida la optimización en nuevos recursos.
- Esto proporciona funcionalidades de automatización descentralizada para reducir costos. Características incluidas:
  - Posponer automáticamente máquinas virtuales de Azure en función de CPU bajo.
  - Programar las máquinas virtuales de Azure para posponerse y no posponerse.
  - Programar las máquinas virtuales de Azure para posponer o no posponerse en orden ascendente y descendente con etiquetas de Azure.
  - Eliminación en masa de grupos de recursos a petición.
- Empezar a trabajar con el kit de herramientas ARO en este [repositorio de GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/azure-resource-optimization-toolkit).

### <a name="partner-optimization-tools"></a>Herramientas de optimización de asociados

Pueden usarse herramientas de asociados, como [Hanu](https://hanu.com/insight) y [Scalr]( https://www.scalr.com/cost-optimization).

## <a name="phase-4-secure-and-manage"></a>Fase 4: Proteger y administrar

En esta fase, Contoso usa los recursos de seguridad y administración de Azure para controlar, proteger y supervisar las aplicaciones en la nube de Azure. Estos recursos le ayudan a ejecutar un entorno protegido y bien administrado mientras utiliza los productos disponibles en Azure Portal. Contoso comienza a usar estos servicios durante la migración y, gracias a la funcionalidad híbrida de Azure, continúa usando muchos de ellos para lograr una experiencia coherente en toda su nube híbrida.

### <a name="security"></a>Seguridad

Contoso confiará en Azure Security Center para lograr una administración unificada de la seguridad y protección contra amenazas avanzada para las cargas de trabajo de su nube híbrida.

- Security Center aporta visibilidad total y control sobre la seguridad de las aplicaciones en la nube de Azure.
- Contoso puede detectar rápidamente posibles amenazas y tomar medidas con rapidez, y reducir su exposición de seguridad usando protección contra amenazas adaptable.

[Más información](https://azure.microsoft.com/services/security-center) acerca de Security Center.

### <a name="monitoring"></a>Supervisión

Contoso necesita visibilidad sobre el estado y el rendimiento de las aplicaciones recién migradas, así como sobre la infraestructura y los datos que ahora se está ejecutando en Azure. Contoso usará las herramientas integradas de supervisión de la nube de Azure, como Azure Monitor, área de trabajo de Log Analytics y Application Insights.

- Con estas herramientas, Contoso puede recopilar datos fácilmente de diversos orígenes y obtener conocimiento con ellos. Por ejemplo, Contoso puede medir el uso de CPU, disco y memoria de sus máquinas virtuales, ver las dependencias de aplicaciones y red entre varias máquinas virtuales y mantener un seguimiento del rendimiento de las aplicaciones.
- Contoso usará estas herramientas de supervisión en la nube para tomar medidas e integrarlas con las soluciones de servicios.
- [Más información](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) sobre la supervisión de Azure.

### <a name="business-continuity-and-disaster-recovery"></a>Continuidad empresarial y recuperación ante desastres

Contoso necesita una estrategia de continuidad empresarial y recuperación ante desastres (BCDR) para sus recursos de Azure.

- Azure proporciona [características integradas de BCDR](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications) para proteger los datos y mantener las aplicaciones y servicios en funcionamiento.
- Además de las características integradas, Contoso desea asegurarse de que puede recuperarse de errores, evitar interrupciones empresariales costosas, satisfacer los objetivos de cumplimiento y proteger sus datos frente a ransomware y errores humanos. Para ello, siga estos pasos:
  - Contoso implementará Azure Backup como una solución rentable para realizar copias de seguridad de los recursos de Azure. Al estar integrado, Contoso permite configurar copias de seguridad en la nube con solo algunos sencillos pasos.
  - Contoso configurará la recuperación ante desastres para máquinas virtuales de Azure con Azure Site Recovery para la replicación, conmutación por error y conmutación por recuperación entre las regiones de Azure que especifique. Esto garantiza que, si se produce una interrupción en la región primaria, las aplicaciones que se ejecutan en máquinas virtuales de Azure seguirán estando disponibles en la región secundaria que elija Contoso. [Más información](https://docs.microsoft.com/azure/site-recovery/azure-to-azure-quickstart).

## <a name="conclusion"></a>Conclusión

En este artículo, Contoso planea una migración con escala a Azure. El proceso de migración se divide en cuatro etapas. Desde la evaluación y la migración, pasando por la optimización, la seguridad y la administración una vez que la migración concluye. En general, es importante planear un proyecto de migración como un proceso completo, pero migrando los sistemas de una organización dividiéndolos en clasificaciones y números que tengan sentido para el negocio. Al evaluar los datos y aplicar clasificaciones, el proyecto se puede dividir en una serie de migraciones más pequeñas, que pueden ejecutarse rápidamente y de forma segura. La suma de estas migraciones más pequeñas se convierte rápidamente en una migración correcta de gran tamaño a Azure.
