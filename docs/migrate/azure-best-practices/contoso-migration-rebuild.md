---
title: Recompilación de una aplicación local en Azure
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga información acerca de cómo Contoso recompila una aplicación en Azure con Azure App Service, Azure Kubernetes Service, Cosmos DB, Azure Functions y Azure Cognitive Services.
author: BrianBlanchard
ms.author: brblanch
ms.date: 10/11/2018
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: migrate
services: site-recovery
ms.openlocfilehash: d98d24e6b2645adf03a94a41b0391b89d5eb2852
ms.sourcegitcommit: a26c27ed72ac89198231ec4b11917a20d03bd222
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2019
ms.locfileid: "70835298"
---
# <a name="rebuild-an-on-premises-app-on-azure"></a>Recompilación de una aplicación local en Azure

En este artículo se muestra cómo la compañía ficticia Contoso recompila una aplicación de Windows .NET de dos niveles que se ejecuta en máquinas virtuales de VMware como parte de una migración a Azure. Contoso migra la máquina virtual de front-end de la aplicación a una aplicación web de Azure App Service. El back-end de la aplicación se compila con microservicios implementados en contenedores administrados por Azure Kubernetes Service (AKS). El sitio interactúa con Azure Functions para ofrecer la funcionalidad de fotos de mascotas.

