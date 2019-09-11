---
title: Preparación de la directiva de TI corporativa para la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Explicación del concepto de directivas corporativas en relación con la gobernanza en la nube.
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: e86eb3408b635eac7c299ae594999ddf619ab81e
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70816795"
---
<!-- markdownlint-disable MD026 -->

# <a name="prepare-corporate-it-policy-for-the-cloud"></a>Preparación de la directiva de TI corporativa para la nube

La gobernanza de la nube es producto de un esfuerzo continuo de adopción a lo largo del tiempo, ya que una verdadera transformación duradera no ocurre de la noche a la mañana. Si intenta ofrecer una gobernanza integral de la nube antes de abordar los cambios clave de las directivas corporativas mediante un método rápido y agresivo, rara vez conseguirá los resultados deseados. En su lugar, le recomendamos que aplique un método incremental.

Lo que diferencia a Cloud Adoption Framework es el ciclo de compra y cómo esto puede permitirle realizar una transformación auténtica. Puesto que no es necesario cumplir con un requisito excesivo de adquisición de gastos de capital, los ingenieros pueden comenzar el proceso de experimentación y adopción mucho antes. En la mayoría de las culturas corporativas, la eliminación de la barrera de los gastos de capital para la adopción puede llevar a ciclos que ofrecen comentarios más precisos, un crecimiento orgánico y una ejecución incremental.

El cambio a la adopción de la nube requiere realizar un cambio en la gobernanza. Por ello, en muchas organizaciones, la transformación de las directivas corporativas les permite alcanzar una gobernanza mejor y mayores tasas de cumplimiento gracias a los cambios realizados en las directivas incrementales y a la aplicación automática de esos cambios, impulsada gracias a las capacidades recién definidas que debe configurar con su proveedor de servicios en la nube.

En este artículo se describen las actividades clave que le ayudarán a configurar las directivas corporativas para habilitar un modelo de gobernanza ampliado.

## <a name="define-corporate-policy-to-mature-cloud-governance"></a>Definir las directivas corporativas para perfeccionar la gobernanza de la nube.

En la gobernanza tradicional y en la incremental, las directivas corporativas crean la definición del trabajo de gobernanza. La mayoría de las acciones de gobernanza de TI buscan implementar tecnología para supervisar, aplicar, usar y automatizar esas directivas corporativas. La gobernanza de la nube se basa en conceptos similares.

![Gobernanza corporativa y disciplinas de gobernanza](../../_images/operational-transformation-govern-highres.png)

*Figura 1: Gobernanza corporativa y disciplinas de gobernanza.*

Para poder crear una estrategia de gobernanza, en la imagen anterior se muestran las interacciones entre el riesgo de negocios, las directivas y el cumplimiento, y la opción de supervisar y exigir. A continuación, verá las cinco materias de gobernanza en la nube para crear la estrategia.

## <a name="review-existing-policies"></a>Revisar las directivas existentes

En la imagen de arriba, la estrategia de gobernanza (riesgo, directivas y cumplimiento, supervisar y exigir) comienza con el reconocimiento de los riesgos del negocio. Descubrir cómo cambian [los riesgos de negocio](understanding-business-risk.md) en la nube es el primer paso para crear una estrategia duradera de gobernanza en la nube. Debe trabajar con sus unidades de negocio para obtener un [medidor preciso de la tolerancia de riesgo que tiene el negocio](risk-tolerance.md); gracias a ello, podrá comprender qué nivel de riesgo se debe corregir. Si entiende en qué consisten los nuevos riesgos y cuál es la tolerancia aceptable para su negocio, podrá mejorar la [revisión de las directivas existentes](what-is-a-cloud-policy-review.md), a fin de determinar el nivel de gobernanza requerido más apropiado para su organización.

> [!TIP]
> Si su organización se rige en función del cumplimiento de directivas de terceros, uno de los mayores riesgos de negocios a considerar puede ser el riesgo que supone el [cumplimiento normativo](what-is-regulatory-compliance.md). Generalmente este riesgo no se puede corregir y, en cambio, puede requerir una adherencia estricta. Asegúrese de entender los requisitos de cumplimiento de terceros antes de comenzar a revisar las directivas.

## <a name="an-incremental-approach-to-cloud-governance"></a>Enfoque incremental para la gobernanza de la nube

