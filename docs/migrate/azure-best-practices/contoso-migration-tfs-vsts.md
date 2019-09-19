---
title: Refactorización de una implementación de Team Foundation Server a Azure DevOps Services en Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información sobre cómo Contoso refactoriza su implementación de TFS local mediante la migración a Azure DevOps Services en Azure.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: 43e577eb429928efd0857549319e46a36c49a9e1
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71025091"
---
# <a name="refactor-a-team-foundation-server-deployment-to-azure-devops-services"></a>Refactorizar una implementación de Team Foundation Server a Azure DevOps Services

En este artículo se muestra cómo la empresa ficticia Contoso refactoriza su implementación de Team Foundation Server (TFS) en el entorno local mediante la migración a Azure DevOps Services en Azure. El equipo de desarrollo de Contoso ha utilizado TFS para la colaboración en equipo y el control de código fuente durante los últimos cinco años. Ahora, quiere pasar a una solución basada en la nube para el trabajo de desarrollo y pruebas, y para el control de código fuente. Azure DevOps Services jugará un papel importante a medida que Contoso cambie a un modelo de Azure DevOps, y desarrollará nuevas aplicaciones nativas de la nube.

## <a name="business-drivers"></a>Impulsores del negocio

El equipo de liderazgo de TI ha trabajado estrechamente con socios comerciales para identificar los objetivos futuros. Los asociados no están demasiado preocupados por las tecnologías ni las herramientas de desarrollo, pero han capturado estos puntos:

- **Software:** Sin tener en cuenta el negocio principal, todas las compañías ahora son compañías de software, incluida Contoso. El liderazgo empresarial está interesado en cómo el departamento de TI puede ayudar a liderar la empresa con nuevas prácticas de trabajo para los usuarios y experiencias para sus clientes.
- **Eficacia:** Contoso debe eliminar los procedimientos innecesarios y optimizar los procesos para los desarrolladores y usuarios. Esto permitirá a la empresa cumplir los requisitos de los clientes de manera más eficaz. La empresa necesita que el departamento de TI sea rápido, sin perder tiempo ni dinero.
- **Agilidad:** El Departamento de TI de Contoso debe responder a las necesidades empresariales y reaccionar más rápidamente que el mercado para permitir el éxito en una economía global. Así mismo, no debe ser un impedimento para la empresa.

## <a name="migration-goals"></a>Objetivos de la migración

El equipo de la nube de Contoso ha establecido los objetivos de la migración a Azure DevOps Services:

- El equipo necesita una herramienta para migrar los datos a la nube. Es posible que sean necesarios algunos procesos manuales.
- El historial y los datos de elementos de trabajo del año pasado deberán migrarse.
- No quiere configurar nuevos nombres de usuario ni contraseñas. Se deben mantener todas las asignaciones del sistema actual.
- Quiere cambiar del Control de versiones de Team Foundation (TFVC) a GIT para el control de código fuente.
- La transición a GIT será una "migración sugerida" que importa solo la versión más reciente del código fuente. Ocurrirá durante un tiempo de inactividad y se detendrá todo el trabajo mientras se desplace el código base. Se entiende que únicamente el historial de la rama maestra actual estará disponible después del movimiento.
- Está preocupado por el cambio y quiere probarlo antes de completarlo totalmente. Quiere conservar el acceso a TFS incluso después de la migración a Azure DevOps Services.
- Tiene varias colecciones y quiere empezar por una que tenga solo unos pocos proyectos para comprender mejor el proceso.
- Comprende que las colecciones de TFS son una relación uno a uno con cuentas de Azure DevOps Services, por lo que tendrá varias direcciones URL. Sin embargo, esto coincide con el modelo actual de separación para proyectos y bases de código.

## <a name="proposed-architecture"></a>Arquitectura propuesta