SmartHotel360, la aplicación usada en este ejemplo, se proporciona como código abierto. Si quiere utilizarla para sus propias pruebas, puede descargarla desde [GitHub](https://github.com/Microsoft/SmartHotel360).

## <a name="business-drivers"></a>Impulsores del negocio

El equipo directivo de TI ha trabajado estrechamente con sus socios comerciales para comprender lo quieren lograr con esta migración:

- **Abordar el crecimiento del negocio.** Contoso está creciendo y quiere ofrecer experiencias diferenciadas para los clientes en sitios web de Contoso.
- **Ser ágil.** Contoso debe poder reaccionar con más rapidez que los cambios del mercado para facilitar el éxito en una economía global.
- **Escala.** A medida que el negocio crece satisfactoriamente, el equipo de TI de Contoso debe facilitar sistemas que puedan crecer al mismo ritmo.
- **Reducir los costos.** Contoso quiere minimizar los costos de licencia.

## <a name="migration-goals"></a>Objetivos de la migración

El equipo de la nube de Contoso ha establecido los requisitos de la aplicación para esta migración. Estos requisitos se usaron para determinar el mejor método de migración:

- La aplicación de Azure sigue siendo tan importante como lo es hoy en día. Debe funcionar correctamente y escalarse fácilmente.
- La aplicación no debe usar componentes de IaaS. Debe compilarse todo para usar servicios PaaS o sin servidor.
- Las compilaciones de la aplicación deben ejecutarse en servicios en la nube y los contenedores deben residir en un registro de contenedor de nivel empresarial y privado en la nube.
- El servicio de API utilizado para las fotos de mascotas debe ser preciso y fiable en el mundo real, ya que las decisiones que toma la aplicación deben cumplirse en los hoteles. Cualquier mascota con acceso autorizado podrá permanecer en los hoteles.
- Para cumplir los requisitos de una canalización de DevOps, Contoso usará Azure DevOps para la administración de código fuente (SCM), con repositorios de Git. Se usarán compilaciones y versiones automatizadas para compilar el código e implementarlo en Azure App Service, Azure Functions y AKS.
- Se requieren distintas canalizaciones de CI/CD para los microservicios en el back-end y para el sitio web en el front-end.
- Los servicios de back-end tienen un ciclo de lanzamiento diferente al de la aplicación web de front-end. Para satisfacer este requisito, se implementarán dos canalizaciones distintas de DevOps.
- Contoso necesita la aprobación de administración en todas las implementaciones de sitio web de front-end y la canalización de CI/CD debe facilitarlo.

## <a name="solution-design"></a>Diseño de la solución

Después de fijar los objetivos y requisitos, Contoso diseña y revisa una solución de implementación e identifica el proceso de migración, incluidos los servicios de Azure que usará para la migración.

### <a name="current-app"></a>Aplicación actual

- La aplicación local de SmartHotel360 se divide en niveles entre dos VM (WEBVM y SQLVM).
- Las VM están ubicadas en el host de VMware ESXi **contosohost1.contoso.com** (versión 6.5).
- El entorno de VMware lo administra vCenter Server 6.5 (**vcenter.contoso.com**), que se ejecuta en una VM.
- Contoso tiene un centro de datos local (contoso-datacenter), con un controlador de dominio local (**contosodc1**).
- Las VM locales del centro de datos de Contoso se retirarán después de realizar la migración.

### <a name="proposed-architecture"></a>Arquitectura propuesta

- El front-end de la aplicación se implementa como una aplicación web de Azure App Service, en la región primaria de Azure.
- Una función de Azure proporciona las cargas de las fotos de mascotas y el sitio interactúa con esta funcionalidad.
- La función de fotos de mascotas aprovecha Azure Cognitive Services Vision API y Cosmos DB.
- El back-end del sitio se ha compilado con microservicios. Estos se implementarán en contenedores administrados en Azure Kubernetes Service (AKS).
- Los contenedores se compilarán con Azure DevOps y se insertarán en Azure Container Registry (ACR).
- Por ahora, Contoso implementará manualmente el código de función y la aplicación web con Visual Studio.
- Los microservicios se implementarán mediante un script de PowerShell que llama a las herramientas de línea de comandos de Kubernetes.

    ![Arquitectura del escenario](./media/contoso-migration-rebuild/architecture.png)

### <a name="solution-review"></a>Revisión de la solución

Contoso evalúa el diseño propuesto y crea una lista de ventajas y desventajas.

<!-- markdownlint-disable MD033 -->

**Consideración** | **Detalles**
--- | ---
**Ventajas** | El uso de PaaS y soluciones sin servidor para la implementación de un extremo a otro reduce significativamente el tiempo de administración que Contoso debe proporcionar.<br/><br/> Cambiar a una arquitectura de microservicios permite que Contoso amplíe fácilmente su solución con el tiempo.<br/><br/> La nueva funcionalidad se puede poner en línea sin interrumpir ninguna de las bases de código de las soluciones existentes.<br/><br/> La aplicación web se configurará con varias instancias y sin ningún único punto de error.<br/><br/> El escalado automático se habilitará para que la aplicación pueda controlar volúmenes de tráfico diferentes.<br/><br/> Con el cambio a los servicios de PaaS, Contoso puede retirar soluciones obsoletas que se ejecutan en el sistema operativo Windows Server 2008 R2.<br/><br/> Cosmos DB tiene tolerancia a errores integrada que no requiere ninguna configuración por parte de Contoso. Esto significa que la capa de datos ya no es un único punto de conmutación por error.
**Desventajas** | Los contenedores son más complejos que otras opciones de migración. La curva de aprendizaje podría ser un problema para Contoso. Contoso introduce un nuevo nivel de complejidad que proporciona un gran valor a pesar de la curva.<br/><br/> El equipo de operaciones de Contoso debe esforzarse en comprender y ofrecer soporte técnico de Azure, los contenedores y los microservicios de la aplicación.<br/><br/> Contoso no ha implementado completamente DevOps para toda la solución. Tiene que pensar en ello para la implementación de servicios en AKS, Azure Functions y Azure App Service.

<!-- markdownlint-enable MD033 -->

### <a name="migration-process"></a>Proceso de migración

1. Contoso aprovisiona ACR, AKS y Cosmos DB.
2. Aprovisionan la infraestructura para la implementación, incluida la aplicación web de Azure App Service, la función, la cuenta de almacenamiento y la API.
3. Una vez instalada la infraestructura, compilará las imágenes del contenedor de microservicios con Azure DevOps, que las inserta en ACR.
4. Contoso implementará estos microservicios en AKS mediante un script de PowerShell.
5. Por último, implementarán la función y la aplicación web.

    ![Proceso de migración](./media/contoso-migration-rebuild/migration-process.png)

### <a name="azure-services"></a>Servicios de Azure

**Servicio** | **Descripción** | **Costee**
--- | --- | ---
[AKS](/sql/dma/dma-overview?view=ssdt-18vs2017) | Simplifica las operaciones, la implementación y la administración de Kubernetes. Proporciona un servicio de orquestación de contenedores de Kubernetes totalmente administrado. | AKS es un servicio gratuito. Solo debe pagar por las máquinas virtuales y el almacenamiento y los recursos de red asociados que utilice. [Más información](https://azure.microsoft.com/pricing/details/kubernetes-service).
[Azure Functions](https://azure.microsoft.com/services/functions) | Acelera el proceso de desarrollo con una experiencia de proceso sin servidor controlada por eventos. Escalado a petición. | Solo debe pagar solo por los recursos consumidos. El plan se factura en función del consumo de recursos y las ejecuciones por segundo. [Más información](https://azure.microsoft.com/pricing/details/functions).
[Azure Container Registry](https://azure.microsoft.com/services/container-registry) | Almacena imágenes para todos los tipos de implementaciones de contenedor. | Costo basado en características, almacenamiento y duración de la utilización. [Más información](https://azure.microsoft.com/pricing/details/container-registry).
[Azure App Service](https://azure.microsoft.com/services/app-service/containers) | Compile, implemente y escale con rapidez aplicaciones web, móviles y de API de naturaleza empresarial que se puedan ejecutar en cualquier plataforma. | Los planes de App Service se facturan por segundo. [Más información](https://azure.microsoft.com/pricing/details/app-service/windows).

## <a name="prerequisites"></a>Requisitos previos

Esto es lo que Contoso requiere en este escenario:

<!-- markdownlint-disable MD033 -->

**Requisitos** | **Detalles**
--- | ---
**Suscripción de Azure** | En un artículo anterior, Contoso creó suscripciones. Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial).<br/><br/> Si crea una cuenta gratuita, será el administrador de su suscripción y podrá realizar todas las acciones.<br/><br/> Si usa una suscripción existente y no es el administrador, tendrá que solicitar al administrador que le asigne permisos de propietario o colaborador.
**Infraestructura de Azure** | [Vea](contoso-migration-infrastructure.md) cómo Contoso configuró una infraestructura de Azure.
**Requisitos previos para desarrolladores** | Contoso necesita las siguientes herramientas en una estación de trabajo de desarrollador:<br/><br/> - [Visual Studio 2017 Community Edition: Versión 15.5](https://www.visualstudio.com)<br/><br/> Carga de trabajo. NET habilitada.<br/><br/> [Git](https://git-scm.com)<br/><br/> [Azure PowerShell](https://azure.microsoft.com/downloads)<br/><br/> [CLI de Azure](/cli/azure/install-azure-cli?view=azure-cli-latest)<br/><br/> [Docker CE (Windows 10) o Docker EE (Windows Server)](https://docs.docker.com/docker-for-windows/install) configurado para usar contenedores de Windows.

<!-- markdownlint-enable MD033 -->

## <a name="scenario-steps"></a>Pasos del escenario

Contoso ejecutará la migración de la forma siguiente:

> [!div class="checklist"]
>
> - **Paso 1: Aprovisionar AKS y ACR.** Contoso aprovisiona el clúster de AKS administrado y el registro de contenedores de Azure mediante PowerShell.
> - **Paso 2: Compilar contenedores de Docker.** configura la integración continua para contenedores de Docker mediante Azure DevOps y los inserta en ACR.
> - **Paso 3: Implementar microservicios de back-end.** Implementan el resto de la infraestructura que aprovecharán los microservicios de back-end.
> - **Paso 4: Implementar la infraestructura de front-end.** implementa la infraestructura de front-end, lo que incluye el almacenamiento de blobs para los teléfonos de mascota, Cosmos DB y Vision API.
> - **Paso 5: Migrar el back-end.** implementa los microservicios y se ejecuta en AKS, para migrar el back-end.
> - **Paso 6: Publicar el front-end.** Publican la aplicación SmartHotel360 en App Service y la instancia de Function App a la que llamará el servicio de mascotas.

## <a name="step-1-provision-back-end-resources"></a>Paso 1: Aprovisionar recursos de back-end

Contoso ejecuta un script de implementación para crear el clúster de Kubernetes administrado con AKS y Azure Container Registry (ACR).

- Las instrucciones de esta sección usan el repositorio **SmartHotel360-Azure-backend**.
- El repositorio **SmartHotel360-Azure-backend** de GitHub contiene todo el software para esta parte de la implementación.

### <a name="prerequisites"></a>Requisitos previos

1. Antes de empezar, los administradores de Contoso se aseguran de que todo el software necesario está instalado en la máquina de desarrollo que se utiliza para la implementación.
2. Clonan el repositorio localmente en la máquina de desarrollo con Git: `git clone https://github.com/Microsoft/SmartHotel360-Azure-backend.git`

### <a name="provision-aks-and-acr"></a>Aprovisionar AKS y ACR

Los administradores de Contoso aprovisionan de la manera siguiente:

Abren la carpeta con Visual Studio Code y se desplazan al directorio **/deploy/k8s**, que contiene el script **gen-aks-env.ps1**.
2. Ejecutan el script para crear el clúster de Kubernetes administrado, con AKS y ACR.
    ![AKS](./media/contoso-migration-rebuild/aks1.png)
3. Con el archivo abierto, actualiza el parámetro $location a **eastus2** y guarda el archivo.
    ![AKS](./media/contoso-migration-rebuild/aks2.png)
4. En Visual Studio Code, seleccionan **Ver** > **Terminal integrado** para abrir el terminal integrado de Visual Studio Code.
    ![AKS](./media/contoso-migration-rebuild/aks3.png)
5. En el terminal integrado de PowerShell, inicia sesión en Azure mediante el comando Connect-AzureRmAccount. [Obtenga más información](/powershell/azure/get-started-azureps) sobre cómo empezar a usar PowerShell.
    ![AKS](./media/contoso-migration-rebuild/aks4.png)
6. Autentica la CLI de Azure mediante la ejecución del comando **az login** y sigue las instrucciones para autenticarse con su explorador web. [Obtenga más información](/cli/azure/authenticate-azure-cli?view=azure-cli-latest) acerca del inicio de sesión con la CLI de Azure.
    ![AKS](./media/contoso-migration-rebuild/aks5.png)
7. Ejecuta el siguiente comando, pasando el nombre del grupo de recursos de ContosoRG, el nombre del clúster de AKS smarthotel-aks-eus2 y el nuevo nombre del registro.

    ```PowerShell
    .\gen-aks-env.ps1  -resourceGroupName ContosoRg -orchestratorName smarthotelakseus2 -registryName smarthotelacreus2
    ```

    ![AKS](./media/contoso-migration-rebuild/aks6.png)

8. Azure crea otro grupo de recursos, que contiene los recursos del clúster de AKS.

    ![AKS](./media/contoso-migration-rebuild/aks7.png)

9. Una vez finalizada la implementación, se instala la herramienta de línea de comandos **kubectl**. La herramienta ya está instalada en Azure CloudShell.

    ```console
    az aks install-cli
    ```

10. Verifica la conexión al clúster ejecutando el comando **kubectl get nodes**. El nodo tiene el mismo nombre que la máquina virtual en el grupo de recursos creado automáticamente.

    ![AKS](./media/contoso-migration-rebuild/aks8.png)

11. Ejecutan el comando siguiente para iniciar el panel de Kubernetes:

    **az aks browse --resource-group ContosoRG --name smarthotelakseus2**

12. Se abre una pestaña del explorador en el panel. Se trata de una conexión de túnel mediante la CLI de Azure.

    ![AKS](./media/contoso-migration-rebuild/aks9.png)

## <a name="step-2-configure-the-back-end-pipeline"></a>Paso 2: Configurar la canalización de back-end

### <a name="create-an-azure-devops-project-and-build"></a>Crear un proyecto de Azure DevOps y compilarlo

Contoso crea un proyecto de Azure DevOps y configura una compilación de CI para crear el contenedor que, luego, inserta en ACR. Las instrucciones de esta sección usan el repositorio [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend).

1. En visualstudio.com, se crea una cuenta (**contosodevops360.visualstudio.com**) y se configura para usar Git.

2. Crean un proyecto (**SmartHotelBackend**) con Git como control de versiones y Agile como flujo de trabajo.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts1.png)

3. Importan el [repositorio de GitHub](https://github.com/Microsoft/SmartHotel360-Backend).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts2.png)

4. En **Canalizaciones**, seleccionan **Compilar** y crean una canalización con el repositorio GIT de Azure Repos como origen en el repositorio.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts3.png)

5. Selecciona la opción para empezar con una fase vacía.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts4.png)

6. Selecciona **Hosted Linux Preview** (Versión preliminar hospedada de Linux) como canalización de la compilación.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts5.png)

7. En **Fase 1**, agrega una tarea de **Docker Compose**. Esta tarea compila Docker Compose.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts6.png)

8. Repite la acción y agrega otra tarea de **Docker Compose**. Esta inserta los contenedores en ACR.

     ![Azure DevOps](./media/contoso-migration-rebuild/vsts7.png)

9. Selecciona la primera tarea (para compilar) y configura la compilación con la suscripción a Azure, la autorización y ACR.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts8.png)

