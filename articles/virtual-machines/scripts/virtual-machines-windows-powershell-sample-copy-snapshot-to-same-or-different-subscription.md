---
title: 从托管磁盘到订阅的快照 (Windows) - PowerShell
description: Azure PowerShell 脚本示例 - 将托管磁盘的快照复制（移动）到相同或不同的订阅
services: virtual-machines-windows
documentationcenter: storage
author: rockboyfor
manager: digimobile
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-windows
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
origin.date: 02/28/2019
ms.date: 08/31/2020
ms.testscope: yes
ms.testdate: 08/31/2020
ms.author: v-yeche
ms.openlocfilehash: 6e031701ee538b1bab5059f186303e8beb64bd0a
ms.sourcegitcommit: 2eb5a2f53b4b73b88877e962689a47d903482c18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89413227"
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell-windows"></a>使用 PowerShell 将托管磁盘的快照复制到同一订阅或不同订阅 (Windows)

此脚本会将托管磁盘的快照复制到相同或不同的订阅。 将此脚本用于以下方案：

1. 将高级存储 (Premium_LRS) 中的快照迁移到标准存储 (Standard_LRS) 以降低成本。
  
    <!--Not Available on Standard_ZRS-->

1. 将快照移到同一区域中的不同订阅，以延长保留时间。

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>示例脚本

```powershell
# Sign-in the Azure China Cloud
Connect-AzAccount -Environment AzureChinaCloud

#Provide the subscription Id of the subscription where snapshot exists
$sourceSubscriptionId='yourSourceSubscriptionId'

#Provide the name of your resource group where snapshot exists
$sourceResourceGroupName='yourResourceGroupName'

#Provide the name of the snapshot
$snapshotName='yourSnapshotName'

#Set the context to the subscription Id where snapshot exists
Select-AzSubscription -SubscriptionId $sourceSubscriptionId

#Get the source snapshot
$snapshot= Get-AzSnapshot -ResourceGroupName $sourceResourceGroupName -Name $snapshotName

#Provide the subscription Id of the subscription where snapshot will be copied to
#If snapshot is copied to the same subscription then you can skip this step
$targetSubscriptionId='yourTargetSubscriptionId'

#Name of the resource group where snapshot will be copied to
$targetResourceGroupName='yourTargetResourceGroupName'

#Set the context to the subscription Id where snapshot will be copied to
#If snapshot is copied to the same subscription then you can skip this step
Select-AzSubscription -SubscriptionId $targetSubscriptionId

#We recommend you to store your snapshots in Standard storage to reduce cost. Please use Standard_LRS
#Please check out the availability of ZRS here: https://docs.microsoft.com/Az.Storage/common/storage-redundancy-zrs#support-coverage-and-regional-availability
$snapshotConfig = New-AzSnapshotConfig -SourceResourceId $snapshot.Id -Location $snapshot.Location -CreateOption Copy -SkuName Standard_LRS

#Create a new snapshot in the target subscription and resource group
New-AzSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $targetResourceGroupName

```

<!--Not Available on #We recommend on Standard_ZRS-->

## <a name="script-explanation"></a>脚本说明

此脚本使用以下命令，通过源快照的 ID 在目标订阅中创建快照。 表中的每条命令均链接到特定于命令的文档。

| 命令 | 说明 |
|---|---|
| [New-AzSnapshotConfig](https://docs.microsoft.com/powershell/module/az.compute/New-AzSnapshotConfig) | 创建用于创建快照的快照配置。 包括父快照的资源 ID 以及与父快照相同的位置。  |
| [New-AzSnapshot](https://docs.microsoft.com/powershell/module/az.compute/new-azsnapshot) | 使用快照配置、快照名称和作为参数传递的资源组名称创建快照。 |

## <a name="next-steps"></a>后续步骤

[从快照创建虚拟机](./virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fvirtual-machines%2fwindows%2ftoc.json)

有关 Azure PowerShell 模块的详细信息，请参阅 [Azure PowerShell 文档](https://docs.microsoft.com/powershell/azure/)。

可以在 [Azure Windows VM 文档](../windows/powershell-samples.md?toc=%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他虚拟机 PowerShell 脚本示例。

<!-- Update_Description: update meta properties, wording update, update link -->