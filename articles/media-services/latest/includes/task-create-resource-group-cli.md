---
author: WenJason
ms.service: media-services
ms.topic: include
origin.date: 08/17/2020
ms.date: 09/07/2020
ms.author: v-jay
ms.custom: CLI
ms.openlocfilehash: 121f966606a4227653ac86b48ddd056ebbc4b7b9
ms.sourcegitcommit: 2eb5a2f53b4b73b88877e962689a47d903482c18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89413369"
---
<!-- Create a resource group -->

使用以下命令来创建资源组。 选择用于存储媒体服务帐户的媒体和元数据记录的地理区域。 此区域用于处理和流式传输媒体。

```azurecli
az group create --name amsResourceGroup --location chinaeast2
```