10. Especifica la ruta de acceso del archivo **docker-compose.yaml**, en la carpeta **src** del repositorio. Selecciona compilar imágenes de servicio y se incluye la etiqueta más reciente. Cuando la acción cambia a **Build service images** (Compilar imágenes del servicio), el nombre de la tarea de Azure DevOps cambia a **Build services automatically** (Compilar servicios automáticamente).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts9.png)

11. Ahora, configura la segunda tarea de Docker (para insertar). Selecciona la suscripción y la instancia de ACR **smarthotelacreus2**.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts10.png)

12. De nuevo, introduce el archivo en docker-compose.yaml y selecciona **Push service images**  (Insertar imágenes del servicio) e incluye la última etiqueta. Cuando la acción cambia a **Push service images** (Insertar imágenes de servicio), el nombre de la tarea de Azure DevOps cambia a **Push services automatically** (Insertar servicios automáticamente).

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts11.png)

13. Con las tareas de Azure DevOps configuradas, Contoso guarda la canalización de compilación e inicia el proceso de compilación.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts12.png)

14. Seleccionan el trabajo de compilación para comprobar el progreso.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts13.png)

15. Una vez finalizada la compilación, ACR muestra los nuevos repositorios, que se rellenan con los contenedores que usan los microservicios.

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts14.png)

