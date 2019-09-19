---
title: 'Guía para empresa estándar: Mejora de la coherencia de los recursos'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Guía para empresa estándar: Mejora de la coherencia de los recursos'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: ec9263b1e1ab47e2018d86093a5198cdb1ac7b67
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031453"
---
# <a name="standard-enterprise-guide-improving-resource-consistency"></a>Guía para empresa estándar: Mejora de la coherencia de los recursos

En este artículo, la narrativa avanza agregando controles de coherencia de los recursos para dar servicio a aplicaciones críticas.

## <a name="advancing-the-narrative"></a>Continuación de la historia

Las nuevas experiencias de clientes, las nuevas herramientas de predicción y la infraestructura migrada siguen avanzando. La empresa ahora está lista para comenzar a usar esos recursos en un entorno de producción.

### <a name="changes-in-the-current-state"></a>Cambios en el estado actual

En la fase anterior de esta narrativa, los equipos de BI y desarrollo de aplicaciones estaban prácticamente listos para integrar los datos financieros y de clientes en cargas de trabajo de producción. El equipo de TI estaba a punto de retirar el centro de datos de recuperación ante desastres.

Desde entonces, han cambiado algunas cosas que afectarán a la gobernanza:

- TI ha retirado el 100 % del centro de datos de recuperación ante desastres, antes de lo previsto. Durante el proceso, se identificó un conjunto de recursos del centro de datos de producción como candidatos para la migración a la nube.
- Los equipos de desarrollo de aplicaciones ya están preparados para el tráfico de producción.
- El equipo de BI está listo para devolver información y predicciones de fuentes a los sistemas de operaciones del centro de datos de producción.

### <a name="incrementally-improve-the-future-state"></a>Mejora gradual del estado futuro

Antes de usar las implementaciones de Azure en los procesos empresariales de producción, las operaciones en la nube deben madurar. En conjunto, se requieren cambios adicionales de la gobernanza para asegurarse de que los recursos pueden funcionar correctamente.

Los cambios de los estados actual y futuro exponen nuevos riesgos que requerirán nuevas declaraciones de directiva.

## <a name="changes-in-tangible-risks"></a>Cambios en riesgos tangibles

**Interrupción del negocio:** existe un riesgo inherente de que cualquier nueva plataforma cause interrupciones en los procesos de negocio críticos. El equipo de operaciones de TI y los equipos que ejecutan tareas en diversas adopciones de la nube tienen relativamente poca experiencia con las operaciones de la nube. Como esto aumenta el riesgo de interrupción, hay que tomar medidas al respecto para solucionarlo y gobernarlo.

Este riesgo empresarial puede ampliarse a algunos riesgos técnicos:

1. Intrusiones externas o ataques por denegación de servicio podrían provocar una interrupción del negocio.
2. Los recursos críticos podrían no detectarse adecuadamente y, por lo tanto, podrían no utilizarse correctamente.
3. Los recursos desconocidos o mal etiquetados podrían no ser compatibles con los procesos de administración operativa existentes.
4. La configuración de los recursos implementados podría no satisfacer las expectativas de rendimiento.
5. Es posible que el registro no se haya anotado y centralizado correctamente para permitir la solución de problemas de rendimiento.
6. Las directivas de recuperación podrían dar error o tardar más de lo esperado.
7. Unos procesos de implementación incoherentes podrían dar lugar a brechas de seguridad y estas, a su vez, a pérdidas de datos o interrupciones.
8. El desfase de configuración o la falta de revisiones podrían dar lugar a brechas de seguridad y estas, a su vez, a pérdidas de datos o interrupciones.
9. La configuración podría no aplicar los requisitos de los Acuerdos de Nivel de Servicio definidos o los requisitos de recuperación confirmados.
10. Los sistemas operativos o aplicaciones implementados podrían no cumplir con los requisitos de protección.
11. Con tantos equipos que trabajan en la nube, existe un riesgo de incoherencia.

## <a name="incremental-improvement-of-the-policy-statements"></a>Mejora gradual de las declaraciones de las directivas

Los siguientes cambios en la directiva le ayudarán a corregir los nuevos riesgos y le guiarán en la implementación. La lista parece larga, pero la adopción de estas directivas puede ser más fácil de lo que parece.

