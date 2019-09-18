---
title: Ejemplos de resultados fiscales
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Ejemplos de resultados fiscales
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: strategy
ms.custom: governance
ms.openlocfilehash: ac62364b6117e4744b0432a5c4fbb46b7ee914b8
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031764"
---
# <a name="examples-of-fiscal-outcomes"></a>Ejemplos de resultados fiscales

En el nivel superior, las conversaciones fiscales constan de tres conceptos básicos:

- **Ingresos**: ¿entrará más dinero en la empresa como resultado de las ventas de bienes o servicios?
- **Costo**: ¿se dedicará menos dinero a la creación, el marketing, las ventas o la entrega de bienes o servicios?
- **Beneficio**: aunque es poco habitual, algunas transformaciones pueden aumentar los ingresos y reducir los costos. Este es un resultado de beneficios.

En el resto de este artículo se explican estos resultados fiscales en el contexto de una transformación a la nube.

> [!NOTE]
> Los ejemplos siguientes son hipotéticos y no se deben considerar como una garantía de rendimientos al adoptar cualquier estrategia de nube.

## <a name="revenue-outcomes"></a>Resultados de ingresos

### <a name="new-revenue-streams"></a>Nuevos flujos de ingresos

La nube ayuda a crear oportunidades de entrega de nuevos productos a los clientes o de entrega de productos ya existentes de nuevas maneras. Los nuevos canales de ingresos son innovadores, emprendedores y emocionantes para muchas personas del mundo empresarial. Pero también son propensos a errores y en muchas compañías se consideran de alto riesgo. Cuando el equipo de TI propone resultados relacionados con los ingresos, es probable que haya resistencia. Para dar mayor credibilidad a estos resultados, colabore con líderes empresariales que hayan demostrado ser innovadores. La validación de la fuente de ingresos al principio del proceso le ayudará a evitar los escollos del negocio.

- **Ejemplo**: Una compañía lleva más de 100 años vendiendo libros. Un empleado de la empresa se da cuenta de que el contenido se puede enviar electrónicamente. Este empleado crea un dispositivo que se puede vender en la librería, que permite descargar los mismos libros directamente. Esto supone un aumento de X euros en la venta de libros.

### <a name="revenue-increases"></a>Aumento de ingresos

Gracias a la escala global y a la presencia digital, la nube ayuda a las empresas a aumentar los ingresos procedentes de los canales de ingresos existentes. Con frecuencia, este tipo de resultado procede de una alineación con la dirección de marketing o ventas.

- **Ejemplo**: Una compañía que vende widgets podría vender más si los vendedores pudieran acceder de forma segura al catálogo digital y los niveles de existencias de la compañía. Por desgracia, esos datos solo se encuentran en el sistema ERP de la compañía, al que solo se puede acceder mediante un dispositivo conectado a la red. La creación de una fachada de servicio que sirva de interfaz con ERP, de forma que se exponga el catálogo y los niveles de existencias no confidenciales en una aplicación en la nube, permitiría al personal de ventas acceder a los datos que necesitan mientras se encuentran en las instalaciones de un cliente. La extensión de Active Directory con Azure Active Directory (Azure AD) y la integración del acceso basado en rol en la aplicación permitirían a la compañía garantizar la seguridad de los datos. Este sencillo proyecto podría afectar un _X %_ a los ingresos de una línea de productos existente.

### <a name="profit-increases"></a>Aumento de beneficios

Raro es que un único esfuerzo aumente los ingresos y reduzca los costos simultáneamente. Sin embargo, cuando lo haga, alinee los informes de resultados de uno o varios resultados de ingresos con uno o varios de los resultados de costos para comunicar el resultado deseado.

## <a name="cost-outcomes"></a>Resultados de costos

### <a name="cost-reduction"></a>Reducción de costos

