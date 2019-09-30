---
title: 'Guía de gobernanza para empresas complejas: Mejora de la materia de coherencia de los recursos'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Guía de gobernanza para empresas complejas: Mejora de la materia de coherencia de los recursos'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/19/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 9875fb2ebc6948d22ac6eaf350f9784b61fd4dc3
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223811"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-resource-consistency-discipline"></a>Guía de gobernanza para empresas complejas: Mejora de la materia de coherencia de los recursos

En este artículo, la narración avanza añadiendo controles de coherencia de los recursos al producto viable mínimo de gobernanza para dar servicio a aplicaciones críticas.

## <a name="advancing-the-narrative"></a>Continuación de la historia

Los equipos de la adopción de la nube han cumplido todos los requisitos para mover los datos protegidos. Esas aplicaciones incluyen los compromisos del Acuerdo de Nivel de Servicio en relación con el negocio y la necesidad de soporte para operaciones de TI. Justo detrás del equipo de migración de los dos centros de datos, varios equipos de inteligencia empresarial y desarrollo de aplicaciones están listos para poner en marcha nuevas soluciones en producción. El equipo de operaciones de TI no está familiarizado con las operaciones en la nube y necesita integrar rápidamente los procesos operativos existentes.

### <a name="changes-in-the-current-state"></a>Cambios en el estado actual

- El departamento de TI está moviendo activamente las cargas de trabajo de producción con datos protegidos a Azure. Varias cargas de trabajo de prioridad baja atienden el tráfico de producción. Se podrán suprimir más tan pronto como el equipo de operaciones de TI autorice la preparación para dar servicio a las cargas de trabajo.
- Los equipos de desarrollo de aplicaciones están preparados para el tráfico de producción.
- El equipo de inteligencia empresarial está listo para integrar las predicciones y perspectivas en los sistemas que ejecutan operaciones para las tres unidades de negocio.

### <a name="incrementally-improve-the-future-state"></a>Mejora gradual del estado futuro

- El equipo de operaciones de TI no está familiarizado con las operaciones en la nube y necesita integrar rápidamente los procesos operativos existentes.
- Los cambios de los estados actual y futuro exponen nuevos riesgos que requerirán nuevas declaraciones de directiva.

## <a name="changes-in-tangible-risks"></a>Cambios en riesgos tangibles

**Interrupción del negocio:** existe un riesgo inherente de que cualquier nueva plataforma cause interrupciones en los procesos de negocio críticos. El equipo de operaciones de TI y los equipos que ejecutan tareas en diversas adopciones de la nube tienen relativamente poca experiencia con las operaciones de la nube. Como esto aumenta el riesgo de interrupción, hay que tomar medidas al respecto para solucionarlo y gobernarlo.

Este riesgo empresarial puede ampliarse a algunos riesgos técnicos:

1. Los procesos operativos mal alineados podrían provocar interrupciones que no se detectan ni mitigan rápidamente.
2. Intrusiones externas o ataques por denegación de servicio podrían provocar una interrupción del negocio.
3. Los recursos críticos podrían no detectarse adecuadamente y, por lo tanto, podrían pasarse por alto.
4. Los recursos desconocidos o mal etiquetados podrían no ser compatibles con los procesos de administración operativa existentes.
5. La configuración de los recursos implementados podría no satisfacer las expectativas de rendimiento.
6. Es posible que el registro no se haya anotado y centralizado correctamente para permitir la solución de problemas de rendimiento.
7. Las directivas de recuperación podrían dar error o tardar más de lo esperado.
8. Unos procesos de implementación incoherentes podrían dar lugar a brechas de seguridad y estas, a su vez, a pérdidas de datos o interrupciones.
9. El desfase de configuración o la falta de revisiones podrían dar lugar a brechas de seguridad y estas, a su vez, a pérdidas de datos o interrupciones.
10. La configuración podría no aplicar los requisitos del Acuerdo de Nivel de Servicio definidos o los requisitos de recuperación confirmados.
11. Los sistemas operativos o aplicaciones implementados podrían no cumplir con los requisitos de protección de la aplicación y el sistema operativo.
12. Existe un riesgo de incoherencia porque hay varios equipos que trabajan en la nube.

## <a name="incremental-improvement-of-the-policy-statements"></a>Mejora gradual de las declaraciones de las directivas

Los siguientes cambios en la directiva le ayudarán a corregir los nuevos riesgos y le guiarán en la implementación. La lista es larga, pero la adopción de estas directivas podría ser más fácil de lo que parece.

