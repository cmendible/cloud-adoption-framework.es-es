---
title: Introducción al cumplimiento normativo
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Introducción al cumplimiento normativo
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: b0bc28f46671c4ccf62bba9f3fa68f14e2b79aee
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031152"
---
# <a name="introduction-to-regulatory-compliance"></a>Introducción al cumplimiento normativo

Este es un artículo introductorio acerca del cumplimiento normativo; por lo tanto, su finalidad no es implementar una estrategia de cumplimiento. Sirve solo para brindar conocimiento general. Encontrará información más detallada sobre las [ofertas de cumplimiento de Azure](https://aka.ms/allcompliance) en el [Centro de confianza de Microsoft](https://www.microsoft.com/trustcenter/default.aspx). Además, toda la documentación que se puede descargar está disponible para determinados clientes de Azure en [Microsoft Service Trust Portal](https://servicetrust.microsoft.com).

Por cumplimiento normativo se entiende la materia y el proceso consistente en garantizar que una empresa cumple la legislación establecida por las administraciones públicas en su ubicación geográfica, o las normas del sector adoptadas voluntariamente. En el caso del cumplimiento normativo de TI, los usuarios o los procesos supervisan los sistemas de la empresa en un esfuerzo por detectar y evitar las infracciones de las directivas y los procedimientos que establecen la legislación y los reglamentos existentes. Esto se aplica a su vez a un área muy amplia de los procesos de supervisión y aplicación. En función del sector y de la ubicación geográfica, estos procesos pueden ser bastante largos y complejos.

En el caso de las organizaciones multinacionales (especialmente las de los sectores con mucha regulación, como los servicios financieros y la atención sanitaria), el cumplimiento puede ser muy complicado. Hay un gran número de normas y regulaciones que, en ciertos casos, cambian con frecuencia. El resultado es que para las empresas cada vez es más difícil mantenerse al tanto de la evolución de las leyes internacionales de gestión de datos electrónicos.

Al igual que sucede con los controles de seguridad, las organizaciones deben conocer la división de responsabilidades con respecto al cumplimiento normativo en la nube. Los proveedores de servicios en la nube se esfuerzan por asegurarse de que sus servicios y plataformas son cumplen la legislación. Sin embargo, las organizaciones también deben confirmar que sus aplicaciones, la infraestructura de la que dependen las aplicaciones y los servicios proporcionados por terceros también estén certificados como conformes a la norma.

Estas son las descripciones de las regulaciones de cumplimiento de diversos sectores y regiones geográficas:

## <a name="hipaa"></a>HIPAA

Una aplicación de asistencia sanitaria que procesa información médica protegida (PHI) está sujeta tanto a la regla de privacidad como a la regla de seguridad incluidas en la Ley de responsabilidad y transferibilidad de seguros médicos (HIPAA). Como mínimo, es probable que HIPAA requiera que una empresa de atención sanitaria reciba la garantía por escrito del proveedor de nube de que toda la información médica protegida recibida o creada estará segura.

## <a name="pci"></a>PCI

El estándar de seguridad de los datos para la industria de las tarjetas de pago (PCI DSS) es un estándar de seguridad de información privilegiada para las organizaciones que controlan las tarjetas de crédito de las principales empresas de tarjetas, como Visa, Mastercard, American Express, Discover y JCB. El estándar de PCI lo imponen las marcas de tarjeta y lo administra la entidad Payment Card Industry Security Standards Council. Dicho estándar se creó para aumentar los controles de los datos de los titulares, con el fin de reducir el fraude en las tarjetas de crédito. La validación del cumplimiento la realiza anualmente un asesor de seguridad cualificado (QSA), un asesor de seguridad interno (ISA) específico de la firma que crea un informe acerca del cumplimiento (ROC) para las organizaciones que controlan grandes volúmenes de transacciones, o mediante un cuestionario de autoevaluación (SAQ) de las empresas.

## <a name="personal-data"></a>Datos personales

La información personal es cualquier dato que se puede utilizar para identificar a un consumidor, empleado, asociado o cualquier otra entidad viva o legal. Muchas de las leyes recientes, sobre todo las relacionadas con la privacidad y los datos personales, no solo requieren que las empresas las cumplan, sino también que informen acerca del cumplimiento y de las infracciones que se puedan producir.

## <a name="gdpr"></a>GDPR

Uno de los desarrollos más importantes en esta área es la reciente promulgación por parte de la Comisión Europea del Reglamento General de Protección de Datos (RGPD), diseñada para reforzar la protección de los datos de los ciudadanos de la Unión Europea. El RGPD requiere que los datos personales (como "el nombre, la dirección particular, la fotografía, la dirección de correo electrónico, los datos bancarios, las publicaciones en los sitios de redes sociales, la información médica o la dirección IP de un equipo"), se mantengan en servidores que se encuentren dentro de la UE y no transfieran fuera de ella. También requiere que las empresas envíen notificaciones a los usuarios si se produce cualquier vulneración de sus datos y exige que haya un responsable de la protección de los datos. Otros países tienen tipos similares de regulaciones o los están desarrollando.

## <a name="compliant-foundation-in-azure"></a>Base de cumplimiento en Azure

Para ayudar a los clientes a cumplir sus propias obligaciones de cumplimiento en los sectores y mercados regulados de todo el mundo, Azure mantiene la mayor cartera de cumplimiento del sector, tanto en amplitud (número total de ofertas) como en profundidad (número de servicios orientados al cliente en el ámbito de la evaluación). Las ofertas de cumplimiento de Azure se agrupan en cuatro segmentos: aplicables globalmente, gobierno de EE. UU., específicas de un sector y específicas de un país o región.

Las ofertas de cumplimiento de Azure se basan en varios tipos de controles, entre los que se incluyen certificaciones oficiales, atestaciones, validaciones, autorizaciones y evaluaciones generadas por empresas de auditoría de terceros independientes, así como enmiendas contractuales, autoevaluaciones y documentos de instrucciones para el cliente generados por Microsoft. Todas las descripciones de las ofertas de este documento proporcionan declaraciones actualizadas acerca del ámbito que indican qué servicios orientados al cliente de Azure están en el ámbito de la valoración, así como vínculos a recursos descargables para ayudar a los clientes con sus propias obligaciones de cumplimiento.

En [Microsoft Trust Center](https://www.microsoft.com/trustcenter/compliance/complianceofferings), puede encontrar más información acerca de las ofertas de cumplimiento de Azure. Además, toda la documentación que se puede descargar está disponible para determinados clientes de Azure en [Service Trust Portal](https://servicetrust.microsoft.com), en las siguientes secciones:

- **Informes de auditoría:** incluye secciones de FedRAMP, evaluación de GRC, ISO, PCI DSS e informes de SOC.
- **Recursos para la protección de datos:** incluye guías de cumplimiento, preguntas frecuentes y notas del producto, así como secciones de prueba de penetración y evaluaciones de seguridad.

## <a name="next-steps"></a>Pasos siguientes

Más información sobre la preparación de la seguridad en la nube.

> [!div class="nextstepaction"]
> [Preparación de la seguridad en la nube](./cloud-security-readiness.md)
