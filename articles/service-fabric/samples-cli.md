---
title: Azure CLI (az) 和 Azure Service Fabric CLI (sfctl) 示例
description: 关于管理群集、应用程序和服务的 Azure CLI (az) 和 Azure Service Fabric CLI (sfctl) 示例。
ms.topic: sample
origin.date: 04/09/2018
author: rockboyfor
ms.date: 09/14/2020
ms.testscope: no
ms.testdate: ''
ms.author: v-yeche
ms.custom: devx-track-azurecli
ms.openlocfilehash: 3ce702f94ef4b7338fd14f16805935a58a6e10e6
ms.sourcegitcommit: e1cd3a0b88d3ad962891cf90bac47fee04d5baf5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2020
ms.locfileid: "89655540"
---
# <a name="azure-cli-az-and-azure-service-fabric-cli-sfctl-samples"></a>Azure CLI (az) 和 Azure Service Fabric CLI (sfctl) 示例

下表包含有关如何管理 Service Fabric 群集、应用程序和服务的示例的链接。

[!INCLUDE [links to azure cli and service fabric cli](../../includes/service-fabric-sfctl.md)]

| 示例 | 说明 |
|-|-|
| **创建群集**（使用 Azure CLI）||
| [创建安全 Linux 群集](./scripts/cli-create-cluster.md)| 创建 Azure Service Fabric 群集。 |
| **管理应用程序**（使用 Service Fabric CLI）||
| [列出应用程序](./scripts/sfctl-list-applications.md)| 列出预配到群集的应用程序。|
| [部署应用程序](./scripts/cli-deploy-application.md)| 将应用程序部署到群集。|
| [删除应用程序](./scripts/cli-remove-application.md)| 从群集中删除应用程序。|
| [升级应用程序](./scripts/sfctl-upgrade-application.md)| 升级已部署的应用程序。|

<!-- Update_Description: update meta properties, wording update, update link -->