---
title: 'Guía de gobernanza para empresas complejas: Mejora de la materia de base de referencia de la seguridad'
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: 'Guía de gobernanza para empresas complejas: Mejora de la materia de base de referencia de la seguridad'
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/05/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: dc045d26dd855240700341748c189a985f1f6758
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71220556"
---
# <a name="governance-guide-for-complex-enterprises-improve-the-security-baseline-discipline"></a>Guía de gobernanza para empresas complejas: Mejora de la materia de base de referencia de la seguridad

En este artículo se detalla el método de adición de controles de seguridad que ayudan al traslado de datos protegidos a la nube.

## <a name="advancing-the-narrative"></a>Continuación de la historia

El Director de sistemas de información lleva meses colaborando con sus colegas y el personal legal de la empresa. Se contrató un consultor de administración con experiencia en ciberseguridad para ayudar a los equipos de seguridad y gobernanza de TI a redactar una nueva directiva con respecto a los datos protegidos. El grupo pudo promover el apoyo de la dirección para reemplazar las directivas existentes, permitiendo así que los proveedores de nube aprobados hospeden los datos financieros y la información personal confidencial. Debido a ello, es necesario adoptar un conjunto de requisitos de seguridad y un proceso de gobernanza para comprobar y documentar el cumplimiento de esas directivas.

Durante los últimos 12 meses, los equipos de adopción en la nube han retirado la mayoría de los 5000 recursos de los dos centros de datos. Por su parte, los 350 recursos incompatibles se llevaron a un centro de datos alternativo. Así pues, solo quedan las 1250 máquinas virtuales que contienen los datos protegidos.

### <a name="changes-in-the-cloud-governance-team"></a>Cambios en el equipo de gobernanza de la nube

El equipo de gobernanza de la nube continúa cambiando a medida que avanza la historia. Los dos miembros fundadores del equipo se encuentran ahora entre los arquitectos en la nube más respetados de la empresa. La colección de scripts de configuración ha crecido a medida que los nuevos equipos abordan nuevas e innovadoras implementaciones. El equipo de gobernanza de la nube también ha crecido. Hace poco, los miembros del equipo de operaciones de TI se unieron a las actividades del equipo de gobernanza de la nube para prepararse para las operaciones en la nube. Asimismo, los arquitectos en la nube que ayudaron a fomentar esta comunidad son ahora los administradores y aceleradores que revolucionaron y agilizaron la nube.

Aunque la diferencia es sutil, esta es una distinción importante al crear una cultura de TI centrada en la gobernanza. Un administrador en la nube se encarga de solucionar los problemas que crean los arquitectos en la nube con sus innovaciones, así que se puede decir que estos dos roles tienen objetivos encontrados. Un administrador en la nube ayuda a mantener la nube segura, para que los arquitectos en la nube puedan moverse rápidamente y crear menos problemas. Un acelerador de la nube realiza ambas funciones, pero también participa en la creación de plantillas para acelerar la implementación y la adopción, convirtiéndose así en un acelerador de innovaciones y en un defensor de las cinco materias de gobernanza de la nube.

### <a name="changes-in-the-current-state"></a>Cambios en el estado actual

En la fase anterior de esta historia, la compañía había comenzado el proceso de retirar dos centros de datos. Este esfuerzo continuo incluye la migración de algunas aplicaciones con requisitos de autenticación heredados que requirieron mejoras graduales de la línea de base de identidad, como se ha descrito en el [artículo anterior](./identity-baseline-improvement.md).

Desde entonces, han cambiado algunas cosas que afectarán a la gobernanza:

- Miles de recursos de TI y de negocios se han implementado en la nube.
- El equipo de desarrollo de aplicaciones ha implementado una canalización de integración e implementación continua (CI/CD) para implementar una aplicación nativa en la nube y así poder ofrecer una experiencia de usuario mejorada. Como la aplicación aún no interactúa con los datos protegidos, no está lista para la producción.
- El equipo de inteligencia empresarial de TI mantiene activamente los datos en la nube de terceros, inventario y logística. Estos datos se emplean para impulsar nuevas predicciones, que podrían dar forma a procesos empresariales. Sin embargo, no se puede actuar sobre las predicciones y conclusiones hasta que los datos de cliente y financieros puedan integrarse en la plataforma de datos.
- El equipo de TI hace progresos en los planes del Director de sistemas de información y del director financiero para retirar los dos centros de datos. Casi 3500 recursos de los dos centros de datos han sido retirados o migrados.
- Las directivas relativas a la información personal y financiera confidencial se han modernizado. Sin embargo, las nuevas directivas corporativas están supeditadas a la implementación de directivas de seguridad y de gobernanza relacionadas. Así que los equipos siguen estancados.

