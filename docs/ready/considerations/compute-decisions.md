---
title: 'Preparación para Azure: decisiones sobre el diseño del proceso'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Preparación para Azure: decisiones sobre el diseño del proceso'
author: BrianBlanchard
ms.author: brblanch
ms.date: 05/15/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: bd31f07a24a17a50953eff54856118e9b22d054e
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70834750"
---
# <a name="compute-design-decisions"></a>Decisiones de diseño del proceso

La determinación de los requisitos de proceso para hospedar las cargas de trabajo es una consideración importante a la hora de prepararse para la adopción de la nube. Los productos y servicios de proceso de Azure admiten una amplia variedad de escenarios y funcionalidades de computación de la carga de trabajo. El modo en que se configure el entorno de la zona de aterrizaje para satisfacer los requisitos de proceso depende de los requisitos de gobernanza, técnicos y empresariales de la carga de trabajo.

## <a name="identify-compute-services-requirements"></a>Identificación de los requisitos de los servicios de proceso

Como parte de la evaluación y preparación de la zona de aterrizaje, debe identificar todos los recursos de proceso que deba admitir dicha zona. Este proceso implica la evaluación de cada una de las aplicaciones y servicios que componen las cargas de trabajo para determinar los requisitos de proceso y hospedaje. Después de identificar y documentar los requisitos, puede crear directivas para la zona de aterrizaje con el fin de controlar qué tipos de recursos se permiten en función de las necesidades de su carga de trabajo.

Para cada aplicación o servicio que vaya a implementar en el entorno de la zona de aterrizaje, use el siguiente árbol de decisión como punto de partida para ayudarlo a determinar los requisitos de los servicios de proceso:

![Árbol de decisión de los servicios de proceso de Azure](../../_images/ready/compute-decision-tree.png)

> [!NOTE]
> Más información sobre cómo evaluar las opciones de proceso para cada una de sus aplicaciones o servicios [en la guía de arquitectura de aplicaciones de Azure](/azure/architecture/guide/technology-choices/compute-overview).

### <a name="key-questions"></a>Preguntas clave

Responda a las siguientes preguntas sobre las cargas de trabajo como ayuda para tomar decisiones basadas en el árbol de decisión de los servicios de proceso de Azure:

