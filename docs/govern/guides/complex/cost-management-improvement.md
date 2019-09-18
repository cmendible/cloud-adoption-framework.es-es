---
title: 'Guía de gobernanza para empresas complejas: Mejora de la materia de administración de costos'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Guía de gobernanza para empresas complejas: Mejora de la materia de administración de costos'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: f8b78ab958f732920d7282ade80e9da421e5b0e5
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031217"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-cost-management-discipline"></a>Guía de gobernanza para empresas complejas: Mejora de la materia de administración de costos

En este artículo, la narración avanza agregando controles de costos a los mecanismos de gobernanza del producto viable mínimo.

## <a name="advancing-the-narrative"></a>Continuación de la historia

La adopción ha crecido superando el indicador de tolerancia definido en el MVP para la gobernanza. Los aumentos en el gasto ahora justifican una inversión de tiempo por parte del equipo de gobernanza de la nube para supervisar y controlar los patrones de gasto.

En tanto que impulsor claro de la innovación, el departamento de TI ya no se percibe principalmente como un centro de coste. A medida que la organización de TI genera más valor, el director de sistemas de información y el director financiero acuerdan que es el momento de cambiar el papel que desempeña el equipo de TI en la empresa. Entre otros cambios, el director financiero desea probar un enfoque de pago directo para la contabilidad en la nube para la sucursal canadiense de una de las unidades empresariales. Uno de los dos centros de datos retirados eran recursos hospedados exclusivamente para las operaciones en Canadá de esa unidad empresarial. En este modelo, se facturará directamente a la filial canadiense de la unidad empresarial por los gastos operativos relacionados con los recursos hospedados. Este modelo permite que el equipo de TI se centre menos en la administración del gasto de los demás y más en la creación de valor. Sin embargo, para que pueda comenzar esta transición, es necesario que las herramientas de administración de costos estén en vigor.

### <a name="changes-in-the-current-state"></a>Cambios en el estado actual

En la fase anterior de esta narración, el equipo de TI movía activamente las cargas de trabajo de producción con datos protegidos a Azure.

Desde entonces, han cambiado algunas cosas que afectarán a la gobernanza:

- Se quitaron 5000 recursos de los dos centros de datos marcados para la retirada. Los departamentos de adquisiciones y de seguridad de TI ahora están desaprovisionando los recursos físicos restantes.
- Los equipos de desarrollo de aplicaciones han implementado canalizaciones de CI/CD para implementar algunas aplicaciones nativas en la nube, lo cual afecta significativamente a la experiencia del cliente.
- El equipo de inteligencia empresarial ha creado procesos de agregación, protección, conocimiento y predicción que generan beneficios tangibles para las operaciones comerciales. Estas predicciones están dando ahora lugar a nuevos productos y servicios creativos.

### <a name="incrementally-improve-the-future-state"></a>Mejora gradual del estado futuro

La supervisión de costos y los informes se deben agregar a la solución en la nube. Los informes deben vincular los gastos operativos directos a las funciones que consumen los costos de la nube. Los informes adicionales deben permitir que el departamento de TI supervise los gastos y proporcione orientación técnica sobre la administración de costos. En el caso de la sucursal canadiense, se facturará directamente al departamento.

## <a name="changes-in-risk"></a>Cambios en los riesgos

**Control del presupuesto:** Existe un riesgo inherente de que las capacidades de autoservicio generen costos excesivos e inesperados en la nueva plataforma. Los procesos de gobernanza para la supervisión de los costos y la mitigación de los riesgos de costos continuos deben estar implementados para asegurar la alineación continua con el presupuesto planeado.

Este riesgo empresarial puede ampliarse a algunos riesgos técnicos:

- Existe el riesgo de que los costos reales superen el plan.
- Las condiciones empresariales cambian. Cuando lo hacen, habrá casos en que una función empresarial necesite consumir más servicios en la nube de lo esperado, provocando anomalías en el gasto. Existe el riesgo de que estos costos adicionales se consideren excesivos en lugar de un ajuste necesario para el plan. Si se realiza correctamente, el experimento canadiense debe ayudar a corregir este riesgo.
- Existe el riesgo de que se sobreaprovisionen los sistemas, lo que daría lugar a un exceso en los gastos.