### <a name="incrementally-improve-the-future-state"></a>Mejora gradual del estado futuro

- Los primeros experimentos de los equipos de desarrollo de aplicaciones y BI han mostrado mejoras potenciales en las experiencias de los clientes y las decisiones basadas en datos. Ambos equipos quieren expandir la adopción de la nube en los próximos 18 meses mediante la implementación de esas soluciones en producción.
- Asimismo, el quipo de TI ha desarrollado una justificación comercial para migrar cinco centros de datos más a Azure, lo que reducirá aún más los costos de TI y proporcionará una mayor agilidad empresarial. Aunque es menor en escala, se espera que la retirada de esos centros de datos duplique el ahorro en cuanto a costos totales.
- Los presupuestos de gastos de capital y gastos operativos se han aprobado para implementar las directivas, herramientas y procesos de seguridad y gobernanza requeridos. Los ahorros de costos esperados al retirar el centro de datos son más que suficientes para pagar esta nueva iniciativa. Los líderes de TI y de negocios confían en que esta inversión acelerará la realización de devoluciones en otras áreas. El equipo comunitario de gobernanza de la nube se convirtió en un equipo reconocido con directivos y personal dedicados.
- En conjunto, los equipos de adopción de la nube, el equipo de gobernanza de la nube, el equipo de seguridad de TI y el equipo de gobernanza de TI implementan los requisitos de gobernanza y seguridad para permitir que los equipos de adopción de la nube migren datos protegidos a la nube.

## <a name="changes-in-tangible-risks"></a>Cambios en riesgos tangibles

**Vulneración de datos:** Existe un aumento inherente en las responsabilidades relacionadas con las vulneraciones de datos al adoptar cualquier nueva plataforma de datos. Los técnicos que adoptan las tecnologías de la nube tienen mayores responsabilidades para implementar soluciones que puedan reducir este riesgo. Para asegurarse de que los técnicos cumplen con estas responsabilidades se debe implementar una estrategia eficaz de seguridad y gobernanza.

Este riesgo empresarial puede ampliarse a algunos riesgos técnicos:

1. Se podrían implementar aplicaciones críticas o datos protegidos de forma no intencionada.
2. Los datos protegidos podrían exponerse durante el almacenamiento debido a decisiones de cifrado deficiente.
3. Usuarios no autorizados podrían tener acceso a datos protegidos.
4. Podrían producirse intrusiones externas a datos protegidos.
5. Las intrusiones externas o ataques por denegación de servicio podrían provocar una interrupción del negocio.
6. Los cambios de la organización o empleo podrían permitir el acceso no autorizado a los datos protegidos.
7. Las nuevas vulnerabilidades de seguridad podrían crear oportunidades para la intrusión o el acceso no autorizado.
8. Los procesos incoherentes de implementación podrían dar lugar a brechas de seguridad y estas, a su vez, a pérdidas de datos o interrupciones.
9. El desfase de la configuración o la falta revisiones podrían dar lugar a brechas de seguridad y estas, a su vez, a pérdidas de datos o interrupciones.
10. Diversos dispositivos perimetrales podrían aumentar los costos de operación de la red.
11. Diversas opciones de configuración de dispositivos podrían provocar negligencias en la configuración y la seguridad podría verse comprometida.
12. El equipo de ciberseguridad insiste en que existe el riesgo de que un proveedor no genere claves de cifrado en la plataforma de un solo proveedor de nube. Si bien esta afirmación no está demostrada, el equipo la acepta por el momento.

## <a name="incremental-improvement-of-the-policy-statements"></a>Mejora gradual de las declaraciones de las directivas

Los siguientes cambios en la directiva le ayudarán a corregir los nuevos riesgos y le guiarán en la implementación. La lista es larga, pero la adopción de estas directivas podría ser más fácil de lo que parece.

