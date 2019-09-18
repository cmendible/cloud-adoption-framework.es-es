---
title: Seguimiento de los costos en unidades de negocio, entornos o proyectos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Seguimiento de los costos en unidades de negocio, entornos o proyectos
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: ready
ms.openlocfilehash: e026ac8c46fd8c39d2c6ff36c3612fed2bed7e82
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71022163"
---
# <a name="track-costs-across-business-units-environments-or-projects"></a>Seguimiento de los costos en unidades de negocio, entornos o proyectos

Para [crear una organización con control de costos](../../organize/cost-conscious-organization.md), hay que tener visibilidad de los datos relacionados con los costos y contar también con un acceso (o ámbito) definido correctamente. En este artículo de procedimientos recomendados se describen las decisiones y los enfoques de implementación para crear mecanismos de seguimiento.

![Esquema del proceso de control de costos](../../_images/ready/cost-optimization-process.png)

## <a name="establish-a-well-managed-environment-hierarchy"></a>Establecimiento de la jerarquía de un entorno bien administrado

El control de costos, al igual que la gobernanza y otros elementos de administración, depende de que tengamos un entorno bien administrado. El establecimiento de este tipo de entorno (especialmente uno complejo) requiere procesos coherentes en la clasificación y organización de todos los recursos.

Los recursos incluyen todas las máquinas virtuales, los orígenes de datos y las aplicaciones que se implementan en la nube. Azure proporciona varios mecanismos para clasificar y organizar los recursos. En [Escalado con varias suscripciones de Azure](../considerations/scaling-subscriptions.md) se detallan las opciones para organizar los recursos en función de varios criterios para establecer un entorno bien administrado. Este artículo se centra en la aplicación de conceptos fundamentales de Azure para proporcionar visibilidad de costos de la nube.

### <a name="classification"></a>clasificación

El *etiquetado* es una forma sencilla de clasificar los recursos, ya que asocia los metadatos a un recurso. Esos metadatos se pueden usar para clasificar el recurso en función de varios puntos de datos. Cuando se usan etiquetas para clasificar recursos como parte de un trabajo de administración de costos, las empresas suelen necesitar las siguientes etiquetas: unidad de negocio, departamento, código de facturación, zona geográfica, entorno, proyecto y carga de trabajo o "categorización de aplicaciones". Azure Cost Management puede usar estas etiquetas para crear vistas diferentes de los datos de costo.

El etiquetado es la principal forma de comprender los datos en los informes de costos. Se trata de una parte fundamental de cualquier entorno bien administrado. También supone el primer paso para establecer la gobernanza adecuada de cualquier entorno.

El primer paso para realizar un seguimiento preciso de la información de costos entre unidades de negocio, entornos y proyectos es definir un estándar de etiquetado. El segundo paso es asegurarse de que el estándar de etiquetado se aplica de forma coherente. Los siguientes artículos pueden ayudarlo a realizar cada uno de estos pasos:

- [Desarrollo de estándares de nomenclatura y etiquetado](../considerations/naming-and-tagging.md)
- [Establecimiento de un MVP de gobernanza para aplicar los estándares de etiquetado](../../govern/guides/complex/index.md)

### <a name="resource-organization"></a>Organización de recursos

Existen varios métodos para organizar los recursos. En esta sección se describe un procedimiento recomendado en función de las necesidades de una gran empresa con estructuras de costos distribuidas entre unidades de negocio, zonas geográficas y organizaciones de TI. Hay un procedimiento recomendado similar para una organización más pequeña y menos compleja en [Recorrido de gobernanza de pequeñas y medianas empresas](../../govern/guides/standard/index.md).

En el caso de una empresa grande, el siguiente modelo para grupos de administración, suscripciones y grupos de recursos creará una jerarquía que permite a cada equipo tener el nivel adecuado de visibilidad para realizar sus tareas. Cuando la empresa necesita controles de costos para evitar la saturación del presupuesto, puede aplicar herramientas de gobernanza como Azure Blueprints o Azure Policy a las suscripciones de esta estructura para evitar rápidamente futuros errores de costos.

![Diagrama de la organización de recursos de una gran empresa](../../_images/govern/large-enterprise-resource-organization.png)

En el diagrama anterior, la raíz de la jerarquía del grupo de administración contiene un nodo para cada unidad de negocio. En este ejemplo, la compañía multinacional necesita visibilidad de las unidades de negocio regionales, por lo que crea un nodo para la zona geográfica en cada unidad de negocio de la jerarquía.

En cada zona geográfica, hay un nodo independiente para entornos de producción y de otros tipos con el objetivo de aislar los controles de costos, acceso y gobernanza. Para que haya operaciones más eficientes y sensatas, la empresa usa suscripciones para aislar aún más los entornos de producción con distintos grados de compromisos de rendimiento operativo. Finalmente, la empresa usa grupos de recursos para capturar las unidades que se pueden implementar de una función, denominadas "aplicaciones".

En el diagrama se muestran los procedimientos recomendados, pero no se incluyen estas opciones:

