---
author: WenJason
ms.service: media-services
ms.topic: include
origin.date: 08/18/2020
ms.date: 09/07/2020
ms.author: v-jay
ms.custom: cURL
ms.openlocfilehash: d52f7d55e2cbcac9db4d36beb595a0e8da584d4a
ms.sourcegitcommit: 2eb5a2f53b4b73b88877e962689a47d903482c18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89414098"
---
<!--Create a media services asset cURL-->

以下 Azure cURL 命令创建新的媒体服务资产。 将 `subscriptionID`、`resourceGroup` 和 `amsAccountName` 值替换为当前正在使用的值。 通过在此处设置 `assetName` 来为资产提供名称。

```cURL
curl -X PUT 'https://management.chinacloudapi.cn/subscriptions/00000000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Media/mediaServices/amsAccountName/assets/myOutputAsset?api-version=2018-07-01' -H 'Accept: application/json' -H 'Content-Type: application/json' -d '{"properties": {"description": "",}}'
```
