---
author: WenJason
ms.service: media-services
ms.topic: include
origin.date: 08/18/2020
ms.date: 09/07/2020
ms.author: v-jay
ms.custom: CLI
ms.openlocfilehash: eae4a5aa575071e8013d42569839d9a42f18f83d
ms.sourcegitcommit: 2eb5a2f53b4b73b88877e962689a47d903482c18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89414092"
---
<!--Create a media services asset CLI-->

以下 Azure CLI 命令创建新的媒体服务资产。 将 `assetName`、`amsAccountName` 和 `resourceGroup` 值替换为当前正在使用的值。

```azurecli
az ams asset create -n assetName -a amsAccountName -g resourceGroup
```
