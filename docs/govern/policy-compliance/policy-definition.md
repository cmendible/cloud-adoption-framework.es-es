---
title: Definición de directivas corporativas para la gobernanza de la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Aprenda a establecer directivas para reflejar y corregir los riesgos.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.openlocfilehash: 4184ccdd4a0efa06d6a842f7ba1d9cbf0dc77ea6
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71223733"
---
# <a name="define-corporate-policy-for-cloud-governance"></a>Definición de directivas corporativas para la gobernanza de la nube

Una vez que haya analizado los riesgos conocidos y las tolerancias a riesgos relacionadas del proceso de transformación hacia la nube de la organización, el siguiente paso consiste en establecer directivas que aborden explícitamente tales riesgos y definan los pasos necesarios para corregirlos siempre que sea posible.

<!-- markdownlint-disable MD026 -->

## <a name="how-can-corporate-it-policy-become-cloud-ready"></a>¿Cómo se puede adaptar la directiva de TI de la empresa a las soluciones en la nube?

En la gobernanza tradicional y en la incremental, las directivas corporativas crean la definición del trabajo de gobernanza. La mayoría de las acciones de gobernanza de TI buscan implementar tecnología para supervisar, aplicar, usar y automatizar esas directivas corporativas. La gobernanza de la nube se basa en conceptos similares.

![Gobernanza corporativa y materias de gobernanza.](../../_images/operational-transformation-govern-highres.png)

*Figura 1: Gobernanza corporativa y disciplinas de gobernanza.*

La imagen anterior muestra la relación entre el riesgo empresarial, las directivas y el cumplimiento, y los mecanismos de supervisión y cumplimiento que deben interactuar como parte de la estrategia de gobernanza. Las cinco materias de gobernanza de la nube permiten administrar estas interacciones y aplicar la estrategia.

La gobernanza de la nube es producto de un esfuerzo continuo de adopción a lo largo del tiempo, ya que una verdadera transformación duradera no ocurre de la noche a la mañana. Si intenta ofrecer una gobernanza integral de la nube antes de abordar los cambios clave de las directivas corporativas mediante un método rápido y agresivo, rara vez conseguirá los resultados deseados. En su lugar, le recomendamos que aplique un método incremental.

Lo que diferencia a un Marco de adopción de la nube es el ciclo de compra y que puede permitir una transformación auténtica. Puesto que no hay un requisito grande de inversión de capital, los ingenieros pueden comenzar con la experimentación y la adopción mucho antes. En la mayoría de las culturas corporativas, la eliminación de la barrera de los gastos de capital para la adopción puede llevar a ciclos que ofrecen comentarios más precisos, un crecimiento orgánico y una ejecución incremental.

El cambio a la adopción de la nube requiere realizar un cambio en la gobernanza. Por ello, en muchas organizaciones, la transformación de las directivas corporativas les permite alcanzar una gobernanza mejor y mayores tasas de cumplimiento gracias a los cambios realizados en las directivas incrementales y a la aplicación automática de esos cambios, impulsada gracias a las capacidades recién definidas que debe configurar con su proveedor de servicios en la nube.

<!-- markdownlint-enable MD026 -->

## <a name="review-existing-policies"></a>Revisar las directivas existentes

Puesto que la gobernanza es un proceso en curso, las directivas deben revisarse regularmente con el personal de TI y las partes interesadas a fin de garantizar que los recursos hospedados en la nube sigan cumpliendo los requisitos y objetivos corporativos generales. Si entiende en qué consisten los nuevos riesgos y cuál es la tolerancia aceptable para su negocio, podrá mejorar la [revisión de las directivas existentes](./cloud-policy-review.md), a fin de determinar el nivel de gobernanza requerido más apropiado para su organización.

> [!TIP]
> Si la organización usa proveedores u otros socios comerciales de confianza, uno de los mayores riesgos empresariales que se debe tener en cuenta puede ser la falta de [cumplimiento normativo](./regulatory-compliance.md) por parte de estas organizaciones externas. Generalmente, este riesgo no se puede corregir y, en cambio, puede requerir un cumplimiento estricto de los requisitos por parte de todos los interesados. Asegúrese de identificar y entender los requisitos de cumplimiento de terceros antes de comenzar a revisar las directivas.

## <a name="create-cloud-policy-statements"></a>Creación de declaraciones de directiva en la nube

Las directivas de TI basadas en la nube establecen los requisitos, estándares y objetivos que su personal de TI y los sistemas automatizados deberán cumplir. Las decisiones de directiva son el factor principal del [diseño de la arquitectura en la nube](./governance-alignment.md) y para decidir cómo implementar los [procesos de cumplimiento de la directiva](./processes.md).

Cada declaración de directiva de nube es una guía para abordar los riesgos específicos identificados durante el proceso de evaluación de riesgos. Aunque estas directivas se pueden integrar en la documentación de directivas corporativas general, las declaraciones de directivas en la nube tratadas en la guía del Marco de adopción de la nube suelen ser un resumen más conciso de los riesgos y los planes para corregirlos. Cada definición debe incluir estos fragmentos de información:

- **Riesgo empresarial**: Un resumen del riesgo que esta directiva abordará.
- **Declaración de directiva**: Una explicación concisa de los objetivos y los requisitos de la directiva.
- **Diseño u orientación técnica:** Recomendaciones prácticas, especificaciones u otras guías para respaldar y aplicar esta directiva que los desarrolladores y equipos de TI pueden utilizar para diseñar y crear sus implementaciones en la nube.

Si necesita ayuda para empezar a definir directivas, consulte las [materias de gobernanza](../governance-disciplines.md) presentadas en la información general de la sección de gobernanza. Los artículos de cada una de estas materias incluyen ejemplos de riesgos empresariales comunes detectados al realizar la migración a la nube y directivas de ejemplo usadas para corregir tales riesgos (por ejemplo, vea las [definiciones de directivas de ejemplo](../cost-management/policy-statements.md) de la materia de administración de costos).

## <a name="incremental-governance-and-integrating-with-existing-policy"></a>Gobernanza incremental e integración con la directiva existente

Las adiciones planeadas al entorno de nube siempre deben analizarse para garantizar su cumplimiento con la directiva existente, y también es necesario actualizar la directiva para tener en cuenta todos los problemas que aún no se han detectado. También debe realizar una [revisión de la directiva en la nube](./cloud-policy-review.md) periódica para asegurarse de que dicha directiva está actualizada y sincronizada con cualquier nueva directiva corporativa.

La necesidad de integrar la directiva en la nube con las directivas de TI heredadas depende en gran medida de la madurez de los procesos de gobernanza en la nube y del tamaño de su entorno de nube. Consulte el artículo sobre la [gobernanza incremental y el MVP de la directiva](./index.md) para obtener una explicación más amplia sobre cómo tratar la integración de una directiva durante la transformación de la nube.

## <a name="next-steps"></a>Pasos siguientes

Después de definir las directivas, elabore una guía de diseño de la arquitectura para ofrecer instrucciones prácticas a los desarrolladores y al personal de TI.

> [!div class="nextstepaction"]
> [Alinee la guía de diseño de gobernanza con las directivas corporativas](./governance-alignment.md)
