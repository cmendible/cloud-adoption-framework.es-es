---
title: Información general sobre la migración del sistema central
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migre aplicaciones desde entornos del sistema central a Azure, una infraestructura que se ha probado de alta disponibilidad y escalable para los sistemas que se ejecutan actualmente en sistemas centrales.
author: njray
ms.author: v-nanra
ms.date: 12/27/2018
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: f4e8f8c1ef9a145fc1497727738d6d12e8f13d7b
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025064"
---
# <a name="mainframe-migration-overview"></a>Información general sobre la migración del sistema central

Muchas empresas y organizaciones se benefician del traslado de algunas o todas sus bases de datos, aplicaciones y cargas de trabajo de sistema central a la nube. Azure proporciona características similares al sistema central en el escalado de la nube sin muchos de los inconvenientes asociados a los sistemas centrales.

Normalmente, el término sistema central hace referencia a un equipo de gran tamaño, pero, actualmente, la inmensa mayoría de los sistemas centrales implementados son servidores IBM System Z o sistemas compatibles con enchufe IBM que ejecutan MVS, DOS, VSE, OS/390 o z/OS. Los sistemas centrales continúan usándose en muchos sectores para ejecutar sistemas de información vitales y ocupan un lugar en situaciones muy específicas, como entornos de TI donde se realizan una gran cantidad de transacciones y que tienen gran volumen y tamaño.

La migración a la nube permite a las empresas modernizar su infraestructura. Con los servicios en la nube, puede hacer que las aplicaciones de sistema central y el valor que proporcionan estén disponibles como carga de trabajo siempre que su organización así lo necesite. Muchas cargas de trabajo pueden transferirse a Azure con solo leves cambios en el código, como la actualización de los nombres de las bases de datos. Puede migrar cargas de trabajo más complejas con un enfoque por fases.

La mayoría de las empresas Fortune 500 ya ejecutan Azure para sus cargas de trabajo críticas. Incentivos finales significativos de Azure fomentan muchos proyectos de migración. Normalmente, las empresas trasladan las cargas de trabajo de desarrollo y pruebas a Azure primero. A esto le siguen DevOps, el correo electrónico y la recuperación ante desastres como servicio.

## <a name="intended-audience"></a>Destinatarios

Si tiene en cuenta una migración o la adición de servicios en la nube como opción para su entorno de TI, esta guía es para usted.

Ayuda a las organizaciones de TI a iniciar la conversación sobre la migración. Puede que esté más familiarizado con Azure y las infraestructuras basadas en la nube que con los sistemas centrales, de modo que esta guía comienza con información general sobre el funcionamiento de los sistemas centrales y continúa con diversas estrategias para determinar qué y cómo migrar.

## <a name="mainframe-architecture"></a>Arquitectura de sistema central

En los últimos años de la década de los 50, los sistemas centrales se diseñaron como servidores de escalabilidad vertical para ejecutar transacciones en línea de gran volumen y procesamiento por lotes. Por ello, los sistemas centrales tienen software para formularios de transacciones en línea (a veces llamados pantallas verdes) y sistemas de E/S de alto rendimiento para procesar ejecuciones por lotes.

Los sistemas centrales tienen una reputación de alta confiabilidad y disponibilidad, y se les conoce por su capacidad de ejecución de grandes transacciones en línea y trabajos por lotes. Una transacción deriva de un componente del procesamiento iniciado por una sola solicitud, normalmente de un usuario en un terminal. Las transacciones también pueden proceder de varios orígenes distintos, incluidas páginas web, estaciones de trabajo y aplicaciones de otros sistemas de información. Una transacción también se puede desencadenar automáticamente en un tiempo predefinido como se muestra en la figura siguiente.

![Componentes en una arquitectura de sistema central IBM típica](../../_images/mainframe-migration/mainframe-architecture.png)

Una arquitectura de sistema central IBM típica incluye estos componentes comunes:

- **Sistemas de front-end:** los usuarios pueden iniciar las transacciones desde terminales, páginas web o estaciones de trabajo remotas. Las aplicaciones de sistema central suelen tener interfaces de usuario personalizadas que se pueden conservar tras la migración a Azure. Los emuladores de terminal se siguen usando para obtener acceso a las aplicaciones de sistema central y también se les llama terminales de pantalla verde.