La informática en la nube puede reducir los gastos de capital del hardware y el software, la configuración de centros de datos, el funcionamiento de centros de datos locales in situ, etc. Los costos de los bastidores de servidores, el suministro eléctrico ininterrumpido para alimentación y refrigeración y los expertos de TI que administran la infraestructura los aumentan rápidamente. Apagar un centro de datos puede reducir los gastos de capital. A esto se le conoce normalmente como "salir del negocio del centro de datos". La reducción de los costos se mide normalmente en dólares en el presupuesto actual, que puede abarcar de 1 a 5 años, según cómo administre las finanzas el director financiero (CFO).

- **Ejemplo 1**: El centro de datos de una compañía gasta un gran porcentaje del presupuesto de TI anual. El departamento de TI decide ejecutar una migración a la nube y traslada los recursos del centro de datos a soluciones de infraestructura como servicio (IaaS), de forma que se crea una reducción de costos de 3 años.
- **Ejemplo 2**: Una sociedad de cartera ha adquirido recientemente una nueva compañía. En la adquisición, los términos dictaminan que la nueva entidad se debe retirar de los centros de datos actuales en un plazo de 6 meses. Si no lo hace, deberá pagar una multa de 1 millón de euros al mes a la sociedad de cartera. Mover los recursos digitales a la nube mediante una migración podría permitir una rápida retirada de los recursos antiguos.
- **Ejemplo 3**: Una compañía de impuestos de renta que atiende a consumidores obtiene un 70 % de sus ingresos anuales durante los tres primeros meses del año. El resto del año, su enorme inversión en TI permanece relativamente inactiva. Una migración a la nube permitiría al equipo de TI implementar la capacidad de proceso y hospedaje necesaria para esos tres meses. Durante los nueve meses restantes, se podrían rebajar considerablemente los costos de IaaS mediante la reducción de la superficie de proceso.

### <a name="example-coverdell"></a>Ejemplo: Coverdell

Coverdell moderniza su infraestructura para impulsar el ahorro en los costos de registro con Azure. La decisión de Coverdell de invertir en Azure y de unir su red de sitios web, aplicaciones, datos e infraestructura dentro de este entorno, les condujo a unos ahorros en los costos mayores de lo que jamás habrían esperado. La migración a un entorno solo de Azure eliminó 54 000 dólares USD en costos mensuales por servicios de ubicación. Solo con la nueva infraestructura unida de la compañía, Coverdell espera ahorrar casi 1 millón de dólares durante los próximos 2 o 3 años.

> "Tener acceso a la pila de tecnología de Azure abre la puerta a soluciones escalables, fáciles de implementar y con una gran disponibilidad que son rentables. Así nuestros arquitectos pueden ser mucho más creativos con las soluciones que proporcionan".  
> Ryan Sorensen  
> Director de desarrollo de aplicaciones y arquitectura empresarial  
> Coverdell

### <a name="cost-avoidance"></a>Prevención de costos

La terminación de los centros de datos también proporciona prevención de costos al impedir futuros ciclos de actualizaciones. Un ciclo de actualización es el proceso de comprar nuevo hardware y software para reemplazar los sistemas antiguos locales. En Azure, el hardware y el sistema operativo reciben habitualmente mantenimiento, revisiones y actualizaciones sin costo adicional para los clientes. De esta manera, el director financiero puede eliminar los gastos futuros planeados de las previsiones financieras a largo plazo. La prevención de costos se mide en dólares. Se diferencia de la reducción de costos en que normalmente se centra en un presupuesto futuro que aún no se ha aprobado completamente.

- **Ejemplo**: El centro de datos de una compañía está pendiente de una renovación del alquiler en 6 meses. El centro de datos ha estado en servicio durante ocho años. Hace 4 años, todos los servidores se actualizaron y virtualizaron, lo que supuso un costo para la compañía de millones de dólares. El próximo año, la compañía planea actualizar de nuevo el hardware y el software. La migración de los recursos de ese centro de datos, como parte de una migración a la nube, permitiría una prevención de costos al eliminar la actualización planeada del presupuesto previsto para el próximo año. También podría generar una reducción de los costos, ya que se reducen o eliminan los costos de arrendamiento de bienes inmuebles.