- Contoso moverá sus proyectos de TFS a la nube y dejará de hospedar sus proyectos o control de código fuente localmente.
- TFS se migrará a Azure DevOps Services.
- Actualmente, Contoso tiene una colección de TFS denominada `ContosoDev`, que se migrará a una organización Azure DevOps Services denominada `contosodevmigration.visualstudio.com`.
- Los proyectos, los elementos de trabajo, los errores y las iteraciones del último año se migrarán a Azure DevOps Services.
- Contoso usará su instancia de Azure Active Directory, que se configuró al [implementar su infraestructura de Azure](./contoso-migration-infrastructure.md) al principio del planeamiento de la migración.

![Arquitectura del escenario](./media/contoso-migration-tfs-vsts/architecture.png)

## <a name="migration-process"></a>Proceso de migración

Contoso completará el proceso de migración como se indica a continuación:

1. El proceso requiere mucha preparación. Como primer paso, Contoso debe actualizar su implementación de TFS a un nivel admitido. Contoso ejecuta actualmente TFS 2017 Update 3, pero para usar la migración de base de datos es necesario ejecutar una versión de 2018 compatible con las actualizaciones más recientes.
2. Después de la actualización, Contoso ejecutará la herramienta de migración de TFS y validará su colección.
3. Contoso compilará un conjunto de archivos de preparación y realizará un simulacro de migración de prueba.
4. Después, Contoso ejecutará otra migración, esta vez una migración completa, que incluye elementos de trabajo, errores, sprints y código.
5. Después de la migración, Contoso moverá el código de TFVC a GIT.

![Proceso de migración](./media/contoso-migration-tfs-vsts/migration-process.png)

## <a name="prerequisites"></a>Requisitos previos

Esto es lo que tiene hacer Contoso para ejecutar este escenario.

<!-- markdownlint-disable MD033 -->

**Requisitos** | **Detalles**
--- | ---
**Suscripción de Azure** | En un artículo anterior de esta serie, Contoso creó suscripciones. Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Si crea una cuenta gratuita, será el administrador de su suscripción y podrá realizar todas las acciones.<br/><br/> Si usa una suscripción existente y no es el administrador, tendrá que solicitar al administrador que le asigne permisos de propietario o colaborador.<br/><br/> Si necesita permisos más específicos, consulte [este artículo](https://docs.microsoft.com/azure/site-recovery/site-recovery-role-based-linked-access-control).
**Infraestructura de Azure** | Contoso configura la infraestructura de Azure según se describe en [Infraestructura de Azure para la migración](./contoso-migration-infrastructure.md).
**Servidor TFS local** | En el entorno local, se debe ejecutar TFS 2018 Upgrade 2 o actualizarse a él como parte de este proceso.

## <a name="scenario-steps"></a>Pasos del escenario

Así es como Azure realizará la migración:

> [!div class="checklist"]
>
> - **Paso 1: Creación de una cuenta de almacenamiento de Azure.** Esta cuenta de almacenamiento se usará durante el proceso de migración.
> - **Paso 2: Actualización de TFS.** Contoso actualizará su implementación a TFS 2018 Upgrade 2.
> - **Paso 3: Validación de la colección.** Contoso validará la colección de TFS para prepararla para la migración.
> - **Paso 4: Compilación del archivo de preparación.** Contoso creará los archivos de migración mediante la herramienta de migración de TFS.

## <a name="step-1-create-a-storage-account"></a>Paso 1: Crear una cuenta de almacenamiento

1. En Azure Portal, los administradores de Contoso crean una cuenta de almacenamiento (**contosodevmigration**).
2. La cuenta se colocará en la región secundaria que se usa para la conmutación por error: Centro de EE. UU. Se usa una cuenta de uso general estándar con almacenamiento con redundancia local.

    ![Cuenta de almacenamiento](./media/contoso-migration-tfs-vsts/storage1.png)

**¿Necesita más ayuda?**

- [Introducción a Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-introduction).
- [Crear una cuenta de almacenamiento](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).

## <a name="step-2-upgrade-tfs"></a>Paso 2: Actualizar TFS

Los administradores de Contoso actualizan el servidor de TFS a TFS 2018 Update 2. Antes de empezar:

- Contoso descarga [TFS 2018 Update 2](https://visualstudio.microsoft.com/downloads).
- Verifica los [requisitos de hardware](https://docs.microsoft.com/tfs/server/requirements) y lee las [notas de la versión](https://docs.microsoft.com/visualstudio/releasenotes/tfs2018-relnotes) y los [problemas de la actualización](https://docs.microsoft.com/tfs/server/upgrade/get-started#before-you-upgrade-to-tfs-2018).

Realiza la actualización como se muestra a continuación:

1. Para empezar, realiza una copia de seguridad de su servidor TFS (que se ejecuta en una máquina virtual de VMware) y toma una instantánea de VMware.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade1.png)

2. Se inicia el programa de instalación TFS y elige la ubicación de instalación. El instalador necesita acceso a Internet.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade2.png)

3. Una vez finalizada la instalación, se inicia el Asistente para configuración de servidor.

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade3.png)

