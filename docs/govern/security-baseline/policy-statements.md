---
title: Declaraciones de directiva de ejemplo de la base de referencia de la seguridad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Declaraciones de directiva de ejemplo de la base de referencia de la seguridad
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: f92f3846f0282123fab8049dd47227db0843d955
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221659"
---
# <a name="security-baseline-sample-policy-statements"></a>Declaraciones de directiva de ejemplo de la base de referencia de la seguridad

Cada declaración de directiva de nube es una guía para abordar los riesgos específicos identificados durante el proceso de evaluación de riesgos. Estas declaraciones deben proporcionar un breve resumen de los riesgos y los planes para resolverlos. La definición de cada declaración debe incluir estos fragmentos de información:

- **Riesgo técnico**: Un resumen del riesgo que esta directiva abordará.
- **Declaración de directiva**: Una explicación clara que resuma los requisitos de la directiva.
- **Opciones técnicas**: Recomendaciones que requieren acción, especificaciones u otras instrucciones que los equipos de TI y los desarrolladores pueden usar al implementar la directiva.

Las siguientes instrucciones de directiva de ejemplo abordan algunos riesgos empresariales comunes relacionados con la seguridad. Estas instrucciones son ejemplos a los que se puede hacer referencia al elaborar el borrador de instrucciones de directiva para satisfacer las necesidades de su organización. Estos ejemplos no pretenden ser excluyentes y hay varias opciones posibles de directiva para solucionar cada riesgo concreto identificado. Trabaje estrechamente con los equipos de TI, seguridad y negocio para identificar las mejores directivas para su conjunto de riesgos en particular.

## <a name="asset-classification"></a>Clasificación de los recursos

**Riesgo técnico**: los recursos que no están identificados correctamente como críticos para la misión o que trabajan con datos confidenciales podrían no estar suficientemente protegidos, dando lugar a posibles pérdidas de datos o interrupciones de la actividad.

**Declaración de directiva**: Todos los recursos implementados deben categorizarse por importancia y clasificación de datos. El equipo de gobernanza de la nube y el propietario de la aplicación deben revisar las clasificaciones antes de la implementación en la nube.

**Opción de diseño posible**: establezca [normas de etiquetado de los recursos](../../decision-guides/resource-tagging/index.md) y asegúrese de que el personal de TI las aplique de forma coherente a los recursos implementados mediante las [etiquetas de recursos de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags).

## <a name="data-encryption"></a>Cifrado de datos

**Riesgo técnico**: hay un riesgo de exposición durante el almacenamiento de datos protegidos.

**Declaración de directiva**: todos los datos protegidos deben estar cifrados cuando están en reposo.

