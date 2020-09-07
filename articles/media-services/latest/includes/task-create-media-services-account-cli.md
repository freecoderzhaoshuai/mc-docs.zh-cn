---
author: WenJason
ms.service: media-services
ms.topic: include
origin.date: 08/17/2020
ms.date: 09/07/2020
ms.author: v-jay
ms.custom: CLI
ms.openlocfilehash: d52b7dd428ff1c1b382b46b9b63f8abe6bc740cc
ms.sourcegitcommit: 2eb5a2f53b4b73b88877e962689a47d903482c18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89413371"
---
<!--Create a media services account -->

以下 Azure CLI 命令创建新的媒体服务帐户。 可以替换以下值：`amsaccount``storageaccountforams`（必须与提供给存储帐户的值相符）和 `amsResourceGroup`（必须与提供给资源组的值相符）。

```azurecli
az ams account create --name amsaccount -g amsResourceGroup --storage-account storageaccountforams -l chinaeast2
```