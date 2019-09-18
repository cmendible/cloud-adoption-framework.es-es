---
title: 'Guía de gobernanza para empresas complejas: Mejora de la materia de línea de base de identidad'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Guía de gobernanza para empresas complejas: Mejora de la materia de línea de base de identidad'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/06/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 0c17f9043dd88f401b07293a6b93e50ccefe0137
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032082"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-identity-baseline-discipline"></a>Guía de gobernanza para empresas complejas: Mejora de la materia de línea de base de identidad

En este artículo se desarrolla la narración al agregar controles de línea de base de identidad al producto viable mínimo de gobernanza.

## <a name="advancing-the-narrative"></a>Continuación de la historia

El director financiero aprobó la justificación empresarial para la migración a la nube de los dos centros de datos. Durante el estudio de viabilidad técnica, se detectaron varios obstáculos:

- Los datos protegidos y las aplicaciones críticas representan el 25 % de las cargas de trabajo en los dos centros de datos. No se puede eliminar ninguno hasta que las directivas de gobernanza actuales con respecto a la información personal confidencial y a las aplicaciones críticas se hayan modernizado.
- El 7 % de los recursos de esos centros de datos no son compatibles con la nube. Se moverán a un centro de datos alternativo antes de la finalización del contrato del centro de datos.
- El 15 % de los recursos en el centro de datos (750 máquinas virtuales) tiene una dependencia en la autenticación heredada o autenticación multifactor de terceros.
- La conexión VPN que se conecta a Azure y a los centros de datos existentes no ofrece suficientes velocidades de transmisión de datos ni la latencia para migrar el volumen de recursos dentro del plazo de dos años para retirar el centro de datos.

Los dos primeros obstáculos se están administrando en paralelo. En este artículo se abordará la resolución del tercer y cuarto obstáculos.

### <a name="expanding-the-cloud-governance-team"></a>Expansión del equipo de gobernanza de la nube

El equipo de gobernanza de la nube se está expandiendo. Dada la necesidad de soporte adicional con respecto a la administración de identidades, un administrador del sistema del equipo de línea de base de identidad ahora participa en una reunión semanal para mantener a los miembros del equipo existente al tanto de los cambios.

### <a name="changes-in-the-current-state"></a>Cambios en el estado actual

El equipo de TI tiene la aprobación para avanzar con los planes del director de información y el director financiero para retirar dos centros de datos. Sin embargo, a TI le preocupa que 750 máquinas virtuales (el 15 % de los recursos) de esos centros de datos tendrán que moverse a algún lugar distinto de la nube.

### <a name="incrementally-improve-the-future-state"></a>Mejora gradual del estado futuro

Los nuevos planes de estado futuro requieren una solución más sólida de línea de base de identidad para migrar las máquinas virtuales 750 con los requisitos de autenticación heredados. Más allá de estos dos centros de datos, es previsible que este problema afecte a un porcentaje similar de recursos en otros centros de datos.

El estado futuro ahora también requiere una conexión desde el proveedor de nube a la solución MPLS o de línea dedicada de la empresa.

Los cambios de los estados actual y futuro exponen nuevos riesgos que requerirán nuevas declaraciones de directiva.

## <a name="changes-in-tangible-risks"></a>Cambios en riesgos tangibles

**Interrupción del negocio durante la migración.** La migración a la nube crea un riesgo controlado y temporal que se puede administrar. El traslado de hardware antiguo a otra parte del mundo es un riesgo mucho mayor. Se necesita una estrategia de mitigación para evitar las interrupciones en las operaciones empresariales.

**Dependencias de identidad existentes.** Las dependencias en los servicios existentes de autenticación e identidad pueden retrasar o impedir la migración de algunas cargas de trabajo a la nube. La incapacidad de devolver los dos centros de datos a tiempo generará millones de dólares en las tarifas de concesión de centros de datos.

Este riesgo empresarial puede ampliarse a algunos riesgos técnicos:

- La autenticación heredada puede no estar disponible en la nube, lo que limita la implementación de algunas aplicaciones.
- La solución actual de autenticación multifactor de terceros puede no estar disponible en la nube, lo que limita la implementación de algunas aplicaciones.
- Cambiar sus herramientas o moverlas podría crear interrupciones y sumar costos.
- La velocidad y la estabilidad de la VPN podrían impedir la migración.
- El tráfico de entrada en la nube podría producir problemas de seguridad en otras partes de la red global.

## <a name="incremental-improvement-of-the-policy-statements"></a>Mejora gradual de las declaraciones de las directivas

Los siguientes cambios en la directiva le ayudarán a corregir los nuevos riesgos y le guiarán en la implementación.

- El proveedor de nube elegido debe ofrecer un medio de autenticación a través de métodos heredados.
- El proveedor de nube elegido debe ofrecer un medio de autenticación con la solución actual de autenticación multifactor de terceros.
- Debe establecerse una conexión privada de alta velocidad entre el proveedor de nube y el proveedor de telecomunicaciones de la empresa, que conecte al proveedor de nube con la red mundial de centros de datos.
- Hasta que no se establezcan requisitos de seguridad suficientes, ningún tráfico público entrante podrá acceder a los recursos de la empresa hospedados en la nube. Todos los puertos se bloquean desde cualquier origen fuera de la WAN global.

## <a name="incremental-improvement-of-the-best-practices"></a>Mejoras graduales de los procedimientos recomendados

El diseño del producto viable mínimo de gobernanza cambia para incluir nuevas directivas de Azure y una implementación de Active Directory en una máquina virtual. Juntos, estos dos cambios de diseño cumplen con las nuevas instrucciones de directiva corporativa.

Estos son los nuevos procedimientos recomendados:

- **Plano técnico de red virtual híbrida segura:** El lado local de la red híbrida debe configurarse para permitir la comunicación entre la siguiente solución y los servidores locales de Active Directory. Este procedimiento recomendado requiere una DMZ para habilitar Active Directory Domain Services más allá de los límites de la red.
- **Plantillas de Azure Resource Manager:**
    1. Defina un grupo de seguridad de red para bloquear el tráfico externo y permitir el interno.
    1. Implemente dos máquinas virtuales de Active Directory en un par con equilibrio de carga basado en una imagen maestra. En el primer arranque, esa imagen ejecuta un script de PowerShell para unirse al dominio y registrarse en los servicios de dominio. Para más información, consulte [Extensión de Active Directory Domain Services (AD DS) a Azure](https://docs.microsoft.com/azure/architecture/reference-architectures/identity/adds-extend-domain).
- Azure Policy: Aplique el NSG a todos los recursos.
- Plano técnico de Azure:
    1. Cree un plano técnico denominado `active-directory-virtual-machines`.
    1. Agregue cada una de las directivas y plantillas de Active Directory al plano técnico.
    1. Publique el plano técnico en cualquier grupo de administración correspondiente.
    1. Aplique el plano técnico a cualquier suscripción que requiera autenticación multifactor de terceros o heredada.
    1. Ahora se puede usar la instancia de Active Directory que se ejecuta en Azure como extensión de la solución local de Active Directory, lo que le permite integrarse en la herramienta de autenticación multifactor existente y proporcionar autenticación basada en notificaciones, ambas a través de la funcionalidad de Active Directory existente.

## <a name="conclusion"></a>Conclusión

Agregar estos cambios al producto viable mínimo de gobernanza ayuda a solucionar muchos de los riesgos indicados en este artículo, lo que permite a cada equipo de adopción de la nube superar rápidamente este obstáculo.

## <a name="next-steps"></a>Pasos siguientes

A medida que avanza la adopción de la nube y aporta valores empresariales adicionales, también cambian los riesgos y necesidades de gobernanza de la nube. Las siguientes son algunos cambios que pueden presentarse. Para esta empresa ficticia, el siguiente desencadenador es la inclusión de datos protegidos en el plan de adopción de la nube. Este cambio requiere controles de seguridad adicionales.

> [!div class="nextstepaction"]
> [Mejora de la materia de base de referencia de la seguridad](./security-baseline-improvement.md)
