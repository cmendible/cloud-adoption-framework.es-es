<!-- TEMPLATE FILE - DO NOT ADD METADATA -->
<!-- markdownlint-disable MD002 MD041 -->
> [!NOTE]
>En caso de que se produzcan cambios en sus requisitos empresariales, los grupos de administración de Azure permiten reorganizar fácilmente la jerarquía de administración y las asignaciones de los grupos de suscripciones. Sin embargo, tenga en cuenta que las asignaciones de directivas y roles que se aplican a un grupo de administración las heredan todas las suscripciones que se encuentren debajo de ese grupo en la jerarquía. Si planea reasignar suscripciones entre los distintos grupos de administración, asegúrese de que conoce todos los cambios en las asignaciones de directivas y roles que pueden producirse. Para más información, consulte la [documentación de los grupos de administración de Azure](https://docs.microsoft.com/azure/governance/management-groups).

### <a name="governance-of-resources"></a>Gobernanza de recursos

Un conjunto de roles RBAC y directivas globales proporcionará un nivel base de referencia de cumplimiento de gobernanza. Para satisfacer los requisitos de directivas del equipo de gobernanza de la nube, la implementación del MVP de gobernanza requiere completar las tareas siguientes:

1. Identifique las definiciones de Azure Policy personalizadas necesarias para cumplir los requisitos empresariales. Esto puede incluir el uso de definiciones integradas y la creación de nuevas definiciones personalizadas.
2. Cree una definición del plano técnico mediante estas directivas integradas y personalizadas y las asignaciones de roles que requiere el MVP de gobernanza.
3. Aplique las directivas y la configuración globalmente mediante la asignación de la definición del plano técnico a todas las suscripciones.

#### <a name="identify-policy-definitions"></a>Identificación de las definiciones de directivas

Azure proporciona varias directivas integradas y definiciones de roles que se pueden asignar a cualquier grupo de administración, suscripción o grupo de recursos. Muchos requisitos habituales de gobernanza pueden controlarse mediante definiciones integradas. Sin embargo, es probable que también necesite crear definiciones de directivas personalizadas para administrar sus requisitos específicos.

Las definiciones de las directivas personalizadas se guardan en un grupo de administración o en una suscripción y se heredan a través de la jerarquía de los grupos de administración. Si la ubicación de guardado de la definición de una directiva es un grupo de administración, dicha definición está disponible para asignarla a cualquiera de las suscripciones o grupos de administración secundarios de ese grupo.

Dado que las directivas necesarias para dar soporte al MVP de gobernanza están destinadas a aplicarse a todas las suscripciones actuales, se implementarán los siguientes requisitos empresariales mediante una combinación de definiciones integradas y personalizadas creadas en el grupo de administración raíz:

1. Restrinja la lista de asignaciones de roles disponibles al conjunto de roles de Azure integrados que autorice el equipo de gobernanza de la nube. Esto requerirá una [definición de directiva personalizada](https://github.com/Azure/azure-policy/tree/master/samples/Authorization/allowed-role-definitions).
2. Exija el uso de las siguientes etiquetas en todos los recursos: *Departamento/unidad de facturación*, *Geografía*, *Clasificación de los datos*, *Importancia crítica*, *Acuerdo de Nivel de Servicio*, *Entorno*, *Arquetipo de aplicación*, *Aplicación* y *Propietario de aplicación*. Esto puede controlarse mediante la definición integrada "Solicitar la etiqueta especificada".
3. Solicite que la etiqueta *Aplicación* de los recursos deba coincidir con el nombre del grupo de recursos relevante. Esto puede controlarse mediante la definición integrada "Requerir etiqueta y su valor".

Para obtener información acerca de cómo definir directivas personalizadas, consulte la [documentación de Azure Policy](https://docs.microsoft.com/azure/governance/policy/tutorials/create-custom-policy-definition). Para obtener una guía y ejemplos de directivas personalizadas, consulte el [sitio de ejemplos de Azure Policy](https://docs.microsoft.com/azure/governance/policy/samples) y el [repositorio de GitHub](https://github.com/Azure/azure-policy) asociado.

#### <a name="assign-azure-policy-and-rbac-roles-using-azure-blueprints"></a>Asignación de roles de RBAC y de Azure Policy mediante Azure Blueprints

Las directivas de Azure se pueden asignar en el nivel de grupo de recursos, suscripción y grupo de administración, y se pueden incluir en las definiciones de [Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview). Aunque los requisitos de directiva que se definen en este MVP de gobernanza se aplican a todas las suscripciones actuales, es muy probable que las futuras implementaciones requieran excepciones o directivas alternativas. Como resultado, la asignación de una directiva mediante grupos de administración. y que todas las suscripciones secundarias heredan estas asignaciones, puede no ser lo suficientemente flexible para admitir estos escenarios.

Azure Blueprints permiten la asignación coherente de roles y directivas, la aplicación de plantillas de Resource Manager y la implantación de grupos de recursos en varias suscripciones. Igual que sucede con las definiciones de directiva, las definiciones de plano técnico se guardan en grupos de administración o suscripciones, y están disponibles a través de la herencia para cualquier elemento secundario de la jerarquía de grupos de administración.

El equipo de gobernanza en la nube ha decidido que el cumplimiento de las asignaciones de RBAC y directivas de Azure necesarias en las suscripciones se implementará a través de Azure Blueprints y los artefactos asociados:

1. En el grupo de administración raíz, cree una definición de plano técnico denominada `governance-baseline`.
2. Agregue los siguientes artefactos de plano técnico a dicha definición:
    1. Asignaciones de directivas para las definiciones de Azure Policy personalizadas definidas en la raíz del grupo de administración.
    2. Definiciones de grupo de recursos para los grupos necesarios en las suscripciones creadas i regidas por el MVP de gobernanza.
    3. Asignaciones de roles estándar necesarias en las suscripciones que el MVP de gobernanza ha creado o regido.
3. Publique la definición del plano técnico.
4. Asigne la definición del plano técnico `governance-baseline` a todas las suscripciones.

Consulte la [documentación de Azure Blueprints](https://docs.microsoft.com/azure/governance/blueprints/overview) para obtener más información sobre cómo crear y usar definiciones del plano técnico.

### <a name="secure-hybrid-vnet"></a>Red virtual híbrida segura

A menudo, determinadas suscripciones requieren cierto nivel de acceso a los recursos locales. Esto es habitual en escenarios de migración o escenarios de desarrollo en los que los recursos dependientes residen en el centro de datos local.

Hasta que la confianza en el entorno de nube está completamente establecida es importante controlar y supervisar estrechamente no solo todas las comunicaciones que se permiten entre el entorno local y las cargas de trabajo en la nube, sino también que la red local está protegida contra el potencial acceso no autorizado de recursos basados en la nube. Para admitir estos escenarios, el MVP de gobernanza agrega las siguientes prácticas recomendadas:

1. Establezca una red virtual híbrida segura en la nube.
    1. La [arquitectura de referencia de la VPN](https://docs.microsoft.com/azure/architecture/reference-architectures/hybrid-networking/vpn) establece un patrón y un modelo de implementación para crear una instancia de VPN Gateway en Azure.
    2. Compruebe que los mecanismos locales de seguridad y administración del tráfico traten las redes en la nube conectadas como recursos que no son de confianza. Los recursos y servicios hospedados en la nube solo deben tener acceso a los servicios locales autorizados.
    3. Valide que el dispositivo de extremo local que se encuentra en el centro de datos local es compatible con los [requisitos de Azure VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-devices) y está configurado para acceder a la red Internet pública.
    4. Tenga en cuenta que los túneles de VPN no deben considerarse circuitos preparados para producción salvo para las cargas de trabajo más simples. Todo lo que sea más de unas cuantas cargas de trabajo sencillas que requieren conectividad local deberían emplear Azure ExpressRoute.
1. En el grupo de administración raíz, cree una segunda definición del plano técnico llamada `secure-hybrid-vnet`.
    1. Agregue la plantilla de Resource Manager para la instancia de VPN Gateway como un artefacto para la definición del plano técnico.
    2. Agregue la plantilla de Resource Manager para la red virtual como un artefacto para la definición del plano técnico.
    3. Publique la definición del plano técnico.
1. Asigne la `secure-hybrid-vnet`definición del plano técnico a todas las suscripciones que requieran conectividad local. Esta definición se debe asignar además de la definición del plano técnico `governance-baseline`.

Una de las mayores preocupaciones que plantea la seguridad de TI y los equipos de gobernanza tradicional, es el riesgo de que la adopción de la nube en una etapa temprana vaya a poner en peligro los recursos existentes. El método anterior permite a los equipos de adopción de la nube crear y migrar soluciones híbridas, con un riesgo reducido para los recursos locales. Cuando la confianza en el entorno en la nube aumente, las posteriores evoluciones podrán quitar esta solución temporal.

> [!NOTE]
> La información anterior es solo un punto de partida para crear rápidamente un MVP de gobernanza de línea de base. Esto es solo el comienzo del recorrido hacia la gobernanza. De todos modos, será necesaria una evolución aún mayor a medida que la empresa continúe adoptando la nube y asuma más riesgos en las siguientes áreas:
>
> - Cargas de trabajo críticas
> - Datos protegidos
> - Administración de costos
> - Escenarios de nube múltiple
>
> Además, los detalles concretos de este MVP se basan en el proceso de ejemplo de una empresa ficticia, que se describe en los artículos siguientes. Le recomendamos encarecidamente que se familiarice con los otros artículos de esta serie antes de implementar este procedimiento recomendado.