El enfoque incremental para la gobernanza de la nube asume que no se puede superar la [tolerancia de riesgo de la empresa](risk-tolerance.md). En su lugar, asume que la función de gobernanza consiste en acelerar el cambio comercial, ayudar a los ingenieros a entender las pautas de la arquitectura y asegurar que los [riesgos de negocio](understanding-business-risk.md) se notifican y corrigen regularmente. Alternativamente, el rol tradicional de gobernanza puede convertirse en un obstáculo para que los ingenieros o la empresa en general puedan realizar la adopción.

Debido a un enfoque incremental de la gobernanza de la nube, a veces hay una fricción natural entre los equipos que crean nuevas soluciones de negocios y los que protegen el negocio de los riesgos. Sin embargo, gracias a este modelo, esos dos equipos pueden convertirse en compañeros que trabajan tanto en incrementos o en sprints. Ahora que son compañeros, el equipo de gobernanza en la nube y los equipos de adopción de la nube comienzan a trabajar juntos para exponer, evaluar y corregir los riesgos del negocio. Todo este esfuerzo puede crear un medio natural para reducir la fricción y mejorar la colaboración entre equipos.

## <a name="minimum-viable-product-mvp-for-policy"></a>Producto mínimo viable (MVP) para las directivas

El primer paso a dar cuando se surge una asociación emergente entre sus equipos de gobernanza y adopción en la nube, es crear un acuerdo con respecto a la directiva de MVP. Su MVP para la gobernanza de la nube debe reconocer que los riesgos del negocio pueden ser pequeños al principio, pero es probable que crezcan a medida que su organización adopte más servicios en la nube con el tiempo.

Por ejemplo, el riesgo para el negocio es pequeño para un negocio que implementa cinco máquinas virtuales que no contienen datos de alto impacto para el negocio (HBI). Más adelante en el proceso de adopción de la nube, cuando el número alcance las 1 000 máquinas virtuales y el negocio empiece a mover datos HBI, aumentará el riesgo empresarial.

MVP de directivas intenta definir una base requerida para las directivas necesarias para implementar las primeras _x_ máquinas virtuales o las primeras _x_ número de aplicaciones, donde _x_ es una pequeña aunque significativa cantidad de las unidades que se van a adoptar. Este conjunto de directivas requiere pocas restricciones, pero debe contener los aspectos fundamentales necesarios para poder crecer rápidamente de un incremento de esfuerzo de adopción de la nube a otro. Gracias al desarrollo incremental de directivas, esta estrategia de gobernanza crecerá con el tiempo. A través de cambios sutiles y constantes, el MVP de la directiva crecerá en paridad de características con los resultados del ejercicio de revisión de directivas.

## <a name="incremental-policy-growth"></a>Crecimiento incremental de la directiva

El crecimiento incremental de las directivas es el mecanismo clave para aumentar las directivas y la gobernanza en la nube a lo largo del tiempo. También es el requisito clave para adoptar un modelo incremental de gobernanza. Para que este modelo funcione bien, el equipo de gobernanza debe comprometerse a realizar asignaciones continuas de tiempo en cada sprint, a fin de evaluar e implementar las disciplinas cambiantes de la gobernanza.

**Requisitos de tiempo del sprint:** Al comienzo de cada iteración, cada equipo de adopción de la nube crea una lista de recursos que se van a migrar o adoptar en el incremento actual. Se supone que el equipo de gobernanza en la nube debe otorgar el tiempo suficiente para revisar la lista, validar las clasificaciones de datos de los recursos, evaluar los nuevos riesgos asociados a cada recurso, actualizar las pautas de la arquitectura e informar al equipo de los cambios. Estos compromisos comúnmente necesitan entre 10 y 30 horas por sprint. También se espera que este nivel de participación requiera al menos un empleado dedicado a administrar la gobernanza; este empleado realizará un gran esfuerzo de adopción de la nube.

**Requisitos de tiempo de lanzamiento:** Al comienzo de cada versión, los equipos de adopción de la nube y el equipo de estrategia en la nube deben priorizar una lista de aplicaciones o cargas de trabajo que se migrarán en la iteración actual, junto con las actividades de cambio de negocio. Esos puntos de datos permiten que el equipo de gobernanza en la nube entienda los nuevos riesgos del negocio antes. Gracias a ello, los equipos tienen tiempo suficiente para ponerse al día con el negocio y medir la tolerancia de ese negocio en cuanto a los posibles riesgos.

## <a name="next-steps"></a>Pasos siguientes

Una estrategia eficaz de gobernanza en la nube empieza por conocer el riesgo empresarial.

> [!div class="nextstepaction"]
> [Descripción del riesgo empresarial](./understanding-business-risk.md)
