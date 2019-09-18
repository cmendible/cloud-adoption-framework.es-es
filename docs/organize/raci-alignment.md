---
title: Alineación de responsabilidades entre los equipos
titleSuffix: Microsoft Cloud adoption Framework for Azure
description: Aprenda a alinear las responsabilidades entre los equipos.
author: BrianBlanchard
ms.author: brblanch
ms.date: 09/10/2019
ms.topic: article
ms.service: cloud-adoption-framework
ms.subservice: organize
ms.custom: organize
ms.openlocfilehash: 818d2fa74c480b8aee36c4d268ae7a83cb93fab3
ms.sourcegitcommit: 443c28f3afeedfbfe8b9980875a54afdbebd83a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2019
ms.locfileid: "71031828"
---
# <a name="align-responsibilities-across-teams"></a>Alineación de responsabilidades entre los equipos

Aprenda a alinear las responsabilidades de los equipos mediante el desarrollo de una matriz entre equipos que identifique a las entidades *responsables, encargadas, consultadas e informadas* (RACI por sus siglas en inglés). En este artículo se proporciona una matriz RACI de ejemplo para las estructuras organizativas que se describen en [Establecimiento de estructuras de equipo](./organization-structures.md):

- [Equipo de adopción de la nube solo](#cloud-adoption-team-only)
- [Procedimiento recomendado de producto viable mínimo](#best-practice-minimum-viable-product-mvp)
- [TI central](#central-it)
- [Alineación estratégica](#strategic-alignment)
- [Alineación operativa](#operational-alignment)
- [Centro de excelencia de la nube (CCoE)](#cloud-center-of-excellence-ccoe)

Para realizar un seguimiento de las decisiones sobre la estructura de la organización a lo largo del tiempo, descargue y modifique la [plantilla de hoja de cálculo de RACI](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx).

En los ejemplos de este artículo se especifican estos componentes de RACI:

- El equipo *encargado* de una función.
- Los equipos *responsables* de los resultados.
- Los equipos que deben *consultarse* durante el planeamiento.
- Los equipos a los que se debe *informar* una vez finalizado el trabajo.

La última fila de cada tabla (excepto la primera) contiene un vínculo a la funcionalidad de la nube más adecuada para más información.

## <a name="cloud-adoption-team-only"></a>Equipo de adopción de la nube solo

|  |Entrega de soluciones  |Alineación empresarial  |Administración de cambios  |Operaciones de soluciones  |Gobernanza |Madurez de la plataforma  |Operaciones de la plataforma  |Automatización de la plataforma  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Equipo de adopción de la nube |Encargado|Encargado|Encargado|Encargado|Encargado|Encargado|Encargado|Encargado|

## <a name="best-practice-minimum-viable-product-mvp"></a>Procedimiento recomendado: producto viable mínimo

|  |Entrega de soluciones  |Alineación empresarial  |Administración de cambios  |Operaciones de soluciones  |Gobernanza |Madurez de la plataforma  |Operaciones de la plataforma  |Automatización de la plataforma  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Equipo de adopción de la nube|Encargado|Encargado|Encargado|Encargado|Consultado|Consultado|Consultado|Informado|
|Equipo de gobernanza de la nube|Consultado|Informado|Informado|Informado|Encargado|Encargado|Encargado|Encargado|
||||||||||
|Funcionalidad en la nube alineada|[Adopción de la nube](./cloud-adoption.md)|[Estrategia de la nube](./cloud-strategy.md)|[Estrategia de la nube](./cloud-strategy.md)|[Operaciones de la nube](./cloud-operations.md)|[CCoE](./cloud-center-of-excellence.md)-[Gobernanza de la nube](./cloud-governance.md)|[CCoE](./cloud-center-of-excellence.md)-[Plataforma en la nube](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Plataforma en la nube](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Automatización de la nube](./cloud-automation.md)|

## <a name="central-it"></a>TI central

| |Entrega de soluciones  |Alineación empresarial  |Administración de cambios  |Operaciones de soluciones  |Gobernanza |Madurez de la plataforma  |Operaciones de la plataforma  |Automatización de la plataforma  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Equipo de adopción de la nube  |Encargado|Encargado|Responsable    |Responsable|Informado   |Informado   |Informado   |Informado   |
|Equipo de gobernanza de la nube|Consultado  |Informado   |Informado   |Informado   |Encargado|Consultado  |Responsable|Informado   |
|TI central           |Consultado  |Informado   |Encargado   |Encargado   |Responsable  |Encargado|Encargado|Encargado|
||||||||||
|Funcionalidad en la nube alineada|[Adopción de la nube](./cloud-adoption.md)|[Estrategia de la nube](./cloud-strategy.md)|[Estrategia de la nube](./cloud-strategy.md)|[Operaciones de la nube](./cloud-operations.md)|[Gobernanza de la nube](./cloud-governance.md)|[TI central](./central-it.md)|[TI central](./central-it.md)|[TI central](./central-it.md)|

## <a name="strategic-alignment"></a>Alineación estratégica

|  |Entrega de soluciones  |Alineación empresarial  |Administración de cambios  |Operaciones de soluciones  |Gobernanza |Madurez de la plataforma  |Operaciones de la plataforma  |Automatización de la plataforma  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Equipo de estrategia de la nube  |Consultado  |Encargado|Encargado|Consultado  |Consultado  |Informado   |Informado   |Informado   |
|Equipo de adopción de la nube  |Encargado|Consultado  |Responsable|Encargado|Informado   |Informado   |Informado   |Informado   |
|CCoE modelo RACI      |Consultado  |Informado   |Informado   |Informado   |Encargado|Encargado|Encargado|Encargado|
||||||||||
|Funcionalidad en la nube alineada|[Adopción de la nube](./cloud-adoption.md)|[Estrategia de la nube](./cloud-strategy.md)|[Estrategia de la nube](./cloud-strategy.md)|[Operaciones de la nube](./cloud-operations.md)|[CCoE](./cloud-center-of-excellence.md)-[Gobernanza de la nube](./cloud-governance.md)|[CCoE](./cloud-center-of-excellence.md)-[Plataforma en la nube](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Plataforma en la nube](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Automatización de la nube](./cloud-automation.md)|

## <a name="operational-alignment"></a>Alineación operativa

|  |Entrega de soluciones  |Alineación empresarial  |Administración de cambios  |Operaciones de soluciones  |Gobernanza |Madurez de la plataforma  |Operaciones de la plataforma  |Automatización de la plataforma  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Equipo de estrategia de la nube  |Consultado  |Encargado|Encargado|Consultado  |Consultado  |Informado   |Informado   |Informado   |
|Equipo de adopción de la nube  |Encargado|Consultado  |Responsable|Consultado  |Informado   |Informado   |Informado   |Informado   |
|Equipo de operaciones en la nube|Consultado  |Consultado  |Responsable|Encargado|Consultado  |Informado   |Encargado|Consultado  |
|CCoE modelo RACI      |Consultado  |Informado   |Informado   |Informado   |Encargado|Encargado|Responsable|Encargado|
||||||||||
|Funcionalidad en la nube alineada|[Adopción de la nube](./cloud-adoption.md)|[Estrategia de la nube](./cloud-strategy.md)|[Estrategia de la nube](./cloud-strategy.md)|[Operaciones de la nube](./cloud-operations.md)|[CCoE](./cloud-center-of-excellence.md)-[Gobernanza de la nube](./cloud-governance.md)|[CCoE](./cloud-center-of-excellence.md)-[Plataforma en la nube](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Plataforma en la nube](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Automatización de la nube](./cloud-automation.md)|

## <a name="cloud-center-of-excellence-ccoe"></a>Centro de excelencia de la nube (CCoE)

|  |Entrega de soluciones  |Alineación empresarial  |Administración de cambios  |Operaciones de soluciones  |Gobernanza |Madurez de la plataforma  |Operaciones de la plataforma  |Automatización de la plataforma  |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|Equipo de estrategia de la nube  |Consultado  |Encargado|Encargado|Consultado  |Consultado  |Informado   |Informado   |Informado   |
|Equipo de adopción de la nube  |Encargado|Consultado  |Responsable|Consultado  |Informado   |Informado   |Informado   |Informado   |
|Equipo de operaciones en la nube|Consultado  |Consultado  |Responsable|Encargado|Consultado  |Informado   |Encargado|Consultado  |
|Equipo de gobernanza de la nube|Consultado  |Informado   |Informado   |Consultado  |Encargado|Consultado  |Responsable|Informado   |
|Equipo de plataforma de la nube  |Consultado  |Informado   |Informado   |Consultado  |Consultado  |Encargado|Responsable|Responsable|
|Equipo de automatización de la nube|Consultado  |Informado   |Informado   |Informado   |Consultado  |Responsable|Responsable|Encargado|
||||||||||
|Funcionalidad en la nube alineada|[Adopción de la nube](./cloud-adoption.md)|[Estrategia de la nube](./cloud-strategy.md)|[Estrategia de la nube](./cloud-strategy.md)|[Operaciones de la nube](./cloud-operations.md)|[CCoE](./cloud-center-of-excellence.md)-[Gobernanza de la nube](./cloud-governance.md)|[CCoE](./cloud-center-of-excellence.md)-[Plataforma en la nube](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Plataforma en la nube](./cloud-platform.md)|[CCoE](./cloud-center-of-excellence.md)-[Automatización de la nube](./cloud-automation.md)|

## <a name="next-steps"></a>Pasos siguientes

Para realizar un seguimiento de las decisiones sobre la estructura de la organización a lo largo del tiempo, descargue y modifique la [plantilla de hoja de cálculo de RACI](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx). Copie y modifique el ejemplo que se adapte mejor de las matrices de RACI de este artículo.

> [!div class="nextstepaction"]
> [Descargar la plantilla de hoja de cálculo de RACI](https://archcenter.blob.core.windows.net/cdn/fusion/management/raci-template.xlsx)