1. Todos los recursos implementados deben categorizarse por importancia y clasificación de datos. Asimismo, el equipo de gobernanza de la nube y el propietario de la aplicación deben revisar las clasificaciones antes de realizar la implementación en la nube.
2. Las aplicaciones que almacenan u obtienen acceso a datos protegidos se deben administrar de manera diferente a las demás. Como mínimo, deben segmentarse para evitar el acceso no intencionado de los datos protegidos.
3. Todos los datos protegidos deben estar cifrados cuando están en reposo.
4. Los permisos elevados en los segmentos que contienen datos protegidos deben ser una excepción. Estas excepciones se registrarán con el equipo de gobernanza de la nube y se auditarán periódicamente.
5. las subredes que contengan datos protegidos deben aislarse de las otras subredes. El tráfico de red entre subredes de datos protegidos se auditará periódicamente.
6. No se podrá tener acceso a ninguna subred que contenga datos protegidos directamente a través de Internet o entre centros de datos. El acceso a estas subredes debe enrutarse a través de subredes intermedias. Todo acceso a estas subredes debe realizarse a través de una solución de firewall que pueda realizar funciones de análisis y bloqueo de paquetes.
7. Las herramientas de gobernanza deben auditar y aplicar los requisitos de configuración de red que estableció el equipo de administración de seguridad.
8. Las herramientas de gobernanza deben limitar la implementación de máquina virtual a solo las imágenes aprobadas.
9. Siempre que sea posible, la administración de configuración de nodos debe aplicar los requisitos de directiva a la configuración de cualquier sistema operativo invitado. La administración de configuración de nodos debe respetar la inversión existente en el objeto de directiva de grupo (GPO) para la configuración de recursos.
10. Las herramientas de gobernanza deben auditar las actualizaciones automáticas para que estén habilitadas en todos los recursos implementados. Cuando sea posible, se aplicarán las actualizaciones automáticas. Cuando las herramientas no puedan aplicar esto, las infracciones deben revisarse con los equipos de administración de operaciones y corregirse de acuerdo a las directivas de operaciones. Los recursos que no se actualicen automáticamente deben incluirse en procesos que sean propiedad del departamento de operaciones de TI.
11. La creación de nuevas suscripciones o grupos de administración para las aplicaciones críticas o datos protegidos requiere una revisión del equipo de gobernanza de la nube para garantizar que se ha asignado el plano técnico correcto.
12. Un modelo de acceso con privilegios mínimos se aplicará a cualquier suscripción que contenga aplicaciones críticas o datos protegidos.
13. El proveedor en la nube debe ser capaz de integrar las claves de cifrado que administra la solución del entorno local existente.
14. El proveedor en la nube debe ser capaz de admitir la solución de dispositivos perimetrales existente, así como cualquier configuración requerida para proteger cualquier límite de red expuesto públicamente.
15. El proveedor en la nube debe ser capaz de admitir una conexión compartida a la red WAN global, con la transmisión de datos enrutada a través de la solución de dispositivos perimetrales existente.
16. El equipo de seguridad debe revisar periódicamente las tendencias y vulnerabilidades que podrían afectar a las implementaciones en la nube para proporcionar actualizaciones a las herramientas de línea de base de seguridad que se usan en la nube.
17. El equipo de gobernanza de la nube debe aprobar las herramientas de implementación para garantizar la gobernanza en curso de los recursos implementados.
18. Los scripts de implementación deben conservarse en un repositorio central accesible para el equipo de gobernanza de la nube, y que así se puedan revisar y se realicen auditorías periódicas.
19. Los procesos de gobernanza deben incluir auditorías en el punto de implementación y en ciclos regulares para garantizar la coherencia entre todos los recursos.
20. La implementación de las aplicaciones que requieren autenticación de cliente debe usar un proveedor de identidades aprobado que sea compatible con el proveedor de identidades principal para usuarios internos.
21. Los procesos de gobernanza en la nube deben incluir revisiones trimestrales con los equipos de línea de base de identidad para así poder identificar usuarios malintencionados o patrones de uso que deban evitarse mediante la configuración de recursos en la nube.

## <a name="incremental-improvement-of-the-best-practices"></a>Mejoras graduales de los procedimientos recomendados

En esta sección del artículo se cambiará el diseño del producto viable mínimo de gobernanza para incluir nuevas directivas de Azure y una implementación de Azure Cost Management. Juntos, estos dos cambios de diseño cumplirán con las nuevas declaraciones de directiva corporativa.

Las nuevas recomendaciones se dividen en dos categorías: TI de empresa (Hub) y adopción de la nube (Spoke).

**Establecimiento de una suscripción de tipo hub-and-spoke de TI empresarial para centralizar de base de referencia de la seguridad:** En este procedimiento recomendado, la capacidad de gobernanza existente está encapsulada mediante una [topología de tipo hub-and-spoke con servicios compartidos](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services), además de algunas adiciones clave del equipo de gobernanza de la nube.