4. Después de la verificación, el asistente completa la actualización.

     ![TFS](./media/contoso-migration-tfs-vsts/upgrade4.png)

5. Comprueban la instalación de TFS, para lo que revisan los proyectos, los elementos de trabajo y el código.

     ![TFS](./media/contoso-migration-tfs-vsts/upgrade5.png)

> [!NOTE]
> Algunas actualizaciones de TFS deben ejecutar el asistente de configuración de características una vez finalizada la actualización. [Más información](https://docs.microsoft.com/azure/devops/reference/configure-features-after-upgrade?utm_source=ms&utm_medium=guide&utm_campaign=vstsdataimportguide&view=vsts).

**¿Necesita más ayuda?**

Obtenga información sobre la [actualización de TFS](/tfs/server/upgrade/get-started).

## <a name="step-3-validate-the-tfs-collection"></a>Paso 3: Validar la colección de TFS

Los administradores de Contoso ejecutan la herramienta de migración de TFS en la base de datos de la colección de ContosoDev para validarla antes de la migración.

1. Descargan y descomprimen la [herramienta de migración de TFS](https://www.microsoft.com/download/details.aspx?id=54274). Es importante descargar la versión para la actualización de TFS que se está ejecutando. La versión puede comprobarse en la consola de administración.

    ![TFS](./media/contoso-migration-tfs-vsts/collection1.png)

2. Ejecuta la herramienta para llevar a cabo la validación, mediante la especificación de la dirección URL de la colección de proyectos:

        `TfsMigrator validate /collection:http://contosotfs:8080/tfs/ContosoDev`

3. La herramienta muestra un error.

    ![TFS](./media/contoso-migration-tfs-vsts/collection2.png)

4. Se encuentran los archivos de registro en la carpeta `Logs`, justo antes de la ubicación de la herramienta. Se genera un archivo de registro para cada validación principal. `TfsMigration.log` contiene la información principal.

    ![TFS](./media/contoso-migration-tfs-vsts/collection3.png)

5. Encuentra esta entrada relacionada con la identidad.

    ![TFS](./media/contoso-migration-tfs-vsts/collection4.png)

6. Se ejecuta `TfsMigrator validate /help` en la línea de comandos y se observa que el comando `/tenantDomainName` parece ser necesario para validar las identidades.

     ![TFS](./media/contoso-migration-tfs-vsts/collection5.png)

7. Se vuelve a ejecutar el comando de validación y se incluye este valor, junto con su nombre de Azure AD: `TfsMigrator validate /collection: http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com`.

    ![TFS](./media/contoso-migration-tfs-vsts/collection7.png)

8. Aparece la pantalla de inicio de sesión de Azure AD y se escriben las credenciales de un usuario administrador global.

     ![TFS](./media/contoso-migration-tfs-vsts/collection8.png)

9. La validación se pasa y la herramienta la confirma.

    ![TFS](./media/contoso-migration-tfs-vsts/collection9.png)

## <a name="step-4-create-the-migration-files"></a>Paso 4: Crear los archivos de migración

Con la validación completa, los administradores de Contoso pueden usar la herramienta de migración de TFS para compilar los archivos de migración.

1. Ejecuta el paso de preparación en la herramienta.

    `TfsMigrator prepare /collection:http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com /accountRegion:cus`

     ![Preparación](./media/contoso-migration-tfs-vsts/prep1.png)

    La preparación hace lo siguiente:
    - Examina la colección para obtener una lista de todos los usuarios y rellena el registro de mapa de identificación (**IdentityMapLog.csv**).
    - Prepara la conexión a Azure Active Directory para buscar una coincidencia para cada identidad.
    - Contoso ya ha implementado y sincronizado Azure AD con Azure AD Connect, por lo que con la preparación se deberían poder buscar las identidades coincidentes y marcarlas como activas.

2. Aparece la pantalla de inicio de sesión de Azure AD y se escriben las credenciales de un administrador global.

    ![Preparación](./media/contoso-migration-tfs-vsts/prep2.png)

3. La preparación se completa, y la herramienta notifica que se han generado correctamente los archivos de importación.

    ![Preparación](./media/contoso-migration-tfs-vsts/prep3.png)

4. Ya pueden ver que los archivos IdentityMapLog.csv y import.json se han creado en una carpeta nueva.

    ![Preparación](./media/contoso-migration-tfs-vsts/prep4.png)

5. El archivo import.json proporciona opciones de importación. Incluye información como el nombre de organización deseado e información de la cuenta de almacenamiento. La mayoría de los campos se rellenan automáticamente. Algunos campos requieren la intervención del usuario. Contoso abre el archivo y agrega el nombre de la organización de Azure DevOps Services que se va a crear: **contosodevmigration**. Con este nombre, su dirección URL de Azure DevOps Services será **contosodevmigration.visualstudio.com**.

    ![Preparación](./media/contoso-migration-tfs-vsts/prep5.png)

    > [!NOTE]
    > La organización se debe crear antes de la migración y se puede cambiar una vez concluida.

6. Revisa el archivo de asignación de registros de identidad en el que se muestran las cuentas que se van a incluir en Azure DevOps Services durante la importación.

    - Las identidades activas hacen referencia a las identidades que se convertirán en usuarios de Azure DevOps Services después de la importación.
    - En Azure DevOps Services, se concederá una licencia a estas identidades y se mostrarán como un usuario en la organización después de la migración.
    - Estas identidades se marcan como **Active**  (Activas) en la columna **Expected Import Status**  (Estado de importación esperado) del archivo.

    ![Preparación](./media/contoso-migration-tfs-vsts/prep6.png)

## <a name="step-5-migrate-to-azure-devops-services"></a>Paso 5: Migrar a Azure DevOps Services

Una vez realizada la preparación, los administradores de Contoso pueden centrarse en la migración. Después de ejecutar la migración, pasará de usar TFVC a usar GIT para el control de versiones.

Antes de empezar, los administradores programan el tiempo de inactividad con el equipo de desarrollo, para desconectar la colección para la migración. Estos son los pasos para el proceso de migración:

1. **Desasociar la colección.** Los datos de identidad de la colección residen en la base de datos de configuración del servidor de TFS mientras la colección está adjunta y en línea. Cuando se desasocia una colección del servidor TFS, esta toma una copia de los datos de identidad y la empaqueta con la colección para el transporte. Sin estos datos, no se puede ejecutar la parte de la identidad de la importación. Se recomienda que la colección permanezca desasociada hasta que se complete la importación, ya que no hay ninguna manera de importar los cambios que se produjeron durante la importación.
2. **Generar una copia de seguridad.** El siguiente paso del proceso de migración consiste en generar una copia de seguridad que se pueda importar en Azure DevOps Services. Los paquetes de componentes de aplicación de capa de datos (DACPAC) son una característica de SQL Server que permite que los cambios de la base de datos se empaqueten en un único archivo e implementen en otras instancias de SQL. También se pueden restaurar directamente en Azure DevOps Services y, por tanto, usarse como método de empaquetado para introducir los datos de la colección en la nube. Contoso usará la herramienta SqlPackage.exe para generar el archivo DACPAC. Esta herramienta se incluye en SQL Server Data Tools.
3. **Cargar en el almacenamiento.** Tras crear el archivo DACPAC, lo cargan en Azure Storage. Una vez cargado, obtiene una firma de acceso compartido (SAS), para permitir el acceso de la herramienta de migración de TFS al almacenamiento.
4. **Rellenar la importación.** A continuación, Contoso puede rellenar los campos que faltan en el archivo de importación, incluida la configuración de DACPAC. Para empezar, especificará que quiere hacer una importación de **simulacro** para comprobar que todo funciona correctamente antes de la migración completa.
5. **Hacer un simulacro.** El simulacro de importaciones ayuda a probar la migración de la colección. Los simulacros tienen una vida limitada y se eliminan antes de que se ejecute la migración de producción. Se eliminan automáticamente tras un período determinado. Se incluye una nota acerca de cuándo se eliminará el simulacro en el correo electrónico de operación correcta que se recibirá cuando finalice la importación. Le recomendamos anotar la fecha y realizar una planeación en consecuencia.
6. **Completar la migración de producción.** Una vez completado el simulacro de migración, los administradores de Contoso realizan la migración final actualizando el archivo **import.json** y volviendo a ejecutar la importación.

### <a name="detach-the-collection"></a>Desasociar la colección

Antes de empezar, los administradores de Contoso realizan una copia de seguridad local de SQL Server y una instantánea de VMware del servidor TFS antes de realizar la desasociación.

1. En la consola de administración de TFS, se selecciona la recopilación que se quiere desasociar (**ContosoDev**).

    ![Migrar](./media/contoso-migration-tfs-vsts/migrate1.png)

2. En **General**, se selecciona **Desasociar colección**.

    ![Migrar](./media/contoso-migration-tfs-vsts/migrate2.png)

3. En Detach Team Project Collection Wizard (Asistente de la colección de proyectos de equipo para desasociar) > **Mensaje de mantenimiento**, proporciona un mensaje para los usuarios que puede que intenten conectarse a proyectos de la colección.

    ![Migrar](./media/contoso-migration-tfs-vsts/migrate3.png)

4. En **Progreso de desasociación**, se supervisa el progreso y, cuando el proceso finaliza, se selecciona **Siguiente**.

    ![Migrar](./media/contoso-migration-tfs-vsts/migrate4.png)

5. En **Comprobaciones de disponibilidad**, al finalizar las comprobaciones, se selecciona **Desasociar**.

    ![Migrar](./media/contoso-migration-tfs-vsts/migrate5.png)

6. Para finalizar, se selecciona **Cerrar**.

    ![Migrar](./media/contoso-migration-tfs-vsts/migrate6.png)

7. Ya no se hace referencia a la colección en la consola de administración de TFS.

    ![Migrar](./media/contoso-migration-tfs-vsts/migrate7.png)

### <a name="generate-a-dacpac"></a>Generar un archivo DACPAC

Contoso crea una copia de seguridad (DACPAC) para la importación en Azure DevOps Services.

- SqlPackage.exe en SQL Server Data Tools se usa para crear el archivo DACPAC. Hay varias versiones de SqlPackage.exe que se instalan con SQL Server Data Tools, ubicadas en carpetas con nombres como 120, 130 y 140. Es importante usar la versión correcta para preparar el archivo DACPAC.
- Las importaciones de TFS 2018 deben usar SqlPackage.exe desde la carpeta 140 o superior. Para CONTOSOTFS, este archivo se encuentra en la carpeta: **C:\Archivos de programa (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Extensions\Microsoft\SQLDB\DAC\140**.

Los administradores de Contoso generan el archivo DACPAC como se indica a continuación:

1. Abre un símbolo del sistema y se desplaza hasta la ubicación de SQLPackage.exe. Escribe el comando siguiente para generar el archivo DACPAC:

    ``` console
    SqlPackage.exe /sourceconnectionstring:"Data Source=SQLSERVERNAME\INSTANCENAME;Initial Catalog=Tfs_ContosoDev;Integrated Security=True" /targetFile:C:\TFSMigrator\Tfs_ContosoDev.dacpac /action:extract /p:ExtractAllTableData=true /p:IgnoreUserLoginMappings=true /p:IgnorePermissions=true /p:Storage=Memory
    ```

    ![Copia de seguridad](./media/contoso-migration-tfs-vsts/backup1.png)

2. Aparece el siguiente mensaje después de que se ejecute el comando.

    ![Copia de seguridad](./media/contoso-migration-tfs-vsts/backup2.png)

3. Verifica las propiedades del archivo DACPA.

    ![Copia de seguridad](./media/contoso-migration-tfs-vsts/backup3.png)

### <a name="update-the-file-to-storage"></a>Actualizar el archivo al almacenamiento

Una vez creado el archivo de DACPAC, Contoso lo carga en Azure Storage.

1. Descarga e instala el [Explorador de Azure Storage](https://azure.microsoft.com/features/storage-explorer).

    ![Cargar](./media/contoso-migration-tfs-vsts/backup5.png)

2. Se conecta a su suscripción y localiza la cuenta de almacenamiento que se creó para la migración (**contosodevmigration**). Crea un contenedor de blobs, **azuredevopsmigration**.

    ![Cargar](./media/contoso-migration-tfs-vsts/backup6.png)

3. Especifica el archivo DACPAC para la carga como un blob en bloques.

    ![Cargar](./media/contoso-migration-tfs-vsts/backup7.png)

4. Después de cargar el archivo, se selecciona el nombre de archivo > **Generar SAS**. Se expanden los contenedores de blobs en la cuenta de almacenamiento, se selecciona el contenedor con los archivos de importación y se selecciona **Obtener firma de acceso compartido**.

    ![Cargar](./media/contoso-migration-tfs-vsts/backup8.png)

5. Se aceptan los valores predeterminados y se selecciona **Crear**. Esto permite el acceso durante 24 horas.

    ![Cargar](./media/contoso-migration-tfs-vsts/backup9.png)

6. Copia la URL de Firma de acceso compartido, para que la pueda usar la herramienta de migración de TFS.

    ![Cargar](./media/contoso-migration-tfs-vsts/backup10.png)

> [!NOTE]
> La migración debe realizarse antes de que transcurra el tiempo permitido o los permisos expirarán.
> No genere ninguna clave SAS desde Azure Portal. Las claves generadas así son para el ámbito de cuenta y no funcionarán con la importación.

### <a name="fill-in-the-import-settings"></a>Rellenar la configuración de importación

Anteriormente, los administradores de Contoso rellenaron de forma parcial el archivo de especificación de importación (import.json). Ahora, debe agregar el resto de configuraciones.

Abre el archivo import.json y rellena los campos siguientes:

- **Ubicación:** Ubicación de la clave SAS que se generó anteriormente.
- **Dacpac:** Establece el nombre en el archivo DACPAC que cargó en la cuenta de almacenamiento. Incluye la extensión ".dacpac".
- **ImportType:** Se establece en DryRun por ahora.

![Importar configuración](./media/contoso-migration-tfs-vsts/import1.png)

### <a name="do-a-dry-run-migration"></a>Realizar una migración de simulacro

Los administradores de Contoso comienzan con un simulacro de migración para asegurarse de que todo funciona de la forma esperada.

1. Abre un símbolo del sistema y va a la ubicación de TfsMigration (`C:\TFSMigrator`).
2. Como primer paso, valida el archivo de importación. Quiere asegurarse de que el archivo tiene el formato correcto y de que la clave SAS está funcionando.

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly`

3. La validación devuelve un error que indica que la clave SAS necesita un tiempo de expiración más largo.

    ![Simulacro](./media/contoso-migration-tfs-vsts/test1.png)

4. Usa el Explorador de Azure Storage para crear una nueva clave SAS cuya expiración se establece en siete días.

    ![Simulacro](./media/contoso-migration-tfs-vsts/test2.png)

5. Actualiza el archivo `import.json` y ejecuta nuevamente la validación. Ahora, se completa correctamente.

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly`

    ![Simulacro](./media/contoso-migration-tfs-vsts/test3.png)

6. Se inicia el simulacro:

    `TfsMigrator import /importFile:C:\TFSMigrator\import.json`

7. Se emite un mensaje para confirmar la migración. Tenga en cuenta el período de tiempo durante el cual se mantendrán los datos almacenados provisionalmente después del simulacro.

    ![Simulacro](./media/contoso-migration-tfs-vsts/test4.png)

8. Se muestra el inicio de sesión de Azure AD que debería completarse con el inicio de sesión de administración de Contoso.

    ![Simulacro](./media/contoso-migration-tfs-vsts/test5.png)

9. Se muestra un mensaje con información acerca de la importación.

    ![Simulacro](./media/contoso-migration-tfs-vsts/test6.png)

10. Alrededor de 15 minutos después, consultan la dirección URL y ven la siguiente información:

     ![Simulacro](./media/contoso-migration-tfs-vsts/test7.png)

11. Después de que finalice la migración, un director de desarrollo de Contoso inicia sesión en Azure DevOps Services para comprobar que el simulacro ha funcionado correctamente. Después de la autenticación, Azure DevOps Services necesita algunos detalles para confirmar la organización.

    ![Simulacro](./media/contoso-migration-tfs-vsts/test8.png)

12. En Azure DevOps Services, el director de desarrollo puede ver que los proyectos se han migrado a Azure DevOps Services. Hay un aviso de que la organización se eliminará en 15 días.

    ![Simulacro](./media/contoso-migration-tfs-vsts/test9.png)

13. El director de desarrollo abre uno de los proyectos y abre **Elementos de trabajo** > **Asignados a mí**. Esto muestra que se han migrado los datos de los elementos de trabajo, junto con su identidad.

    ![Simulacro](./media/contoso-migration-tfs-vsts/test10.png)

14. El director de desarrollo también comprueba otros proyectos y el código, con el fin de confirmar que se han migrado el código fuente y el historial.

    ![Simulacro](./media/contoso-migration-tfs-vsts/test11.png)

### <a name="run-the-production-migration"></a>Ejecutar la migración de producción

Una vez que se ha completado el simulacro, los administradores de Contoso pasan a la migración de producción. Elimina el simulacro, actualiza la configuración de importación y vuelve a ejecutar la importación.

1. En el portal de Azure DevOps Services, se elimina la organización de simulacro.
2. Actualiza el archivo import.json para establecer **ImportType** en **ProductionRun**.

    ![Producción](./media/contoso-migration-tfs-vsts/full1.png)

3. Inicia la migración tal como lo hizo con el simulacro: `TfsMigrator import /importFile:C:\TFSMigrator\import.json`.
4. Se muestra un mensaje para confirmar la migración y se advierte de que es posible que los datos se queden almacenados en una ubicación segura, como un área de almacenamiento provisional, durante un máximo de siete días.

    ![Producción](./media/contoso-migration-tfs-vsts/full2.png)

5. En el inicio de sesión de Azure AD, especifican un inicio de sesión de administrador de Contoso.

    ![Producción](./media/contoso-migration-tfs-vsts/full3.png)

6. Se muestra un mensaje con información acerca de la importación.

    ![Producción](./media/contoso-migration-tfs-vsts/full4.png)

7. Aproximadamente 15 minutos después, se desplazan a la dirección URL y ven la siguiente información:

    ![Producción](./media/contoso-migration-tfs-vsts/full5.png)

8. Después de que finalice la migración, un director de desarrollo de Contoso inicia sesión en Azure DevOps Services para comprobar que la migración ha funcionado correctamente. Después de iniciar sesión, ve que los proyectos se han migrado.

    ![Producción](./media/contoso-migration-tfs-vsts/full6.png)

9. El director de desarrollo abre uno de los proyectos y abre **Elementos de trabajo** > **Asignados a mí**. Esto muestra que se han migrado los datos de los elementos de trabajo, junto con su identidad.

    ![Producción](./media/contoso-migration-tfs-vsts/full7.png)

10. El director de desarrollo comprueba otros datos de elementos de trabajo para confirmarlos.

    ![Producción](./media/contoso-migration-tfs-vsts/full8.png)

11. El director de desarrollo también comprueba otros proyectos y el código, con el fin de confirmar que se han migrado el código fuente y el historial.

    ![Producción](./media/contoso-migration-tfs-vsts/full9.png)

### <a name="move-source-control-from-tfvc-to-git"></a>Mover el control de código fuente de TFVC a GIT

Con la migración completa, Contoso quiere cambiar de TFVC a GIT la administración del código fuente. Debe importar el código fuente actualmente en la organización de Azure DevOps Services como repositorios de Git en la misma organización.

1. En el portal de Azure DevOps Services, abre uno de los repositorios de TFVC ( **$/PolicyConnect**) y lo revisa.

    ![Git](./media/contoso-migration-tfs-vsts/git1.png)

2. Se selecciona el menú desplegable **Código fuente** > **Importación**.

    ![Git](./media/contoso-migration-tfs-vsts/git2.png)

3. En **Tipo de origen**, selecciona **TFVC** y especifica la ruta de acceso al repositorio. Contoso decide no migrar el historial.

    ![Git](./media/contoso-migration-tfs-vsts/git3.png)

    > [!NOTE]
    > Dadas las diferencias en la forma en que TFVC y GIT almacenan la información del control de versiones, se recomienda que Contoso no migre el historial. Este es el enfoque que Microsoft adoptó cuando migró tanto Windows como otros productos desde el control de versiones centralizado a GIT.

4. Después de la importación, los administradores revisan el código.

    ![Git](./media/contoso-migration-tfs-vsts/git4.png)

5. Repite el proceso para el segundo repositorio ( **$/ SmartHotelContainer**).

    ![Git](./media/contoso-migration-tfs-vsts/git5.png)

6. Después de revisar el código fuente, los directores de desarrollo aceptan realizar la migración a Azure DevOps Services. Azure DevOps Services se convierte ahora en el origen de todo el desarrollo dentro de los equipos implicados en la migración.

    ![Git](./media/contoso-migration-tfs-vsts/git6.png)

**¿Necesita más ayuda?**

[Más información](https://docs.microsoft.com/azure/devops/repos/git/import-from-TFVC?view=vsts) sobre la importación desde TFVC.

## <a name="clean-up-after-migration"></a>Limpiar después de la migración

Con la migración completa, Contoso debe hacer lo siguiente:

- Deberá revisar el artículo [posterior a la importación](https://docs.microsoft.com/azure/devops/articles/migration-post-import?view=vsts) para obtener información acerca de las actividades de importación adicionales.
- También deberá eliminar los repositorios TFVC, o definirlos en modo de solo lectura. Las bases de código no deben usarse, pero se puede hacer referencia a su historial.

## <a name="post-migration-training"></a>Entrenamiento posterior a la migración

Contoso tendrá que proporcionar formación sobre Azure DevOps Services y GIT a los miembros del equipo pertinentes.
