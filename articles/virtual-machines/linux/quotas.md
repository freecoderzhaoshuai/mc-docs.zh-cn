---
title: vCPU 配额
description: 了解 Azure 的 vCPU 配额。
author: Johnnytechn
ms.service: virtual-machines
ms.workload: infrastructure-services
ms.topic: how-to
ms.date: 09/03/2020
ms.author: v-johya
ms.openlocfilehash: dcef232e20f99888c98e9236ac7666a232e09e88
ms.sourcegitcommit: f45809a2120ac7a77abe501221944c4482673287
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2020
ms.locfileid: "90057511"
---
# <a name="check-vcpu-quotas-using-the-azure-cli"></a>使用 Azure CLI 检查 vCPU 配额

虚拟机和虚拟机规模集的 vCPU 配额已根据每个区域中的每个订阅划分成两层。 第一层是区域的 vCPU 总数，第二层是各种 VM 大小系列核心（如 D 系列 vCPU）。 每当部署新 VM 时，VM 的 vCPU 数不能超过 VM 大小系列的 vCPU 配额或区域 vCPU 配额总数。 如果超过了上述任一配额，将不允许部署 VM。 此外，区域中的虚拟机总数也有一个配额。 有关上述每个配额的详细信息，可以在 [Azure 门户](https://portal.azure.cn)的“订阅”页的“使用情况 + 配额”部分中查看，也可以使用 Azure CLI 查询值。

> [!NOTE]
> 配额基于所使用的核心总数（已分配和已解除分配）进行计算。 如果需要额外核心，则请求增加配额或删除不再需要的 VM。 


## <a name="check-usage"></a>检查使用情况

可以使用 [az vm list-usage](https://docs.azure.cn/cli/vm?view=azure-cli-latest#az-vm-list-usage) 检查配额用量。

```azurecli
az vm list-usage --location "China East" -o table
```

输出应类似于：


```
Name                                CurrentValue    Limit
--------------------------------  --------------  -------
Availability Sets                              0     2000
Total Regional vCPUs                          29      100
Virtual Machines                               7    10000
Virtual Machine Scale Sets                     0     2000
Standard DSv3 Family vCPUs                     8      100
Standard DSv2 Family vCPUs                     3      100
Standard Dv3 Family vCPUs                      2      100
Standard D Family vCPUs                        8      100
Standard Dv2 Family vCPUs                      8      100
Basic A Family vCPUs                           0      100
Standard A0-A7 Family vCPUs                    0      100
Standard DS Family vCPUs                       0      100
Standard F Family vCPUs                        0      100
Standard FS Family vCPUs                       0      100
Standard Storage Managed Disks                 5    10000
Premium Storage Managed Disks                  5    10000
```
<!-- Not Available on Standard A8-A11 Family vCPUs -->
<!-- Not Available on Standard G Family vCPUs -->
<!-- Not Available on Standard GS Family vCPUs -->

<!--Not Available on ## Reserved VM Instances-->

## <a name="next-steps"></a>后续步骤

有关计费和配额的详细信息，请参阅 [Azure 订阅和服务限制、配额与约束](../../azure-resource-manager/management/azure-subscription-service-limits.md)。

<!-- Update_Description: update meta properties, wording update, update link -->