1. Todos los recursos implementados deben categorizarse por importancia y clasificación de datos. El equipo de gobernanza de la nube y el propietario de la aplicación deben revisar las clasificaciones antes de la implementación en la nube.
2. Las subredes que contienen aplicaciones críticas deben estar protegidas por una solución de firewall capaz de detectar intrusiones y responder a los ataques.
3. las herramientas de gobernanza deben auditar y aplicar los requisitos de configuración de red definidos por el equipo de la base de referencia de la seguridad.
4. Las herramientas de gobernanza deben validar que todos los recursos relacionados con aplicaciones críticas o datos protegidos se incluyen en la supervisión de la disminución y optimización de recursos.
5. Las herramientas de gobernanza deben validar que se recopila el nivel adecuado de datos de registro para todas las aplicaciones críticas o datos protegidos.
6. El proceso de gobernanza debe validar que la copia de seguridad, la recuperación y el cumplimiento de los Acuerdos de Nivel de Servicios se implementen correctamente para aplicaciones críticas y datos protegidos.
7. Las herramientas de gobernanza deben limitar la implementación de máquina virtual a solo las imágenes aprobadas.
8. Las herramientas de gobernanza deben hacer cumplir que las actualizaciones automáticas se **impidan** en todos los recursos implementados que admitan aplicaciones críticas. Las infracciones deben revisarse con los equipos de administración de operaciones y corregirse de acuerdo con las directivas de operaciones. Los recursos que no se actualicen automáticamente deben incluirse en procesos que sean propiedad del departamento de operaciones de TI para actualizar de forma rápida y eficaz esos servidores.
9. Las herramientas de gobernanza deben validar el etiquetado relacionado con el costo, la importancia, el Acuerdo de Nivel de Servicio, la aplicación y la clasificación de los datos. Todos los valores deben alinearse con los valores predefinidos que administra el equipo de gobernanza de la nube.
10. Los procesos de gobernanza deben incluir auditorías en el punto de implementación y en ciclos regulares para garantizar la coherencia entre todos los recursos.
11. El equipo de seguridad debe revisar periódicamente las tendencias y vulnerabilidades que podrían afectar a las implementaciones en la nube para proporcionar actualizaciones a las herramientas de línea de base de seguridad que se usan en la nube.
12. Antes de su publicación en producción, todas las aplicaciones críticas y los datos protegidos deben agregarse a la solución de supervisión operativa designada. Los recursos que no pueden detectarse por las herramientas de operaciones de TI elegidas no pueden liberarse para su uso en producción. Cualquier cambio requerido para hacer que los recursos sean detectables debe aplicarse a los procesos de implementación correspondientes para garantizar que los recursos sean detectables en futuras implementaciones.
13. Tras la detección, los equipos de administración operativa validarán el tamaño de los recursos para verificar que estos cumplen con los requisitos de rendimiento.
14. El equipo de gobernanza de la nube debe aprobar las herramientas de implementación para garantizar la gobernanza en curso de los recursos implementados.
15. Los scripts de implementación deben conservarse en un repositorio central accesible para el equipo de gobernanza de la nube para su revisión y auditoría periódicas.
16. Los procesos de revisión de gobernanza deben validar que los recursos implementados se configuren correctamente de acuerdo con el Acuerdo de Nivel de Servicio y los requisitos de recuperación.

## <a name="incremental-improvement-of-the-best-practices"></a>Mejoras graduales de los procedimientos recomendados

En esta sección del artículo se mejorará el diseño de un producto viable mínimo de gobernanza para que incluya nuevas directivas de Azure y una implementación de Azure Cost Management. Juntos, estos dos cambios de diseño cumplirán con las nuevas declaraciones de directiva corporativa.

Después de la experiencia de este ejemplo ficticio, se supone que ya se han producido los cambios de los datos protegidos. A partir de este procedimiento recomendado, a continuación se agregarán los requisitos de supervisión operativa, preparando una suscripción para aplicaciones críticas.

**Suscripción de TI corporativa:** agregue lo siguiente a la suscripción de TI corporativa, que actúa como un concentrador.

1. Como una dependencia externa, el equipo de operaciones de la nube deberá definir herramientas de supervisión operativa, herramientas de continuidad empresarial y recuperación ante desastres y herramientas de corrección automatizadas. El equipo de gobernanza de la nube podrá entonces dar servicio a los procesos de detección necesarios.
    1. En este caso de uso, el equipo de operaciones de la nube eligió Azure Monitor como herramienta principal para la supervisión de aplicaciones críticas.
    2. El equipo eligió también Azure Site Recovery como herramienta principal de continuidad empresarial y recuperación ante desastres.
2. Implementación de Azure Site Recovery.
    1. Defina e implemente el almacén de Azure Site Recovery para los procesos de copia de seguridad y recuperación.
    2. Cree una plantilla de Azure Resource Manager para crear un almacén en cada suscripción.
3. Implementación de Azure Monitor.
    1. Una vez que se identifica una suscripción crítica, se puede crear un área de trabajo de análisis de registro.

**Suscripción de adopción de la nube individual**: con el proceso siguiente se asegurará que cada suscripción sea detectable por la solución de supervisión y esté lista para incluirse en las prácticas de continuidad empresarial y recuperación ante desastres.

1. Azure Policy para nodos críticos:
    1. Audite y aplique solo el uso de roles estándar.
    2. Audite y aplique la aplicación de cifrado para todas las cuentas de almacenamiento.
    3. Audite y aplique el uso de la subred de red aprobada y red virtual por interfaz de red.
    4. Audite y aplique la limitación de las tablas de enrutamiento definidas por el usuario.
    5. Audite y aplique la implementación de agentes de Log Analytics para máquinas virtuales Windows y Linux.
2. Plano técnico de Azure:
    1. Cree un plano técnico denominado `mission-critical-workloads-and-protected-data`. Este plano técnico aplicará recursos además del plano técnico de datos protegidos.
    2. Agregue las nuevas directivas de Azure al plano técnico.
    3. Aplique el plano técnico a las suscripciones que se espera que alojen una aplicación crítica.

## <a name="conclusion"></a>Conclusión

La adición de estos procesos y cambios realizados en el producto viable mínimo de gobernanza ayudan a corregir muchos de los riesgos asociados con la gobernanza de recursos. Juntos, agregan los controles de recuperación, tamaño y supervisión necesarios para permitir las operaciones basadas en la nube.

## <a name="next-steps"></a>Pasos siguientes

A medida que avanza la adopción de la nube y aporta valores empresariales adicionales, también cambian los riesgos y necesidades de gobernanza de la nube. Para la compañía ficticia de esta guía, el siguiente desencadenador se da cuando la escala de implementación supera los 1000 recursos en la nube o el gasto mensual supera los 10 000 USD al mes. En este punto, el equipo de gobernanza de la nube agrega controles de administración de costos.

> [!div class="nextstepaction"]
> [Mejora de la materia de administración de costos](./cost-management-improvement.md)
