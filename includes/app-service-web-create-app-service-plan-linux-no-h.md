---
title: include 文件
description: include 文件
services: app-service
author: cephalin
ms.service: app-service
ms.topic: include
origin.date: 12/20/2019
ms.date: 08/13/2020
ms.author: v-tawe
ms.custom: include file
ms.openlocfilehash: f98597e260d9777b79a95575d9ff3236a5770383
ms.sourcegitcommit: 9d9795f8a5b50cd5ccc19d3a2773817836446912
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "89503356"
---
在 Azure CLI 中，使用 [`az appservice plan create`](/cli/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) 命令在资源组中创建应用服务计划。

[!INCLUDE [app-service-plan](app-service-plan-linux.md)]

以下示例在**免费**定价层 (`--sku F1`) 和 Linux 容器 (`--is-linux`) 中创建名为 `myAppServicePlan` 的应用服务计划。

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku F1 --is-linux
```

创建应用服务计划后，Azure CLI 会显示类似于以下示例的信息：

<pre>
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "China East 2",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "linux",
  "location": "China East 2",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  &lt; JSON data removed for brevity. &gt;
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
} 
</pre>
