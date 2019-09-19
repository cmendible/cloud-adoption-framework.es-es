---
title: 'Guía para empresa estándar: Mejora de la materia de administración de costos'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Guía para empresa estándar: Mejora de la materia de administración de costos'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 5cbf9a6cdb3776e763fc27492ad499679b4d1327
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032410"
---
# <a name="standard-enterprise-guide-improve-the-cost-management-discipline"></a>Guía para empresa estándar: Mejora de la materia de administración de costos

En este artículo se detalla la incorporación de controles de costos al producto viable mínimo de gobernanza.

## <a name="advancing-the-narrative"></a>Continuación de la historia

La adopción ha aumentado superando el indicador de tolerancia de costos que se definió en el producto mínimo viable de gobernanza. Esto es algo bueno, ya que se corresponde con las migraciones desde el centro de datos de "Recuperación ante desastres". Los aumentos en el gasto ahora justifican una inversión de tiempo por parte del equipo de gobernanza de la nube.

### <a name="changes-in-the-current-state"></a>Cambios en el estado actual

En una fase anterior de esta narración, TI había retirado el 100 % del centro de datos de recuperación ante desastres. Los equipos de desarrollo de aplicaciones y de inteligencia empresarial estaban preparados para el tráfico de producción.

Desde entonces, han cambiado algunas cosas que afectarán a la gobernanza:

- El equipo de migración ha empezado a migrar las máquinas virtuales fuera del centro de datos de producción.
- Los equipos de desarrollo de aplicaciones están insertando activamente aplicaciones de producción en la nube a través de canalizaciones de CI/CD. Esas aplicaciones se pueden escalar de forma reactiva según las demandas de los usuarios.
- El equipo de inteligencia empresarial del departamento de TI ha entregado varias herramientas de análisis predictivo en la nube. Los volúmenes de datos agregados en la nube siguen creciendo.
- Todo este crecimiento es compatible con los resultados empresariales comprometidos. Sin embargo, los costos han comenzado a multiplicarse. Los presupuestos proyectados están creciendo más rápido de lo esperado. El departamento de dirección financiera necesita enfoques mejorados para administrar los costos.

### <a name="incrementally-improve-the-future-state"></a>Mejora gradual del estado futuro

La supervisión de costos y los informes se agregarán a la solución en la nube. TI aún actúa como un centro de compensación de costos. Esto significa que los pagos para los servicios en la nube proceden aún de la contratación de TI. Sin embargo, los informes deben vincular los gastos operativos directos a las funciones que consumen los costos de la nube. A este modelo se le conoce como modelo de "simulación de la repercusión de los costos" en relación con la contabilidad de la nube.

Los cambios de los estados actual y futuro exponen nuevos riesgos que requerirán nuevas declaraciones de directiva.

## <a name="changes-in-tangible-risks"></a>Cambios en riesgos tangibles

**Control del presupuesto:** Existe un riesgo inherente de que las capacidades de autoservicio generen costos excesivos e inesperados en la nueva plataforma. Los procesos de gobernanza para la supervisión de los costos y la mitigación de los riesgos de costos continuos deben estar implementados para asegurar la alineación continua con el presupuesto planeado.

Este riesgo empresarial puede ampliarse a algunos riesgos técnicos:

- Los costos reales podrían superar los planeados.
- Las condiciones empresariales cambian. Cuando lo hacen, habrá casos en que una función empresarial necesite consumir más servicios en la nube de lo esperado, provocando anomalías en el gasto. Existe el riesgo de que estos gastos adicionales se consideren como un uso por encima del límite, en lugar de considerar la posibilidad de realizar un ajuste en el plan.
- Los sistemas se podrían sobreaprovisionar, lo que daría lugar a un exceso en los gastos.

## <a name="incremental-improvement-of-the-policy-statements"></a>Mejora gradual de las declaraciones de las directivas

Los siguientes cambios en la directiva le ayudarán a corregir los nuevos riesgos y le guiarán en la implementación.

- El equipo de gobernanza debe supervisar semanalmente todos los costos de la nube comparándolos con los que están en el plan. Los informes sobre las desviaciones entre los costos en la nube y los del plan deben compartirse con la dirección financiera y de TI mensualmente. Todos los costos de la nube y las actualizaciones del plan se deben revisar mensualmente con los departamentos de finanzas y de TI.
- Todos los costos deben asignarse a una función empresarial con fines de rendición de cuentas.
- Se deben supervisar continuamente los recursos en la nube para detectar las oportunidades de optimización.
- Las herramientas de gobernanza de la nube deben limitar las opciones de tamaño de los recursos a una lista de configuraciones aprobadas. Las herramientas deben asegurarse de que todos los recursos sean detectables y estén controlados por la solución de supervisión de costos.
- Durante la planeación de la implementación, se deben documentar todos los recursos en la nube necesarios asociados con el hospedaje de las cargas de trabajo de producción. Esta documentación ayudará a ajustar los presupuestos y preparar las automatizaciones adicionales para impedir el uso de opciones más costosas. Durante este proceso, debe prestarse atención a las diferentes herramientas de descuento que ofrece el proveedor de servicios en la nube, como instancias reservadas o reducciones en los costos de la licencia.
- Todos los propietarios de aplicaciones deben asistir a prácticas de aprendizaje para optimizar las cargas de trabajo a fin de controlar mejor los costos de la nube.

## <a name="incremental-improvement-of-the-best-practices"></a>Mejoras graduales de los procedimientos recomendados

En esta sección del artículo se cambiará el diseño del producto viable mínimo de gobernanza para incluir nuevas directivas de Azure y una implementación de Azure Cost Management. Juntos, estos dos cambios de diseño cumplirán con las nuevas declaraciones de directiva corporativa.

1. Implemente Azure Cost Management.
    1. Establezca el ámbito adecuado de acceso para alinearlo con el patrón de suscripciones y la materia sobre la coherencia de los recursos. Asumiendo la alineación con el producto viable mínimo de gobernanza definido en artículos anteriores, esto requiere acceso al **ámbito de la cuenta de inscripción** para que el equipo de gobernanza de la nube ejecute el informe detallado. Los equipos adicionales fuera de la gobernanza pueden requerir acceso al **ámbito del grupo de recursos**.
    1. Establezca un presupuesto en Azure Cost Management.
    1. Revise las recomendaciones iniciales y actúe sobre ellas. Disponga un proceso periódico que admita informes.
    1. Configure y ejecute los informes de Azure Cost Management, al inicio y de manera periódica.
2. Actualización de Azure Policy
    1. Audite los valores de etiquetado, grupo de administración, suscripción y grupo de recursos para identificar cualquier desviación.
    1. Establezca las opciones de tamaño de SKU para limitar las implementaciones a las SKU que aparecen en la documentación de la planeación de implementación.

## <a name="conclusion"></a>Conclusión

La adición de estos procesos y los cambios realizados en el producto viable mínimo de gobernanza ayudan a corregir muchos de los riesgos asociados con la gobernanza de los costos. Juntos, crean la visibilidad, la responsabilidad y la optimización necesarias para controlar los costos.

## <a name="next-steps"></a>Pasos siguientes

A medida que avanza la adopción de la nube y aporta valores empresariales adicionales, también cambian los riesgos y necesidades de gobernanza de la nube. Para la empresa ficticia de esta guía, el siguiente paso es usar esta inversión de gobernanza para administrar varias nubes.

> [!div class="nextstepaction"]
> [Evolución en varias nubes](./multicloud-improvement.md)
