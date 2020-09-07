---
author: WenJason
ms.service: media-services
ms.topic: include
origin.date: 08/17/2020
ms.date: 09/07/2020
ms.author: v-jay
ms.custom: CLI
ms.openlocfilehash: c0a3e300a9fb002d0ea9417e94247d9545fa7133
ms.sourcegitcommit: 2eb5a2f53b4b73b88877e962689a47d903482c18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89414091"
---
<!-- List and set subscriptions -->

1. 使用 [az account list](https://docs.microsoft.com/cli/azure/account#az-account-list) 命令获取订阅列表。

    ```
    az account list --output table
    ```

2. 结合你要切换到的订阅 ID 或名称使用 `az account set`。

    ```
    az account set --subscription "My Demos"
    ```
