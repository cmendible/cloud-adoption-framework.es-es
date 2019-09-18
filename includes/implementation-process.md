<!-- TEMPLATE FILE - DO NOT ADD METADATA -->
<!-- markdownlint-disable MD002 MD041 -->

## <a name="dependent-decisions"></a>Decisiones dependientes

Las siguientes decisiones proceden de equipos fuera del equipo de gobernanza de la nube. La implementación de cada una procederá de esos mismos equipos. No obstante, el equipo de gobernanza de la nube es responsable de implementar una solución para validar que esas implementaciones se aplican de forma coherente.

### <a name="identity-baseline"></a>Línea de base de identidad

La línea de base de identidad es el punto de partida fundamental para toda gobernanza. Antes de intentar aplicar la gobernanza, se debe establecer la identidad. A continuación, las soluciones de gobernanza harán cumplir la estrategia de identidad establecida.
En esta guía de gobernanza, el equipo de administración de identidades implementa el patrón de **[sincronización de directorios](/azure/architecture/cloud-adoption/decision-guides/identity/overview#directory-synchronization)** :

- Azure Active Directory (Azure AD) proporcionará RBAC, mediante la sincronización de directorios o el "mismo inicio de sesión" que se implementó durante la migración de la empresa a Office 365. Para una guía sobre la implementación, consulte [Arquitectura de referencia para Integración de Azure AD](/azure/architecture/reference-architectures/identity/azure-ad).
- El inquilino de Azure AD también regirá la autenticación y el acceso a los recursos implementados en Azure.

En el producto viable mínimo de gobernanza, el equipo de gobernanza hará cumplir la aplicación del inquilino replicado mediante herramientas de gobernanza de la suscripción que se describen más adelante en este artículo. En iteraciones futuras, el equipo de gobernanza podría también aplicar herramientas enriquecidas de Azure AD para ampliar esta funcionalidad.

### <a name="security-baseline-networking"></a>Base de referencia de seguridad: Redes

Una red definida por software es un aspecto inicial importante de la línea de base de seguridad. Establecer el MVP de gobernanza depende de decisiones tempranas por parte del equipo de administración de seguridad para definir cómo se pueden configurar con seguridad las redes.

Debido a la falta de requisitos, el equipo de seguridad de TI busca protección y ha solicitado un patrón de **[nube DMZ](/azure/architecture/cloud-adoption/decision-guides/software-defined-network/cloud-dmz)** . Esto significa que la gobernanza de las implementaciones de Azure mismas será muy ligero.

- Las suscripciones de Azure pueden conectarse a un centro de datos existente mediante VPN, pero deben seguir todas las directivas locales de gobernanza de TI con respecto a la conexión de una zona desmilitarizada a los recursos protegidos. Para una guía de implementación con respecto a la conectividad VPN, consulte [Arquitectura de referencia sobre VPN](/azure/architecture/reference-architectures/hybrid-networking/vpn).
- Actualmente se están aplazando las decisiones con respecto a subredes, firewalls y enrutamiento a cada cliente potencial de aplicación y carga de trabajo.
- Se requiere un análisis adicional antes de la publicación de datos protegidos o cargas de trabajo críticas.

En este patrón, las redes en la nube solo pueden conectarse a los recursos locales a través de una VPN existente que sea compatible con Azure. El tráfico a través de esa conexión se tratará como cualquier tráfico procedente de una zona desmilitarizada. Puede que sean necesarias consideraciones adicionales relativas al dispositivo perimetral local para controlar el tráfico de Azure de forma segura.

El equipo de gobernanza de la nube ha invitado activamente a los miembros de los equipos de redes y de seguridad de TI a reuniones periódicas para anticiparse a las demandas y los riesgos de las redes.

### <a name="security-baseline-encryption"></a>Base de referencia de seguridad: Cifrado

El cifrado es otra decisión fundamental en la materia de línea de base de seguridad. Dado que la empresa actualmente todavía no almacena ningún dato protegido en la nube, el equipo de seguridad ha decidido un patrón menos agresivo para el cifrado.
En este momento, se sugiere un **[patrón nativo de la nube para el cifrado](/azure/architecture/cloud-adoption/decision-guides/encryption/overview#key-management)** , pero no es obligatorio para ningún equipo de desarrollo.

- No se han establecido requisitos de gobernanza con respecto al uso de cifrado, ya que la actual directiva corporativa no permite datos críticos ni protegidos en la nube.
- Serán necesarios análisis adicionales antes de la publicación de datos protegidos o cargas de trabajo críticas.

## <a name="policy-enforcement"></a>Aplicación de directivas

La primera decisión que se deberá tomar en cuanto a la aceleración de la implementación es el patrón para el cumplimiento. En esta narración, el equipo de gobernanza ha decidido implementar el patrón de **[cumplimiento automatizado](/azure/architecture/cloud-adoption/decision-guides/policy-enforcement/overview#automated-enforcement)** .

- Azure Security Center estará disponible para que los equipos de seguridad e identidad supervisen los riesgos de seguridad. También es probable que ambos equipos usen Security Center para identificar los nuevos riesgos y mejorar la directiva corporativa.
- RBAC se requiere en todas las suscripciones para controlar el cumplimiento de autenticación.
- Azure Policy se publicará en cada grupo de administración y se aplicará a todas las suscripciones. Sin embargo, el nivel de las directivas que se aplique será muy limitado en este MVP de gobernanza inicial.
- Aunque se usen grupos de administración de Azure, se espera una jerarquía relativamente sencilla.
- Azure Blueprints se usará para implementar y actualizar las suscripciones mediante la aplicación de requisitos de RBAC, plantillas de Resource Manager y Azure Policy en los grupos de administración.

## <a name="applying-the-dependent-patterns"></a>Aplicación de los patrones dependientes

Las siguientes decisiones representan los patrones que se harán cumplir a través de la estrategia de cumplimiento de directivas anterior:

**Línea de base de identidad.** Azure Blueprints establecerá los requisitos de RBAC en un nivel de suscripción para asegurarse de que se configure una identidad coherente para todas las suscripciones.

**Línea de base de seguridad: Redes.** El equipo de gobernanza de la nube mantiene una plantilla de Resource Manager para establecer una puerta de enlace de VPN entre Azure y el dispositivo de VPN local. Cuando un equipo de aplicación requiera una conexión VPN, el equipo de gobernanza de la nube aplicará la plantilla de Resource Manager de la puerta de enlace mediante Azure Blueprints.

**Línea de base de seguridad: cifrado.** En este punto, no se requiere ningún cumplimiento de directivas en esta área. Se revisará durante las iteraciones posteriores.