**Opción de diseño posible**: consulte el artículo [Introducción al cifrado de Azure](https://docs.microsoft.com/azure/security/security-azure-encryption-overview) para ver cómo se realiza el cifrado de los datos en reposo en la plataforma Azure. También se deben tener en cuenta controles adicionales, como el cifrado de datos de la cuenta y el control sobre cómo se puede cambiar la configuración de la cuenta de almacenamiento.

## <a name="network-isolation"></a>Aislamiento de red

**Riesgo técnico**: la conectividad entre las redes y subredes presenta posibles vulnerabilidades que pueden dar lugar a la pérdida de datos o la interrupción de servicios críticos.

**Declaración de directiva**: las subredes que contengan datos protegidos deben aislarse de las otras subredes. El tráfico de red entre las subredes de datos protegidos se debe auditar periódicamente.

**Opción de diseño posible**: en Azure, el aislamiento de las redes y subredes se administra mediante [Azure Virtual Networks](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).

## <a name="secure-external-access"></a>Acceso externo seguro

**Riesgo técnico**: permitir el acceso a las cargas de trabajo desde la red pública de Internet presenta un riesgo de intrusión y, como consecuencia, una exposición no autorizada de los datos o la interrupción del negocio.

**Declaración de directiva**: no se podrá acceder directamente desde Internet a ninguna subred que contenga datos protegidos, ni desde un centro de datos a otro. El acceso a esas subredes debe enrutarse a través de subredes intermedias. Todo el acceso a esas subredes debe realizarse a través de una solución de firewall que pueda realizar funciones de análisis y bloqueo de paquetes.

**Opción de diseño posible**: en Azure, proteja los puntos de conexión públicos mediante la implementación de una [red perimetral entre la red pública de Internet y su red en la nube](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz). Considere la posibilidad de realizar la implementación, configuración y automatización de [Azure Firewall](https://docs.microsoft.com/azure/firewall).

## <a name="ddos-protection"></a>Protección contra DDOS

**Riesgo técnico**: los ataques por denegación de servicio distribuido (DDoS) pueden provocar una interrupción del negocio.

**Declaración de directiva**: implemente mecanismos automatizados de mitigación de ataques DDoS en todos los puntos de conexión de red accesibles públicamente. No se debe exponer a Internet ningún sitio web público con respaldo de IaaS sin DDoS.

**Opción de diseño posible**: use [Azure DDoS Protection](https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview) Estándar para minimizar las interrupciones causadas por ataques DDoS.

## <a name="secure-on-premises-connectivity"></a>Protección de la conectividad local

**Riesgo técnico**: el tráfico sin cifrar que circula entre su red en la nube y el entorno local a través de la red pública de Internet puede ser interceptado, con el riesgo de que los datos queden expuestos.

**Declaración de directiva**: todas las conexiones entre el entorno local y las redes en la nube deben realizarse mediante una conexión de VPN cifrada segura o un vínculo WAN privado dedicado.

**Opción de diseño posible**: en Azure, use ExpressRoute o Azure VPN para establecer conexiones privadas entre el entorno local y las redes en la nube.

## <a name="network-monitoring-and-enforcement"></a>Supervisión de la red y cumplimiento

**Riesgo técnico**: los cambios realizados en la configuración de la red pueden provocar nuevas vulnerabilidades y riesgos de exposición de los datos.

**Declaración de directiva**: las herramientas de gobernanza deben auditar y aplicar los requisitos de configuración de red definidos por el equipo de la base de referencia de la seguridad.

**Opción de diseño posible**: en Azure, la actividad de la red se puede supervisar con [Azure Network Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview), y [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-network-recommendations) puede ayudar a identificar las vulnerabilidades de seguridad. Azure Policy permite restringir los recursos de red y la directiva de configuración de los recursos según los límites definidos por el equipo de seguridad.

## <a name="security-review"></a>Revisión de la seguridad

**Riesgo técnico**: con el tiempo, aparecen nuevas amenazas para la seguridad y nuevos tipos de ataques, que aumentan el riesgo de exposición o la interrupción de los recursos en la nube.

**Declaración de directiva**: el equipo de seguridad debe revisar periódicamente las tendencias y vulnerabilidades que podrían afectar a las implementaciones en la nube para proporcionar actualizaciones a las herramientas de la base de referencia de la seguridad que se usan en la nube.

**Opción de diseño posible**: establezca una reunión periódica para revisar la seguridad, que incluya a los miembros pertinentes de los equipos de TI y gobernanza. Revise las métricas y los datos de seguridad existentes para identificar deficiencias en las herramientas y la directiva de la base de referencia de la seguridad, y actualice la directiva para poner remedio a los nuevos riesgos. Utilice [Azure Advisor](https://docs.microsoft.com/azure/advisor/advisor-overview) y [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) para obtener información útil sobre las amenazas emergentes específicas de las implementaciones.

## <a name="next-steps"></a>Pasos siguientes

Use los ejemplos mencionados en este artículo como punto de partida para desarrollar directivas que aborden los riesgos específicos para su negocio, en línea con sus planes de adopción de la nube.

Para comenzar a desarrollar sus propias declaraciones de directiva personalizadas relativas a la base de referencia de la seguridad, descargue la [plantilla de base de referencia de la seguridad](./template.md).

Para acelerar la adopción de esta disciplina, elija la [guía de gobernanza accionable](../guides/index.md) que más se aproxime a su entorno. Después, modifique el diseño para incorporar las decisiones de directiva específicas de su organización.

A partir de los riesgos y la tolerancia, establezca un proceso para gobernar y comunicar la adhesión a la directiva de base de referencia de seguridad.

> [!div class="nextstepaction"]
> [Definición de procesos para el cumplimiento de directivas](./compliance-processes.md)
