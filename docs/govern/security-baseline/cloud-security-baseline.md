---
title: Descripción de la línea de base de seguridad en la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Más información sobre la línea de base de seguridad en la nube.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: dfb7969d19017c003ef961c18e87b8cb110ccd4e
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031750"
---
# <a name="understand-the-cloud-security-baseline"></a>Descripción de la línea de base de seguridad en la nube

Este es un artículo introductorio sobre el tema general de una línea de base de seguridad en la nube que se basa en las [cinco materias de gobernanza de la nube](../governance-disciplines.md) para establecer un marco de gobernanza. Hay disponible información más detallada sobre la seguridad en la nube en la [nube de confianza de Azure](https://azure.microsoft.com/overview/trusted-cloud). Los enfoques para mejorar el planteamiento de seguridad de las organizaciones pueden encontrarse en el [catálogo de servicios de seguridad en la nube](https://www.microsoft.com/security/information-protection)

> [!NOTE]
> Este artículo no está concebido para ofrecer un contexto suficiente que permita al lector implementar una estrategia de seguridad. Sirve solo para brindar conocimiento general.

## <a name="cloud-security"></a>Seguridad en la nube

La seguridad en la nube es una extensión de las prácticas de seguridad de la información tradicionales. La seguridad de TI tradicional incluiría las directivas y controles que rigen la seguridad de los equipos, la seguridad de red, la protección de datos, el uso de la información, etc. Estas mismas directivas y controles se necesitan en la nube. Durante cualquier transformación hacia la nube, es imperativo que el director de seguridad de la información participe activamente y entienda el entorno de la nube a fin de garantizar que las directivas de TI heredadas se asignen a los niveles adecuados de control en la nube.

Como mínimo, cualquier estrategia de seguridad en la nube debe tener en cuenta los siguientes aspectos:

- **Clasificar los datos.** clasificación de datos adecuada para comprender los orígenes de datos privados, protegidos o extremadamente confidenciales. Esto ayudará a administrar el riesgo durante la planeación.
- **Planear para un escenario de nube híbrida.** La comprensión del modo en que las redes locales heredadas se van a conectar a la nube ayuda al director de seguridad de la información a identificar y corregir los riesgos.
- **Planear para ataques y errores.** en los primeros meses de una transformación, se cometerán errores a medida que el equipo vaya aprendiendo. Comience con implementaciones de bajo riesgo y muy restringidas para aprender de forma segura.
- **Dar prioridad a la privacidad.** a lo largo de cualquier transformación, todo el equipo debe tener en mente como elemento fundamental la privacidad del cliente y el empleado. Los datos están seguros en la nube, pero el equipo debe ser consciente y extremadamente cauteloso al tratar con datos confidenciales.

## <a name="protecting-data-and-privacy"></a>Protección de los datos y la privacidad

Para las organizaciones de todo el mundo, ya sean gobiernos, organizaciones sin ánimo de lucro o empresas, la informática en la nube se ha convertido en una parte fundamental de su estrategia de TI en curso. Los servicios en la nube brindan a las organizaciones de todos los tamaños acceso a un almacenamiento de datos prácticamente ilimitado, a la vez que los libera de la necesidad de comprar, mantener y actualizar sus propias redes y sistemas informáticos. Microsoft y otros proveedores de servicios en la nube ofrecen infraestructura, plataforma y software como servicio (SaaS) para la TI, lo que permite a los clientes escalar o reducir verticalmente según sus necesidades y pagar solo por la capacidad de proceso y el almacenamiento que usen.

Sin embargo, a medida que las organizaciones continúan sacando partido de los beneficios de los servicios en la nube, como el aumento de las opciones, la agilidad y la flexibilidad, y aumentan la eficiencia y reducen los costos de TI, deben considerar cómo afecta la introducción de los servicios en la nube a su postura relativa con la privacidad, la seguridad y el cumplimiento normativo. Microsoft ha trabajado para que sus ofertas de nube no sean solo escalables, confiables y fáciles de administrar, sino que también garanticen que los datos de nuestros clientes estén protegidos y se utilicen de forma transparente.

La seguridad es un componente esencial de unas eficaces medidas de protección de los datos en todos los entornos informáticos en línea. Pero solo con la seguridad no basta. La disposición de los consumidores y las empresas a utilizar un producto de informática en la nube en particular también depende de su capacidad para confiar en que se protegerá la privacidad de su información y que sus datos solo se utilizarán de manera compatible con las expectativas del cliente. Obtenga más información sobre el enfoque de Microsoft en relación con la [protección de datos y privacidad en la nube](https://go.microsoft.com/fwlink/?LinkId=808242&clcid=0x409)

## <a name="risk-mitigation"></a>Mitigación de riesgos

Los dos mayores riesgos en cualquier centro de datos se pueden agrupar en dos orígenes: Envejecimiento de sistemas y error humano. La protección contra estos dos riesgos es lo mínimo cuando se define una estrategia de seguridad de TI. Pues lo mismo puede decirse de la nube. Los siguientes son algunos ejemplos de controles que pueden implementarse a fin de corregir los riesgos y de fortalecer la estrategia de seguridad en la nube.

- **Sistemas heredados:** Muchos componentes de las soluciones de centros de datos locales constan de software, hardware y procesos que son anteriores a los riesgos de seguridad actuales. Cuando sea posible, corrija, reemplace o retire estos sistemas durante una transformación hacia la nube. Por supuesto, no siempre es factible. Si algún sistema heredado va a permanecer en producción en una solución híbrida, es importante que dicho sistema se haya inventariado y comprendido durante el diseño del centro de datos virtual. Esto permitirá al equipo de diseño eliminar o controlar el acceso a esos sistemas desde la nube.
- **Controles y procesos de seguridad de TI:** como mínimo, los equipos de diseño de la nube deben ponerse al día de los procesos y controles de seguridad de TI existentes para llevarlos a la nube. En un escenario ideal, un miembro del equipo de seguridad de TI estaría formado en ciberseguridad y participaría en los equipos de diseño e implementación.
- **Supervisión y auditoría:** Al diseñar los procesos y las herramientas de gobernanza, asegúrese de que las soluciones de supervisión y auditoría incluyan los riesgos o infracciones de seguridad.

> [!NOTE]
> **Divulgación de deuda técnica:** En este tema no contiene a continuación pasos prácticos. Se sumarán artículos con el tiempo para ampliar esta información. Hay disponible información más detallada acerca de la seguridad en la nube en [Seguridad en una nube de confianza](https://azure.microsoft.com/overview/trusted-cloud). Los enfoques para mejorar el planteamiento de seguridad de las organizaciones pueden encontrarse en el [catálogo de servicios de seguridad en la nube](https://www.microsoft.com/security/information-protection)
