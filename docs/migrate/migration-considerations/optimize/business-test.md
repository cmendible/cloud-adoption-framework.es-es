---
title: Guía sobre las pruebas empresariales (UAT) durante la migración
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Un proceso de la migración a la nube que se centra en las tareas de migración de cargas de trabajo.
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: migrate
ms.openlocfilehash: 0f1ba39ae283b1ab2fdb276310a9490af6bf87b7
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70836634"
---
# <a name="guidance-for-business-testing-uat-during-migration"></a>Guía sobre las pruebas empresariales (UAT) durante la migración

Tradicionalmente consideradas como una función del equipo de TI, las pruebas de aceptación de usuario durante una transformación empresarial las puede organizar exclusivamente dicho equipo. Sin embargo, esta función se ejecuta a menudo de forma más eficaz como una función empresarial. El equipo de TI respalda esta actividad empresarial facilitando los planes de pruebas y desarrollo, y automatizando las pruebas cuando es posible. Aunque a menudo el equipo de TI puede actuar como suplente para las pruebas, no hay mejor sustituto que la observación de primera mano de usuarios reales que intentan usar una nueva solución en el contexto de un proceso empresarial real o replicado.

> [!NOTE]
> Cuando están disponibles, las pruebas automatizadas son un medio mucho más eficaz de probar cualquier sistema. Sin embargo, las migraciones en la nube a menudo se centran principalmente en sistemas heredados o en sistemas de producción menos estables. A menudo, esos sistemas no se administran mediante pruebas automatizadas exhaustivas y bien conservadas. En este artículo se da por supuesto que no hay ninguna de esas pruebas disponible en el momento de la migración.

Por detrás de las pruebas automatizadas, se encuentran las pruebas de los cambios de procesos y tecnologías por parte de usuarios avanzados. Los usuarios avanzados son las personas que normalmente ejecutan un proceso real que requiere interacciones con una herramienta o conjunto de herramientas tecnológicas. Un cliente externo que usa un sitio de comercio electrónico para adquirir bienes o servicios podría constituir un buen ejemplo. Otro ejemplo de usuarios avanzados lo podría constituir un grupo de empleados que ejecutan un proceso empresarial como, por ejemplo, un centro de llamadas que atiende a clientes y registra sus experiencias.

El objetivo de las pruebas empresariales es solicitar la validación de los usuarios avanzados para certificar que la nueva solución funciona según las expectativas y no impide los procesos empresariales. Si no se cumple ese objetivo, las pruebas empresariales pueden servir como circuito de retroalimentación que puede ayudar a definir cómo y por qué la carga de trabajo no satisface las expectativas.

## <a name="business-activities-during-business-testing"></a>Actividades del negocio durante las pruebas empresariales

Durante las pruebas empresariales, la primera iteración se controla manualmente directamente con los clientes. Esta es la forma más pura, y la que consume más tiempo, de un circuito de retroalimentación.

- **Identificación de los usuarios avanzados.** La propia empresa tiene generalmente una mejor percepción de los usuarios avanzados a los que un cambio técnico puede afectar.
- **Alineación y preparación de los usuarios avanzados.** Asegúrese de que los usuarios avanzados entienden los objetivos de negocio, los resultados deseados y los cambios previsibles de los procesos empresariales. Prepáreles a ellos y a su infraestructura de administración para el proceso de pruebas.
- **Participación en la interpretación de los comentarios del circuito de retroalimentación.** Ayude al personal de TI a comprender el impacto de los distintos puntos de los comentarios de los usuarios avanzados.
- **Aclaración del cambio de proceso.** Si la transformación puede desencadenar un cambio en los procesos empresariales, comunique el cambio y cualquier posible impacto en los niveles afectados.
- **Clasificación de los comentarios.** Ayude al equipo de TI a clasificar los comentarios en función del impacto empresarial.

En ocasiones, el equipo de TI puede emplear analistas o propietarios de productos que puedan actuar como representantes de las actividades detalladas de las pruebas empresariales. Sin embargo, la participación empresarial es muy recomendable y probablemente producirá resultados empresariales favorables.

## <a name="it-activities-during-business-testing"></a>Actividades del equipo de TI durante las pruebas empresariales

El equipo de TI actúa como uno de los destinatarios del resultado de las pruebas empresariales. Los ciclos de retroalimentación expuestos durante las pruebas empresariales se convierten en elementos de trabajo que definen el cambio técnico o el cambio de proceso. Como destinatario, se espera que el equipo de TI ayude en la facilitación, recopilación de comentarios y administración de las acciones técnicas resultantes. Entre las actividades habituales que realiza el equipo de TI durante las pruebas empresariales se incluyen:

- Proporcionar la estructura y la logística para las pruebas empresariales.
- Ayudar con la facilitación durante la realización de las pruebas.
- Proporcionar un medio y un proceso para registrar los comentarios.
- Ayudar a la empresa a priorizar y validar los comentarios.
- Desarrollar planes para actuar sobre cambios técnicos.
- Identificar las pruebas automatizadas existentes que puedan optimizar las pruebas por parte de los usuarios avanzados.
- Estudiar los procesos de las pruebas, definir pruebas comparativas y crear automatización para optimizar aún más las pruebas de los usuarios avanzados (en el caso de cambios que requieran procesos de implementación o prueba repetidos).

## <a name="next-steps"></a>Pasos siguientes

Junto con las pruebas de negocio, la [optimización de los recursos migrados](./optimize.md) puede contribuir a refinar el costo y el rendimiento de la carga de trabajo.

> [!div class="nextstepaction"]
> [Pruebas comparativas y ajuste del tamaño de los recursos de la nube](./optimize.md)
