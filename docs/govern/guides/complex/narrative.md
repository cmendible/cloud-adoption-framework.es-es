---
title: 'Guía de gobernanza para empresas complejas: Narrativa de apoyo'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Este artículo establece un caso de uso de gobernanza durante el recorrido de adopción de la nube de una empresa compleja.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 0d1aaa76f36125819ebb8f5c6225dc74bb60aabf
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031741"
---
# <a name="governance-guide-for-complex-enterprises-the-supporting-narrative"></a>Guía de gobernanza para empresas complejas: Narrativa de apoyo

El siguiente artículo establece un caso de uso de [gobernanza durante el recorrido de adopción de la nube de una empresa grande](./index.md). Antes de actuar sobre las recomendaciones de la guía, es importante comprender las suposiciones y los razonamientos que se reflejan en esta narrativa. Solo entonces podrá alinear mejor la estrategia de gobernanza con el recorrido de adopción de la nube de su propia organización.

## <a name="back-story"></a>Antecedentes

Los clientes exigen una mejor experiencia al interactuar con esta empresa. La experiencia actual ha causado la erosión del mercado y ha llevado a la junta a contratar a un director ejecutivo de tecnología digital (CDO). El CDO trabaja con marketing y ventas para impulsar una transformación digital que potenciará las experiencias mejoradas. Además, varias unidades de negocio contrataron recientemente a científicos de datos para las granjas de datos y para mejorar muchas de las experiencias manuales mediante el aprendizaje y la predicción. TI apoya estos esfuerzos en la medida de lo posible. Sin embargo, se están llevando a cabo actividades de "TI en la sombra" que quedan fuera de los controles de gobernanza y seguridad necesarios.

La organización de TI también se enfrenta a sus propios retos. Finanzas está planeando reducciones continuas en el presupuesto de TI durante los próximos cinco años, lo que llevará a algunos recortes de gastos necesarios a partir de este año. Por el contrario, los requisitos de RGPD y otros requisitos de gobierno de datos están obligando a TI a invertir en recursos en otros países para localizar datos. Dos de los centros de datos existentes están atrasados en la actualización de hardware, lo que causa más problemas con la satisfacción de los empleados y los clientes. Tres centros de datos más requieren actualizaciones de hardware durante la ejecución del plan quinquenal. El CFO está presionando al CIO para que considere la nube como una alternativa para esos centros de datos, con objeto de liberar gastos de capital.

El CIO tiene ideas innovadoras que podrían ayudar a la empresa, pero él y sus equipos se limitan a apagar fuegos y controlar costos. En un almuerzo con el CDO y uno de los responsables de la unidad de negocios, la conversación sobre la migración a la nube generó el interés de los compañeros del CIO. El objetivo de los tres responsables es apoyarse mutuamente en el uso de la nube para alcanzar sus objetivos de negocio, y han comenzado las fases de exploración y planeación de la adopción de la nube.

## <a name="business-characteristics"></a>Características empresariales

La empresa tiene el siguiente perfil de negocio:

- Las ventas y operaciones abarcan varias áreas geográficas con clientes globales en múltiples mercados.
- El negocio ha crecido mediante adquisiciones y opera en tres unidades de negocio basadas en la base de clientes objetivo. La realización de presupuestos es una matriz compleja que abarca todas las unidades de negocio y funciones.
- La empresa considera la mayor parte de la TI como una fuga de capital o un centro de coste.

## <a name="current-state"></a>Estado actual

A continuación se muestra el estado actual de las operaciones de TI y de la nube de la empresa:

- TI opera más de 20 centros de datos privados en todo el mundo.
- Debido al crecimiento orgánico y a varias zonas geográficas, hay algunos equipos de TI que tienen requisitos únicos de soberanía de datos y cumplimiento que afectan a una sola unidad de negocio que funciona dentro de una zona geográfica específica.
- Cada centro de datos está conectado por una serie de líneas regionales alquiladas, que crean una WAN global sin conexión directa.
- El departamento de TI entró en la nube al migrar todas las cuentas de correo electrónico de los usuarios finales a Office 365. Esta migración se completó hace más de seis meses. Desde entonces, solo se han implementado unos pocos recursos de TI en la nube.
- El equipo de desarrollo principal del CDO está trabajando en una capacidad de desarrollo y pruebas para aprender sobre las funcionalidades nativas en la nube.
- Una unidad de negocio está experimentando con grandes cantidades de datos en la nube. El equipo de la unidad de negocio dentro de TI participa en ese esfuerzo.
- La actual directiva de gobernanza de TI establece que la información personal del cliente y los datos financieros se deben hospedar en recursos que pertenecen directamente a la empresa. Esta directiva bloquea la adopción de la nube para cualquier aplicación crítica o con datos protegidos.
- Las inversiones en TI están controladas en gran medida por el gasto de capital. Estas inversiones se planean anualmente y a menudo incluyen planes de mantenimiento continuo, así como ciclos de actualización establecidos de tres a cinco años, dependiendo del centro de datos.
- La mayoría de las inversiones en tecnología que no se alinean con el plan anual se abordan con los trabajos de TI en la sombra. Estos esfuerzos suelen estar administrados por las unidades de negocio y financiarse mediante los gastos operativos de la unidad de negocio.

## <a name="future-state"></a>Estado futuro

Se prevén los siguientes cambios para los próximos años:

- El CIO está liderando un esfuerzo para modernizar la directiva sobre la información personal y los datos financieros para apoyar los objetivos futuros. Dos miembros del equipo de gobernanza de TI tienen visibilidad de este esfuerzo.
- El CIO quiere usar la migración a la nube como una función de impulso para mejorar la coherencia y la estabilidad entre las unidades de negocio y las zonas geográficas. Sin embargo, el estado futuro debe respetar cualquier requisito de cumplimiento externo que requiera la desviación de los enfoques estándar de los equipos de TI específicos.
- Si los primeros experimentos en el desarrollo de aplicaciones y en la unidad de negocio muestran indicadores de éxito, a cada uno de ellos les gustaría lanzar soluciones de producción a pequeña escala a la nube en los próximos 24 meses.
- El CIO y el CFO han asignado un arquitecto y al vicepresidente de infraestructura para crear un análisis de costos y un estudio de viabilidad. Estos esfuerzos determinarán si la empresa puede y debe mover 5000 recursos a la nube en los próximos 36 meses. Una migración correcta permitiría al CIO eliminar dos centros de datos, con lo que se reducen los costos en más de 100 millones de dólares durante el plan quinquenal. Si tres o cuatro centros de datos pueden experimentar resultados similares, el presupuesto volverá a la senda de los beneficios, lo que permitirá que el presupuesto del CIO apoye iniciativas más innovadoras.
    ![Costos locales frente a los costos de Azure, que muestran un beneficio de 100 millones de dólares en los próximos cinco años](../../../_images/govern/calculator-enterprise.png)
- Junto con este ahorro de costos, la empresa planea cambiar la administración de algunas inversiones en TI cambiando la posición del gasto de capital comprometido como un gasto operativo dentro de TI. Este cambio proporcionará un mayor control de los costos, que la TI puede utilizar para acelerar otros esfuerzos previstos.

## <a name="next-steps"></a>Pasos siguientes

La empresa ha desarrollado una directiva corporativa para dar forma a la implementación de la gobernanza. La directiva corporativa dirige muchas de las decisiones técnicas.

> [!div class="nextstepaction"]
> [Revisión de la directiva corporativa inicial](./initial-corporate-policy.md)
