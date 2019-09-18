---
title: 'Guía para empresa estándar: La narrativa detrás de la estrategia de gobernanza'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Este artículo establece un caso de uso de gobernanza durante el recorrido de adopción de la nube de una empresa estándar.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 434a4d0238a4633210d31013e9787c3a0a92fc7a
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032350"
---
# <a name="standard-enterprise-guide-the-narrative-behind-the-governance-strategy"></a>Guía para empresa estándar: La narrativa detrás de la estrategia de gobernanza

La narrativa siguiente describe un caso de uso de gobernanza durante el [recorrido de adopción de la nube de una empresa estándar](./index.md). Antes de implementar el recorrido, es importante comprender las suposiciones y los razonamientos que se reflejan en esta descripción. Solo entonces podrá alinear mejor la estrategia de gobernanza con el recorrido de su propia organización.

## <a name="back-story"></a>Historia retrospectiva

La junta directiva comenzó el año con planes para dinamizar el negocio de varias maneras. Están impulsando el liderazgo para mejorar las experiencias de los clientes y ganar cuota de mercado. También están apostando por nuevos productos y servicios que posicionarán a la compañía como líder indiscutible del sector. Asimismo, iniciaron un esfuerzo paralelo para reducir los desperdicios y los costos innecesarios. Aunque pueden ser intimidantes, las acciones que la junta quiere llevar a cabo y su liderazgo muestran que el propósito de invertir la mayor cantidad de capital posible está enfocado a conseguir un crecimiento futuro.

En el pasado, el Director de sistemas de información de la empresa había sido excluido de estas conversaciones estratégicas. Sin embargo, debido a que la visión de futuro está intrínsecamente vinculada al crecimiento técnico, el departamento de TI tiene un lugar en la mesa para aportar sus ideas en estos grandes planes. Así pues, se espera que el departamento de TI ofrezca nuevas formas de crecimiento. De todos modos, el equipo no está preparado para estos cambios y es probable que tenga problemas con la curva de aprendizaje.

## <a name="business-characteristics"></a>Características empresariales

La empresa tiene el siguiente perfil de negocio:

- Todas las ventas y operaciones residen en un solo país, lo que supone un bajo porcentaje de clientes globales.
- El negocio funciona como una sola unidad de negocio y cuenta con un presupuesto alineado a las funciones, entre las que se incluyen los departamentos de Ventas, Marketing, Operaciones y TI.
- La empresa considera la mayor parte del departamento de TI como una fuga de capital o un centro de coste.

## <a name="current-state"></a>Estado actual

A continuación se muestra el estado actual de las operaciones de TI y de la nube de la empresa:

- El departamento de TI operaba en dos entornos de infraestructura hospedados. Un entorno contiene activos de producción. El segundo entorno contiene la opción de recuperación ante desastres y algunos recursos de desarrollo y prueba. Estos entornos se hospedan en dos proveedores diferentes. El departamento de TI se refiere a estos dos centros de datos como Prod y DR, respectivamente.
- Asimismo, el departamento de TI entró en la nube al migrar todas las cuentas de correo electrónico de los usuarios finales a Office 365. Esta migración se completó hace seis meses. Desde entonces, solo se han implementado unos pocos recursos de TI en la nube.
- Los equipos de desarrollo de aplicaciones están trabajando en una capacidad de desarrollo y prueba para aprender más sobre las funcionalidades nativas de la nube.
- El equipo de inteligencia empresarial (BI) está experimentando con los macrodatos en la nube y la protección de datos en nuevas plataformas.
- La empresa tiene una directiva definida de manera general que indica que la información personal del cliente y los datos financieros no se pueden hospedar en la nube, lo que limita las aplicaciones críticas en las implementaciones actuales.
- Las inversiones en TI están controladas en gran medida por el gasto de capital. Además, esas inversiones se planifican anualmente. En los últimos años, en las inversiones se ha incluido poco más que los requisitos básicos de mantenimiento.

## <a name="future-state"></a>Estado futuro

Se prevén los siguientes cambios para los próximos años:

- El Director de sistemas de información está revisando la directiva sobre información personal y datos financieros para poder llevar a cabo los futuros objetivos de estado.
- Los equipos de desarrollo de aplicaciones y de BI quieren ponerse a producir y lanzar soluciones basadas en la nube en los próximos 24 meses, según el objetivo para atraer clientes y ofrecer nuevos productos.
- Este año, el equipo de TI terminará de retirar las cargas de trabajo de recuperación ante desastres del centro de datos de DR al migrar 2000 máquinas virtuales a la nube. Se espera que esto produzca un ahorro de costos estimado de 25 millones de USD en los próximos cinco años.
    ![Costos locales frente a costos de Azure que muestran un beneficio de 25 millones de USD en los próximos cinco años](../../../_images/govern/calculator-small-to-medium-enterprise.png)
- Debido a esto, la empresa planea cambiar la forma en que realiza las inversiones en TI cambiando la posición del gasto de capital comprometido, que se ha establecido como un gasto operativo dentro del departamento de TI. Este cambio proporcionará un mayor control de los costos, y permitirá que el departamento de TI pueda acelerar otros esfuerzos previstos.

## <a name="next-steps"></a>Pasos siguientes

La empresa ha desarrollado una directiva corporativa para dar forma a la implementación de la gobernanza. La directiva corporativa dirige muchas de las decisiones técnicas.

> [!div class="nextstepaction"]
> [Revisión de la directiva corporativa inicial](./initial-corporate-policy.md)
