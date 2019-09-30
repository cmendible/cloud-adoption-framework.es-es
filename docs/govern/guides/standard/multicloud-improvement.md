---
title: 'Guía para empresa estándar: Mejora de la nube múltiple'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Guía para empresa estándar: Mejora de la nube múltiple'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 2616193b01b252a74ad17a241d97bfd0ebc4860c
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223793"
---
# <a name="small-to-medium-enterprise-guide-multicloud-improvement"></a>Guía para pequeñas y medianas empresas: Mejora de la nube múltiple

En este artículo se desarrolla la narrativa con la adición de controles para la adopción de varias nubes.

## <a name="advancing-the-narrative"></a>Continuación de la historia

Microsoft reconoce que los clientes pueden adoptar varias nubes para propósitos específicos. El cliente ficticio de esta guía no es una excepción. Paralelamente al recorrido de adopción de Azure, el éxito del negocio ha llevado a la adquisición de una empresa pequeña, pero complementaria. Ese negocio ejecuta todas sus operaciones de TI en un proveedor de servicios en la nube diferente.

En este artículo se describen cómo cambian las cosas cuando se integra la nueva organización. A efectos de la narrativa, asumimos que esta empresa ha completado cada una de las iteraciones de gobernanza descritas en esta guía de gobernanza.

### <a name="changes-in-the-current-state"></a>Cambios en el estado actual

En la fase anterior de esta narrativa, la empresa había comenzado a insertar activamente las aplicaciones de producción en la nube mediante canalizaciones de CI/CD.

Desde entonces, han cambiado algunas cosas que afectarán a la gobernanza:

- La identidad se controla mediante una instancia local de Active Directory. La identidad híbrida se facilita mediante la replicación a Azure Active Directory.
- Las operaciones de TI o las operaciones en la nube se administran en gran parte en Azure Monitor y en automatizaciones relacionadas.
- La recuperación ante desastres y la continuidad empresarial se controlan por instancias de Azure Vault.
- Azure Security Center se utiliza para supervisar infracciones de seguridad y ataques.
- Tanto Azure Security Center como Azure Monitor se utilizan para supervisar la gobernanza de la nube.
- Azure Blueprints, Azure Policy y los grupos de administración de Azure se utilizan para automatizar el cumplimiento con la directiva.

### <a name="incrementally-improve-the-future-state"></a>Mejora gradual del estado futuro

El objetivo es integrar la empresa de adquisición en las operaciones existentes siempre que sea posible.

## <a name="changes-in-tangible-risks"></a>Cambios en riesgos tangibles

**Costo de adquisición de negocios:** se estima que la adquisición del nuevo negocio sea rentable en aproximadamente cinco años. Debido a la lenta tasa de retorno, la junta quiere controlar los costos de adquisición, en la medida de lo posible. Existe el riesgo de que el control de costos y la integración técnica entren en conflicto entre sí.

Este riesgo empresarial puede ampliarse a algunos riesgos técnicos:

- La migración a la nube podría producir costos de adquisición adicionales.
- Es posible que el nuevo entorno no esté gobernado adecuadamente, lo que podría dar lugar a infracciones de las directivas.

## <a name="incremental-improvement-of-the-policy-statements"></a>Mejora gradual de las declaraciones de las directivas

Los siguientes cambios en la directiva le ayudarán a corregir los nuevos riesgos y le guiarán en la implementación:

- Todos los recursos en una nube secundaria deben supervisarse mediante las herramientas existentes de administración operativa y supervisión de seguridad.
- Todas las unidades organizativas deben integrarse en el proveedor de identidades existente.
- El proveedor de identidades principal debe regir la autenticación de los recursos en la nube secundaria.

## <a name="incremental-improvement-of-governance-practices"></a>Mejora incremental de las prácticas de gobernanza

En esta sección del artículo se cambiará el diseño del producto viable mínimo de gobernanza para incluir nuevas directivas de Azure y una implementación de Azure Cost Management. Juntos, estos cambios de diseño cumplirán con las nuevas declaraciones de directiva corporativa.

1. Conecte las redes. Este paso lo ejecutan los equipos de redes y de seguridad de TI y lo apoya el equipo de gobernanza de la nube. La adición de una conexión desde el proveedor de líneas alquiladas o MPLS a la nueva nube integrará las redes. La adición de tablas de enrutamiento y configuraciones de firewall controlará el acceso y el tráfico entre los entornos.
2. Consolide los proveedores de identidades. Dependiendo de las cargas de trabajo que se hospeden en la nube secundaria, hay una variedad de opciones para la consolidación de proveedores de identidades. Estos son algunos ejemplos:
    1. Para las aplicaciones que se autentican mediante OAuth 2, los usuarios de Active Directory en la nube secundaria pueden simplemente replicarse al inquilino de Azure AD existente. Esto asegura que todos los usuarios se puedan autenticar en el inquilino.
    2. En el otro extremo, la federación permite que las unidades organizativas fluyan a Active Directory local y después a la instancia de Azure AD.
3. Agregue recursos a Azure Site Recovery.
    1. Azure Site Recovery se ha diseñado desde el principio como una herramienta híbrida o de varias nubes.
    2. Las máquinas virtuales en la nube secundaria podrían estar protegidas por los mismos procesos de Azure Site Recovery utilizados para proteger los recursos locales.
4. Agregue recursos a Azure Cost Management.
    1. Azure Cost Management se ha diseñado desde el principio como una herramienta para varias nubes.
    2. Las máquinas virtuales en la nube secundaria pueden ser compatibles con Azure Cost Management para algunos proveedores de servicios en la nube. Se pueden aplicar costos adicionales.
5. Agregue recursos a Azure Monitor.
    1. Azure Monitor se ha diseñado desde el principio como una herramienta de nube híbrida.
    2. Las máquinas virtuales en la nube secundaria pueden ser compatibles con los agentes de Azure Monitor, lo que permite incluirlas en Azure Monitor para la supervisión operativa.
6. Adopte las herramientas de aplicación de la gobernanza.
    1. El cumplimiento de gobernanza es específico de la nube.
    2. Las directivas corporativas establecidas en la guía de gobernanza no son específicas de la nube. Aunque la implementación puede variar de una nube a otra, las directivas pueden aplicarse al proveedor secundario.

La adopción de varias nubes se debe implementar donde sea necesaria en función de necesidades técnicas o requisitos empresariales específicos. A medida que progresa la adopción de varias nubes, aumenta la complejidad y los riesgos de seguridad.

## <a name="conclusion"></a>Conclusión

En esta serie de artículos se describe el desarrollo incremental de los procedimientos recomendados de gobernanza, alineados con las experiencias de esta empresa ficticia. Al comenzar con una base pequeña, pero con los cimientos adecuados, la empresa podría moverse rápidamente y aún así aplicar la cantidad adecuada de gobernanza en el momento adecuado. El producto mínimo viable por sí mismo no ha protegido al cliente. En cambio, ha creado las bases para administrar los riesgos y agregar protecciones. A partir de ahí, se aplicaron capas de gobernanza para corregir los riesgos tangibles. El recorrido exacto que aquí se ha presentado no se alinea al 100 % con las experiencias de ningún lector. Más bien, sirve como patrón para la gobernanza incremental. Se aconseja al lector moldear estos procedimientos recomendados para que se ajusten a sus propias limitaciones y requisitos de gobernanza.
