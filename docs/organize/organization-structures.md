---
title: Establecimiento de estructuras de equipo
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Establecimiento de estructuras de equipo
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/27/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 8000847a46082be6116abb22e52def03243c69b0
ms.sourcegitcommit: 1dccf1aed8e98aa0f58c4f86d90c65f5fa5ac84d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2019
ms.locfileid: "71811085"
---
# <a name="establish-team-structures"></a>Establecimiento de estructuras de equipo

En cada esfuerzo de adopción de la nube, hay alguien encargado de proporcionar las funcionalidades de la nube. Estas asignaciones y estructuras de equipo se pueden desarrollar de forma orgánica o diseñarse de manera intencionada para ajustarse a una estructura de equipo definida.

A medida que aumentan las necesidades de adopción, lo mismo ocurre con la necesidad de equilibrio y estructura. En este artículo se proporcionan ejemplos de estructuras de equipo comunes en varias fases de madurez de la organización. En el gráfico y la lista siguientes se indican esas estructuras en función de fases de madurez típicas. Use estos ejemplos para encontrar la estructura organizativa que mejor se ajuste a sus necesidades operativas.

![Ciclo de madurez de la organización](../_images/ready/org-ready-maturity.png)

Las estructuras organizativas tienden a avanzar según el modelo de madurez común descrito aquí:

