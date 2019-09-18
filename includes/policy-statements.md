<!-- TEMPLATE FILE - DO NOT ADD METADATA -->
<!-- markdownlint-disable MD002 MD041 -->

## <a name="policy-statements"></a>Policy statements

Las siguientes declaraciones de la directiva establecen los requisitos necesarios para corregir los riesgos definidos. Estas directivas definen los requisitos funcionales para el MVP de gobernanza. Cada uno se representará en la implementación del MVP de gobernanza.

Administración de costos:

- Con fines de seguimiento, todos los recursos deben asignarse a un propietario de aplicación dentro de una de las principales funciones empresariales.
- Cuando surjan problemas de costos, se establecerán requisitos de gobernanza adicionales con el equipo de finanzas.

Base de referencia de seguridad:

- Cualquier recurso implementado en la nube debe tener una clasificación de datos aprobada.
- Ningún recurso identificado con un nivel de datos protegidos se puede implementar en la nube, hasta que se aprueben e implementen los suficientes requisitos de seguridad y gobernanza.
- Hasta que se puedan validar y gobernar los requisitos mínimos de seguridad de red, los entornos en la nube se perciben como una zona desmilitarizada y deben cumplir con requisitos de conexión similares a otros centros de datos o redes internas.

Coherencia de recursos:

- Dado que no se implementa ninguna carga de trabajo crítica en esta fase, no hay ningún requisito de SLA, rendimiento o BCDR que se deba gobernar.
- Cuando se implementen cargas de trabajo críticas, se establecerán requisitos de gobernanza adicionales con las operaciones de TI.

Base de referencia de identidad:

- todos los recursos que se implementan en la nube deben controlarse mediante identidades y roles aprobados por las directivas de gobernanza actuales.
- todos los grupos de la infraestructura local de Active Directory que tienen privilegios elevados deben asignarse a un rol RBAC aprobado.

Aceleración de la implementación:

- Todos los recursos se deben agrupar y etiquetar en función de las estrategias de agrupación y etiquetado definidas.
- Todos los recursos deben usar un modelo de implementación aprobado.
- Una vez que se ha establecido una base de gobernanza para un proveedor de nube, las herramientas de implementación deben ser compatibles con las herramientas definidas por el equipo de gobernanza.

## <a name="processes"></a>Procesos

No se ha asignado ningún presupuesto para la supervisión en curso y el cumplimiento de estas directivas de gobernanza. Por este motivo, el equipo de gobernanza de la nube tiene algunas maneras ad hoc para supervisar el cumplimiento de las declaraciones de las directivas.

- **Educación:** el equipo de gobernanza de la nube está invirtiendo tiempo en formar a los equipos de adopción de la nube en las guías de gobernanza que admiten estas directivas.
- **Revisiones de la implementación:** antes de implementar cualquier recurso, el equipo de gobernanza de la nube revisará la guía de gobernanza con los equipos de adopción de la nube.
