---
title: Descripción de las opciones de colaboración y soporte técnico
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Describe las opciones y los enfoques para brindar soporte técnico a los esfuerzos de migración
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: b19353ebe22faf089ff56b5ee84289928a8eaca7
ms.sourcegitcommit: 5846ed4d0bf1b6440f5e87bc34ef31ec8b40b338
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70905623"
---
# <a name="understand-partnership-options"></a>Descripción de las opciones de colaboración

Durante la migración, el equipo de adopción de la nube realiza la migración real de cargas de trabajo a la nube. A diferencia de las tareas de colaboración y solución de problemas a la hora de definir [el patrimonio digital](../../../digital-estate/index.md) o de crear la infraestructura en la nube principal, la migración tiende a ser una serie de tareas de ejecución repetitivas. Más allá de los aspectos repetitivos, es probable que haya esfuerzos de prueba y optimización que requieren un conocimiento profundo del proveedor de nube elegido. En algunas ocasiones, un asociado puede abordar mejor la naturaleza repetitiva de este proceso, lo que reduce la presión sobre el personal a tiempo completo. Además, los asociados pueden ser capaces de alinear mejor los conocimientos técnicos cuando los procesos repetitivos detectan anomalías en una ejecución.

Los asociados tienden a estar estrechamente alineados con un solo proveedor de nube o con un número reducido de proveedores de nube. Para ilustrar mejor las opciones de asociación, para el resto de este artículo se presupone que Microsoft Azure es el proveedor de nube elegido.

Durante el plan, la compilación o la migración, una empresa generalmente tiene cuatro opciones de colaboración para la ejecución:

- **Autoservicio guiado.** El equipo técnico existente ejecuta la migración, con la ayuda de Microsoft.
- **FastTrack for Azure.** Use el programa Microsoft FastTrack for Azure para acelerar la migración.
- **Asociado de soluciones.** Póngase en contacto con asociados de soluciones de Azure o asociados de soluciones en la nube (CSP) para acelerar la migración.
- **Autoservicio compatible.** La ejecución la lleva a cabo el personal técnico existente con soporte técnico de Microsoft.

## <a name="guided-self-service"></a>Autoservicio guiado

Si una organización planea realizar una migración a Azure por sí misma, Microsoft siempre está ahí para ayudarle durante el recorrido. Para ayudar a realizar una migración acelerada a Azure, Microsoft y sus asociados han desarrollado un amplio conjunto de arquitecturas, guías, herramientas y servicios con el fin de disminuir el riesgo y acelerar la migración de máquinas virtuales, aplicaciones y bases de datos. Estas herramientas y servicios admiten una amplia selección de sistemas operativos, lenguajes de programación, marcos y bases de datos.

- **Herramientas de evaluación y migración.** Azure proporciona una amplia variedad de herramientas que se pueden usar en distintas fases para la transformación en la nube, incluida la evaluación de la infraestructura existente. Para más información, consulte la sección "Evaluación" en el capítulo "Migración" que aparece a continuación.
- **[Plataforma de adopción de la nube de Microsoft](../../index.md).** Esta plataforma presenta un enfoque estructurado para la adopción y la migración a la nube. Se basa en prácticas probadas en muchas de las interacciones con los clientes compatibles con Microsoft y se organiza como una serie de pasos, desde la arquitectura y el diseño hasta la implementación. Para cada paso, hay instrucciones auxiliares que lo ayudarán con el diseño de la arquitectura de la aplicación.
- **[Patrones de diseño en la nube](/azure/architecture/patterns).** Azure proporciona algunos patrones útiles de diseño en la nube para crear cargas de trabajo confiables, escalables y seguras en la nube. Cada patrón describe el problema al que hace frente, las consideraciones sobre su aplicación y un ejemplo basado en Azure. La mayoría incluye ejemplos de código o fragmentos de código que muestran cómo implementar el patrón en Azure. Sin embargo, son importantes para todos los sistemas distribuidos, tanto si se hospedan en Azure como en otras plataformas en la nube.
- **[Aspectos básicos de la nube](/azure/architecture/guide).** Estos ayudan a enseñar los enfoques básicos para la implementación de los conceptos básicos. Esta guía ayuda a los técnicos a pensar en soluciones que van más allá de un único servicio de Azure.
- **[Escenarios de ejemplo](/azure/architecture/example-scenario).** En esta guía se proporcionan referencias de implementaciones de clientes reales, donde se describen las herramientas, los enfoques y los procesos que los clientes han seguido para lograr objetivos empresariales específicos.
- **[Arquitecturas de referencia](/azure/architecture/reference-architectures).** Las arquitecturas de referencia se organizan por escenario, agrupando juntas aquellas arquitecturas relacionadas. Cada arquitectura incluye procedimientos recomendados junto con consideraciones sobre escalabilidad, disponibilidad, capacidad de administración y seguridad. La mayoría también incluye una solución que se puede implementar.