1. Repositorio de Azure DevOps. Cree un repositorio en Azure DevOps para almacenar y edite todas las plantillas de Azure Resource Manager pertinentes y configuraciones con script.
2. Plantilla de topología de red en estrella tipo hub-and-spoke:
    1. La guía de la arquitectura de referencia sobre la [topología de red en estrella tipo hub-and-spoke con servicios compartidos](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services) se puede usar para generar plantillas de Resource Manager para los recursos necesarios de un centro de TI de empresa.
    2. Gracias a esas plantillas, esta estructura puede repetirse como parte de una estrategia de gobernanza central.
    3. Además de la arquitectura de referencia actual, le recomendamos que cree una plantilla de grupo de seguridad de red que capture los requisitos de bloqueo de puertos o listas blancas, para que la red virtual pueda hospedar el firewall. Este grupo de seguridad de red difiere de los grupos anteriores, porque será el primer grupo de seguridad de red que permita el tráfico público hacia una red virtual.
3. Crear directivas de Azure. Cree una directiva denominada `Hub NSG Enforcement` para aplicar la configuración del grupo de seguridad de red asignado a cualquier red virtual creada en esta suscripción. Aplique las directivas integradas para la configuración de invitado de la manera siguiente:
    1. Confirme que los servidores web de Windows usan protocolos de comunicación segura.
    2. Confirme que la configuración de seguridad de contraseñas es correcta en máquinas de Linux y Windows.
4. Plano técnico de TI de empresa
    1. Cree un plano técnico de Azure denominado `corporate-it-subscription`.
    2. Agregue las plantillas de la topología en estrella tipo hub-and-spoke y la directiva `Hub NSG Enforcement`.
5. Ampliar la jerarquía inicial del grupo de administración.
    1. Para cada grupo de administración que ha solicitado soporte técnico para los datos protegidos, el plano técnico `corporate-it-subscription-blueprint` proporciona una solución de centro acelerada.
    2. Debido a que los grupos de administración en este ejemplo ficticio incluyen una jerarquía regional además de una jerarquía de unidades de negocio, este plano técnico se implementará en cada región.
    3. Cree una suscripción denominada `Corporate IT Subscription` para cada región de la jerarquía del grupo de administración.
    4. Aplique el plano técnico `corporate-it-subscription-blueprint` a cada instancia regional.
    5. Esto establecerá un centro para cada unidad de negocio de cada región. Nota: Se podrían lograr mayores ahorros de costos, pero para ello debe compartir centros en las unidades de negocio de cada región.