1. [Equipo de adopción de la nube solo](#cloud-adoption-team-only)
2. [Procedimiento recomendado de producto viable mínimo](#best-practice-minimum-viable-product-mvp)
3. [TI central](#central-it)
4. [Alineación estratégica](#strategic-alignment)
5. [Alineación operativa](#operational-alignment)
6. [Centro de excelencia de la nube (CCoE)](#cloud-center-of-excellence)

La mayoría de las empresas comienzan con poco más que un *equipo de adopción de la nube*, aunque se recomienda establecer una estructura organizativa que se parezca más a la estructura del [procedimiento recomendado de MVP](#best-practice-minimum-viable-product-mvp).

## <a name="cloud-adoption-team-only"></a>Equipo de adopción de la nube solo

El núcleo de todos los esfuerzos de adopción de la nube es el equipo de adopción de la nube. Este equipo impulsa los cambios técnicos que permiten la adopción. En función de los objetivos del esfuerzo de adopción, este equipo puede estar compuesto por una gama diversa de miembros que se ocupan de un amplio conjunto de tareas técnicas y comerciales.

![Equipo de adopción de la nube, con equipos de gobernanza y seguridad](../_images/ready/org-ready-adoption-only.png)

En los esfuerzos de adopción de pequeña escala o de fase temprana, este equipo podría constar incluso de una sola persona. En esfuerzos de mayor escala o de fase avanzada, es habitual tener varios equipos de adopción de la nube, cada uno con aproximadamente seis ingenieros. Independientemente del tamaño o las tareas, el aspecto común de cualquier equipo de adopción de la nube es que proporciona los medios para incorporar soluciones a la nube. En algunas organizaciones, esta puede ser una estructura organizativa suficiente. El artículo [Funcionalidades de adopción en la nube](./cloud-adoption.md) proporciona más información sobre la estructura, la composición y la función del equipo de adopción de la nube.

> [!WARNING]
> Trabajar *solo* con un equipo de adopción de la nube (o varios equipos de adopción de la nube) se considera un *antipatrón* y debe evitarse. Como mínimo, considere el [procedimiento recomendado de MVP](#best-practice-minimum-viable-product-mvp).

## <a name="best-practice-minimum-viable-product-mvp"></a>Procedimiento recomendado: producto viable mínimo (MVP)

Se recomienda contar con dos equipos para crear equilibrio entre los esfuerzos de adopción de la nube. Estos dos equipos son responsables de diversas funcionalidades a lo largo del esfuerzo de adopción.

- **Equipo de adopción de la nube:** responsable de las soluciones técnicas, la alineación del negocio, la administración de proyectos y el funcionamiento de las soluciones adoptadas.
- **Equipo de gobernanza de la nube:** para equilibrar el equipo de adopción de la nube, un equipo de gobernanza de la nube se dedica a garantizar la excelencia en las soluciones adoptadas. El equipo de gobernanza de la nube es responsable de la madurez de la plataforma, las operaciones de esta, la gobernanza y la automatización.

![Adopción de la nube con contrapartida de gobernanza de la nube](../_images/ready/org-ready-best-practice.png)

Este enfoque probado se considera un MVP porque puede no ser sostenible. Cada equipo se ocupa de muchas tareas, como se explica en los [gráficos RACI (*comprometido, responsable, consultado e informado*)](./raci-alignment.md).

En las secciones siguientes se describe una estructura organizativa probada y dotada del personal necesario junto con enfoques para alinear la estructura adecuada con la organización.

## <a name="central-it"></a>TI central

A medida que la adopción avanza, el equipo de gobernanza de la nube puede tener problemas para seguir el ritmo del flujo de innovación de los distintos equipos de adopción de la nube. Esto es especialmente cierto en entornos con requisitos intensivos de cumplimiento, operaciones o seguridad. En esta fase, es habitual que las empresas pasen las responsabilidades de la nube a un equipo de TI central existente. Si ese equipo puede volver a evaluar las herramientas, los procesos y las personas para facilitar una mejor adopción de la nube a escala, la incorporación del equipo de TI central puede agregar un valor considerable. La incorporación de expertos en la materia de operaciones, automatización, seguridad y administración para modernizar la TI central puede dar lugar a innovaciones operativas eficaces.

![Adopción de la nube con un modelo de TI central](../_images/ready/org-ready-central-it.png)

Desafortunadamente, la fase de TI central puede ser una de las fases con más riesgo de madurez de la organización. El equipo de TI central debe sentarse a la mesa con una profunda mentalidad de crecimiento. Si el equipo ve la nube como una oportunidad de crecer y adaptar sus funcionalidades, puede proporcionar un magnífico valor a lo largo del proceso. Pero si el equipo de TI central considera la adopción de la nube fundamentalmente como una amenaza para su modelo existente, se convierte en un obstáculo para los equipos de adopción de la nube y los objetivos empresariales que apoyan. Algunos equipos de TI central han dedicado meses o incluso años a intentar forzar la alineación de la nube con los enfoques locales, con resultados negativos únicamente. La nube no exige que todo cambie en la TI central, pero requiere cambios. Si la resistencia a los cambios es generalizada en el equipo de TI central, esta fase de madurez puede convertirse rápidamente en un antipatrón cultural.

Los planes de adopción de la nube muy centrados en soluciones de plataforma como servicio (PaaS), DevOps u otras que requieren menos soporte de operaciones es menos probable que noten valor durante esta fase de madurez. Por el contrario, estos tipos de soluciones son los más susceptibles de resultar entorpecidos o bloqueados por intentos de centralizar la TI. Es más probable que un nivel superior de madurez, como un [centro de excelencia de la nube (CCoE)](#cloud-center-of-excellence), genere resultados positivos para esos tipos de esfuerzos de transformación. Para comprender las diferencias entre la TI central en la nube y un CCoE, vea [Centro de excelencia en la nube](./cloud-center-of-excellence.md).

## <a name="strategic-alignment"></a>Alineación estratégica

A medida que crece la inversión en la adopción de la nube y se obtienen valores empresariales, las partes interesadas del negocio suelen implicarse más. Un equipo de estrategia de la nube definido, como se muestra en la siguiente imagen, alinea esas partes interesadas del negocio a fin de maximizar el valor obtenido por las inversiones en la adopción de la nube.

![Incorporación de un equipo de estrategia de la nube definido](../_images/ready/org-ready-strategy-aligned.png)

Si la madurez se produce de manera orgánica, como resultado de esfuerzos de adopción de la nube dirigidos por TI, la alineación estratégica suele ir precedida por un equipo de gobernanza o de TI central. Si los esfuerzos de adopción de la nube son dirigidos por el negocio, el enfoque en el modelo operativo y la organización tiende a producirse con anterioridad. Siempre que sea posible, se deben definir los resultados empresariales y el equipo de estrategia de la nube en una fase temprana del proceso.

## <a name="operational-alignment"></a>Alineación operativa

La obtención de valor empresarial a partir de los esfuerzos de adopción de la nube requiere operaciones estables. Las operaciones en la nube pueden requerir nuevas herramientas, procesos o aptitudes. Si se requieren operaciones de TI estables para lograr resultados empresariales, es importante agregar un equipo de operaciones en la nube definido, como se muestra aquí.

![Incorporación de un equipo de operaciones en la nube](../_images/ready/org-ready-operations-aligned.png)

Los roles de operaciones de TI existentes pueden realizar las operaciones en la nube. Pero no es raro que las operaciones en la nube se deleguen en otras partes ajenas a las operaciones de TI. Los proveedores de servicios administrados, los equipos de DevOps y la TI de unidad de negocio suelen asumir las responsabilidades asociadas con las operaciones en la nube, con soporte y protección de las operaciones de TI. Esto es cada vez más común en los esfuerzos de adopción de la nube muy centrados en implementaciones de DevOps o PaaS.

## <a name="cloud-center-of-excellence"></a>Centro de excelencia de la nube

En el estado superior de madurez, un centro de excelencia en la nube alinea los equipos en torno a un modelo operativo moderno primero en la nube. Este enfoque proporciona funciones de TI central como gobernanza, seguridad, plataforma y automatización.

![Centro de excelencia de la nube](../_images/ready/org-ready-ccoe.png)

La principal diferencia entre esta estructura y la estructura de TI central anterior es que se centra en el autoservicio. Los equipos de esta estructura se organizan con la intención de delegar el control tanto como sea posible. La alineación de los procedimientos de gobernanza y cumplimiento con las soluciones nativas de la nube crea mecanismos de salvaguarda y protección. A diferencia del modelo de TI central, el enfoque nativo en la nube maximiza la innovación y minimiza la sobrecarga operativa. Para que se adopte este modelo, se necesita acuerdo mutuo entre la dirección de negocio y TI para modernizar los procesos de TI. No es probable que este modelo se desarrolle de forma orgánica y suele requerir soporte ejecutivo.

## <a name="next-steps"></a>Pasos siguientes

Después de alinear con una determinada fase de madurez de la estructura organizativa, puede usar [gráficos RACI](./raci-alignment.md) para alinear la responsabilidad y el compromiso en cada equipo.

> [!div class="nextstepaction"]
> [Alineación de la matriz RACI](./raci-alignment.md)