## <a name="fasttrack-for-azure"></a>FastTrack for Azure

[FastTrack for Azure](https://azure.microsoft.com/roadmap/fasttrack-for-azure) ofrece asistencia directa por parte de los ingenieros de Azure, en estrecha colaboración con los asociados, para ayudar a los clientes a compilar las soluciones de Azure con rapidez y confianza. FastTrack aporta procedimientos recomendados y herramientas de experiencias reales del cliente para guiar a los clientes desde la instalación, la configuración y el desarrollo hasta la producción de soluciones de Azure, lo que incluye:

- Migración de centros de datos
- Windows Server en Azure
- Linux en Azure
- SAP en Azure
- Recuperación ante desastres y continuidad empresarial (BCDR)
- Informática de alto rendimiento*
- Aplicaciones nativas de la nube
- DevOps
- Modernización de aplicaciones
- Análisis a escala de nube**
- Aplicaciones inteligentes
- Agentes inteligentes**
- Modernización de datos en Azure
- Seguridad y administración
- Datos distribuidos globalmente
- IoT***

\* Versión preliminar limitada en Estados Unidos, Canadá, Reino Unido y Europa Occidental

** Versión preliminar limitada en el Reino Unido y Europa Occidental

*** Disponible en el segundo semestre de 2019

Durante una interacción típica de FastTrack for Azure, Microsoft ayuda a definir la visión empresarial para planear y desarrollar correctamente soluciones de Azure. El equipo evalúa las necesidades de diseño y proporciona instrucciones, principios de diseño, herramientas y recursos para ayudar a compilar, implementar y administrar soluciones de Azure. El equipo empareja asociados cualificados para los servicios de implementación a petición y se registran periódicamente para asegurarse de que la implementación está en buen pie y para ayudar a quitar los bloqueadores.

Las principales fases de una interacción típica de FastTrack for Azure son:

- **Detección.** Identifique a las partes interesadas clave, comprenda el objetivo o la visión de los problemas que se van a resolver y evalúe las necesidades de diseño.
- **Habilitación de soluciones.** Aprenda principios de diseño para crear aplicaciones, revisar la arquitectura de aplicaciones y soluciones y obtenga instrucciones y herramientas para impulsar el trabajo de prueba de concepto hasta producción.
- **Colaboración continua.** Los administradores de programas y los ingenieros de Azure se registran cada tanto para asegurarse de que la implementación está en buen pie y para ayudar a quitar los bloqueadores.

## <a name="microsoft-services-offerings-aligned-to-cloud-adoption-framework-approaches"></a>Ofertas de los Servicios de Microsoft alineadas con los enfoques de la Plataforma de adopción de la nube

![Enfoque de la Plataforma de adopción de la nube de los Servicios de Microsoft](../../../_images/mcs-program-approach.jpg)

**Evaluación:** los Servicios de Microsoft usan un [enfoque unificado, de datos y de herramientas](https://download.microsoft.com/download/C/7/C/C7CEA89D-7BDB-4E08-B998-737C13107361/Secure_Cloud_Insights_Datasheet_EN_US.pdf) que se compone de talleres de diseño, información en tiempo real de Azure, modelos de amenazas de seguridad e identidad y diversas herramientas para proporcionar información sobre los desafíos, los riesgos, las recomendaciones y los problemas a un entorno de Azure existente con un resultado clave como la [hoja de ruta de modernización de alto nivel](https://download.microsoft.com/download/F/7/2/F72FAD7E-8BBD-4E04-8C7B-9AC4FE04A150/Cloud_Adoption_Discovery_and_Roadmap_Datasheet.pdf).

**Adopción:** a través de [Azure Cloud Foundation](https://download.microsoft.com/download/D/8/7/D872DFD0-1C46-4145-95E4-B5EAB2958B96/Hybrid_Cloud_Foundation_Datasheet_EN_US.pdf) de los Servicios de Microsoft, establezca sus diseños, patrones y arquitectura de gobernanza principales de Azure mediante la asignación de sus requisitos a la arquitectura de referencia más adecuada y planee, diseñe e implemente la infraestructura, la administración, la seguridad y la identidad necesarias para las cargas de trabajo.

**Migración/optimización:** la [solución de modernización de la nube](https://download.microsoft.com/download/3/7/3/373F90E3-8568-44F3-B096-CD9C1CD28AB7/Cloud_Modernization_Datasheet_EN_US.pdf) de los Servicios de Microsoft ofrece un enfoque integral para trasladar aplicaciones e infraestructura a Azure, así como para optimizar y modernizar una vez en la nube con el respaldo de una migración simplificada.

**Innovación:** la solución [Centro de excelencia en la nube (CCoE)](https://download.microsoft.com/download/F/8/B/F8BBE4BD-E5F8-4DFB-82F7-C0A4E17051BB/Cloud_Center_of_Excellence_Datasheet_EN_US.pdf) de los Servicios de Microsoft ofrece un compromiso de preparación para DevOps y usa principios de DevOps combinados con controles prescriptivos de seguridad y administración de servicios nativos de la nube para ayudar a impulsar la innovación empresarial, aumentar la agilidad y reducir el tiempo de amortización dentro de una funcionalidad de administración de operaciones y entrega de servicios segura, predecible y flexible.

## <a name="azure-support"></a>Compatibilidad para Azure

Si tiene alguna pregunta o necesita ayuda, [cree una solicitud de soporte técnico](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest). Si su solicitud de soporte técnico requiere una guía técnica profunda, visite los [planes de soporte técnico de Azure](https://azure.microsoft.com/support/plans) para alinear el mejor plan según sus necesidades.

## <a name="azure-solutions-partner"></a>Asociado de soluciones de Azure

Los proveedores de soluciones certificados de Microsoft se especializan en brindar soluciones de cliente actualizadas basadas en la tecnología de Microsoft en todo el mundo. Optimice su negocio en la nube con la ayuda de un asociado experimentado.

Obtenga ayuda de asociados que tengan soluciones de Azure personalizadas o listas para usar, así como asociados que lo puedan ayudar a implementar y administrar esas soluciones:

- **[Buscar un asociado de soluciones en la nube](https://www.microsoft.com/solution-providers/home).** Un CSP certificado puede ayudarle a sacar el máximo provecho de la nube mediante la evaluación de los objetivos empresariales para la adopción de la nube, la identificación de la solución en la nube adecuada que satisface las necesidades empresariales y ayuda a la empresa a ser más ágil y eficaz.
- **[Buscar un asociado de servicios administrados](https://www.microsoft.com/solution-providers/search?cacheId=16a3b49b-fef2-449d-bdf0-628008114cca).** Un asociado de servicios administrados (MSP) de Azure ayuda a una empresa a hacer la transición a Azure y guía todos los aspectos del recorrido en la nube. Desde la consultoría hasta la administración de operaciones y migraciones, los MSP de la nube muestran a los clientes todas las ventajas que aporta la adopción de la nube. También actúan como un lugar único donde ofrecer soporte técnico común, aprovisionamiento y la experiencia de facturación, todo ello con un modelo empresarial de pago por uso (PAYG) flexible.

## <a name="next-steps"></a>Pasos siguientes

Una vez que se selecciona un asociado y una estrategia de soporte técnico, los [trabajos pendientes de liberación e iteración](./release-iteration-backlog.md) se pueden actualizar para reflejar los esfuerzos y las asignaciones planeados.

> [!div class="nextstepaction"]
> [Administración de cambios con trabajos pendientes de liberación e iteración](./release-iteration-backlog.md)
