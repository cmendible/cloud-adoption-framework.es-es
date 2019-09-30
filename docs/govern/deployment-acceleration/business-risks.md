---
title: Motivaciones y riesgos empresariales que impulsan la aceleración de la implementación
titleSuffix: Microsoft Cloud Adoption Framework for Azure
description: Obtenga más información acerca de la materia sobre la aceleración de la implementación como parte de una estrategia de gobernanza de la nube.
author: alexbuckgit
ms.author: abuck
ms.date: 09/17/2019
ms.topic: guide
ms.service: cloud-adoption-framework
ms.subservice: govern
ms.custom: governance
ms.openlocfilehash: d827b4de1c938180579303e60c6808d65fcd14a8
ms.sourcegitcommit: d19e026d119fbe221a78b10225230da8b9666fe1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2019
ms.locfileid: "71220725"
---
# <a name="deployment-acceleration-motivations-and-business-risks"></a>Motivaciones y riesgos empresariales de la aceleración de la implementación

En este artículo se describen las razones por las que los clientes normalmente adoptan la materia sobre la aceleración de la implementación dentro de una estrategia de gobernanza de la nube. También se proporcionan algunos ejemplos de riesgos empresariales que impulsan las declaraciones de directiva.

<!-- markdownlint-disable MD026 -->

## <a name="deployment-acceleration-relevancy"></a>Importancia de la aceleración de la implementación

Los sistemas locales a menudo se implementan mediante imágenes de base referencia o scripts de instalación. Por lo general, es necesaria una configuración adicional, que puede implicar múltiples pasos o la intervención humana. Estos procesos manuales son propensos a errores y a menudo dan lugar a un "desfase de configuración", lo que requiere tareas de solución de problemas y de corrección que necesitan mucho tiempo.

La mayoría de los recursos de Azure se pueden implementar y configurar manualmente mediante Azure Portal. Este enfoque puede ser suficiente para sus necesidades cuando solo tiene unos pocos recursos para administrar. Sin embargo, a medida que el patrimonio en la nube crece, su organización debe comenzar a integrar funciones de automatización en los procesos de implementación para garantizar el desfase de configuración de los recursos en la nube u otros problemas que presentan los procesos manuales. Adoptar un enfoque DevOps o [DevSecOps](https://www.microsoft.com/en-us/securityengineering/devsecops) suele ser la mejor manera de administrar las implementaciones cuando la adopción de la nube está en una fase más avanzada.

<!-- "en-us" location is required for the URL above. -->

Un sólido plan de aceleración de la implementación garantiza que los recursos de nube se implementen, actualicen y configuren de forma correcta y coherente, y que permanezcan así. La madurez de la estrategia de aceleración de la implementación también puede ser un factor significativo en la [estrategia de administración de costos](../cost-management/index.md). El aprovisionamiento y la configuración automatizados de los recursos de nube le permiten reducir o desasignar los recursos cuando la demanda es baja o está limitada en el tiempo, por lo que solo paga por los recursos cuando los necesita.

## <a name="business-risk"></a>Riesgo empresarial

La material sobre la aceleración de la implementación intenta abordar los siguientes riesgos empresariales. Durante la adopción de la nube, supervise cada uno de los siguientes aspectos para determinar su relevancia:

- **Interrupción del servicio.** La falta de procesos de implementación predecibles y repetibles o de cambios no administrados en las configuraciones del sistema puede interrumpir las operaciones normales y provocar una pérdida de productividad o de negocio.
- **Sobrecostos:** Los cambios inesperados en la configuración de los recursos del sistema pueden dificultar la identificación de la causa raíz de los problemas, lo que aumenta los costos de desarrollo, operaciones y mantenimiento.
- **Ineficacias de la organización:** Las barreras entre los equipos de desarrollo, operaciones y seguridad pueden causar numerosos desafíos para la adopción efectiva de las tecnologías de nube y el desarrollo de un modelo unificado de gobernanza de la nube.

## <a name="next-steps"></a>Pasos siguientes

Utilice la [plantilla de administración de la nube](./template.md) para documentar los riesgos empresariales que probablemente se presentarán en el plan de adopción de la nube actual.

Una vez que se consigue una comprensión realista de los riesgos empresariales, el siguiente paso es documentar la tolerancia al riesgo de la empresa y los indicadores y métricas clave para supervisar esa tolerancia.

> [!div class="nextstepaction"]
> [Métricas, indicadores y tolerancia al riesgo](./metrics-tolerance.md)
