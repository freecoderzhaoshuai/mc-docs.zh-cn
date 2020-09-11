---
title: 并置 VM 以缩短延迟
description: 了解并置 Azure VM 资源如何改善延迟。
ms.service: virtual-machines
ms.topic: conceptual
ms.workload: infrastructure-services
origin.date: 10/30/2019
author: rockboyfor
ms.date: 09/07/2020
ms.testscope: no
ms.testdate: ''
ms.author: v-yeche
ms.openlocfilehash: 4751271be39925c031e277556e0b32d0acf95cd8
ms.sourcegitcommit: 22e1da9309795e74a91b7241ac5987a802231a8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2020
ms.locfileid: "89463178"
---
<!--Verified successfully-->
# <a name="co-locate-resource-for-improved-latency"></a>并置资源以改善延迟

在 Azure 中部署应用程序时，跨区域或可用性区域分布实例会造成网络延迟，这可能会影响应用程序的总体性能。 

## <a name="proximity-placement-groups"></a>邻近放置组 

[!INCLUDE [virtual-machines-common-ppg-overview](../../../includes/virtual-machines-common-ppg-overview.md)]

## <a name="next-steps"></a>后续步骤

使用 Azure PowerShell 将 VM 部署到[邻近放置组](proximity-placement-groups.md)。

了解如何[测试网络延迟](https://docs.azure.cn/virtual-network/virtual-network-test-latency?toc=%2fvirtual-machines%2fwindows%2ftoc.json)。

了解如何[优化网络吞吐量](../../virtual-network/virtual-network-optimize-network-bandwidth.md?toc=%2fvirtual-machines%2fwindows%2ftoc.json)。  

<!--Not Available on [use proximity placement groups with SAP applications](/virtual-machines/workloads/sap/sap-proximity-placement-scenarios?toc=%2fvirtual-machines%2fwindows%2ftoc.json)-->

<!-- Update_Description: update meta properties, wording update, update link -->