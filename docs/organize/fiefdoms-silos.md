---
title: Islas y feudos
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Comprenda los antipatrones de islas y feudos.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 170054f07cb7e8282b3abd582e484a730aca1280
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71032052"
---
# <a name="organizational-antipatterns-silos-and-fiefdoms"></a>Antipatrones de la organización: Islas y feudos

El éxito de cualquier cambio importante en las prácticas empresariales, la cultura o las operaciones tecnológicas requiere una mentalidad de crecimiento. En el fondo de la mentalidad de crecimiento se encuentra la aceptación del cambio y la capacidad de liderazgo a pesar de la ambigüedad.

Algunos antipatrones pueden bloquear una mentalidad de crecimiento en las organizaciones que quieren crecer y transformarse, como la microadministración, el pensamiento sesgado y las prácticas excluyentes. Muchos de estos bloqueadores son desafíos personales que crean oportunidades de crecimiento personal para todo el mundo. Pero hay dos antipatrones comunes de TI que requieren más que el crecimiento o la madurez individuales: islas y feudos.

![Comparación de equipos sin problemas y antipatrones de la organización](../_images/ready/fiefdom-and-silo.png)

Estos antipatrones son el resultado de cambios orgánicos en varios equipos, lo que da lugar a comportamientos incorrectos de la organización. Para abordar la resistencia causada por cada antipatrón, es importante comprender la causa principal de esta formación.

## <a name="healthy-organic-it-teams"></a>Equipos de TI orgánicos y sin problemas

Es natural crear una división del trabajo en TI. Es recomendable establecer equipos que tengan una experiencia similar, procesos compartidos, un objetivo común y una visión alineada. También es natural que esos equipos tengan su propia microcultura, normas compartidas y perspectivas.

Los equipos de TI sin problemas se centran en asociarse con otros equipos para promover el correcto cumplimiento de sus tareas. Los equipos de TI sin problemas tratan de comprender los objetivos empresariales para los que está diseñada su contribución tecnológica. Los detalles y el impacto fiscal pueden ser aproximados, pero la contribución de valor del equipo suele comprenderse dentro del equipo.

Aunque los equipos de TI sin problemas sienten entusiasmo por la tecnología que apoyan, están abiertos al cambio y dispuestos a probar cosas nuevas. Estos equipos suelen ser los colaboradores más antiguos y fuertes con el trabajo del [centro de excelencia de la nube (CCoE)](./cloud-center-of-excellence.md). Su contribución debe fomentarse intensamente.

### <a name="natural-resistance-to-change"></a>Resistencia natural al cambio

En ocasiones, las microculturas comprendidas en equipos de TI sin problemas pueden reaccionar mal a las decisiones ejecutivas o jerárquicas para impulsar el cambio. Esta reacción es natural, ya que los colectivos de seres humanos con normas compartidas a menudo cooperan para superar las amenazas externas.

Los cambios que afectan al trabajo diario del equipo, la sensación de seguridad o la autonomía pueden verse como un riesgo para el colectivo. Las señales de resistencia son a menudo un indicador temprano de que los miembros del equipo no sienten que formen parte del proceso de toma de decisiones.

Cuando los arquitectos y otros responsables de la nube invierten en erradicar los sesgos personales y en promover la inclusión de los equipos de TI existentes, es probable que esta resistencia disminuya rápidamente y se resuelva con el tiempo. Una herramienta disponible para que arquitectos y responsables de la nube creen una toma de decisiones inclusiva es la formación de un CCoE.

### <a name="healthy-friction"></a>Fricción sin problemas

Es fácil confundir resistencia con fricción. Los equipos de TI existentes pueden tener conocimientos sobre errores del pasado, riesgos tangibles, conocimientos del sector sobre soluciones y deudas técnicas no documentadas. Desafortunadamente, incluso los mejores equipos de TI pueden caer en la trampa de describir estos importantes puntos de datos como parte de una solución técnica específica, que no debe cambiarse. Este enfoque de la comunicación enmascara los conocimientos de los equipos, lo que crea una percepción de resistencia.

