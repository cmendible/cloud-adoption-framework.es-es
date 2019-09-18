---
title: Guía de preparación de CISO para la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Cómo se puede preparar un CISO para la nube
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/03/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 935012e6b2de78e4698a7d484da25cf888d00071
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031541"
---
# <a name="ciso-cloud-readiness-guide"></a>Guía de preparación de CISO para la nube

Las guías de Microsoft, como Cloud Adoption Framework, no están en posición de determinar o guiar las restricciones de seguridad únicas de las miles de empresas a las que se puede aplicar esta documentación. Al cambiar a la nube, sus tecnologías no reemplazarán el rol de responsable de la seguridad de la información. Al contrario, el Director de seguridad de la información y la Oficial principal de seguridad de la información se integran aún más. En esta guía se da por supuesto que el lector está familiarizado con los procesos de seguridad de la información y que desea modernizar esos procesos para habilitar la transformación a la nube.

La adopción de la nube permite obtener servicios que a menudo no se tenían en cuenta en los entornos de TI tradicionales. Normalmente, las implementaciones de autoservicio o automatizadas las ejecuta el equipo de desarrollo de aplicaciones u otros equipos de TI que tradicionalmente no estaban en línea con la implementación de producción. En algunas organizaciones, los componentes del negocio tienen capacidades de autoservicio. Esta opción puede desencadenar nuevos requisitos de seguridad que no eran necesarios en el entorno local. La seguridad centralizada es un desafío mayor, puesto que a menudo se convierte en una responsabilidad compartida en la cultura empresarial y de TI. Este artículo puede servirle de ayuda para preparar un CISO para ese enfoque y que así pueda participar en una gobernanza incremental.

<!-- markdownlint-disable MD026 -->

## <a name="how-can-a-ciso-prepare-for-the-cloud"></a>¿Cómo se puede preparar un CISO para la nube?

Tal y como sucede con la mayoría de las directivas, las directivas de seguridad y gobernanza de una organización tienden a crecer de forma orgánica. Cuando ocurren incidentes de seguridad, se crea la directiva oportuna para informar a los usuarios y reducir la probabilidad de que estos incidentes se repitan. Si bien es normal, este método crea una gran cantidad de directivas y dependencias técnicas. Por ello, los recorridos de transformación a la nube crean una oportunidad única para modernizar y restablecer las directivas. Mientras se prepara para realizar un recorrido de transformación, el CISO puede crear un valor inmediato y mensurable al actuar como la parte interesada en una [revisión de la directiva](./cloud-policy-review.md).

En dicha revisión, el rol del CISO radica en crear un equilibrio seguro entre las restricciones y el cumplimiento de la directiva y seleccionar la mejor opción de seguridad de los proveedores en la nube. La medición de este progreso se puede realizar de muchas formas, aunque a menudo se mide en función de la cantidad de directivas de seguridad que se pueden descargar de forma segura al proveedor en la nube.

**Transferencia de riesgos de seguridad.** A medida que los servicios se trasladan a los modelos de hospedaje de infraestructura como servicio (IaaS), la empresa asume menos riesgos directos con respecto al aprovisionamiento de hardware. El riesgo no se elimina, sino que se transfiere al proveedor en la nube. Si el enfoque de un proveedor de nube para el aprovisionamiento de hardware proporciona el mismo nivel de mitigación de riesgos y el proceso es seguro y repetible, el riesgo de la ejecución del aprovisionamiento de hardware se elimina del área de responsabilidad del departamento de TI corporativo y se transfiere al proveedor de nube. Esto reduce el riesgo de seguridad general que la empresa es responsable de administrar, aunque el riesgo en sí debe seguirse y revisarse periódicamente.

A medida que las soluciones se incorporan a modelos de plataforma como servicio (PaaS) o software como servicio (SaaS), se pueden evitar o transferir otros riesgos adicionales. Cuando el riesgo se transfiere de manera segura a un proveedor en la nube, el costo de ejecutar, supervisar y aplicar las directivas de seguridad u otras directivas de cumplimiento también se puede reducir de manera segura.

