---
author: ggailey777
ms.service: azure-functions
ms.topic: include
ms.date: 09/03/2020
ms.author: v-junlch
ms.openlocfilehash: 96f4313a1e4ca953884dee3b80cf2439762ea814
ms.sourcegitcommit: 2eb5a2f53b4b73b88877e962689a47d903482c18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89413618"
---
```json
{
    "version": "2.0",
    "extensionBundle": {
        "id": "Microsoft.Azure.Functions.ExtensionBundle",
        "version": "[1.*, 2.0.0)"
    }
}
```

`extensionBundle` 中提供了以下属性：

| properties | 说明 |
| -------- | ----------- |
| id | Azure Functions 扩展捆绑的命名空间。 |
| 版本 | 要安装的捆绑包的版本。 Functions 运行时始终选取由版本范围或间隔定义的可允许最高版本。 上述版本值允许从 1.0.0 到（但不包括）2.0.0 的所有捆绑包版本。 有关详细信息，请参阅[用于指定版本范围的间隔表示法](https://docs.microsoft.com/nuget/reference/package-versioning#version-ranges)。 |

