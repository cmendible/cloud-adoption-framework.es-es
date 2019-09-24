---
title: Guía de decisiones sobre registros e informes
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información sobre registros, informes y supervisión de los servicios principales en las migraciones de Azure.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 9d2f4a6c8541d8967f26db1a38591c7ce775d5e8
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223631"
---
# <a name="logging-and-reporting-decision-guide"></a>Guía de decisiones sobre registros e informes

Todas las organizaciones necesitan mecanismos para informar a los equipos de TI sobre los problemas de rendimiento, tiempo de actividad y seguridad antes de que se conviertan en problemas graves. Una correcta estrategia de supervisión permite comprender cómo funcionan los componentes individuales que componen la infraestructura de red y las cargas de trabajo. En el contexto de una migración en la nube pública, la integración de registros e informes con cualquiera de los sistemas de supervisión existentes, al presentar métricas y eventos importantes al personal de TI adecuado, es fundamental para garantizar que su organización cumple los objetivos de tiempo de actividad, seguridad y cumplimiento de directivas.

![A continuación, se presenta el trazado de opciones de registro, informes y supervisión de menos a más complejas, alineadas con vínculos](../../_images/decision-guides/decision-guide-logging-and-reporting.png)

Vaya a: [Planeamiento de una infraestructura de supervisión](#planning-your-monitoring-infrastructure) | [Nativo de la nube](#cloud-native) | [Extensión local](#on-premises-extension) | [Agregación de puerta de enlace](#gateway-aggregation) | [Supervisión híbrida (local)](#hybrid-monitoring-on-premises) | [Supervisión híbrida (en la nube)](#hybrid-monitoring-cloud-based) | [Nube múltiple](#multicloud) | [Más información](#learn-more)

El punto de inflexión al determinar una estrategia de generación de informes y registro en la nube se basa principalmente en las inversiones que una organización haya realizado en los procesos operativos y, hasta cierto punto, en los requisitos que hay que cumplir para respaldar una estrategia de nube múltiple.

Hay varias formas de registrar y notificar las actividades en la nube. El registro nativo de la nube y centralizado son dos opciones de software como servicio (SaaS) comunes basadas en el diseño de la suscripción y en el número de suscripciones.

## <a name="planning-your-monitoring-infrastructure"></a>Planeamiento de la infraestructura de supervisión

Al planear la implementación, debe pensar en dónde se almacenarán los datos de registro y en cómo integrará los informes basados en la nube y los servicios de supervisión con las herramientas y los procesos existentes.

| Pregunta | Nativo de la nube | Extensión local | Supervisión híbrida | Agregación de puerta de enlace |
|-----|-----|-----|-----|-----|
| ¿Dispone de una infraestructura de supervisión local existente? | Sin | Sí | Sí |  Sin |
| ¿Existen requisitos que impidan almacenar los datos de registro en ubicaciones de almacenamiento externas? | Sin | Sí | No | Sin |
| ¿Necesita integrar la supervisión en la nube con sistemas locales? | Sin | No | Sí | Sin |
¿Necesita procesar o filtrar datos de telemetría  antes de enviarlos a los sistemas de supervisión? | Sin | No | No | Sí |

### <a name="cloud-native"></a>Nativo de la nube

Si una organización no dispone de sistemas de registro y generación de informes establecidos, o si la implementación planeada no necesita integrarse con los sistemas de supervisión locales existentes u otros externos, la opción más sencilla es una solución SaaS nativa en la nube, como [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview).

En este escenario, todos los datos del registro se graban y almacenan en la nube, mientras que las herramientas de registro y generación de informes que procesan y muestran la información al personal de TI se proporcionan por la plataforma Azure y Azure Monitor.

Las soluciones de registro personalizadas basadas en Azure Monitor se pueden implementar ad hoc en cada suscripción o carga de trabajo en implementaciones experimentales o más pequeñas, y se organizan de forma centralizada para supervisar los datos de registro en todo el entorno de la nube.

**Hipótesis nativas de la nube.** Al usar un sistema de registro y generación de informes nativo de la nube, se asume lo siguiente:

- No es necesario integrar los datos de registro de las cargas de trabajo de la nube en los sistemas locales existentes.
- No usará los sistemas de informes basados en la nube para supervisar los sistemas locales.

### <a name="on-premises-extension"></a>Extensión local

El uso de soluciones de registro y generación de informes, como Azure Monitor, puede requerir un considerable esfuerzo de desarrollo para las aplicaciones y servicios que migran a la nube. En esos casos puede tener sentido permitir que estas cargas de trabajo sigan enviando datos de telemetría a sistemas locales existentes.

Para admitir este enfoque, será preciso que los recursos en la nube puedan comunicarse directamente con los sistemas locales mediante una combinación de [redes híbridas](../software-defined-network/hybrid.md) y [servicios de dominio hospedados en la nube](../identity/index.md#cloud-hosted-domain-services). Gracias a esto, la red virtual en la nube funciona como una extensión de red del entorno local. Por tanto, las cargas de trabajo hospedadas en la nube pueden comunicarse directamente con el sistema local de registros e informes.

Este enfoque saca el máximo rendimiento a la inversión existente en herramientas de supervisión con una modificación limitada de todos los servicios o las aplicaciones implementados en la nube. Este enfoque a menudo es el que menos tarda en dar soporte a la supervisión durante una migración mediante "lift-and-shift". Sin embargo, no capturará los datos de registro creados por los recursos PaaS y SaaS basados en la nube y omitirá los registros relacionados con las máquinas virtuales generados por la plataforma de la nube, como el estado de dichas máquinas. Como resultado, este patrón debe ser una solución temporal hasta que se implemente una solución de supervisión híbrida más completa.

Hipótesis solo&ndash;en un entorno local:

- Debe mantener los datos de registro solo en el entorno local, bien para satisfacer los requisitos técnicos o para cumplir las disposiciones legales o de las directivas.
- Los sistemas locales no admiten soluciones híbridas de registros e informes o agregación de puerta de enlace.
- Las aplicaciones basadas en la nube pueden enviar los datos de telemetría directamente a los sistemas locales de registro, o los agentes de supervisión que envían al entorno local pueden implementarse en las máquinas virtuales de la carga de trabajo.
- Las cargas de trabajo no dependen de servicios PaaS o SaaS que requieren registro y generación de informes basados en la nube.

### <a name="gateway-aggregation"></a>Agregación de puerta de enlace

En los escenarios en que hay gran cantidad de datos de telemetría basados en la nube o en que los sistemas de supervisión locales necesitan modificar los datos de registro para poder procesarlos, puede que sea necesario un servicio de [agregación de puerta de enlace](/azure/architecture/patterns/gateway-aggregation) para datos de registro.

Se implementa un servicio de puerta de enlace en el proveedor de servicios en la nube. A continuación, se configuran las aplicaciones o los servicios pertinentes para que envíen datos de telemetría a la puerta de enlace en lugar de a un sistema de registro predeterminado. A continuación, la puerta de enlace puede procesar los datos: agregarlos, combinarlos o darles formato antes de enviarlos al servicio de supervisión para su ingesta y análisis.

Además, se puede utilizar una puerta de enlace para agregar y preprocesar datos de telemetría destinados a sistemas híbridos o nativos en la nube.

En una agregación de puerta de enlace, se da por hecho lo siguiente:

- Espera volúmenes altos de datos de telemetría de los servicios o las aplicaciones basados en la nube.
- Necesitar dar formato u optimizar los datos de telemetría antes de enviarlos a los sistemas de supervisión.
- Los sistemas de supervisión tienen API u otros mecanismos disponibles para la ingesta de datos de registro después de que la puerta de enlace los procese.

### <a name="hybrid-monitoring-on-premises"></a>Supervisión híbrida (local)

Una solución de supervisión híbrida combina los datos de registro de los recursos locales y los recursos en la nube para proporcionar una visión integrada del estado operativo del entorno de TI.

Si ya ha realizado una inversión en sistemas de supervisión local que le resultaría difícil o caro sustituir, puede que necesite integrar los datos de telemetría de las cargas de trabajo en la nube en las soluciones de supervisión locales preexistentes. En un sistema de supervisión local híbrida, los datos de telemetría locales siguen usando el sistema de supervisión local existente. Los datos de telemetría basados en la nube se envían directamente al sistema de supervisión en la nube, o bien los datos se envían a Azure Monitor y luego se compilan e ingieren en el sistema local a intervalos regulares.

**Hipótesis para la supervisión híbrida local.** Al usar un sistema de registros e informes local para una supervisión híbrida, se da por hecho lo siguiente:

- Deberá usar los sistemas de informes locales existentes para supervisar las cargas de trabajo en la nube.
- Debe mantener la propiedad local de los datos de registro.
- Los sistemas de administración locales tienen API u otros mecanismos disponibles para la ingesta de datos de registro de los sistemas basados en la nube.

> [!TIP]
> Como parte de la naturaleza iterativa de migración a la nube, el paso de una supervisión local y nativa de la nube claramente diferenciadas a un enfoque híbrido parcial se puede realizar cuando madure la integración de servicios y recursos en la nube en un entorno de TI general.

### <a name="hybrid-monitoring-cloud-based"></a>Supervisión híbrida (basada en la nube)

Si no tiene una necesidad imperiosa de mantener un sistema de supervisión local o desea reemplazar los sistemas de supervisión locales por una solución centralizada basada en la nube, también puede elegir la opción de integrar los datos de registro locales con Azure Monitor para proporcionar un sistema de supervisión centralizado basado en la nube.

Mediante la creación de un reflejo del enfoque centrado en un entorno local, las cargas de trabajo basadas en la nube de este escenario enviarían los datos de telemetría directamente a Azure Monitor, mientras que los servicios y aplicaciones locales enviarían los datos de telemetría directamente a Azure Monitor o agregarían dichos datos de forma local para que los ingiera Azure Monitor a intervalos regulares. Azure Monitor podría actuar como sistema de supervisión y generación de informes principal para todo el entorno de TI.

Suposiciones para la supervisión híbrida basada en la nube: Al usar sistemas de registros e informes basados en la nube para una supervisión híbrida, se da por hecho lo siguiente:

- No depende de los sistemas de supervisión locales existentes.
- Las cargas de trabajo no tienen requisitos de directiva o normativos para almacenar los datos de registro localmente.
- Los sistemas de supervisión basados en la nube tienen API u otros mecanismos disponibles para la ingesta de datos de registro de aplicaciones y servicios locales.

### <a name="multicloud"></a>Nube múltiple

La integración de las funcionalidades de informes y registros en una plataforma de varias nubes puede resultar complicada. Los servicios ofrecidos entre las plataformas no suelen ser comparables directamente, y las funcionalidades de registro y telemetría proporcionadas por estos servicios también varían.
La compatibilidad con el registro de nube múltiple requiere que el uso de servicios de puerta de enlace procesen los datos de registro en un formato común antes de enviarlos a una solución híbrida de registros.

## <a name="learn-more"></a>Más información

[Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) es el servicio de informes y supervisión predeterminado para Azure. Ofrece:

- Una plataforma unificada para recopilar datos de telemetría de aplicaciones, telemetría de host (como máquinas virtuales), métricas de contenedor, métricas de la plataforma Azure y registros de eventos.
- Herramientas de visualización, consultas, alertas y análisis. Pueden proporcionar información sobre las máquinas virtuales, los sistemas operativos invitados, las redes virtuales y los eventos de aplicaciones de carga de trabajo.
- [API REST](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-rest-api-walkthrough) para la integración con servicios externos y automatización de los servicios de supervisión y alertas.
- [Integración](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-partners) con muchos proveedores externos populares.

## <a name="next-steps"></a>Pasos siguientes

El registro y la generación de informes no es más que uno de los componentes de la infraestructura central que requieren decisiones arquitectónicas durante un proceso de adopción en la nube. Visite la [introducción a las guías de decisión](../index.md) para obtener información acerca de los patrones o modelos alternativos que se usan al tomar decisiones de diseño para otros tipos de infraestructura.

> [!div class="nextstepaction"]
> [Guías de decisiones sobre arquitectura](../index.md)
