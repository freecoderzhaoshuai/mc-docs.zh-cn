---
title: VM 大小
description: 列出 Azure 中虚拟机的不同可用大小。
author: rockboyfor
ms.service: virtual-machines
ms.subservice: sizes
ms.topic: conceptual
ms.workload: infrastructure-services
origin.date: 07/21/2020
ms.date: 08/31/2020
ms.testscope: yes
ms.testdate: 08/31/2020
ms.author: v-yeche
ms.openlocfilehash: 1d6db7bce580cd0b2d894763791f0da5ca63f098
ms.sourcegitcommit: 63a4bc7c501fb6dd54a31d39c87c0e8692ac2eb0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89052350"
---
<!--Verified Successfully-->
# <a name="sizes-for-virtual-machines-in-azure"></a>Azure 中虚拟机的大小

本文介绍可用于运行应用和工作负载的 Azure 虚拟机的可用大小与选项。 此外，还提供在计划使用这些资源时要考虑的部署注意事项。 

| 类型 | 大小 | 说明 |
|------|-------|-------------|
| [常规用途](sizes-general.md)   | B、Dsv3、Dv3、DSv2、Dv2、Av2 | CPU 与内存之比平衡。 适用于测试和开发、小到中型数据库和低到中等流量 Web 服务器。 |
| [计算优化](sizes-compute.md) | Fsv2 | 高 CPU 与内存之比。 适用于中等流量的 Web 服务器、网络设备、批处理和应用程序服务器。 |
| [内存优化](sizes-memory.md) | Esv3、Ev3、M、DSv2、Dv2  | 高内存与 CPU 之比。 适用于关系数据库服务器、中到大型规模的缓存和内存中分析。 |
| [GPU](sizes-gpu.md) | NC、NCv2、NCv3、NCasT4_v3（预览版）、ND、NDv2（预览版）、NV、NVv3、NVv4 | 针对大量图形绘制和视频编辑的专用虚拟机，以及带有深度学习功能的模型定型和推断 (ND)。 可选择单个或多个 GPU。 |

<!-- Not Available  Dasv4, Dav4, DC series -->
<!-- Not Available  Easv4, Eav4, Mv2, -->
<!-- Not Available [Storage optimized](../virtual-machines-windows-sizes-storage.md)        | Lsv2 -->
<!-- Not Available [GPU](sizes-gpu.md)            | NC, NVv2, ND, NDv2 (Preview), NV, NVv3, NVv4 (Preview)   -->
<!-- Not Available [High performance compute](sizes-hpc.md) | HB, HBv2, HC, H-->

- 有关不同大小的定价信息，请参阅 [Linux](https://www.azure.cn/pricing/details/virtual-machines/) 或 [Windows](https://www.azure.cn/pricing/details/virtual-machines/) 的定价页。
- 如需了解 Azure 区域中各种 VM 大小的可用性，请参阅 [可用产品（按区域）](https://azure.microsoft.com/regions/services/)。
- 若要查看 Azure VM 的一般限制，请参阅 [Azure 订阅和服务限制、配额与约束](../azure-resource-manager/management/azure-subscription-service-limits.md)。
- 有关 Azure 如何命名其 VM 的详细信息，请参阅 [Azure 虚拟机大小命名约定](./vm-naming-conventions.md)。

## <a name="rest-api"></a>REST API

有关使用 REST API 来查询 VM 大小的信息，请参阅以下文章：

- [List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/listavailablesizes)（列出可用的虚拟机大小以便调整大小）
- [List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/resourceskus/list)（列出订阅的可用虚拟机大小）
- [List available virtual machine sizes in an availability set](https://docs.microsoft.com/rest/api/compute/availabilitysets/listavailablesizes)（列出可用性集中的可用虚拟机大小）

## <a name="acu"></a>ACU

了解有关 [Azure 计算单元 (ACU)](acu.md) 如何帮助跨 Azure SKU 比较计算性能的详细信息。

## <a name="benchmark-scores"></a>基准评分

使用 [CoreMark 基准测试分数](./linux/compute-benchmark-scores.md)，详细了解 Linux VM 的计算性能。

使用 [SPECInt 基准测试分数](./windows/compute-benchmark-scores.md)，详细了解 Windows VM 的计算性能。

<!--Not Available on ## Manage costs-->

<!--Not Suitable on [!INCLUDE [cost-management-horizontal](../../includes/cost-management-horizontal.md)]-->
<!--For cost-management-billing is not Available on Azure China-->

## <a name="next-steps"></a>后续步骤

了解关于可用的各种 VM 大小的详细信息：

- [常规用途](sizes-general.md)
- [计算优化](sizes-compute.md)
- [内存优化](sizes-memory.md)
    
    <!--Not Avaialble on - [Storage optimized](sizes-storage.md)-->
    
- [GPU](sizes-gpu.md)
    
    <!-- Not Available on - [High performance compute](sizes-hpc.md)-->
    
- 查看[上一代](sizes-previous-gen.md)页面，了解 A Standard、Dv1（D1-4 和 D11-14 v1）以及 A8-A11 系列

<!-- Update_Description: new article about sizes -->
<!--NEW.date: 08/31/2020-->