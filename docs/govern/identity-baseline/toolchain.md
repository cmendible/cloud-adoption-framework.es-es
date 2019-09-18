---
title: Herramientas de la base de referencia de identidad en Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Herramientas de la base de referencia de identidad en Azure
author: BrianBlanchard
ms.author: brblanch
ms.date: 02/11/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: 8a0de3d3cc5174e3e18bdca4af8c7f314eead59d
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031271"
---
# <a name="identity-baseline-tools-in-azure"></a>Herramientas de la base de referencia de identidad en Azure

La [base de referencia de la identidad](./index.md) es una de las [cinco materias de gobernanza de la nube](../governance-disciplines.md). Esta materia se centra en las maneras de establecer directivas que garanticen la coherencia y continuidad de las identidades de usuario, independientemente del proveedor de servicios en la nube que hospede la aplicación o carga de trabajo.

Las siguientes herramientas se incluyen en la Guía de descubrimiento de la identidad híbrida.

**Active Directory (local):** Active Directory es el proveedor de identidades que más se usa en la empresa para almacenar y validar credenciales de usuario.

**Azure Active Directory:** un equivalente de software como servicio (SaaS) a Active Directory, capaz de federarse con una instancia local de Active Directory.

**Active Directory (IaaS):** una instancia de la aplicación de Active Directory que se ejecuta en una máquina virtual de Azure.

Identidad es el plano de control de la seguridad de TI. Por consiguiente, la autenticación es la forma de proteger el acceso de una organización a la nube. Las organizaciones necesitan un plano de control de identidad que fortalezca su seguridad y mantenga las aplicaciones en la nube a salvo de intrusos.

## <a name="cloud-authentication"></a>Autenticación en la nube

La elección del método de autenticación correcto es la primera preocupación para las organizaciones que desean mover sus aplicaciones a la nube.

Cuando se elige este método, Azure AD controla el proceso de inicio de sesión de los usuarios. Junto con el inicio de sesión único (SSO) completo, los usuarios pueden iniciar sesión en las aplicaciones en la nube sin tener que volver a escribir sus credenciales. Con la autenticación en la nube puede elegir entre dos opciones:

**Sincronización de hash de contraseñas de Azure AD:** Es la manera más sencilla de habilitar la autenticación para los objetos de directorio local en Azure AD. Este método también se puede usar utiliza con cualquier otro como método de autenticación de la conmutación por error de copia de seguridad, en caso de que el servidor local deje de funcionar.

**Autenticación de paso a través de Azure AD:** proporciona una validación de contraseñas persistente para los servicios de autenticación de Azure AD mediante un agente de software que se ejecuta en uno o varios servidores locales.

> [!NOTE]
> Las empresas con un requisito de seguridad para aplicar de inmediato los estados de cuenta de los usuarios locales, las directivas de contraseña y las horas de inicio de sesión deberían considerar la posibilidad de usar el método de autenticación de paso a través.

**Autenticación federada:**

si se elige este método, Azure AD pasa el proceso de autenticación a un sistema de autenticación de confianza como, por ejemplo, una instancia local de Servicios de federación de Active Directory (AD FS) o un proveedor de federación independiente de confianza para validar la contraseña del usuario.