- **¿Va a crear aplicaciones y servicios o a migrar a partir de cargas de trabajo locales existentes?** El desarrollo de nuevas aplicaciones como parte de las labores de adopción de la nube permite sacar el máximo partido de las modernas tecnologías de hospedaje basadas en la nube desde la fase de diseño en adelante.
- **Si va a migrar cargas de trabajo existentes, ¿pueden aprovechar las modernas tecnologías de la nube?** La migración de cargas de trabajo locales requiere análisis: ¿Se pueden optimizar fácilmente las aplicaciones y los servicios existentes para aprovechar las modernas tecnologías de la nube o funcionará mejor un enfoque de *migración mediante lift-and-shift* con las cargas de trabajo?
- **¿Pueden aprovechar las aplicaciones o servicios los contenedores?** Si las aplicaciones son buenas candidatas para el hospedaje en contenedor, puede aprovechar las funcionalidades de eficacia de recursos, escalabilidad y orquestación proporcionadas por los [servicios de contenedor de Azure](https://azure.microsoft.com/product-categories/containers). Los servicios [Azure Disk Storage](/azure/virtual-machines/windows/managed-disks-overview) y [Azure Files](/azure/storage/files/storage-files-introduction) se pueden usar para el almacenamiento persistente de las aplicaciones en contenedor.
- **¿Están basadas las aplicaciones en web o en API y usan PHP, ASP.NET, Node.js o tecnologías similares?** Las aplicaciones web se pueden implementar en instancias de [Azure App Service](/azure/app-service/overview) administradas, por lo que no tiene que mantener máquinas virtuales con fines de hospedaje.
- **¿Necesitará control total sobre el sistema operativo y el entorno de hospedaje de la carga de trabajo?** Si necesita controlar el entorno de hospedaje, incluidos el sistema operativo, los discos, el software que se ejecuta localmente y otras configuraciones, puede usar [Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines) para hospedar sus aplicaciones y servicios. Además de elegir los tamaños de máquina virtual y los niveles de rendimiento, las decisiones relacionadas con el almacenamiento de discos virtuales afectarán al rendimiento y a los Acuerdos de Nivel de Servicio (SLA) relacionados con las cargas de trabajo basadas en la infraestructura como servicio (IaaS). Para más información, consulte la documentación de [Azure Disk Storage](/azure/virtual-machines/windows/managed-disks-overview).
- **¿En la carga de trabajo intervienen funcionalidades de informática de alto rendimiento (HPC)?** [Azure Batch](/azure/batch/batch-technical-overview) proporciona programación de trabajos y escalabilidad automática de recursos de proceso como servicio de plataforma, lo que facilita la ejecución de aplicaciones de HPC y paralelas a gran escala en la nube.
- **¿Van a usar las aplicaciones una arquitectura de microservicios?** Las aplicaciones que usan una arquitectura basada en microservicios pueden aprovechar varias tecnologías de proceso optimizadas. Las cargas de trabajo basadas en eventos independientes pueden usar [Azure Functions](/azure/azure-functions/functions-overview) para compilar aplicaciones escalables y sin servidor que no necesitan una infraestructura. En el caso de las aplicaciones que requieren más control sobre el entorno en el que se ejecutan los microservicios, puede usar servicios de contenedor, como [Azure Container Instances](/azure/container-instances/container-instances-overview), [Azure Kubernetes Service](/azure/aks/intro-kubernetes) y [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).

> [!NOTE]
> La mayoría de los servicios de proceso de Azure se usan en combinación con Azure Storage. Consulte la [guía de decisiones de almacenamiento](./storage-guidance.md) para información sobre las decisiones relacionadas con el almacenamiento.

## <a name="common-compute-scenarios"></a>Escenarios comunes de proceso

En la tabla siguiente se muestran algunos escenarios de uso comunes y los servicios de proceso recomendados para gestionarlos:

| **Escenario** | **Servicio de proceso** |
| --- | --- |
| Necesito aprovisionar máquinas virtuales Linux y Windows en cuestión de segundos con las configuraciones de mi elección. | [Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines) |
| Necesito conseguir alta disponibilidad con la escalabilidad automática para crear miles de máquinas virtuales en cuestión de minutos. | [Conjuntos de escalado de máquinas virtuales](https://azure.microsoft.com/services/virtual-machine-scale-sets) |
| Quiero simplificar la implementación, la administración y las operaciones de Kubernetes. | [Azure Kubernetes Service (AKS)](https://azure.microsoft.com/services/kubernetes-service) |
| Necesito acelerar el desarrollo de aplicaciones con una arquitectura sin servidor basada en eventos. | [Azure Functions](https://azure.microsoft.com/services/functions) |
| Necesito desarrollar microservicios y organizar los contenedores en Windows y Linux. | [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric) |
| Quiero crear rápidamente aplicaciones en la nube para web y móviles mediante una plataforma totalmente administrada. | [Azure App Service](https://azure.microsoft.com/services/app-service) |
| Quiero incluir aplicaciones en contenedores y ejecutar fácilmente contenedores con un solo comando. | [Azure Container Instances](https://azure.microsoft.com/services/container-instances) |
| Necesito escalar a la nube la programación de trabajos y la administración de procesos con la posibilidad de escalar hasta decenas, centenares o miles de máquinas virtuales. | [Azure Batch](https://azure.microsoft.com/services/batch) |
| Necesito crear aplicaciones en la nube escalables y de alta disponibilidad, así como API que me ayuden a centrarme en las aplicaciones y no en el hardware. | [Azure Cloud Services](https://azure.microsoft.com/services/cloud-services) |

## <a name="regional-availability"></a>Disponibilidad regional

Azure le permite ofrecer servicios a la escala que necesita para llegar a sus clientes y asociados,  _dondequiera que se encuentren_. Uno de los factores clave a la hora de planear la implementación en la nube es determinar qué región de Azure hospedará los recursos de la carga de trabajo.

Algunas opciones de proceso, como Azure App Service, están disponibles con carácter general en la mayoría de las regiones de Azure. Sin embargo, algunos servicios de proceso solo se admiten en algunas regiones. Algunos tipos de máquinas virtuales y sus tipos de almacenamiento asociados tienen una disponibilidad regional limitada. Antes de decidir en qué regiones va a implementar los recursos de proceso, se recomienda que consulte la [página de regiones](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=azure-vmware-cloudsimple,cloud-services,batch,container-instances,app-service,service-fabric,functions,kubernetes-service,virtual-machine-scale-sets,virtual-machines)  para comprobar el estado más reciente de la disponibilidad regional.

Para más información sobre la infraestructura global de Azure, consulte la  [página de regiones de Azure](https://azure.microsoft.com/global-infrastructure/regions). También puede ver los  [productos disponibles por región](https://azure.microsoft.com/global-infrastructure/services/?regions=all&products=all) para obtener detalles específicos sobre los servicios generales que están disponibles en cada región de Azure.

## <a name="data-residency-and-compliance-requirements"></a>Requisitos de cumplimiento y residencia de datos

Con frecuencia, se aplicarán a las cargas de trabajo los requisitos legales y contractuales que están relacionados con el almacenamiento de datos. Estos requisitos pueden variar en función de la ubicación de la organización, la jurisdicción en la que se almacenan y procesan los archivos y los datos y el sector empresarial aplicable. Entre los componentes de las obligaciones de datos que deben tenerse en cuenta se incluyen la clasificación de los datos, la ubicación de los datos y las responsabilidades correspondientes relativas a la protección de datos en el modelo de responsabilidad compartida. Muchas soluciones de proceso dependen de recursos de almacenamiento vinculados. Este requisito también podría influir en las decisiones de proceso. Para obtener ayuda con la comprensión de estos requisitos, consulte las notas del producto  [Consecución de la seguridad y la residencia de datos compatibles con Azure](https://azure.microsoft.com/resources/achieving-compliant-data-residency-and-security-with-azure).

Parte de sus esfuerzos de cumplimiento puede incluir el control del lugar donde sus recursos de base de datos se encuentran físicamente. Las regiones de Azure se organizan en grupos llamados zonas geográficas. Una  [zona geográfica de Azure](https://azure.microsoft.com/global-infrastructure/geographies)  garantiza que se cumplan los requisitos de residencia, soberanía, cumplimiento normativo y resistencia de los datos dentro de las fronteras geográficas y políticas. Si sus cargas de trabajo están sujetas a la soberanía de datos u otros requisitos de cumplimiento, debe implementar sus recursos de almacenamiento en regiones que se encuentren en una zona geográfica de Azure compatible.

## <a name="establish-controls-for-compute-services"></a>Establecimiento de controles para servicios de proceso

Al preparar el entorno de la zona de aterrizaje, puede establecer controles que limiten qué recursos puede implementar cada usuario. Los controles pueden ayudarle a administrar los costos y a limitar los riesgos de seguridad, al tiempo que permiten a los desarrolladores y equipos de TI implementar y configurar los recursos necesarios para admitir las cargas de trabajo.

Después de identificar y documentar los requisitos de la zona de aterrizaje, puede usar [Azure Policy](/azure/governance/policy/overview) para controlar los recursos de proceso que permite que creen los usuarios. Los controles pueden tener la forma de [permitir o denegar la creación de tipos de recursos de proceso](/azure/governance/policy/samples/allowed-resource-types). Por ejemplo, puede restringir a los usuarios que solo creen recursos Azure App Service o Azure Functions. También puede usar directivas para controlar las opciones permitidas cuando se crea un recurso, como [restringir las SKU de máquina virtual que se pueden aprovisionar](https://docs.microsoft.com/azure/governance/policy/samples/allowed-skus-storage) o [permitir solo imágenes de máquina virtual específicas](https://docs.microsoft.com/azure/governance/policy/samples/allowed-custom-images).

Las directivas se pueden limitar a recursos, grupos de recursos, suscripciones y grupos de administración. Puede incluir las directivas en las definiciones de [Azure Blueprints](/azure/governance/blueprints/overview) y aplicarlas varias veces a todo el patrimonio de la nube.

