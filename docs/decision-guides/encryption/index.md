---
title: Guía de decisiones sobre cifrado
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información acerca del cifrado como un servicio principal en las migraciones de Azure.
author: rotycenh
ms.author: v-tyhopk
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: decision-guide
ms.custom: governance
ms.openlocfilehash: 82ad7e2c4e7e7eac375e99daa0815c8482492e15
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223902"
---
# <a name="encryption-decision-guide"></a>Guía de decisiones sobre cifrado

El cifrado de datos protege contra accesos no autorizados. Una directiva de cifrado correctamente implementada proporciona niveles adicionales de seguridad para las cargas de trabajo basadas en la nube y protege contra atacantes y otros usuarios no autorizados dentro o fuera de su organización y sus redes.

Vaya a: [Administración de claves](#key-management) | [Cifrado de datos](#data-encryption) | [Más información](#learn-more)

La estrategia de cifrado en la nube se centra en directivas corporativas y en las órdenes de cumplimiento normativo. El cifrado de recursos es deseable y muchos servicios de Azure, como Azure Storage y Azure SQL Database, habilitan el cifrado de forma predeterminada. Sin embargo, el cifrado tiene como inconvenientes que pueden aumentar la latencia y el uso global de los recursos.

Para las cargas de trabajo más exigentes, encontrar el equilibrio adecuado entre el cifrado y el rendimiento, y determinar cómo se cifran los datos y el tráfico puede ser fundamental. Los mecanismos de cifrado pueden variar en costo y complejidad, y los requisitos técnicos y de directivas pueden influir en las decisiones sobre cómo se aplica el cifrado y cómo se almacenan y administran los secretos y claves críticos.

La directiva corporativa y el cumplimiento de terceros son los factores más importantes a la hora de planear una estrategia de cifrado. Azure proporciona varios mecanismos estándar que pueden satisfacer los requisitos comunes de cifrado de datos tanto en reposo como en tránsito. Sin embargo, para los requisitos de directivas y cumplimiento que exigen controles más estrictos como, por ejemplo, la administración estandarizada de secretos y claves, el cifrado en uso o el cifrado de datos específico, deberá desarrollar una estrategia de cifrado más sofisticada que admita estos requisitos.

## <a name="key-management"></a>Administración de claves

El cifrado de datos en la nube depende del almacenamiento, administración y uso operativo seguros de las claves de cifrado. Tener un sistema de administración de claves es fundamental para que la organización pueda crear, almacenar y administrar claves criptográficas así como contraseñas importantes, cadenas de conexión y otra información confidencial de TI.

Los sistemas de administración de claves actuales como, por ejemplo, Azure Key Vault, admiten el almacenamiento y administración de claves protegidas de software para el uso de desarrolladores y de pruebas, y de claves protegidas del módulo de seguridad del hardware (HSM) para ofrecer la máxima protección de las cargas de trabajo de producción o de la información confidencial.

Al planear una migración a la nube, la tabla siguiente puede ayudarle a decidir cómo almacenar y administrar claves de cifrado, certificados y secretos, fundamentales para crear implementaciones en la nube seguras y fáciles de administrar:

| Pregunta | Nativas de la nube | Bring Your Own Key | Hold your own key |
|---------------------------------------------------------------------------------------------------------------------------------------|--------------|--------|-------------|
| ¿Su organización carece de administración centralizada de claves y secretos?                                                                    | Sí          | No     | Sin          |
| ¿Necesitará limitar la creación de claves y secretos para dispositivos al hardware local, pero se usarán en la nube? | Sin           | Sí    | Sin          |
| ¿Su organización cuenta con reglas o directivas vigentes que podrían impedir que las claves se almacenen externamente?                | Sin           | No     | Sí         |

### <a name="cloud-native"></a>Nativas de la nube

Con la administración nativa de claves en la nube, todas las claves y los secretos se generan, administran y almacenan en un almacén basado en la nube como Azure Key Vault. Este enfoque simplifica muchas tareas de TI relacionadas con la administración de claves, como la copia de seguridad, el almacenamiento y la renovación de claves.

En el uso de un sistema de administración nativa de claves en la nube se da por hecho lo siguiente:

- Confía en la solución de administración de claves en la nube para crear, administrar y hospedar los secretos y las claves de su organización.
- Permite el acceso al sistema de administración de claves en la nube a todas las aplicaciones y los servicios locales que dependan del acceso a los secretos o servicios de cifrado.

### <a name="bring-your-own-key"></a>Bring Your Own Key

Con el enfoque "Bring Your Own Key" puede generar claves en el hardware del HSM dedicado en el entorno local para transferirlas, posteriormente, a un sistema de administración basado en la nube, como Azure Key Vault, para el uso de los recursos hospedados en la nube.

**Suposiciones del enfoque "Bring Your Own Key":** La generación de claves en el entorno local y su uso con un sistema de administración de claves basado en la nube incluye estas suposiciones:

- Confía en la infraestructura subyacente de seguridad y control de acceso de la plataforma de nube para hospedar y usar sus claves y secretos.
- Las aplicaciones y servicios hospedados en la nube pueden acceder y utilizar claves y secretos de una manera sólida y segura.
- Está obligado por ley o por una directiva de la organización a mantener en el entorno local la creación y administración de los secretos y las claves de su organización.

### <a name="on-premises-hold-your-own-key"></a>Local (mantenga su propia clave)

En algunos casos, podría haber normativas, directivas o razones técnicas por las que las claves no se pueden almacenar en un sistema de administración de claves basado en la nube. En tales casos, deberá generar las claves mediante el hardware local y almacenarlas y administrarlas mediante un sistema de administración de claves local, y deberá aprovisionar un mecanismo que permita a un recurso basado en la nube acceder a estas claves con fines de cifrado. Tenga en cuenta que el enfoque "Hold Your Own Key" puede que no sea compatible con todos los servicios basados en Azure.

**Suposiciones para la administración local de claves:** En el uso de un sistema de administración de claves local se da por hecho lo siguiente:

- Está obligado por ley o por una directiva de la organización a mantener en el entorno local la creación, la administración y el hospedaje de los secretos y las claves de su organización.
- Todas las aplicaciones y los servicios locales que dependan del acceso a los secretos o servicios de cifrado pueden acceder al sistema de administración local de claves.

## <a name="data-encryption"></a>Cifrado de datos

Tenga en cuenta los diferentes estados de los datos, con sus diferentes necesidades de cifrado, a la hora de planear la directiva de cifrado:

| Estado de los datos | Datos |
|-----|-----|
| Datos en tránsito | Tráfico de red interno, conexiones a Internet, conexiones entre centros de datos o redes virtuales |
| Datos en reposo    | Bases de datos, archivos, unidades virtuales, almacenamiento de PaaS |
| Datos en uso     | Datos cargados en la memoria RAM o en las memorias caché de la CPU |

### <a name="data-in-transit"></a>Datos en tránsito

Los datos en tránsito son aquellos que se transfieren internamente entre los recursos, entre los centros de datos o las redes externas o a través de Internet.

Normalmente, para cifrar los datos en tránsito se requiere los protocolos SSL/TLS para el tráfico. Siempre se debe cifrar el tráfico en tránsito entre los recursos hospedados en la nube a la red externa o a la red de Internet pública. Recursos de PaaS generalmente también aplican cifrado SSL/TLS al tráfico de forma predeterminada. Si debe aplicar o no cifrado al tráfico entre los recursos de IaaS hospedados en sus redes virtuales es una decisión del equipo de adopción de la nube y de los propietarios de la carga de trabajo y, por lo general, se recomienda.

**Suposiciones sobre el cifrado de datos en tránsito:** Al implementar una directiva de cifrado para los datos en tránsito, se da por hecho lo siguiente:

- Todos los puntos de conexión accesibles públicamente en su entorno de nube se comunicarán con la red pública de Internet mediante los protocolos SSL/TLS.
- Al conectar redes en la nube con un entorno local u otra red externa mediante la red pública de Internet, se usan protocolos de VPN cifrados.
- Al conectar redes en la nube con un entorno local u otra red externa mediante una conexión WAN dedicada, como ExpressRoute, se usará una VPN u otro dispositivo de cifrado local emparejado con el correspondiente dispositivo de red virtual o de cifrado implementado en la red en la nube.
- Si tiene datos confidenciales que no deberían incluirse en los registros de tráfico u otros informes de diagnóstico visibles para el personal de TI, se cifrará todo el tráfico entre los recursos de la red virtual.

### <a name="data-at-rest"></a>Datos en reposo

Los datos en reposo son aquellos que no se están moviendo ni procesando activamente; incluye archivos, bases de datos, unidades de máquina virtual, cuentas de almacenamiento de PaaS o recursos similares. El cifrado de datos almacenados protege los archivos o dispositivos virtuales contra el acceso no autorizado, ya sea por intrusión desde la red externa, usuarios internos deshonestos o liberaciones accidentales.

Por lo general, los recursos de almacenamiento y base de datos de PaaS aplican el cifrado de forma predeterminada. Los recursos de IaaS se pueden proteger mediante el cifrado de datos en el nivel de disco virtual o mediante el cifrado de la cuenta de almacenamiento completa que hospeda las unidades de disco virtuales. Todos estos recursos pueden usar las claves administradas por Microsoft o por el cliente que están almacenadas en Azure Key Vault.

El cifrado de datos en reposo también incluye técnicas de cifrado de base de datos más avanzadas, como el cifrado en el nivel de columna y en el nivel de fila, que ofrece mucho más control sobre qué datos se protegen.

Los requisitos generales de directiva y cumplimiento, la confidencialidad de los datos almacenados y los requisitos de rendimiento de las cargas de trabajo determinarán qué recursos necesitan cifrado.

**Suposiciones sobre el cifrado de datos en reposo**. Para el cifrado de datos en reposo se da por hecho lo siguiente:

- Almacena datos que no están destinados al consumo público.
- Las cargas de trabajo pueden aceptar el costo de latencia agregada que supone el cifrado de los discos.

### <a name="data-in-use"></a>Datos en uso

El cifrado de datos en uso implica proteger datos en un almacenamiento no persistente, como la RAM o la memoria caché de la CPU. Usa tecnologías como el cifrado de memoria completo o tecnologías de enclave, como Intel Secure Guard Extensions (SGX). Esto también incluye técnicas de cifrado, como el cifrado homomorfo, que puede usarse para crear entornos de ejecución seguros y de confianza.

**Suposiciones sobre el cifrado de datos en uso:** Para el cifrado de datos en uso se da por hecho lo siguiente:

- Necesita mantener la propiedad de los datos independiente de la plataforma de nube subyacente en todo momento, incluso en el nivel de RAM y CPU.

## <a name="learn-more"></a>Más información

Para más información acerca del cifrado y administración de claves en Azure, consulte:

- [Introducción al cifrado de Azure](https://docs.microsoft.com/azure/security/security-azure-encryption-overview). Descripción detallada de cómo utiliza Azure el cifrado para proteger los datos en reposo y en tránsito.
- [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-overview) Key Vault es el principal sistema de administración de claves para almacenar y administrar claves de cifrado, secretos y certificados dentro de Azure.
- [Procedimientos recomendados de cifrado y seguridad de datos en Azure](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices). Un análisis sobre los procedimientos recomendados de cifrado y seguridad de datos en Azure.
- [Computación confidencial en Azure](https://azure.microsoft.com/solutions/confidential-compute). La iniciativa de computación confidencial de Azure ofrece herramientas y tecnología para crear entornos de ejecución de confianza u otros mecanismos de cifrado para proteger los datos de uso.

## <a name="next-steps"></a>Pasos siguientes

El cifrado es solo uno de los componentes principales de infraestructura que requiere decisiones de arquitectura durante el proceso de adopción de la nube. Visite la [introducción a las guías de decisión](../index.md) para obtener información sobre los patrones alternativos o los modelos que se usan al tomar decisiones de diseño para otros tipos de infraestructura.

> [!div class="nextstepaction"]
> [Guías de decisiones sobre arquitectura](../index.md)