## <a name="changes-to-the-policy-statements"></a>Cambios en las declaraciones de directiva

Los siguientes cambios en la directiva le ayudarán a corregir los nuevos riesgos y le guiarán en la implementación.

- El equipo de gobernanza de la nube debe supervisar todos los costos de la nube en comparación con el plan de forma semanal. Los informes sobre las desviaciones entre los costos en la nube y los del plan deben compartirse con la dirección financiera y de TI mensualmente. Todos los costos de la nube y las actualizaciones del plan se deben revisar mensualmente con los departamentos de finanzas y de TI.
- Todos los costos deben asignarse a una función empresarial con fines de rendición de cuentas.
- Se deben supervisar continuamente los recursos en la nube para detectar las oportunidades de optimización.
- Las herramientas de gobernanza de la nube deben limitar las opciones de tamaño de los recursos a una lista de configuraciones aprobadas. Las herramientas deben asegurarse de que todos los recursos sean detectables y estén controlados por la solución de supervisión de costos.
- Durante la planeación de la implementación, se deben documentar todos los recursos en la nube necesarios asociados con el hospedaje de las cargas de trabajo de producción. Esta documentación ayudará a ajustar los presupuestos y preparar las herramientas de automatización adicionales para impedir el uso de opciones más costosas. Durante este proceso, debe prestarse atención a las diferentes herramientas de descuento que ofrece el proveedor de servicios en la nube, como instancias reservadas o reducciones en los costos de la licencia.
- Todos los propietarios de aplicaciones deben asistir a prácticas de aprendizaje para optimizar las cargas de trabajo a fin de controlar mejor los costos de la nube.

## <a name="incremental-improvement-of-the-best-practices"></a>Mejoras graduales de los procedimientos recomendados

En esta sección del artículo se mejorará el diseño de un producto viable mínimo de gobernanza para que incluya nuevas directivas de Azure y una implementación de Azure Cost Management. Juntos, estos dos cambios de diseño cumplirán con las nuevas declaraciones de directiva corporativa.

1. Cambie Azure Enterprise Portal para facturar al administrador del departamento para la implementación canadiense.
1. Implemente Azure Cost Management.
    1. Establezca el nivel adecuado de ámbito de acceso para alinearlo con el patrón de suscripción y el patrón de agrupación de recursos. Asumiendo la alineación con el producto viable mínimo de gobernanza definido en artículos anteriores, esto requeriría acceso al **ámbito de la cuenta de inscripción** para que el equipo de gobernanza de la nube ejecute el informe detallado. Los equipos adicionales fuera de la gobernanza, como el equipo de adquisiciones canadiense, requerirá acceso al **ámbito del grupo de recursos**.
    1. Establezca un presupuesto en Azure Cost Management.
    1. Revise las recomendaciones iniciales y actúe sobre ellas. Se recomienda establecer un proceso periódico compatible con el proceso de generación de informes.
    1. Configure y ejecute los informes de Azure Cost Management, al inicio y de manera periódica.
1. Actualice Azure Policy.
    1. Audite los valores de etiquetado, grupo de administración, suscripción y grupo de recursos para identificar cualquier desviación.
    1. Establezca las opciones de tamaño de SKU para limitar las implementaciones a las SKU que aparecen en la documentación de la planeación de implementación.

## <a name="conclusion"></a>Conclusión

La adición de los procesos anteriores y los cambios realizados en el producto viable mínimo de gobernanza ayudan a corregir muchos de los riesgos asociados con la administración de los costos. Juntos, crean la visibilidad, la responsabilidad y la optimización necesarias para controlar los costos.

## <a name="next-steps"></a>Pasos siguientes

A medida que avanza la adopción de la nube y aporta valores empresariales adicionales, también cambian los riesgos y necesidades de gobernanza de la nube. Para esta empresa ficticia, el siguiente paso es usar esta inversión en gobernanza para administrar varias nubes.

> [!div class="nextstepaction"]
> [Mejora de la nube múltiple](./multicloud-improvement.md)