**Mentalidad de crecimiento.** Este cambio puede intimidar a la empresa y a los implementadores técnicos. Cuando el CISO lidera un cambio en la mentalidad de crecimiento de una organización, descubrimos que esos temores naturales se reemplazan con un mayor interés en la seguridad y el cumplimiento de directivas. Si se combina una [revisión de directivas](./cloud-policy-review.md), un recorrido de transformación o sencillas revisiones de implementación con una mentalidad de crecimiento, el equipo tendrá la oportunidad de reaccionar rápidamente, pero no a costa de un perfil de riesgo razonable y manejable.

## <a name="resources-for-the-chief-information-security-officer"></a>Recursos para el Director de seguridad de la Información

El conocimiento sobre la nube es fundamental para combinar una [revisión de directivas](./cloud-policy-review.md) con una mentalidad de crecimiento. Los siguientes recursos pueden ayudar al CISO a comprender mejor la postura de seguridad de la plataforma Azure de Microsoft.

Recursos de la plataforma de seguridad:

- [Ciclo de vida de desarrollo de la seguridad, auditorías internas](https://www.microsoft.com/sdl)
- [Entrenamiento de seguridad obligatorio, comprobación de antecedentes](https://downloads.cloudsecurityalliance.org/star/self-assessment/StandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx)
- [Pruebas de penetración, detección de intrusiones, DDoS, auditorías y registros](https://www.microsoft.com/trustcenter/Security/AuditingAndLogging)
- [Centro de datos de vanguardia](https://www.microsoft.com/cloud-platform/global-datacenters), seguridad física, [red segura](https://docs.microsoft.com/azure/security/security-network-overview)
- [Microsoft Azure Security Response in the Cloud (PDF)](https://aka.ms/SecurityResponsePaper) (Respuesta de seguridad de Microsoft Azure en la nube [en PDF]).

Privacidad y controles:

- [Administración constante de los datos](https://www.microsoft.com/trustcenter/Privacy/You-own-your-data)
- [Control en la ubicación de los datos](https://www.microsoft.com/trustcenter/Privacy/Where-your-data-is-located)
- [Proporcionar acceso a datos en sus propios términos](https://www.microsoft.com/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms)
- [Respuesta a las autoridades judiciales](https://www.microsoft.com/trustcenter/Privacy/Responding-to-govt-agency-requests-for-customer-data)
- [Rigurosos estándares de privacidad](https://www.microsoft.com/TrustCenter/Privacy/We-set-and-adhere-to-stringent-standards)

Cumplimiento:

- [Microsoft Trust Center](https://www.microsoft.com/trustcenter/default.aspx)
- [Centro de controles comunes](https://www.microsoft.com/trustcenter/Common-Controls-Hub)
- [Lista de comprobación de diligencia debida para los servicio en la nube](https://www.microsoft.com/trustcenter/Compliance/Due-Diligence-Checklist)
- [Cumplimiento por servicio, ubicación y sector](https://www.microsoft.com/trustcenter/Compliance/default.aspx)

Transparencia:

- [Cómo Microsoft protege los datos de clientes en servicios de Azure](https://www.microsoft.com/trustcenter/Transparency/default.aspx)
- [Cómo administra Microsoft la ubicación de datos en los servicios de Azure](https://azuredatacentermap.azurewebsites.net)
- [Personas de Microsoft que pueden acceder a sus datos y bajo qué términos](https://www.microsoft.com/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms)
- [Cómo Microsoft protege los datos de clientes en servicios de Azure](https://www.microsoft.com/trustcenter/Transparency/default.aspx)
- [Revisión de la certificación para servicios de Azure, centro de transparencia](https://www.microsoft.com/trustcenter/Compliance/default.aspx)

## <a name="next-steps"></a>Pasos siguientes

El primer paso para tomar medidas en cualquier estrategia de gobernanza, es realizar una [revisión de directiva](./cloud-policy-review.md). La sección [Directiva y cumplimiento](./index.md) puede ser una guía útil durante la revisión de las directivas.

> [!div class="nextstepaction"]
> [Prepararse para una revisión de la directiva](./cloud-policy-review.md)