### <a name="deploy-the-back-end-infrastructure"></a>Implementar la infraestructura de back-end

Con el clúster de AKS creado y las imágenes de Docker compiladas, los administradores de Contoso implementan ahora el resto de la infraestructura que usarán los microservicios de back-end.

- En las instrucciones de esta sección se usa el repositorio [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend).
- En la carpeta **/deploy/k8s/arm**, hay un único script que permite crear todos los elementos.

La implementación se realiza de la manera siguiente:

1. Los administradores abren un símbolo del sistema para desarrolladores y utilizan el comando az login con la suscripción de Azure.
2. Usan el archivo deploy.cmd para implementar los recursos de Azure en el grupo de recursos ContosoRG y la región EUS2, escribiendo el comando siguiente:

    ```console
    .\deploy.cmd azuredeploy ContosoRG -c eastus2
    ```

    ![Implementación de back-end](./media/contoso-migration-rebuild/backend1.png)

3. En Azure Portal, capturan la cadena de conexión de cada base de datos, para usarla más adelante.

    ![Implementación de back-end](./media/contoso-migration-rebuild/backend2.png)

### <a name="create-the-back-end-release-pipeline"></a>Crear la canalización de versión de back-end

Ahora, los administradores de Contoso hacen lo siguiente:

- Implementan el controlador de entrada NGINX que permite el tráfico entrante a los servicios.
- Implementan los microservicios en el clúster de AKS.
- Como primer paso, actualizan las cadenas de conexión a los microservicios con Azure DevOps. Luego configuran una nueva canalización de versión de Azure DevOps para implementar los microservicios.
- Las instrucciones de esta sección usan el repositorio [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend).
- Tenga en cuenta que en este artículo no se tratan algunas de las opciones de configuración (por ejemplo, Active Directory B2C). Hay más información sobre estas opciones en el repositorio.

