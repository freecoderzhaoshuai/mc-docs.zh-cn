---
ms.date: 07/17/2020
ms.author: v-junlch
ms.openlocfilehash: 650d08e0a5c7f4054b6e0c10c8e9452926f81783
ms.sourcegitcommit: daf7317c80f13e459469bbc507786520c8fa6d70
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89046364"
---
| 功能 |[消耗计划](../articles/azure-functions/functions-scale.md#consumption-plan) |[专用计划](../articles/azure-functions/functions-scale.md#app-service-plan)|[ASE](../articles/app-service/environment/intro.md)| Kubernetes |
|----------------|-----------|----------------|---------|-----------------------| ---|
|[入站 IP 限制和专用站点访问](../articles/azure-functions/functions-networking-options.md#inbound-ip-restrictions)|✅是 |✅是|✅是|✅是|
|[虚拟网络集成](../articles/azure-functions/functions-networking-options.md#virtual-network-integration)|❌否|✅是（区域） |✅是| ✅是|
|[虚拟网络触发器（非 HTTP）](../articles/azure-functions/functions-networking-options.md#virtual-network-triggers-non-http)|❌否 |✅是|✅是|✅是|
|[混合连接](../articles/azure-functions/functions-networking-options.md#hybrid-connections)（仅限 Windows）|❌否 |✅是|✅是|✅是|
|[出站 IP 限制](../articles/azure-functions/functions-networking-options.md#outbound-ip-restrictions)|❌否 |✅是|✅是|✅是|