1. Todos los recursos implementados deben categorizarse por importancia y clasificación de datos. El equipo de gobernanza de la nube y el propietario de la aplicación deben revisar las clasificaciones antes de la implementación en la nube.
2. Las subredes que contienen aplicaciones críticas deben estar protegidas por una solución de firewall capaz de detectar intrusiones y responder a los ataques.
3. Las herramientas de gobernanza deben auditar y aplicar los requisitos de configuración de red que estableció el equipo de administración de seguridad.
4. Las herramientas de gobernanza deben validar que todos los recursos relacionados con aplicaciones críticas o datos protegidos se incluyen en la supervisión de la disminución y optimización de recursos.
5. Las herramientas de gobernanza deben validar que se recopila el nivel adecuado de datos de registro para todas las aplicaciones críticas o datos protegidos.
6. El proceso de gobernanza debe validar que la copia de seguridad, la recuperación y el cumplimiento de los Acuerdos de Nivel de Servicios se implementen correctamente para aplicaciones críticas y datos protegidos.
7. Las herramientas de gobernanza deben limitar la implementación de máquina virtual a solo las imágenes aprobadas.
8. Las herramientas de gobernanza debe exigir que las actualizaciones automáticas se impidan en todos los recursos implementados que admitan aplicaciones críticas. Las infracciones deben revisarse con los equipos de administración de operaciones y corregirse de acuerdo con las directivas de operaciones. Los recursos que no se actualicen automáticamente deben incluirse en procesos que sean propiedad del departamento de operaciones de TI.
9. Las herramientas de gobernanza deben validar el etiquetado relacionado con el costo, la importancia, el Acuerdo de Nivel de Servicio, la aplicación y la clasificación de los datos. Todos los valores deben alinearse con valores predefinidos, administrados por el equipo de gobernanza.
10. Los procesos de gobernanza deben incluir auditorías en el punto de implementación y en ciclos regulares para garantizar la coherencia entre todos los recursos.
11. El equipo de seguridad debe revisar periódicamente las tendencias y vulnerabilidades que podrían afectar a implementaciones en la nube para proporcionar actualizaciones a las herramientas de administración de seguridad utilizadas en la nube.
12. Antes de su publicación en producción, todas las aplicaciones críticas y los datos protegidos deben agregarse a la solución de supervisión operativa designada. Los recursos que no pueden detectarse por las herramientas de operaciones de TI elegidas no pueden liberarse para su uso en producción. Cualquier cambio requerido para hacer que los recursos sean detectables debe aplicarse a los procesos de implementación correspondientes para garantizar que los recursos sean detectables en futuras implementaciones.
13. Tras la detección, los equipos de administración operativa ajustarán el tamaño de los recursos, a fin de garantizar que estos cumplan los requisitos de rendimiento.
14. El equipo de gobernanza de la nube debe aprobar las herramientas de implementación para garantizar la gobernanza en curso de los recursos implementados.
15. Los scripts de implementación deben conservarse en un repositorio central accesible para el equipo de gobernanza de la nube, y que así se puedan revisar y se realicen auditorías periódicas.
16. Los procesos de revisión de gobernanza deben validar que los recursos implementados se configuren correctamente de acuerdo con el Acuerdo de Nivel de Servicio y los requisitos de recuperación.

## <a name="incremental-improvement-of-governance-practices"></a>Mejora incremental de las prácticas de gobernanza

En esta sección del artículo se cambiará el diseño del producto viable mínimo de gobernanza para incluir nuevas directivas de Azure y una implementación de Azure Cost Management. Juntos, estos dos cambios de diseño cumplirán con las nuevas declaraciones de directiva corporativa.

1. El equipo de operaciones de la nube definirá las herramientas de supervisión operativa y las herramientas de corrección automáticas. El equipo de gobernanza de la nube apoyará estos procesos de detección. En este caso de uso, el equipo de operaciones de la nube eligió Azure Monitor como herramienta principal para la supervisión de aplicaciones críticas.
1. Cree un repositorio en Azure DevOps para almacenar y editar todas las plantillas de Resource Manager pertinentes y las configuraciones con script.
1. Implementación en Azure Vault:
    1. Defina e implemente Azure Vault para los procesos de copia de seguridad y recuperación.
    1. Cree una plantilla de Resource Manager para crear un almacén en cada suscripción.
1. Actualice Azure Policy en todas las suscripciones:
    1. Audite y exija la clasificación de datos y la importancia en todas las suscripciones, para identificar aquellas que tienen recursos críticos.
    1. Audite y exija el uso de imágenes aprobadas únicamente.
1. Implementación de Azure Monitor:
    1. Una vez que se identifica una suscripción crítica, cree un área de trabajo de Azure Monitor con PowerShell. Se trata de un proceso anterior a la implementación.
    1. Durante las pruebas de implementación, el equipo de operaciones de la nube implementa la detección de pruebas y los agentes necesarios.
1. Actualice Azure Policy en todas las suscripciones que contengan aplicaciones críticas.
    1. Audite y exija la aplicación de un NSG a todos los NIC y subredes. Los equipos de redes y seguridad de TI definen los NSG.
    1. Audite y exija el uso de redes virtuales y subredes de red aprobadas para cada interfaz de red.
    1. Audite y exija que se aplique la limitación de las tablas de enrutamiento que defina el usuario.
    1. Audite y exija la implementación de agentes de Azure Monitor para todas las máquinas virtuales.
    1. Audite y exija la existencia de Azure Vault en la suscripción.
1. Configuración del firewall:
    1. Identifique una configuración de Azure Firewall que cumpla los requisitos de seguridad. También puede identificar un dispositivo de terceros que sea compatible con Azure.
    1. Cree una plantilla de Resource Manager para implementar el firewall con las configuraciones necesarias.
1. Plano técnico de Azure:
    1. Cree un plano técnico de Azure denominado `protected-data`.
    1. Agregue el firewall y las plantillas de Azure Vault al plano técnico.
    1. Agregue las nuevas directivas para suscripciones de datos protegidos.
    1. Publique el plano técnico en cualquier grupo de administración destinado a hospedar aplicaciones críticas.
    1. Aplique el nuevo plano técnico a cada suscripción afectada, además de los planos técnicos existentes.

## <a name="conclusion"></a>Conclusión

Estos procesos y cambios adicionales aplicados al producto viable mínimo de gobernanza ayudan a corregir muchos de los riesgos asociados con la regulación de recursos. Juntos, agregan los controles de recuperación, tamaño y supervisión que permiten las operaciones basadas en la nube.

## <a name="next-steps"></a>Pasos siguientes

A medida que avanza la adopción de la nube y aporta valores empresariales adicionales, también cambian los riesgos y necesidades de gobernanza de la nube. Para la compañía ficticia de esta guía, el siguiente desencadenador se da cuando la escala de implementación supera los 100 recursos en la nube o el gasto mensual supera los 1 000 USD al mes. En este punto, el equipo de gobernanza de la nube agrega controles de administración de costos.

> [!div class="nextstepaction"]
> [Mejora de la administración de costos](./cost-management-improvement.md)