Al proporcionar a estos equipos un mecanismo para comunicarse con una terminología de futuro, se agregarán puntos de datos, se identificarán lagunas y se creará una fricción sin problemas en torno a las soluciones propuestas. Esa fricción adicional lijará las aristas de las soluciones e impulsará los valores a largo plazo. Con tan solo cambiar la conversación se puede aumentar la claridad sobre temas complejos y generar energía que se traduzca en mejores soluciones.

La guía sobre la [definición de la directiva corporativa](../govern/corporate-policy.md) tiene por objeto facilitar las conversaciones basadas en el riesgo con las partes interesadas de la empresa. Aunque este mismo modelo se puede usar para facilitar las conversaciones con los equipos que se perciben como antagonistas a la nube. Cuando la percepción de la resistencia esté muy extendida, sería prudente incluir prácticas de resolución de resistencia en los estatutos de un [equipo de gobernanza en la nube](./cloud-governance.md).

## <a name="antipatterns"></a>Antipatrones

El crecimiento orgánico y dinámico en TI que crea equipos de TI sin problemas también puede dar lugar a antipatrones que bloquean la transformación y la adopción de la nube. Las islas y los feudos de TI son distintos de las microculturas naturales presentes en equipos de TI sin problemas. En cualquiera de los dos patrones, el enfoque del equipo tiende a estar dirigido a la protección de su "territorio". Cuando los miembros del equipo se enfrentan a la oportunidad de impulsar el cambio y mejorar las operaciones, invertirán más tiempo y energía en bloquear el cambio que en encontrar una solución positiva.

Como se mencionó anteriormente, los equipos de TI sin problemas pueden crear resistencia natural y fricción positiva. Las islas y los feudos son otro desafío. No se ha documentado ningún indicador adelantado para ninguno de los dos antipatrones. Estos antipatrones tienden a identificarse después de meses de trabajo del [centro de excelencia de la nube](./cloud-center-of-excellence.md) y el [equipo de gobernanza en la nube](./cloud-governance.md). Se detectan como resultado de la resistencia continuada.

Incluso en las culturas tóxicas, el trabajo del CCoE y el equipo de gobernanza en la nube deberían contribuir a impulsar el crecimiento cultural y el progreso técnico. Después de meses de trabajo, es posible que algunos equipos no muestren todavía signos de conductas inclusivas y se mantengan firmes en su resistencia al cambio. Es probable que estos equipos funcionen en uno de los siguientes modelos de antipatrón: islas y feudos. Aunque estos modelos presentan síntomas similares, la causa raíz y los enfoques para resolver la resistencia son radicalmente diferentes entre ellos.

## <a name="it-silos"></a>Islas de TI

Es probable que los miembros del equipo de una isla de TI se definan a sí mismos a través de su alineación con un pequeño número de proveedores de TI o un área de especialización técnica. Aunque no deben confundirse las islas de TI con los feudos de TI. Las islas de TI suelen estar determinadas por la comodidad y el entusiasmo y, por lo general, son más fáciles de superar que los motivos basados en el miedo que subyacen en los feudos.

Este antipatrón suele surgir de un entusiasmo común por una solución concreta. Las islas de TI se ven luego reforzadas por las aptitudes avanzadas del equipo como resultado de la inversión en esa solución específica. Esta aptitud superior puede ser un acelerador del trabajo de adopción en la nube si se puede superar la resistencia a los cambios. También puede convertirse en un bloqueador importante si las islas se dividen o si los miembros del equipo no pueden evaluar con precisión las opciones. Afortunadamente, las islas de TI a menudo se pueden solucionar sin realizar cambios importantes en el organigrama.

### <a name="addressing-resistance-from-it-silos"></a>Resolución de la resistencia de islas de TI

Las islas de TI se pueden solucionar a través de los siguientes enfoques. El mejor enfoque dependerá de la causa raíz de la resistencia.

