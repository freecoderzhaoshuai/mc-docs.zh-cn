---
author: rothja
ms.service: cost-management-billing
ms.topic: include
ms.date: 03/31/2020
ms.author: v-junlch
ms.openlocfilehash: 2780e927f932c950f6035abaa87900a34e05a0f7
ms.sourcegitcommit: 4db9853370c9d4c7e5d54f1e1cfadf40efcc12a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89326532"
---
| 资源 | 限制 |
| --- | --- |
| [每个部署的 Web 角色或辅助角色数](../articles/cloud-services/cloud-services-choose-me.md)<sup>1</sup> |25 |
| 每个部署的[实例输入终结点数](https://docs.microsoft.com/previous-versions/azure/reference/gg557552(v=azure.100)#instanceinputendpoint) |25 |
| 每个部署的[输入终结点数](https://docs.microsoft.com/previous-versions/azure/reference/gg557552(v=azure.100)#inputendpoint) |25 |
| 每个部署的[内部终结点数](https://docs.microsoft.com/previous-versions/azure/reference/gg557552(v=azure.100)#internalendpoint) |25 |
| 每个部署的[托管服务证书数](../articles/cloud-services/cloud-services-certs-create.md#what-are-service-certificates) |199 |

<sup>1</sup>每个具有 Web 角色或辅助角色的 Azure 云服务可以有两个部署，一个用于生产，一个用于过渡。 此限制针对不同角色的数目，即配置。 此限制并非针对每个角色的实例数，即缩放。