- Muchas empresas limitan las operaciones a una única región geopolítica. Este enfoque reduce la necesidad de diversificar las disciplinas de gobernanza o los datos de costos en función de los requisitos de soberanía de datos locales. En esos casos, no se requiere un nodo de zona geográfica.
- Algunas empresas prefieren separar aún más los entornos de desarrollo, pruebas y control de calidad en suscripciones independientes.
- Cuando una empresa integra un equipo de centro de excelencia de la nube (CCoE), las suscripciones de servicios compartidos de cada nodo de zona geográfica pueden reducir los recursos duplicados.
- Las tareas de adopción más reducidas podrían tener una jerarquía de administración mucho más pequeña. Es habitual ver un solo nodo raíz para el grupo de TI corporativo, con un único nivel de nodos subordinados en la jerarquía para varios entornos. Aunque no se trata de una infracción de los procedimientos recomendados para un entorno bien administrado, hace más difícil proporcionar un modelo de acceso con derechos mínimos para el control de costos y otras funciones importantes.

En el resto de este artículo se da por hecho que se utiliza el enfoque de procedimientos recomendados del diagrama anterior. Sin embargo, los siguientes artículos pueden ayudarlo a aplicar el enfoque a una organización de recursos que se adapta mejor a su empresa:

- [Escalado de varias suscripciones de Azure](../considerations/scaling-subscriptions.md)
- [Implementación de un MVP de gobernanza para controlar los estándares de un entorno bien administrado](../../govern/guides/complex/index.md)

## <a name="provide-the-right-level-of-cost-access"></a>Proporcionar el nivel adecuado de acceso a los costos

La administración de costos es una actividad que tiene que realizar el equipo. La sección de preparación de la plataforma de adopción de la nube (CAF) define un número reducido de equipos principales y describe cómo esos equipos asumen los esfuerzos de adopción de la nube. En este artículo se amplían las definiciones de equipo para definir el ámbito y los roles que se asignan a los miembros de cada equipo para tener el nivel de visibilidad adecuado de los datos de administración de costos.

- Los *roles* definen lo que un usuario puede hacer en varios recursos.
- El *ámbito* establece los recursos (usuario, grupo, entidad de servicio o identidad administrada) en los que un usuario puede llevar a cabo operaciones.

Como procedimiento recomendado general, sugerimos un modelo con privilegios mínimos para asignar personas a varios roles y ámbitos.

### <a name="roles"></a>Roles

Azure Cost Management admite los siguientes roles integrados para cada uno de los siguientes ámbitos:

- [Propietario](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner). Puede ver los costos y administrar todo, incluida la configuración de costos.
- [Colaborador](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor). Puede ver los costos y administrar todo, incluida la configuración de costos, pero sin incluir el control de acceso.
- [Lector](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#reader). Puede ver todo, incluidos la configuración y los datos de costos, pero no realizar cambios.
- [Colaborador de Cost Management](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor). Puede ver los costos y administrar la configuración de costos.
- [Lector de Cost Management](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-reader). Puede ver la configuración y los datos de costos.

Como procedimiento recomendado general, a los miembros de todos los equipos se les debe asignar el rol Colaborador de Cost Management, ya que concede a los usuarios acceso para crear y administrar presupuestos y exportaciones con el objetivo de supervisar y notificar de manera más eficaz los costos. Sin embargo, los miembros del [equipo de estrategia de la nube](../../organize/cloud-strategy.md) deben tener solamente el rol Lector de Cost Management. El motivo es que no tienen que establecer presupuestos dentro de la herramienta Azure Cost Management.

### <a name="scope"></a>Ámbito

La siguiente configuración de ámbito y rol creará la visibilidad necesaria de la administración de costos. Este procedimiento recomendado podría requerir realizar cambios menores para que estén en consonancia con las decisiones de la organización de recursos.

- [Equipo de adopción de la nube](../../organize/cloud-adoption.md). Las responsabilidades de los cambios de optimización continua requieren el acceso de Colaborador de Cost Management en el nivel de grupo de recursos.

  - **Entorno de trabajo**. Como mínimo, el equipo de adopción de la nube ya debe tener acceso de [Colaborador](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) a todos los grupos de recursos afectados o, al menos, a los grupos relacionados con las actividades de implementación en curso o de desarrollo/pruebas. No se requiere ninguna configuración de ámbito adicional.
  - **Entornos de producción**. Cuando se establece una separación adecuada de la responsabilidad, es probable que el equipo de adopción de la nube no siga teniendo acceso a los grupos de recursos relacionados con sus proyectos. Los grupos de recursos que admiten las instancias de producción de sus cargas de trabajo necesitarán un ámbito adicional para dar a este equipo visibilidad del impacto de sus decisiones en el costo de producción. Al establecer el ámbito [Colaborador de Cost Management](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) para los grupos de recursos de producción de este equipo, el equipo podrá supervisar los costos y definir presupuestos en función del uso y la inversión continua en las cargas de trabajo admitidas.

- [Equipo de estrategia de la nube](../../organize/cloud-strategy.md). La responsabilidad de realizar un seguimiento de los costos en varios proyectos y unidades de negocio requiere el acceso de Lector de Cost Management en el nivel raíz de la jerarquía de grupos de administración.

  - Asigne [Lector de Cost Management](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-reader) a este equipo en el grupo de administración. Esto garantizará una visibilidad continua de todas las implementaciones asociadas a las suscripciones controladas por esa jerarquía de grupos de administración.

- [Equipo de gobernanza de la nube](../../organize/cloud-governance.md). La responsabilidad de administrar el costo, la alineación del presupuesto y los informes en todos los esfuerzos de adopción requiere el acceso de Colaborador de Cost Management en el nivel de raíz de la jerarquía de grupos de administración.

  - En un entorno bien administrado, el equipo de gobernanza de la nube probablemente tiene un mayor grado de acceso, por lo que la asignación del ámbito adicional de [Colaborador de Cost Management](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) resulta innecesaria.

- [Centro de excelencia de la nube](../../organize/cloud-center-of-excellence.md). La responsabilidad de administrar los costos relacionados con los servicios compartidos requiere acceso de Colaborador de Cost Management en el nivel de suscripción. Además, es posible que este equipo necesite el acceso de Colaborador de Cost Management a grupos de recursos o suscripciones que contengan recursos implementados mediante automatizaciones de CCoE para entender cómo afectan a los costos.

  - **Servicios compartidos**. Cuando se activa un centro de excelencia en la nube, los procedimientos recomendados sugieren que los recursos administrados mediante CCoE se admitan desde una suscripción de servicios compartidos centralizada dentro de un modelo de concentrador/radio. En este escenario, es probable que el CCoE tenga acceso de colaborador o propietario a esa suscripción, por lo que la asignación del ámbito adicional de [Colaborador de Cost Management](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) resulta innecesaria.
  - **Controles/automatización del CCoE**. Normalmente, el CCoE proporciona controles y scripts de implementación automatizados a los equipos de adopción de la nube. El CCoE tiene la responsabilidad de comprender cómo afectan estos aceleradores a los costos. Para obtener esa visibilidad, el equipo necesita acceso de [Colaborador de Cost Management](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) a cualquier grupo de recursos o suscripción que ejecute dichos aceleradores.

- **Equipo de operaciones en la nube**. La responsabilidad de administrar los costos continuos de los entornos de producción requiere el acceso de Colaborador de Cost Management a todas las suscripciones de producción.

  - La recomendación general coloca los recursos de producción y de otros tipos en suscripciones independientes que se rigen por nodos de la jerarquía de grupos de administración asociados con entornos de producción. En un entorno bien administrado, los miembros del equipo de operaciones probablemente ya tienen acceso de propietario o colaborador a las suscripciones de producción, por lo que el rol [Colaborador de Cost Management](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#cost-management-contributor) resulta innecesario.

## <a name="additional-cost-management-resources"></a>Recursos adicionales de administración de costos

Azure Cost Management es una herramienta bien documentada para establecer presupuestos y obtener visibilidad de los costos de la nube de Azure o AWS. Después de establecer el acceso a la jerarquía de un entorno bien administrado, los siguientes artículos pueden ayudarlo a usar esa herramienta para supervisar y controlar los costos.

### <a name="get-started-with-azure-cost-management"></a>Introducción a Azure Cost Management

Para obtener más información sobre cómo empezar a usar Azure Cost Management, consulte [Optimización de la inversión en la nube con Azure Cost Management](https://docs.microsoft.com/azure/cost-management/cost-mgt-best-practices?toc=https://docs.microsoft.com/azure/cloud-adoption-framework/toc.json&bc=https://docs.microsoft.com/azure/cloud-adoption-framework/bread/toc.json).

### <a name="use-azure-cost-management"></a>Uso de Azure Cost Management

- [Creación y administración de presupuestos](https://docs.microsoft.com/azure/cost-management/tutorial-acm-create-budgets)
- [Exportación de datos de costos](https://docs.microsoft.com/azure/cost-management/tutorial-export-acm-data)
- [Optimización de los costos a partir de recomendaciones](https://docs.microsoft.com/azure/cost-management/tutorial-acm-opt-recommendations)
- [Uso de alertas de costos para supervisar el uso y los gastos](https://docs.microsoft.com/azure/cost-management/cost-mgt-alerts-monitor-usage-spending)

### <a name="use-azure-cost-management-to-govern-aws-costs"></a>Uso de Azure Cost Management para controlar los costos de AWS

- [Integración de informes de uso y costos de AWS](https://docs.microsoft.com/azure/cost-management/aws-integration-set-up-configure)
- [Administración de los costos de AWS](https://docs.microsoft.com/azure/cost-management/aws-integration-manage)

### <a name="establish-access-roles-and-scope"></a>Establecimiento de acceso, roles y ámbito

- [Información del ámbito de administración de costos](https://docs.microsoft.com/azure/cost-management/understand-work-scopes)
- [Establecimiento del ámbito de un grupo de recursos](https://docs.microsoft.com/azure/role-based-access-control/quickstart-assign-role-user-portal)