Se crea la canalización:

1. Mediante Visual Studio, actualizan el archivo **/deploy/k8s/config_local.yml** con la información de conexión de base de datos que apuntaron anteriormente.

    ![Conexiones de base de datos](./media/contoso-migration-rebuild/back-pipe1.png)

2. Abren Azure DevOps y, en el proyecto SmartHotel360, en **Versiones**, hacen clic en **+New Pipeline** (+Nueva canalización).

    ![Nueva canalización](./media/contoso-migration-rebuild/back-pipe2.png)

3. Seleccionan **Fase vacía** para iniciar la canalización sin una plantilla.
4. Especifican los nombres de fase y de canalización.

      ![Nombre de fase](./media/contoso-migration-rebuild/back-pipe4.png)

      ![Nombre de la canalización](./media/contoso-migration-rebuild/back-pipe5.png)

5. Agregan un artefacto.

     ![Agregar artefacto](./media/contoso-migration-rebuild/back-pipe6.png)

6. Seleccionan **Git** como tipo de origen y especifican el proyecto, el origen y la rama principal de la aplicación de SmartHotel360.

    ![Configuración del artefacto](./media/contoso-migration-rebuild/back-pipe7.png)

7. Seleccionan el vínculo de tarea.

    ![Vínculo de tarea](./media/contoso-migration-rebuild/back-pipe8.png)

8. Agregan una nueva tarea de Azure PowerShell para poder ejecutar un script de PowerShell en un entorno de Azure.

    ![PowerShell en Azure](./media/contoso-migration-rebuild/back-pipe9.png)

9. Seleccionan la suscripción de Azure para la tarea y eligen el script **deploy.ps1** en el repositorio de Git.

    ![Ejecución de script](./media/contoso-migration-rebuild/back-pipe10.png)

10. Agregan los argumentos al script. El script elimina todo el contenido del clúster (excepto la **entrada** y el **controlador de entrada**) e implementa los microservicios.

    ![Argumentos de script](./media/contoso-migration-rebuild/back-pipe11.png)

11. Establecen la versión de Azure PowerShell preferida en la más reciente y guardan la canalización.

12. Vuelven a la página **Versiones** y crean manualmente una nueva versión.

    ![Nueva versión](./media/contoso-migration-rebuild/back-pipe12.png)

13. Seleccionan la versión después de crearla y, en **Acciones**, seleccionan **Implementar**.

      ![Implementar la versión](./media/contoso-migration-rebuild/back-pipe13.png)

14. Una vez completada la implementación, ejecutan el siguiente comando para comprobar el estado de los servicios con Azure Cloud Shell: **kubectl get services**.

## <a name="step-3-provision-front-end-services"></a>Paso 3: Aprovisionar servicios front-end

Los administradores de Contoso tienen que implementar la infraestructura que se usará en las aplicaciones de front-end. Crean un contenedor de almacenamiento de blobs para almacenar las imágenes de mascotas; la base de datos de Cosmos para almacenar documentos con la información de las mascotas; y la instancia de Vision API para el sitio web.

Las instrucciones de esta sección usan el repositorio [SmartHotel360-public-web](https://github.com/Microsoft/SmartHotel360-public-web).

### <a name="create-blob-storage-containers"></a>Creación de contenedores de almacenamiento de blobs

1. En Azure Portal, abren la cuenta de almacenamiento que se creó y seleccionan **Blobs**.
2. Creará un nuevo contenedor (**Mascotas**) con el nivel de acceso público establecido en el contenedor. Los usuarios cargarán las fotos de sus mascotas en este contenedor.

    ![Blob de almacenamiento](./media/contoso-migration-rebuild/blob1.png)

3. Crea un segundo contenedor nuevo denominado **configuración**. Un archivo con la configuración de aplicación de front-end se colocará en este contenedor.

    ![Blob de almacenamiento](./media/contoso-migration-rebuild/blob2.png)

4. Captura los detalles de acceso de la cuenta de almacenamiento en un archivo de texto, para futuras referencias.

    ![Blob de almacenamiento](./media/contoso-migration-rebuild/blob2.png)

### <a name="provision-a-cosmos-database"></a>Aprovisionar una base de datos de Cosmos

Los administradores de Contoso aprovisionan una base de datos de Cosmos que se usará para la información de las mascotas.

1. Crea una instancia de **Azure Cosmos DB** en Azure Marketplace.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos1.png)

2. Especifica un nombre (**contosomarthotel**), selecciona la API de SQL y la coloca en el grupo de recursos de producción ContosoRG, en la región Este de EE. UU. 2 principal.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos2.png)

3. Agrega una nueva colección a la base de datos, con los valores de capacidad y rendimiento predeterminados.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos3.png)

4. Anota la información de conexión de la base de datos, para futuras referencias.

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos4.png)

### <a name="provision-computer-vision"></a>Aprovisionar Computer Vision

