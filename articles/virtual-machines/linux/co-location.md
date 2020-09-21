---
title: 并置 Linux VM
description: 了解并置 Azure VM 资源如何改善延迟。
author: Johnnytechn
ms.service: virtual-machines
origin.date: 10/30/2019
ms.topic: conceptual
ms.date: 09/03/2020
ms.author: v-johya
ms.openlocfilehash: b285560aff7e561df14a78613c3f89a4b05be198
ms.sourcegitcommit: f45809a2120ac7a77abe501221944c4482673287
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2020
ms.locfileid: "90057490"
---
<!--Verified successfully-->
# <a name="co-locate-resources-for-improved-latency"></a>并置资源以改善延迟

在 Azure 中部署应用程序时，跨区域分布实例会造成网络延迟，这可能会影响应用程序的总体性能。 

## <a name="proximity-placement-groups"></a>邻近放置组

[!INCLUDE [virtual-machines-common-ppg-overview](../../../includes/virtual-machines-common-ppg-overview.md)]

## <a name="next-steps"></a>后续步骤

使用 Azure CLI 将 VM 部署到[邻近放置组](proximity-placement-groups.md)。

了解如何[测试网络延迟](https://docs.azure.cn/virtual-network/virtual-network-test-latency?toc=%2fvirtual-machines%2fwindows%2ftoc.json)。

了解如何[优化网络吞吐量](/virtual-network/virtual-network-optimize-network-bandwidth?toc=%2fvirtual-machines%2fwindows%2ftoc.json)。  

<!--Not Available on [use proximity placement groups with SAP applications](/virtual-machines/workloads/sap/sap-proximity-placement-scenarios?toc=%2fvirtual-machines%2fwindows%2ftoc.json)-->

<!-- Update_Description: new article about co location -->
<!--NEW.date: 04/30/2020-->