**Cree equipos virtuales:** La sección sobre [preparación de la organización](./index.md) del marco de adopción de la nube describe una estructura multicapa para integrar y definir cuatro equipos virtuales. Una ventaja de esta estructura es la visibilidad y la inclusión entre organizaciones. La introducción de un [centro de excelencia de la nube](./cloud-center-of-excellence.md) crea un equipo de aspiraciones de alto perfil en el que los mejores ingenieros querrán participar. Esto ayuda a crear nuevas alineaciones entre soluciones que no están limitadas por las restricciones del organigrama y que impulsarán la inclusión de los mejores ingenieros que se encuentran protegidos por islas de TI.

La introducción de un [equipo de estrategia en la nube](./cloud-strategy.md) creará una visibilidad inmediata de las contribuciones de TI en cuanto al trabajo de adopción. Cuando las islas de TI luchan por la separación, esta visibilidad puede ayudar a motivar a los responsables empresariales y de TI para que apoyen adecuadamente a los miembros del equipo que se resisten. Este proceso es una vía rápida para la involucración y el soporte de las partes interesadas.

**Considere la experimentación y la exposición:** Es probable que los miembros de un equipo en una isla de TI se hayan visto obligados a pensar de cierta manera durante algún tiempo. La ruptura con la mentalidad de vía única es un primer paso para resolver la resistencia.

La experimentación y la exposición son herramientas eficaces para derribar barreras de las islas. Es posible que los miembros del equipo sean resistentes a soluciones de la competencia, por lo que no es aconsejable colocarlos a cargo de un experimento que compite con su solución existente. Aunque, como parte de una primera prueba de carga de trabajo de la nube, la organización debe implementar soluciones que compitan entre sí. Debe invitarse al equipo aislado en la isla a participar como origen de entrada y de revisión, pero no como responsable de la toma de decisiones. Esto debe comunicarse claramente al equipo, junto con el compromiso de involucrar al equipo más profundamente como responsable de la toma de decisiones antes de pasar a las soluciones de producción.

Durante la revisión de la solución competitiva, siga las prácticas descritas en la [definición de la directiva corporativa](../govern/corporate-policy.md) para documentar los riesgos tangibles del experimento y establecer directivas que ayuden a que el equipo aislado en la isla se sienta más cómodo con el estado futuro. Esto expondrá al equipo a nuevas soluciones y afianzará la solución futura.

**No se ponga límites:** A los equipos que impulsan la adopción de la nube les resulta fácil forzar los límites explorando nuevas e interesantes soluciones nativas de la nube. Esta es la mitad del enfoque para eliminar los límites. Aunque ese planteamiento puede reforzar aún más las islas de TI. Si se intenta lograr un cambio demasiado rápido sin respetar las culturas existentes, se puede crear una fricción incorrecta y provocar una resistencia natural.

Cuando las islas de TI comienzan a resistirse, es importante no ponerse límites en las propias soluciones. No olvide una sencilla verdad: una solución nativa de la nube no siempre es la mejor. Plantéese utilizar soluciones híbridas que puedan ofrecer la oportunidad de proyectar las inversiones existentes de la isla de TI en el futuro.

Plantéese también usar versiones basadas en la nube de la solución que el equipo de la isla de TI usa ya. Experimente con esas soluciones y expóngase al punto de vista de quienes viven en la isla de TI. Como mínimo, obtendrá una nueva perspectiva. En muchas situaciones, es posible que gane suficiente respeto de la isla de TI como para disminuir la resistencia.

**Invierta en educación:** Muchas de las personas que viven en una isla de TI se entusiasmaron con la solución actual como resultado de la expansión de su propia educación. Invertir en la educación de estos equipos rara vez está fuera de lugar. Asigne tiempo a estas personas para que participen en aprendizaje autodidacta, clases o incluso conferencias que rompan el enfoque del día a día sobre la solución actual.

Para que la educación sea una inversión, es necesario que el gasto genere algún tipo de rendimiento. A cambio de la inversión, el equipo podría mostrar la solución propuesta al resto de los equipos involucrados en la adopción de la nube. También podría facilitar documentación sobre los riesgos tangibles, los enfoques de administración de riesgos y las directivas esperadas en la adopción de la solución propuesta. Cada uno involucrará a estos equipos en la solución y le ayudará a aprovechar sus conocimientos tribales.