Los administradores de Contoso aprovisionan la instancia de Computer Vision API. La función llamará a la API para evaluar las imágenes cargadas por los usuarios.

1. Crea una instancia de **Computer Vision** en Azure Marketplace.

     ![Computer Vision](./media/contoso-migration-rebuild/vision1.png)

2. Aprovisiona la API (**smarthotelpets**) en el grupo de recursos de producción ContosoRG, en la región Este de EE. UU. 2 principal.

    ![Computer Vision](./media/contoso-migration-rebuild/vision2.png)

3. Guarda la configuración de conexión para la API en un archivo de texto para consultarla más adelante.

     ![Computer Vision](./media/contoso-migration-rebuild/vision3.png)

### <a name="provision-the-azure-web-app"></a>Aprovisionar la aplicación web de Azure

Los administradores de Contoso aprovisionan la aplicación web con Azure Portal.

1. Selecciona **Aplicación web** en el portal.

    ![Aplicación web](media/contoso-migration-rebuild/web-app1.png)

2. Especifican un nombre de aplicación (**smarthotelcontoso**), la ejecutan en Windows y la colocan en el grupo de recursos de producción **ContosoRG**. Crean una instancia de Application Insights para la supervisión de la aplicación.

    ![Nombre de aplicación web](media/contoso-migration-rebuild/web-app2.png)

3. Cuando terminan, van a la dirección de la aplicación para comprobar que se creó correctamente.

4. Ahora, en Azure Portal, crean un espacio de ensayo para el código. La canalización se implementará en este espacio. Así se garantiza que el código no se inserta en producción hasta que los administradores ejecutan una versión.

    ![Espacio de ensayo de la aplicación web](media/contoso-migration-rebuild/web-app3.png)

### <a name="provision-the-azure-function-app"></a>Aprovisionar la instancia de Azure Function App

En Azure Portal, los administradores de Contoso aprovisionan la instancia de Function App.

1. Seleccionan **Function App**.

    ![Crear instancia de Function App](./media/contoso-migration-rebuild/function-app1.png)

2. Especifican un nombre de aplicación (**smarthotelpetchecker**). Insertan la aplicación en el grupo de recursos de producción **ContosoRG**. Establecen el contexto de hospedaje en **Plan de consumo** e insertan la aplicación en la región Este de EE. UU. 2. Se crea una cuenta de almacenamiento, junto con una instancia de Application Insights para la supervisión.

    ![Configuración de Function App](./media/contoso-migration-rebuild/function-app2.png)

3. Una vez implementada la aplicación, van a la dirección de la aplicación para comprobar que se creó correctamente.

## <a name="step-4-set-up-the-front-end-pipeline"></a>Paso 4: Configurar la canalización de front-end

Los administradores de Contoso crean dos proyectos distintos en el sitio de front-end.

1. En Azure DevOps, crean un proyecto **SmartHotelFrontend**.

    ![Proyecto de front-end](./media/contoso-migration-rebuild/function-app1.png)

