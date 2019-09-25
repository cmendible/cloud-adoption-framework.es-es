---
title: Herramientas de base de referencia de seguridad
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Explicación de las herramientas que pueden mejorar la base de referencia de seguridad en Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 3bf3eea5486fbd349094663dc5f37527f5042bb5
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71221691"
---
# <a name="security-baseline-tools-in-azure"></a>Herramientas de base de referencia de seguridad

La [base de referencia de seguridad](./index.md) es una de las [cinco materias de gobernanza en la nube](../governance-disciplines.md). Esta materia se centra en formas de establecer directivas que protegen la red, los recursos y, lo que es más importante, los datos que residirán en una solución del proveedor de nube. Dentro de las cinco materias de gobernanza de la nube, la correspondiente a la base de referencia de seguridad implica la clasificación del patrimonio digital y los datos. También implica documentación de estrategias de mitigación, tolerancia empresarial y riesgos que se asocian a la seguridad de los datos, los recursos y las redes. Desde una perspectiva técnica, esta materia también incluye la participación en decisiones sobre el [cifrado](../../decision-guides/encryption/index.md), los [requisitos de red](../../decision-guides/software-defined-network/index.md), las [estrategias de identidad híbrida](../../decision-guides/identity/index.md) y las herramientas para [automatizar la aplicación](../../decision-guides/policy-enforcement/index.md) de directivas de seguridad en los [grupos de recursos](../../decision-guides/resource-consistency/index.md).

La siguiente lista de herramientas de Azure puede contribuir desarrollar las directivas y los procesos que admiten la base de referencia de seguridad.

| Herramienta | [Azure Portal](https://azure.microsoft.com/features/azure-portal) / [Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)  | [Azure Key Vault](https://docs.microsoft.com/azure/key-vault)  | [Azure AD](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis) | [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) | [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro) | [Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) |
|------------------------------------------------------------|---------------------------------|-----------------|----------|--------------|-----------------------|---------------|
| Aplicación de controles de acceso a recursos y creación de recursos   | Sí                             | Sin              | Sí      | No           | No                    | Sin            |
| Protección de redes virtuales                                    | Sí                             | No              | No       | Sí          | No                    | Sin            |
| Cifrado de discos virtuales                                     | Sin                              | Sí             | No       | No           | No                    | Sin            |
| Cifrado de bases de datos y almacenamiento PaaS                         | Sin                              | Sí             | No       | No           | No                    | Sin            |
| Administración de servicios de identidad híbrida                            | Sin                              | No              | Sí      | No           | No                    | Sin            |
| Restricción de tipos de recurso permitidos                         | Sin                              | No              | No       | Sí          | No                    | Sin            |
| Aplicación de restricciones geográficas regionales                          | Sin                              | No              | No       | Sí          | No                    | Sin            |
| Supervisión del estado de seguridad de redes y recursos          | Sin                              | No              | No       | No           | Sí                   | Sí           |
| Detección de actividad malintencionada                                  | Sin                              | No              | No       | No           | Sí                   | Sí           |
| Detección de vulnerabilidades de forma preventiva                        | Sin                              | No              | No       | No           | Sí                   | Sin            |
| Configuración de copia de seguridad y recuperación ante desastres                     | Sí                             | No              | No       | No           | No                    | Sin            |

Para ver una lista completa de servicios y herramientas de seguridad de Azure, consulte [Servicios y tecnologías de seguridad disponibles en Azure](https://docs.microsoft.com/azure/security/azure-security-services-technologies).

También es habitual que los clientes usen herramientas de terceros para facilitar las actividades de base de referencia de seguridad. Para obtener más información, consulte el artículo [Integración de soluciones de seguridad en Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-partner-integration).

Además de las herramientas de seguridad, el [Centro de confianza de Microsoft](https://www.microsoft.com/trustcenter/guidance/risk-assessment) contiene orientación amplia, informes y documentación relacionada que pueden ayudarle a realizar evaluaciones de riesgos como parte de su proceso de planeación de migración.