6. Integre los objetos de directivas de grupo (GPO) mediante Desired State Configuration (DSC):
    1. Convierta GPO en DSC: el [proyecto de Microsoft de administración de línea de base](https://github.com/Microsoft/BaselineManagement) en GitHub puede acelerar este proceso. * Asegúrese de guardar DSC en el repositorio en paralelo con las plantillas de Resource Manager.
    2. Implemente la configuración de estado de Azure Automation en cualquier instancia de la suscripción de TI de empresa. Azure Automation se puede usar para aplicar DSC en máquinas virtuales implementadas en las suscripciones compatibles del grupo de administración.
    3. En el plan de desarrollo actual se planea habilitar directivas personalizadas de configuración de invitados. Cuando esa característica esté disponible, ya no será necesario usar Azure Automation en este procedimiento recomendado.

**Aplicación de una gobernanza adicional a una suscripción de adopción de la nube (Spoke)** : Sobre la base que ofrece `Corporate IT Subscription`, los cambios menores en el producto viable mínimo de gobernanza aplicados a cada suscripción dedicada al apoyo de arquetipos de aplicaciones pueden producir rápidas mejoras.

En cambios iterativos anteriores del procedimiento recomendado, se definieron grupos de seguridad de red para bloquear el tráfico público y el tráfico interno de la lista blanca. Además, el plano técnico de Azure creó temporalmente las capacidades de DMZ y Active Directory. En esta iteración, ajustaremos esos recursos un poco, para así poder crear una nueva versión del plano técnico de Azure.

1. Plantilla de emparejamiento de redes. Esta plantilla emparejará la red virtual de cada suscripción con la red virtual del centro en la suscripción TI de empresa.
    1. En la arquitectura de referencia de la sección anterior, [Topología en estrella de tipo hub-and-spoke con servicios compartidos](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/shared-services) se generó una plantilla de Resource Manager para habilitar el emparejamiento de redes virtuales.
    2. Esa plantilla se puede usar como guía para modificar la plantilla de DMZ de la iteración de gobernanza anterior.
    3. Ahora estamos agregando la opción de emparejamiento de red virtual a la red virtual de DMZ que se conectó previamente al dispositivo perimetral local a través de VPN.
    4. *** También le recomendamos que elimine la VPN de esta plantilla para garantizar que no se enrute el tráfico directamente al centro de datos local, sin pasar por la solución de Firewall y la suscripción de TI de empresa. También puede establecer esta VPN como un circuito de conmutación por error en caso de una interrupción del circuito de ExpressRoute.
    5. Azure Automation solicitará la [configuración de red](https://docs.microsoft.com/azure/automation/automation-dsc-overview#network-planning) adicional para aplicar DSC a las máquinas virtuales hospedadas.
2. Modifique el grupo de seguridad de red. Bloquee todo el tráfico local público **y** directo en el grupo de seguridad de red. El único tráfico entrante debe venir a través del homólogo de la red virtual en la suscripción correspondiente al TI de empresa.
    1. En la iteración anterior, se creó un grupo de seguridad de red que bloqueaba todo el tráfico público y que incluía en la lista blanca todo el tráfico interno. Ahora queremos cambiar este grupo de seguridad de red un poco.
    2. La nueva configuración del grupo de seguridad de red debería bloquear todo el tráfico público y todo el tráfico del centro de datos local.
    3. El tráfico que entra a esta red virtual solo debe provenir de la red virtual que se encuentra en el otro lado del homólogo de la red virtual.
3. Implementación de Azure Security Center:
    1. Configure Azure Security Center para cualquier grupo de administración que contenga clasificaciones de datos protegidos.
    2. Active de forma predeterminada el aprovisionamiento automático para garantizar el cumplimiento de la aplicación de revisiones.
    3. Establezca configuraciones de seguridad del sistema operativo. Seguridad de TI para definir la configuración.
    4. Habilite el soporte técnico para la seguridad de TI al usar por primera vez Azure Security Center. Cambie el uso de Security Center a la seguridad de TI, pero mantenga el acceso para poder mejorar continuamente la gobernanza.
    5. Cree una plantilla de Resource Manager que refleje los cambios necesarios para la configuración de Azure Security Center de una suscripción.
4. Actualice Azure Policy en todas las suscripciones.
    1. Audite y exija la clasificación de datos y la importancia en todos los grupos de administración y suscripciones, para identificar las suscripciones con clasificaciones de datos protegidos.
    2. Audite y exija el uso exclusivo de imágenes del sistema operativo que se hayan aprobado.
    3. Audite y exija el uso de las configuraciones de los huéspedes según los requisitos de seguridad de cada nodo.
5. Actualice Azure Policy en todas las suscripciones que contengan clasificaciones de datos protegidos.
    1. Audite y aplique solo el uso de roles estándar.
    2. Audite y exija la aplicación del cifrado en todas las cuentas de almacenamiento y los archivos en reposo de los nodos individuales.
    3. Audite y fuerce la aplicación de la nueva versión del grupo de seguridad de red de DMZ.
    4. Audite y exija el uso de la subred de red aprobada y la red virtual por interfaz de red.
    5. Audite y exija que se aplique la limitación de las tablas de enrutamiento que defina el usuario.
6. Plano técnico de Azure:
    1. Cree un plano técnico de Azure denominado `protected-data`.
    2. Agregue las plantillas de la red virtual homóloga, del grupo de seguridad de red y de Azure Security Center al plano técnico.
    3. Asegúrese de que la plantilla de Active Directory correspondiente a la iteración anterior **no** esté incluida en el plano técnico. Cualquier dependencia de Active Directory la proporcionará la suscripción de TI de empresa.
    4. Finalice todas las máquinas virtuales de Active Directory implementadas en la iteración anterior.
    5. Agregue las nuevas directivas para suscripciones de datos protegidos.
    6. Publique el plano técnico en cualquier grupo de administración que vaya a hospedar datos protegidos.
    7. Aplique el nuevo plano técnico a cada suscripción afectada, además de los planos técnicos existentes.

## <a name="conclusion"></a>Conclusión

Al agregar estos procesos y los cambios realizados en el producto viable mínimo de gobernanza, podrá solucionar muchos de los riesgos asociados a la gobernanza de seguridad. Juntos, agregan herramientas de supervisión de red, así como la identidad y la seguridad necesarias para proteger los datos.

## <a name="next-steps"></a>Pasos siguientes

A medida que avanza la adopción de la nube y aporta valores empresariales adicionales, también cambian los riesgos y necesidades de gobernanza de la nube. En cuanto a la empresa ficticia de esta guía, el paso siguiente es dar servicio a las cargas de trabajo críticas. En este punto son necesarios los controles de coherencia de recursos.

> [!div class="nextstepaction"]
> [Mejora de la materia de coherencia de los recursos](./resource-consistency-improvement.md)