2. Importan el repositorio de Git del [front-end de SmartHotel360](https://github.com/Microsoft/SmartHotel360-public-web.git) al nuevo proyecto.
3. En Function App, crean otro proyecto de Azure DevOps (SmartHotelPetChecker) e importan el repositorio de Git de [PetChecker](https://github.com/Microsoft/SmartHotel360-PetCheckerFunction ) a este proyecto.

### <a name="configure-the-web-app"></a>Configuración de la aplicación web

Ahora los administradores de Contoso configuran la aplicación web para usar los recursos de Contoso.

1. Se conectan al proyecto de Azure DevOps y clonan el repositorio localmente en la máquina de desarrollo.
2. En Visual Studio, abre la carpeta para mostrar todos los archivos del repositorio.

    ![Archivos del repositorio](./media/contoso-migration-rebuild/configure-webapp1.png)

3. Actualizan los cambios de configuración según sea necesario.

    - Cuando la aplicación web se inicia, busca la configuración de la aplicación **SettingsUrl**.
    - Esta variable debe contener una dirección URL que apunta un archivo de configuración.
    - De forma predeterminada, esta opción de configuración se usa como un punto de conexión público.

4. Actualizan el archivo /config-sample.json/sample.json.

    - Este es el archivo de configuración para la web cuando se usa el punto de conexión público.
    - Editan las secciones **urls** y **pets_config** con los valores correspondientes a los puntos de conexión de la API de AKS, las cuentas de almacenamiento y la base de datos de Cosmos.
    - Las direcciones URL deben coincidir con el nombre DNS de la nueva aplicación web que Contoso va a crear.
    - Para Contoso, se trata de **smarthotelcontoso.eastus2.cloudapp.azure.com**.

    ![Configuración de Json](./media/contoso-migration-rebuild/configure-webapp2.png)

5. Una vez actualizado el archivo, se le cambia el nombre a **smarthotelsettingsurl** y se carga en el almacenamiento de blobs creado anteriormente.

    ![Cambiar nombre y cargar](./media/contoso-migration-rebuild/configure-webapp3.png)

6. Seleccionan el archivo para obtener la dirección URL. La aplicación usa esta dirección URL cuando extrae los archivos de configuración.

    ![Dirección URL de la aplicación](./media/contoso-migration-rebuild/configure-webapp4.png)

7. En el archivo **appsettings.Production.json**, actualizan **SettingsURL** con la dirección URL del nuevo archivo.

    ![Actualizar dirección URL](./media/contoso-migration-rebuild/configure-webapp5.png)

### <a name="deploy-the-website-to-azure-app-service"></a>Implementación del sitio web en Azure App Service

Los administradores de Contoso ahora pueden publicar el sitio web.

1. Abren Azure DevOps y, en el proyecto **SmartHotelFrontend**, en **Builds and Releases** (Compilaciones y versiones) y seleccionan **+New Pipeline** (+Nueva canalización).
2. Seleccionan **Git de Azure DevOps** como origen.
3. Seleccionan la plantilla **ASP.NET Core**.
4. Revisan la canalización y comprueban que **Publicar proyectos web** y **Comprimir proyectos publicados** están seleccionadas.

    ![Configuración de la canalización](./media/contoso-migration-rebuild/vsts-publishfront2.png)

5. En **Desencadenadores**, habilitan la integración continua y agregan la rama maestra. Así se garantiza que, cada vez que la solución tiene código nuevo confirmado en la rama maestra, se inicia la canalización de compilación.

    ![Integración continua](./media/contoso-migration-rebuild/vsts-publishfront3.png)

6. Seleccionan **Guardar y poner en cola** para iniciar una compilación.
7. Una vez finalizada la compilación, configuran una canalización de versión con **Implementación de Azure App Service**.
8. Especifican un nombre de fase, **Almacenamiento provisional**.

    ![Nombre del entorno](./media/contoso-migration-rebuild/vsts-publishfront4.png)

9. Agregan un artefacto y seleccionan la compilación que acaban de configurar.

     ![Agregar artefacto](./media/contoso-migration-rebuild/vsts-publishfront5.png)

10. Seleccionan el icono de rayo en el artefacto y habilitan la implementación continua.

    ![Implementación continua](./media/contoso-migration-rebuild/vsts-publishfront6.png)
11. En **Entorno**, seleccionan **1 job, 1 task** (1 trabajo, 1 tarea) en **Almacenamiento provisional**.
12. Después de seleccionar la suscripción y el nombre de la aplicación, abren la tarea **Implementar Azure App Service**. La implementación está configurada para usar la ranura de implementación de **ensayo**. Así se genera automáticamente código para su revisión y aprobación en esta ranura.

     ![Slot](./media/contoso-migration-rebuild/vsts-publishfront7.png)

13. En **Canalización**, agregan una nueva fase.

    ![Nuevo entorno](./media/contoso-migration-rebuild/vsts-publishfront8.png)

14. Seleccionan **Implementación de Azure App Service con espacio** y asignan el nombre **Prod** al entorno.
15. Seleccionan **1 job, 2 tasks** (1 trabajo, 2 tareas) y seleccionan la suscripción, el nombre de App Service y el espacio de **ensayo**.

    ![Nombre del entorno](./media/contoso-migration-rebuild/vsts-publishfront10.png)

16. Quitan **Deploy Azure App Service to Slot** (Implementar Azure App Service con espacio) de la canalización. Se había colocado allí en los pasos anteriores.

    ![Quitar de la canalización](./media/contoso-migration-rebuild/vsts-publishfront11.png)

17. Guardan la canalización. En la canalización, seleccionan **Condiciones posteriores a la implementación**.

    ![Posterior a la implementación](./media/contoso-migration-rebuild/vsts-publishfront12.png)

18. Habilitan **Aprobaciones posteriores a la implementación** y agregan un responsable de desarrollo como aprobador.

    ![Aprobación posterior a la implementación](./media/contoso-migration-rebuild/vsts-publishfront13.png)

19. En la canalización de compilación, inician manualmente una compilación. Así se desencadena la nueva canalización de versión, que implementa el sitio en el espacio de ensayo. En el caso de Contoso, la dirección URL del espacio es `https://smarthotelcontoso-staging.azurewebsites.net/`.

20. Una vez finalizada la compilación e implementada la versión en el espacio, Azure DevOps solicita su aprobación por correo electrónico al responsable de desarrollo.

21. El responsable de desarrollo selecciona **Ver aprobación** en el portal de Azure DevOps, donde puede aprobar o rechazar la solicitud.

    ![Correo electrónico de aprobación](./media/contoso-migration-rebuild/vsts-publishfront14.png)

22. El responsable realiza un comentario y aprueba. Así se inicia el intercambio entre el espacio de **ensayo** y de **producción** y se traslada la compilación a producción.

    ![Aprobar e intercambiar](./media/contoso-migration-rebuild/vsts-publishfront15.png)

23. La canalización finaliza el intercambio.

    ![Intercambio completo](./media/contoso-migration-rebuild/vsts-publishfront16.png)

24. El equipo comprueba el espacio de **producción** en `https://smarthotelcontoso.azurewebsites.net/` para asegurarse de que la aplicación web se encuentra en producción.

### <a name="deploy-the-petchecker-function-app"></a>Implementación de PetChecker Function App

Los administradores de Contoso implementan la aplicación de la manera siguiente.

1. Se conectan al proyecto de Azure DevOps y clonan el repositorio localmente en la máquina de desarrollo.
2. En Visual Studio, abre la carpeta para mostrar todos los archivos del repositorio.
3. Abren el archivo **src/PetCheckerFunction/local.settings.json** y agregan la configuración de almacenamiento de la aplicación, la base de datos de Cosmos y Computer Vision API.

    ![Implementación de la función](./media/contoso-migration-rebuild/function5.png)

4. Confirman el código y lo sincronizan con Azure DevOps, lo que inserta los cambios.
5. Agregan una nueva canalización de compilación y seleccionan **Git de Azure DevOps** como origen.
6. Seleccionan la plantilla **ASP.NET Core (.NET Framework)** .
7. Aceptan los valores predeterminados de la plantilla.
8. En **Desencadenadores**, seleccionan **Habilitar la integración continua** y seleccionan **Guardar y poner en cola** para iniciar una compilación.
9. Una vez iniciada la compilación, compilan una canalización de versión, lo que agrega **Implementación de Azure App Service con espacio**.
10. Asignan el nombre **Producción** al entorno y seleccionan la suscripción. Establecen el **Tipo de aplicación** en **Function App** y el nombre del servicio como **smarthotelpetchecker**.

    ![Aplicación de función](./media/contoso-migration-rebuild/petchecker2.png)

11. Agregan un artefacto de **compilación**.

    ![Artefacto](./media/contoso-migration-rebuild/petchecker3.png)

12. Habilitan la opción **Desencadenador de implementación continua** y seleccionan **Guardar**.
13. Seleccionan **Poner nueva compilación en cola** para ejecutar la canalización de CI/CD completa.
14. Una vez implementada la función, aparece en Azure Portal, con el estado **En ejecución**.

    ![Implementación de la función](./media/contoso-migration-rebuild/function6.png)

15. Contoso va a la aplicación para probar si la aplicación Pet Checker funciona según lo previsto, en [http://smarthotel360public.azurewebsites.net/Pets](http://smarthotel360public.azurewebsites.net/Pets).
16. Seleccionan el avatar para cargar una imagen.
    ![Implementación de la función](./media/contoso-migration-rebuild/function7.png)
17. La primera foto que quiere comprobar es la de un perro pequeño.
    ![Implementación de la función](./media/contoso-migration-rebuild/function8.png)
18. La aplicación devuelve un mensaje de aceptación.
    ![Implementación de la función](./media/contoso-migration-rebuild/function9.png)

## <a name="review-the-deployment"></a>Revisión de la implementación

Con los recursos migrados de Azure, Contoso debe ahora poner completamente en marcha la nueva infraestructura y protegerla.

### <a name="security"></a>Seguridad

- Contoso tiene que asegurarse de que sus nuevas bases de datos son seguras. [Más información](/azure/sql-database/sql-database-security-overview).
- La aplicación necesita actualizarse para usar SSL con certificados. La instancia del contenedor debe reimplementarse para responder en 443.
- Contoso debería plantearse el uso de Key Vault para proteger los secretos de las aplicaciones de Service Fabric. [Más información](/azure/service-fabric/service-fabric-application-secret-management).

### <a name="backups-and-disaster-recovery"></a>Copia de seguridad y recuperación ante desastres

- Contoso necesita revisar los requisitos de copia de seguridad para Azure SQL Database. [Más información](/azure/sql-database/sql-database-automated-backups).
- Contoso debería plantearse la implementación grupos de conmutación por error de SQL para proporcionar conmutación por error regional a la base de datos. [Más información](/azure/sql-database/sql-database-geo-replication-overview).
- Contoso puede usar la replicación geográfica para el SKU premium de ACR. [Más información](/azure/container-registry/container-registry-geo-replication).
- Cosmos DB realiza la copia de seguridad automáticamente. Contoso puede [obtener más información](/azure/cosmos-db/online-backup-and-restore) sobre este proceso.

### <a name="licensing-and-cost-optimization"></a>Optimización de los costos y licencias

- Una vez implementados todos los recursos, Contoso debe asignar etiquetas de Azure según la [planificación de su infraestructura](contoso-migration-infrastructure.md#set-up-tagging).
- Todas las licencias se integran en el costo de los servicios de PaaS que consume Contoso. Esto se deducirá del contrato Enterprise.
- Contoso habilitará Azure Cost Management bajo licencia de Cloudyn, una subsidiaria de Microsoft. Se trata de una solución de administración de costos en varias nubes que le permitirá utilizar y administrar Azure y otros recursos en la nube. [Más información](/azure/cost-management/overview) sobre Azure Cost Management.

## <a name="conclusion"></a>Conclusión

En este artículo, Contoso recompila la aplicación SmartHotel360 en Azure. Se recompila la máquina virtual de front-end de la aplicación local para las aplicaciones web de Azure App Service. El back-end de la aplicación se compila con microservicios implementados en contenedores administrados por Azure Kubernetes Service (AKS). Contoso mejora la funcionalidad de la aplicación con una aplicación de fotos de mascotas.
