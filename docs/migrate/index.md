---
title: Migración a la nube
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Migración a la nube en Cloud Adoption Framework
author: BrianBlanchard
ms.author: brblanch
ms.date: 04/04/2019
ms.topic: landing-page
ms.service: cloud-adoption-framework
ms.subservice: migrate
layout: LandingPage
ms.openlocfilehash: 3734a9b692dd345f45ee6a2987abf773b3391c63
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71224383"
---
# <a name="cloud-migration-in-the-cloud-adoption-framework"></a>Migración a la nube en Cloud Adoption Framework

Cualquier [plan de adopción de nube](../plan/index.md) a escala empresarial incluirá cargas de trabajo que no justifican la realización de inversiones significativas en la creación de la nueva lógica de negocios. Estas cargas de trabajo se pueden mover a la nube mediante diversos métodos: migración mediante lift-and-shift, lift-and-optimize o modernización. Cada uno de estos enfoques se considera una migración. Los ejercicios siguientes le ayudarán a establecer los procesos iterativos para evaluar, migrar, optimizar, proteger y administrar esas cargas de trabajo.

## <a name="getting-started"></a>Introducción

Para prepararse para esta fase del ciclo de vida de adopción de la nube, la plataforma sugiere los cinco ejercicios siguientes:

<!-- markdownlint-disable MD033 -->
<ul class="panelContent cardsF">
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-migration-guide/prerequisites.md?tabs=Checklist">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/1.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Requisitos previos de migración</h3>
Compruebe que se ha implementado una zona de aterrizaje y que está lista para hospedar las primeras cargas de trabajo que se migrarán a Azure. Si no se ha creado una estrategia de adopción de la nube y un plan de adopción de la nube, compruebe que ambas acciones están en curso.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-migration-guide/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/2.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Migración de la primera carga de trabajo</h3>
Aproveche la Guía de migración de Azure para que le ayude a realizar la migración de la primera carga de trabajo. Esta guía le ayudará a familiarizarse con las herramientas y enfoques necesarios para escalar los esfuerzos de adopción.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./expanded-scope/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/3.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Escenarios de migración expandidos</h3>
Aproveche la lista de comprobación de ámbito ampliado para identificar los escenarios que requerirían modificaciones en la arquitectura futura del patrimonio, en los procesos de migración, las configuraciones de zona de aterrizaje o las decisiones sobre herramientas de migración.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./azure-best-practices/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/4.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Prácticas recomendadas</h3>
Compruebe todas las modificaciones en comparación con la sección de procedimientos recomendados para garantizar una implementación adecuada del ámbito ampliado o de los enfoques específicos de migración de carga de trabajo o arquitectura.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li style="display: flex; flex-direction: column;">
        <a href="./migration-considerations/index.md">
            <div class="cardSize">
                <div class="cardPadding" style="padding-bottom:10px;">
                    <div class="card" style="padding-bottom:10px;">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img alt="" src="../_images/icons/5.png" data-linktype="external">
                            </div>
                        </div>
                        <div class="cardText" style="padding-left:0px;">
                            <h3>Mejora de procesos</h3>
La migración es una actividad de proceso intensivo. A medida que se escalan los esfuerzos de migración, utilice la sección de consideraciones sobre la migración para evaluar y madurar diversos aspectos de los procesos.
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
</ul>
<!-- markdownlint-enable MD033 -->

## <a name="iterative-migration-process"></a>Proceso de migración iterativo

En esencia, la migración a la nube consta de cuatro fases simples: Evaluación, Migración, Optimización y Seguridad y administración. Esta sección de Cloud Adoption Framework enseña a los lectores cómo maximizar el rendimiento de cada fase del proceso y cómo alinear esas fases al plan de adopción de la nube. El siguiente gráfico ilustra esas fases en un enfoque iterativo:

![Modelo de migración de Cloud Adoption Framework](../_images/operational-transformation-migrate.png)

## <a name="creating-a-balanced-cloud-portfolio"></a>Creación de una cartera equilibrada en la nube