El artículo [Elección del método de autenticación adecuado para Azure Active Directory](https://docs.microsoft.com/azure/security/azure-ad-choose-authn) contiene un árbol de decisión que le ayuda a elegir la mejor solución para su organización.

La siguiente tabla enumera las herramientas nativas que pueden ayudar a desarrollar las directivas y los procesos que admiten esta materia sobre gobernanza.

<!-- markdownlint-disable MD033 -->

|Consideración|Sincronización de hash de contraseñas + SSO de conexión directa|Autenticación de paso a través + SSO de conexión directa|Federación con AD FS|
|:-----|:-----|:-----|:-----|
|¿Dónde se realiza la autenticación?|En la nube|En la nube, después de un intercambio de comprobación de contraseña segura con el agente de autenticación local|Local|
|¿Cuáles son los requisitos de servidor local más allá del sistema de aprovisionamiento (Azure AD Connect)?|None|Un servidor para cada agente de autenticación adicional|Dos o más servidores de AD FS<br><br>Dos o más servidores WAP en la red perimetral o DMZ|
|¿Cuáles son los requisitos de redes e Internet locales más allá del sistema de aprovisionamiento?|None|[Acceso saliente a Internet](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta-quick-start) desde los servidores que ejecutan los agentes de autenticación|[Acceso entrante a Internet](https://docs.microsoft.com/windows-server/identity/ad-fs/overview/ad-fs-requirements) para los servidores WAP del perímetro<br><br>Acceso entrante de red para los servidores de AD FS desde los servidores WAP del perímetro<br><br>Equilibrio de carga de red|
|¿Hay algún requisito de certificado SSL?|Sin|No|Sí|
|¿Hay alguna solución de supervisión de estado?|No se requiere|El estado del agente lo proporciona el [Centro de administración de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/hybrid/tshoot-connect-pass-through-authentication)|[Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-health-adfs)|
|¿Los usuarios realizan el inicio de sesión único en los recursos de nube desde dispositivos unidos a un dominio de la red de la empresa?|Sí, con [SSO de conexión directa](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)|Sí, con [SSO de conexión directa](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)|Sí|
|¿Qué tipos de inicio de sesión se admiten?|UserPrincipalName + contraseña<br><br>Autenticación integrada de Windows con [SSO de conexión directa](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)<br><br>[Identificador de inicio de sesión alternativo](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-custom)|UserPrincipalName + contraseña<br><br>Autenticación integrada de Windows con [SSO de conexión directa](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)<br><br>[Identificador de inicio de sesión alternativo](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta-faq)|UserPrincipalName + contraseña<br><br>sAMAccountName + contraseña<br><br>Autenticación integrada de Windows<br><br>[Autenticación de certificados y tarjetas inteligentes](/windows-server/identity/ad-fs/operations/configure-user-certificate-authentication)<br><br>[Identificador de inicio de sesión alternativo](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)|
|¿Se admite Windows Hello para empresas?|[Modelo de confianza de clave](/windows/security/identity-protection/hello-for-business/hello-identity-verification)<br><br>[Modelo de confianza de certificado con Intune](https://microscott.azurewebsites.net/2017/12/16/setting-up-windows-hello-for-business-with-intune)|[Modelo de confianza de clave](/windows/security/identity-protection/hello-for-business/hello-identity-verification)<br><br>[Modelo de confianza de certificado con Intune](https://microscott.azurewebsites.net/2017/12/16/setting-up-windows-hello-for-business-with-intune)|[Modelo de confianza de clave](/windows/security/identity-protection/hello-for-business/hello-identity-verification)<br><br>[Modelo de confianza de certificado](/windows/security/identity-protection/hello-for-business/hello-key-trust-adfs)|
|¿Cuáles son las opciones de autenticación multifactor?|[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication)<br><br>[Controles personalizados con acceso condicional*](https://docs.microsoft.com/azure/active-directory/conditional-access/controls#custom-controls-preview)|[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication)<br><br>[Controles personalizados con acceso condicional*](https://docs.microsoft.com/azure/active-directory/conditional-access/controls#custom-controls-preview)|[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication)<br><br>[Servidor de Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/active-directory/authentication/howto-mfaserver-deploy)<br><br>[Autenticación multifactor de terceros](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs)<br><br>[Controles personalizados con acceso condicional*](https://docs.microsoft.com/azure/active-directory/conditional-access/controls#custom-controls-preview)|
|¿Qué estados de cuenta de usuario se admiten?|Cuentas deshabilitadas<br>(retraso de hasta 30 minutos)|Cuentas deshabilitadas<br><br>Cuenta bloqueada<br><br>Cuenta expirada<br><br>Contraseña expirada<br><br>Horas de inicio de sesión|Cuentas deshabilitadas<br><br>Cuenta bloqueada<br><br>Cuenta expirada<br><br>Contraseña expirada<br><br>Horas de inicio de sesión|
|¿Cuáles son las opciones de acceso condicional?|[Acceso condicional de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)|[Acceso condicional de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)|[Acceso condicional de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)<br><br>[Reglas de notificaciones de AD FS](https://adfshelp.microsoft.com/AadTrustClaims/ClaimsGenerator)|
|¿Se admite el bloqueo de protocolos heredados?|[Sí](https://docs.microsoft.com/azure/active-directory/conditional-access/howto-baseline-protect-legacy-auth)|[Sí](https://docs.microsoft.com/azure/active-directory/conditional-access/howto-baseline-protect-legacy-auth)|[Sí](/windows-server/identity/ad-fs/operations/access-control-policies-w2k12)|
|¿Se puede personalizar el logotipo, la imagen y la descripción en las páginas de inicio de sesión?|[Sí, con Azure AD Premium](https://docs.microsoft.com/azure/active-directory/customize-branding)|[Sí, con Azure AD Premium](https://docs.microsoft.com/azure/active-directory/customize-branding)|[Sí](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-management#customlogo)|
|¿Qué escenarios avanzados se admiten?|[Smart Password Lockout](https://docs.microsoft.com/azure/active-directory/active-directory-secure-passwords) (Bloqueo inteligente de contraseñas)<br><br>[Informes de credenciales filtradas](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-risk-events)|[Smart Password Lockout](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-pass-through-authentication-smart-lockout) (Bloqueo inteligente de contraseñas)|Sistema de autenticación multisitio de baja latencia<br><br>[Bloqueo de extranet de AD FS](/windows-server/identity/ad-fs/operations/configure-ad-fs-extranet-soft-lockout-protection)<br><br>[Integración con sistemas de identidad de terceros](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-compatibility)|

<!-- markdownlint-enable MD033 -->

> [!NOTE]
> Actualmente, los controles personalizados del acceso condicional de Azure AD no admiten el registro de dispositivos.

## <a name="next-steps"></a>Pasos siguientes

Las [notas del producto del marco de transformación digital de la identidad híbrida](https://resources.office.com/ww-landing-M365E-EMS-IDAM-Hybrid-Identity-WhitePaper.html?LCID=EN-US) describe diversas combinaciones y soluciones para elegir e integrar estos componentes.

La herramienta [Azure AD Connect](https://aka.ms/aadconnectwiz) le permite integrar sus directorios locales con Azure AD.