**Convierta los muros en baches:** Las islas de TI pueden ralentizar o detener cualquier transformación. La experimentación y la iteración encontrarán salida, pero solo si el proyecto sigue avanzando. Céntrese en convertir los muros en simples baches. Defina directivas con las que todos puedan sentirse temporalmente cómodos a cambio de un progreso continuo.

Por ejemplo, si la seguridad de TI es el obstáculo porque su solución de seguridad no puede supervisar los peligros de los datos protegidos en la nube, establezca directivas de clasificación de datos. Evite la implementación de datos clasificados en la nube hasta que se encuentre una solución aceptable. Invite a la seguridad de TI a la experimentación con soluciones híbridas o nativas de la nube para supervisar los datos protegidos.

Si el equipo de red funciona como una isla, identifique las cargas de trabajo que son autónomas y no tienen dependencias de red. En paralelo, experimente, exponga y enseñe al equipo de red mientras trabaja en soluciones híbridas o alternativas.

**Sea paciente e inclusivo:** Es tentador seguir adelante sin contar con una isla de TI. Pero esta decisión causará interrupciones y presentará obstáculos más adelante. El cambio de mentalidad de los miembros de la isla de TI puede llevar tiempo. Tenga paciencia con su resistencia natural: conviértala en valor. Sea inclusivo e invite a la fricción sin problemas para mejorar la solución futura.

**No compita nunca:** La isla de TI existe por un motivo. Se conserva por un motivo. Existe una inversión en el mantenimiento de la solución que entusiasma a los miembros del equipo. La competencia directa con la solución o la isla de TI distraerá la atención del objetivo real de lograr resultados empresariales. Esta trampa ha bloqueado muchos proyectos de transformación.

Manténgase centrado en el objetivo, y no en un solo componente del objetivo. Contribuya a acentuar los aspectos positivos de la solución de la isla de TI y ayude a los miembros del equipo a tomar decisiones acertadas sobre las mejores soluciones para el futuro. No vaya contra la solución actual, ya que esto sería contraproducente.

**Asóciese a la empresa:** Si la isla de TI no bloquea los resultados empresariales, ¿por qué se preocupa? No existe una solución perfecta ni un proveedor de TI perfecto. La competencia existe por un motivo; cada uno tiene sus propias ventajas.

Adopte la diversidad e incluya la empresa mediante el apoyo y la alineación con un [equipo de estrategia en la nube](./cloud-strategy.md) fuerte. Cuando una isla de TI prefiere una solución que bloquea los resultados empresariales, será más fácil comunicar ese obstáculo sin el ruido de las disputas técnicas. El apoyo a islas de TI sin pegas mostrará la posibilidad de asociar los resultados empresariales esperados. Este trabajo conseguirá un mayor respeto y más apoyos de la empresa cuando una isla de TI presente un bloqueador legítimo.

## <a name="it-fiefdoms"></a>Feudos de TI

Los miembros del equipo de un feudo de TI probablemente se definan a sí mismos a través de su alineación con un proceso o un área de responsabilidad en concreto. El equipo trabaja bajo el supuesto de que la influencia externa en su área de responsabilidad provocará problemas. Los feudos suelen ser un antipatrón basado en el miedo, lo que requerirá un considerable apoyo de liderazgo para superarlos.

Los feudos son especialmente comunes en organizaciones que han experimentado reducción de TI, inestabilidad frecuente del personal de TI o un liderazgo de TI deficiente. Cuando la empresa considera la TI simplemente un centro de costos, es mucho más probable que surjan feudos.

Por lo general, los feudos son consecuencia de un superior jerárquico que teme la pérdida del equipo y de la base de poder asociada. Estos responsables suelen tener un sentido del deber hacia su equipo y sienten la necesidad de proteger a sus subordinados de las consecuencias negativas. Frases como "proteger al equipo del cambio" y "proteger al equipo de la interrupción del proceso" pueden ser indicadores de un jefe demasiado cauteloso que puede necesitar más apoyo del liderazgo.

### <a name="addressing-resistance-from-it-fiefdoms"></a>Resolución de la resistencia de feudos de TI