Cualquier cartera de tecnología equilibrada tiene una mezcla de recursos en varios estados. Algunas aplicaciones están programadas para la retirada y reciben un soporte técnico mínimo. Se admiten otras aplicaciones o recursos en estado de mantenimiento, pero las características de esas soluciones son estables. Para los procesos empresariales más recientes, es probable que las condiciones cambiantes del mercado estimulen mejoras o modernizaciones continuas de las características. Cuando surgen oportunidades para impulsar nuevas fuentes de ingresos, se introducen nuevas aplicaciones o recursos en el entorno. En cada fase del ciclo de vida de un recurso, el impacto de cualquier inversión en los ingresos y las ganancias cambiará. Cuanto más avanzada sea la fase del ciclo de vida, menos probable es que una nueva característica o un esfuerzo de modernización produzcan una fuerte rentabilidad de la inversión.

La nube proporciona varios mecanismos de adopción, cada uno con grados similares de inversión y rentabilidad. La creación de aplicaciones nativas de la nube puede reducir significativamente los gastos operativos. Una vez que una aplicación nativa de la nube se publica, el desarrollo de nuevas características y soluciones puede iterar más rápido. La modernización de una aplicación puede producir beneficios similares al quitar las restricciones heredadas asociadas con los modelos de desarrollo local. Desafortunadamente, estos dos enfoques requieren mucha mano de obra y dependen del tamaño, aptitudes y experiencia de los equipos de desarrollo de software. A menudo, la mano de obra está mal alineada &mdash;las personas con las aptitudes y el talento para modernizar aplicaciones preferirían crear nuevas aplicaciones. En un mercado con limitaciones de mano de obra, los proyectos de modernización a gran escala pueden verse afectados por un problema de satisfacción y talento de los empleados. En una cartera equilibrada, este enfoque debería reservarse a las aplicaciones que recibirían mejoras significativas de las funciones si permanecieran en las instalaciones.

## <a name="envision-an-end-state"></a>Previsión de un estado final

Un viaje efectivo necesita un destino. Establezca una visión aproximada del estado final antes de dar el primer paso. Esta infografía describe un punto inicial que consiste en aplicaciones, datos e infraestructura existentes, que definen el patrimonio digital. Durante el proceso de migración, cada recurso se envía a través de una de las opciones de la derecha.

## <a name="migration-implementation"></a>Implementación de la migración

Estos artículos describen dos recorridos, cada uno con un objetivo similar: migrar un gran porcentaje de los recursos existentes a Azure. Sin embargo, los resultados empresariales y el estado actual influirán de manera significativa en los procesos necesarios para conseguirlo. Esas sutiles desviaciones dan como resultado dos enfoques radicalmente diferentes para alcanzar un estado final similar.

![Modelo de migración de Cloud Adoption Framework](../_images/operational-transformation-migrate.png)

Para guiar la ejecución incremental durante la transición al estado final, este modelo separa la migración en dos áreas de enfoque.

**Preparación de la migración:** Establecer un trabajo pendiente de migración aproximado basado en gran medida en el estado actual y en los resultados deseados.

- **Resultados empresariales:** Los principales objetivos empresariales que promueven esta migración.
- **Estimación del patrimonio digital:** Una estimación aproximada del número y la condición de cargas de trabajo que se van a migrar.
- **Roles y responsabilidades:** Una definición clara de la estructura del equipo, la separación de responsabilidades y los requisitos de acceso.
- **Cambio de los requisitos de administración:** La cadencia, los procesos y la documentación necesarios para revisar y aprobar los cambios.

Estas entradas iniciales conforman el trabajo pendiente de la migración. El resultado del trabajo pendiente de la migración es una lista clasificada por orden de prioridad de las aplicaciones que se van a migrar a la nube. Esta lista da forma a la ejecución del proceso de migración a la nube. Con el tiempo, también crecerá para incluir gran parte de la documentación necesaria para administrar el cambio.

**Proceso de migración:** Cada actividad de migración a la nube está contenida en uno de los siguientes procesos, ya que se relaciona con el trabajo pendiente de la migración.

