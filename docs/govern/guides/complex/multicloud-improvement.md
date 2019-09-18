---
title: 'Guía de gobernanza para empresas complejas: Mejora de la nube múltiple'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Guía para grandes empresas: Mejora de la nube múltiple'
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 6f015fcc7a0cb4000502d90ff971341fd6d26ca5
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032215"
---
# <a name="large-enterprise-guide-multicloud-improvement"></a>Guía para grandes empresas: Mejora de la nube múltiple

## <a name="advancing-the-narrative"></a>Continuación de la historia

Microsoft reconoce que los clientes están adoptando varias nubes para propósitos específicos. La empresa ficticia de esta guía no es una excepción. Paralelamente al recorrido de adopción de Azure, el éxito del negocio ha llevado a la adquisición de una empresa pequeña, pero complementaria. Ese negocio ejecuta todas sus operaciones de TI en un proveedor de servicios en la nube diferente.

En este artículo se describen cómo cambian las cosas cuando se integra la nueva organización. A efectos de la narrativa, asumimos que esta empresa ha completado cada una de las iteraciones de gobernanza descritas en esta guía de gobernanza.

### <a name="changes-in-the-current-state"></a>Cambios en el estado actual

En la fase anterior de esta narrativa, la empresa empezó a implementar controles y supervisión de costos, ya que el gasto en la nube empieza a formar parte de los gastos operativos normales de la empresa.

Desde entonces, han cambiado algunas cosas que afectarán a la gobernanza:

- La identidad se controla mediante una instancia local de Active Directory. La identidad híbrida se facilita mediante la replicación a Azure Active Directory.
- Las operaciones de TI o las operaciones en la nube se administran en gran parte en Azure Monitor y en las funcionalidades de automatización relacionadas.
- La recuperación ante desastres y la continuidad empresarial (DRBC) se controlan mediante instancias de Azure Vault.
- Azure Security Center se utiliza para supervisar infracciones de seguridad y ataques.
- Tanto Azure Security Center como Azure Monitor se utilizan para supervisar la gobernanza de la nube.
- Azure Blueprints, Azure Policy y los grupos de administración se utilizan para automatizar el cumplimiento con la directiva.

### <a name="incrementally-improve-the-future-state"></a>Mejora gradual del estado futuro

El objetivo es integrar la empresa de adquisición en las operaciones existentes siempre que sea posible.

## <a name="changes-in-tangible-risks"></a>Cambios en riesgos tangibles

**Costo de adquisición de negocios:** se estima que la adquisición del nuevo negocio sea rentable en aproximadamente cinco años. Debido a la lenta tasa de retorno, la junta quiere controlar los costos de adquisición, en la medida de lo posible. Existe el riesgo de que el control de costos y la integración técnica entren en conflicto entre sí.

Este riesgo empresarial puede ampliarse a algunos riesgos técnicos:

- Existe el riesgo de que la migración a la nube genere costos de adquisición adicionales.
- También se plantea el riesgo de que el nuevo entorno no esté correctamente regulado o de que se produzcan infracciones de directivas.

## <a name="incremental-improvement-of-the-policy-statements"></a>Mejora gradual de las declaraciones de las directivas

Los siguientes cambios en la directiva le ayudarán a corregir los nuevos riesgos y le guiarán en la implementación.

- Todos los recursos en una nube secundaria deben supervisarse mediante las herramientas existentes de administración operativa y supervisión de seguridad.
- Todas las unidades organizativas deben integrarse en el proveedor de identidades existente.
- El proveedor de identidades principal debe regir la autenticación de los recursos en la nube secundaria.

## <a name="incremental-improvement-of-the-best-practices"></a>Mejoras graduales de los procedimientos recomendados

En esta sección del artículo se mejora el diseño de un producto viable mínimo de gobernanza para incluir nuevas directivas de Azure y una implementación de Azure Cost Management. Juntos, estos dos cambios de diseño cumplirán con las nuevas declaraciones de directiva corporativa.

1. Conecte las redes. Esta instrucción la ejecutan los equipos de redes y seguridad de TI, respaldados por el equipo de gobernanza.
    1. La adición de una conexión desde el proveedor de líneas alquiladas o MPLS a la nueva nube integrará las redes. La adición de tablas de enrutamiento y configuraciones de firewall controlará el acceso y el tráfico entre los entornos.
1. Consolide los proveedores de identidades. Dependiendo de las cargas de trabajo que se hospeden en la nube secundaria, hay una variedad de opciones para la consolidación de proveedores de identidades. Estos son algunos ejemplos:
    1. Para las aplicaciones que se autentican mediante OAuth 2, los usuarios de Active Directory en la nube secundaria podrían replicarse simplemente al inquilino de Azure AD existente.
    1. En el otro extremo, la federación entre los dos proveedores de identidades locales permitiría la replicación de los usuarios de los nuevos dominios de Active Directory en Azure.
1. Agregue recursos a Azure Site Recovery.
    1. Azure Site Recovery se ha diseñado desde el principio como una herramienta híbrida o de varias nubes.
    1. Las máquinas virtuales en la nube secundaria podrían estar protegidas por los mismos procesos de Azure Site Recovery utilizados para proteger los recursos locales.
1. Agregue recursos a Azure Cost Management.
    1. Azure Cost Management se ha diseñado desde el principio como una herramienta de varias nubes.
    1. Las máquinas virtuales en la nube secundaria podrían ser compatibles con Azure Cost Management para algunos proveedores de servicios en la nube. Se pueden aplicar costos adicionales.
1. Agregue recursos a Azure Monitor.
    1. Azure Monitor se ha diseñado desde el principio como una herramienta de nube híbrida.
    1. Las máquinas virtuales en la nube secundaria podrían ser compatibles con los agentes de Azure Monitor, lo que permite incluirlas en Azure Monitor para la supervisión operativa.
1. Herramientas de cumplimiento de gobernanza.
    1. El cumplimiento de gobernanza es específico de la nube.
    1. Las directivas corporativas establecidas en la guía de gobernanza no son específicas de la nube. Aunque la implementación puede variar de una nube a otra, las declaraciones de directivas pueden aplicarse al proveedor secundario.

A medida que crece la adopción de varias nubes, el diseño de la gobernanza continuará evolucionando.

## <a name="next-steps"></a>Pasos siguientes

En muchas grandes empresas, las cinco materias de gobernanza de la nube pueden ser obstáculos para la adopción. El siguiente artículo incluye algunas conclusiones adicionales sobre cómo convertir la gobernanza en un deporte en equipo, a fin de ayudar a garantizar el éxito a largo plazo en la nube.

> [!div class="nextstepaction"]
> [Varias capas de gobernanza](./multiple-layers-of-governance.md)