Los feudos de TI pueden mostrar cierto crecimiento si se siguen los enfoques de [resolución de la resistencia de silos de TI](#addressing-resistance-from-it-silos). Antes de intentar resolver la resistencia de un feudo de TI, se recomienda tratar primero al equipo como una isla de TI. Si ese tipo de enfoques no produce ningún cambio significativo, el equipo resistente podría verse afectado por un antipatrón de feudo de TI. La causa raíz de los feudos de TI es un poco más compleja de resolver, ya que esa resistencia tiende a proceder del superior jerárquico directo (o un responsable superior en el organigrama). Por lo general, es más fácil superar los retos basados en islas de TI.

Cuando la resistencia continua de los feudos de TI bloquea el trabajo de adopción de la nube, sería conveniente realizar un trabajo conjunto para evaluar la situación con los responsables de TI existentes. Los responsables de TI deben considerar detenidamente la información procedente del [equipo de estrategia en la nube](./cloud-strategy.md), el [centro de excelencia de la nube](./cloud-governance.md) y el [equipo de gobernanza en la nube](./cloud-center-of-excellence.md) antes de tomar decisiones.

> [!NOTE]
> Los responsables de TI no deben tomar nunca a la ligera los cambios en el organigrama. También deben validar y analizar los comentarios de cada uno de los equipos auxiliares. Aunque el trabajo de transformación, como la adopción en la nube, tiende a magnificar los problemas subyacentes que han pasado desapercibidos o llevan mucho tiempo sin abordarse antes de este trabajo. Cuando los feudos impiden el éxito de la empresa, es posible que se necesite un cambio de liderazgo.
>
> Afortunadamente, quitar el responsable de un feudo no suele acabar en despido. Estos responsables fuertes y entusiastas a menudo pueden pasar a desempeñar un papel directivo después de un breve período de reflexión. Con el apoyo adecuado, este cambio puede ser recomendable para el responsable del feudo y el equipo actual.

> [!CAUTION]
> En el caso de los jefes de feudos de TI, proteger el equipo de riesgos es un claro valor de liderazgo. Pero hay una fina línea divisoria entre protección y aislamiento. Impedir que el equipo participe en impulsar los cambios puede tener consecuencias psicológicas y profesionales en él. La tentación de resistirse al cambio puede ser fuerte, especialmente durante los momentos de cambio visible.
>
> El jefe de cualquier equipo aislado puede demostrar mejor una mentalidad de crecimiento experimentando con la guía asociada a equipos de TI sin problemas de las secciones anteriores. La participación activa y optimista en actividades de CCoE y de gobernanza puede conducir al crecimiento personal. Los jefes de feudos de TI son los más idóneos para cambiar las mentalidades asfixiantes y ayudar al equipo a desarrollar nuevas ideas.

Los feudos de TI pueden ser una señal de problemas de liderazgo sistémicos. Para superar un feudo de TI, los responsables de TI necesitan tener capacidad para realizar cambios en las operaciones, las responsabilidades y, ocasionalmente, incluso en las personas responsables del mando directo de equipos específicos. Cuando esos cambios son necesarios, es aconsejable abordarlos con puntos de datos claros y defendibles.

Puede que se requiera la alineación con las partes interesadas de la empresa, las motivaciones empresariales y los resultados empresariales para impulsar el cambio necesario. La asociación con el [equipo de estrategia en la nube](./cloud-strategy.md), el [centro de excelencia de la nube](./cloud-center-of-excellence.md) y el [equipo de gobernanza en la nube](./cloud-governance.md) puede proporcionar los puntos de datos necesarios para una posición defendible. Cuando sea necesario, estos equipos deben participar en una escalación de grupo para abordar los desafíos que no se pueden abordar solo con el liderazgo de TI.

## <a name="next-steps"></a>Pasos siguientes

La interrupción de los antipatrones de la organización es un trabajo del equipo. Para actuar según esta guía, revise la introducción a la preparación de la organización para identificar los participantes y las estructuras de equipo correctos:

> [!div class="nextstepaction"]
> [Identificación de los participantes y las estructuras de equipo correctos](./index.md)