### <a name="capital-expenses-vs-operating-expenses"></a>Gastos de capital en comparación con los gastos operativos

Antes de analizar los resultados de costos, es importante comprender las dos opciones de costo principales: gastos de capital y gastos operativos.

Los siguientes términos le ayudarán a comprender las diferencias entre los gastos de capital y los gastos operativos durante los debates empresariales sobre un proceso de transformación.

- **Capital** es el dinero o los activos que pertenecen a una empresa y que contribuyen a un propósito en particular, como aumentar la capacidad del servidor o crear una aplicación.
- Los **gastos de capital** generan beneficios durante un largo período. Estos gastos no son recurrentes por lo general y dan lugar a la adquisición de activos permanentes. La creación de una aplicación podría calificarse como gasto de capital.
- Los **gastos operativos** son los costos continuos que resultan de la actividad de la empresa. El consumo de servicios en la nube en un modelo de pago por uso se podría considerar como gasto operativo.
- Los **activos** son recursos económicos que se pueden tener o controlar para generar valor. Los servidores, lagos de datos y aplicaciones podrían considerarse activos.
- La **depreciación** es una reducción del valor de un activo con el paso del tiempo. Más importante para el debate entre gastos de capital y gastos operativos, es ver cómo los costos de un activo se asignan en los períodos en los que se usan. Por ejemplo, si crea una aplicación este año, pero se espera que tenga una vida útil de 5 años (como la mayoría de las aplicaciones comerciales), el costo del equipo de desarrollo y de las herramientas necesarias para crear e implementar la base de código se depreciaría uniformemente durante cinco años.
- **Valoración** es el proceso de estimar qué valía tiene una compañía. En la mayoría de los sectores, la valoración se basa en la capacidad de la compañía para generar ingresos y beneficios, y respetar al mismo tiempo los costos operativos necesarios para crear los bienes que proporcionan ese ingreso. En otros sectores, como el del comercio minorista, o en algunos tipos de transacción como el capital privado, los activos y la depreciación pueden jugar un papel muy importante en la valoración de la compañía.

A menudo resulta una apuesta segura que distintos ejecutivos, incluido el jefe de inversiones (CIO), analicen el mejor uso del capital para hacer crecer la compañía en la dirección deseada. Dar al jefe de inversiones los medios para convertir conversaciones polémicas sobre gastos de capital en una clara rendición de cuentas de gastos operativos podría ser un atractivo resultado en sí mismo. En muchos sectores, los directores financieros buscan activamente formas de asociar mejor la responsabilidad fiscal con el costo de los bienes vendidos.

Sin embargo, antes de asociar cualquier proceso de transformación con este tipo de conversión de gastos de capital a gastos operativos, es aconsejable reunirse con los miembros de los equipos de CFO o CIO para ver qué estructura de costos prefiere la empresa. En algunas organizaciones, la reducción de los gastos de capital en favor de los gastos operativos es un resultado *no deseado*. Como se mencionó anteriormente, este enfoque se observa a veces en el comercio minorista, las sociedades de cartera y las compañías de capital privado que otorgan un gran valor a los modelos tradicionales de contabilidad de activos fijos y muy poco al protocolo de Internet. También se observa en organizaciones que han tenido experiencias negativas al subcontratar personal de TI u otras funciones en el pasado.

Si el modelo de gastos operativos es deseable, el ejemplo siguiente podría ser un resultado empresarial viable:

- **Ejemplo**: El centro de datos de la compañía se está depreciando actualmente a _x USD_ al año durante los 3 años siguientes. Se espera que se necesiten _Y dólares USD_ adicionales para actualizar el hardware el próximo año. Se pueden convertir todos esos gastos de capital en un modelo de gastos operativos con un índice constante de _Z dólares USD_ al mes, lo que permite una mejor administración y contabilidad de los costos de funcionamiento de la tecnología.

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre [resultados de agilidad](./agility-outcomes.md).

> [!div class="nextstepaction"]
> [Resultados de agilidad](./agility-outcomes.md)