- **Capa de aplicación:** los sistemas centrales suelen incluir un sistema de control de información del cliente (CICS), un conjunto de administración de transacciones inicial para el sistema central z/OS de IBM que a menudo se usa con Information Management System (IMS) de IBM, un administrador de transacciones basado en mensajes. Los sistemas de lotes controlan actualizaciones de datos de alto rendimiento para grandes volúmenes de registros de cuenta.

- **Código:** lenguajes de programación usados por sistemas centrales, incluidos COBOL, Fortran, PL/I y Natural. El lenguaje de control de trabajos (JCL) se usa para trabajar con z/OS.

- **Nivel de base de datos:** un sistema de administración de bases de datos (DBMS) relacionales común para z/OS es IBM DD2. Administra estructuras de datos llamadas *dbspaces* que contienen una o varias tablas y se asignan a bloques de almacenamiento de conjuntos de datos físicos llamados *dbextents*. Dos componentes de base de datos importantes son el directorio que identifica ubicaciones de datos en los bloques de almacenamiento y el registro que contiene un registro de operaciones realizadas en la base de datos. Se admiten diversos formatos de datos de archivos planos. DB2 para z/OS suele usar conjuntos de datos del método de acceso de almacenamiento virtual (VSAM) para almacenar los datos.

- **Nivel de administración:** los sistemas centrales IBM incluyen software de programación como TWS-OPC, herramientas para la administración de salida e impresión como CA-SAR y SPOOL, y un sistema de control de código fuente para el código. El centro de control de acceso a los recursos (RACF) administra un control de acceso seguro para z/OS. Un administrador de base de datos proporciona acceso a los datos de la base de datos y se ejecuta en su propia partición en un entorno z/OS.

- **LPAR:** las particiones lógicas o LPARs se usan para dividir recursos de proceso. Un sistema central físico se particiona en varias LPARs.

- **z/OS:** un sistema operativo de 64 bits que se usa con mayor frecuencia para los sistemas centrales IBM.

Los sistemas IBM usan un monitor de transacciones como CICS para seguir y administrar todos los aspectos de una transacción empresarial. CICS administra el uso compartido de recursos, la integridad de datos y la priorización de la ejecución. CICS autoriza a los usuarios, asigna recursos y pasa solicitudes de base de datos de la aplicación a un administrador de base de datos, como IBM DB2.

Para un ajuste más preciso, CICS se usa habitualmente con IMS/TM (anteriormente IMS/Data Communications o IMS/DC). IMS se diseñó para reducir la redundancia de datos manteniendo una sola copia de los datos. Complementa CICS como monitor de transacciones manteniendo el estado en todo el proceso y registrando funciones empresariales en un almacén de datos.

## <a name="mainframe-operations"></a>Operaciones del sistema central

Estas son operaciones del sistema central típicas:

- **En línea:** entre las cargas de trabajo se incluyen el procesamiento de transacciones, la administración de base de datos y las conexiones. Normalmente se implementan mediante los conectores z/OS, CICS e IBM DB2.

- **Lote:** los trabajos se ejecutan sin la interacción del usuario, normalmente de forma periódica (por ejemplo, todos los días laborables por las mañanas). Los trabajos por lotes se pueden ejecutar en sistemas basados en Windows o Linux mediante un emulador JCL como el software Control-M de BMC o Micro Focus Enterprise Server.

- **Lenguaje de control de trabajos (JCL):** especifique los recursos necesarios para procesar trabajos por lotes. JCL transmite esta información a z/OS a través de un conjunto de instrucciones de control de trabajo. El JCL básico contiene seis tipos de instrucciones: JOB, ASSGN, DLBL, EXTENT, LIBDEF y EXEC. Un trabajo puede contener varias instrucciones EXEC (pasos) y cada paso podría tener varias instrucciones LIBDEF, ASSGN, DLBL y EXTENT.

- **Carga de programas de inicio (IPL):**  hace referencia a la carga de una copia del sistema operativo desde el disco en el almacenamiento real de un procesador y su ejecución. Las IPLs se usan para recuperarse del tiempo de inactividad. Una IPL es algo similar a arrancar el sistema operativo en máquinas virtuales Windows o Linux.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Mitos y verdades](./myths-and-facts.md)
