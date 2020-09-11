---
author: WenJason
ms.service: media-services
ms.topic: include
origin.date: 08/18/2020
ms.date: 09/07/2020
ms.author: v-jay
ms.custom: CLI
ms.openlocfilehash: 32e74655a772676b76439c088528a50e9b126dfd
ms.sourcegitcommit: 2eb5a2f53b4b73b88877e962689a47d903482c18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89414097"
---
<!--Create a media services asset REST-->

以下 Azure REST 命令创建新的媒体服务资产。 将 `subscriptionID`、`resourceGroup` 和 `amsAccountName` 值替换为当前正在使用的值。 通过在此处设置 `assetName` 来为资产提供名称。

```
PUT https://management.chinacloudapi.cn/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Media/mediaServices/{amsAccountName}/assets/{assetName}?api-version=2018-07-01
```