- **Evaluación:** Evalúe un recurso existente y establezca un plan para la migración del recurso.
- **Migración:** Replique la funcionalidad de un recurso en la nube.
- **Optimización:** Equilibre el rendimiento, el costo, el acceso y la capacidad operativa de un recurso en la nube.
- **Protección y administración:** Asegúrese de que un recurso en la nube está listo para las operaciones en curso.

La información recopilada durante el desarrollo de un trabajo pendiente de migración determina la complejidad y el nivel de esfuerzo requerido dentro del proceso de migración de la nube durante cada iteración y para cada etapa de funcionalidad.

## <a name="transition-to-the-end-state"></a>Transición al estado final

El objetivo es una migración suave y parcialmente automatizada a la nube. El proceso de migración utiliza las herramientas proporcionadas por un proveedor de nube para replicar y escalonar rápidamente los recursos en la nube. Una vez comprobado, un simple cambio de red redirecciona a los usuarios a la solución en la nube. Para muchos casos de uso, la tecnología para lograr este objetivo está ampliamente disponible. Hay casos de ejemplo que demuestran la velocidad a la que se pueden replicar 10 000 máquinas virtuales en Azure.

Sin embargo, sigue siendo necesario un enfoque de migración incremental. En la mayoría de los entornos, la larga lista de máquinas virtuales que se van a migrar debe descomponerse en unidades de trabajo más pequeñas para que la migración se realice correctamente. Hay muchos factores que limitan el número de máquinas virtuales que se pueden migrar en un período determinado. La velocidad de la red de salida es uno de los pocos límites técnicos; la mayoría de los límites se imponen a la capacidad de la empresa para validar y adaptarse al cambio.

El enfoque de migración incremental de Cloud Adoption Framework ayuda a crear un plan incremental que refleja y documenta las limitaciones técnicas y culturales. El objetivo de este modelo es maximizar la velocidad de migración y minimizar la sobrecarga de TI y de la empresa. A continuación se presentan dos ejemplos de ejecución de una migración incremental basada en el trabajo pendiente de la migración.

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsZ">
<li style="display: flex; flex-direction: column;">
    <a href="./azure-migration-guide/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Guía de migración a Azure</h3>
                        <p><b>Resumen narrativo:</b> Este cliente está migrando menos de 1000 máquinas virtuales. Menos de diez aplicaciones admitidas son propiedad del propietario de una aplicación que no pertenece a la organización de TI. El resto de aplicaciones, máquinas virtuales y datos asociados son propiedad de los miembros del equipo de adopción de la nube y están admitidos por ellos. Los miembros del equipo de adopción de la nube tienen acceso administrativo a los entornos de producción del centro de datos existente.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li style="display: flex; flex-direction: column;">
    <a href="./expanded-scope/index.md" style="display: flex; flex-direction: column; flex: 1 0 auto;">
        <div class="cardSize" style="flex: 1 0 auto; display: flex;">
            <div class="cardPadding" style="display: flex;">
                <div class="card">
                    <div class="cardText">
                        <h3>Guía del escenario complejo</h3>
                        <p><b>Resumen narrativo:</b> La migración de este cliente tiene complejidad en todo el negocio, la referencia cultural y la tecnología. Esta guía incluye múltiples desafíos específicos de complejidad y formas de superarlos.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

<!-- markdownlint-enable MD033 -->

Estos dos recorridos representan dos extremos de la experiencia para los clientes que invierten en la migración a la nube. La mayoría de las compañías reflejan una combinación de los dos escenarios anteriores. Después de revisar el recorrido, utilice el modelo de migración de Cloud Adoption Framework para iniciar la conversación de migración y modificar los recorridos de línea de base para satisfacer mejor sus necesidades.

## <a name="next-steps"></a>Pasos siguientes

Elija uno de estos recorridos:

> [!div class="nextstepaction"]
> [Guía de migración a Azure](./azure-migration-guide/index.md)
>
> [Guía del ámbito ampliado](./expanded-scope/index.md)
