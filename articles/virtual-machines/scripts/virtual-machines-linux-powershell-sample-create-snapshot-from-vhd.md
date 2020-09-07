---
title: 用于创建多个相同托管磁盘的 VHD 快照 (Linux) - PowerShell
description: Azure PowerShell 脚本示例 - 从 VHD 创建快照以在短时间内创建多个相同的托管磁盘
services: virtual-machines-linux
documentationcenter: storage
manager: kavithag
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-linux
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
origin.date: 06/05/2017
author: rockboyfor
ms.date: 09/07/2020
ms.testscope: yes
ms.testdate: 08/31/2020
ms.author: v-yeche
ms.openlocfilehash: df1f737bb216f5ddc7f361bef5640603233b745a
ms.sourcegitcommit: 2eb5a2f53b4b73b88877e962689a47d903482c18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89414039"
---
# <a name="create-a-snapshot-from-a-vhd-to-create-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell-linux"></a>使用 PowerShell 基于 VHD 创建快照以在短时间内创建多个相同的托管磁盘 (Linux)

此脚本在相同或不同订阅的存储帐户中从 VHD 文件创建快照。 使用此脚本将专用 VHD（未通用化/未进行 sysprep）导入到某快照，然后使用该快照在短时间内创建多个相同的托管磁盘。 同时使用它将数据 VHD 导入到某快照，然后使用该快照在短时间内创建多个托管磁盘。

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>示例脚本

```powershell
# Sign-in the Azure China Cloud
Connect-AzAccount -Environment AzureChinaCloud

#Provide the subscription Id where snapshot will be created
$subscriptionId = 'yourSubscriptionId'

#Provide the name of your resource group where snapshot will be created. 
$resourceGroupName ='yourResourceGroupName'

#Provide the name of the snapshot
$snapshotName = 'yourSnapshotName'

#Provide the storage type for snapshot. PremiumLRS or StandardLRS.
$storageType = 'Standard_LRS'

#Provide the Azure region (e.g. chinanorth) where snapshot will be located.
#This location should be same as the storage account location where VHD file is stored 
#Get all the Azure location using command below:
#Get-AzLocation
$location = 'chinanorth'

#Provide the URI of the VHD file (page blob) in a storage account. Please not that this is NOT the SAS URI of the storage container where VHD file is stored. 
#e.g. https://contosostorageaccount1.blob.core.chinacloudapi.cn/vhds/contosovhd123.vhd
#Note: VHD file can be deleted as soon as Managed Disk is created.
$sourceVHDURI = 'https://yourStorageAccountName.blob.core.chinacloudapi.cn/vhds/yourVHDName.vhd'

#Provide the resource Id of the storage account where VHD file is stored. 
#e.g. /subscriptions/6582b1g7-e212-446b-b509-314e17e1efb0/resourceGroups/MDDemo/providers/Microsoft.Storage/storageAccounts/contosostorageaccount1
#This is an optional parameter if you are creating snapshot in the same subscription
$storageAccountId = '/subscriptions/yourSubscriptionId/resourceGroups/yourResourceGroupName/providers/Microsoft.Storage/storageAccounts/yourStorageAccountName'

#Set the context to the subscription Id where Managed Disk will be created
Select-AzSubscription -SubscriptionId $SubscriptionId

$snapshotConfig = New-AzSnapshotConfig -AccountType $storageType -Location $location -CreateOption Import -StorageAccountId $storageAccountId -SourceUri $sourceVHDURI 

New-AzSnapshot -Snapshot $snapshotConfig -ResourceGroupName $resourceGroupName -SnapshotName $snapshotName

```

## <a name="script-explanation"></a>脚本说明

此脚本使用以下命令在不同订阅中从 VHD 创建托管磁盘。 表中的每条命令均链接到特定于命令的文档。

| 命令 | 注释 |
|---|---|
| [New-AzDiskConfig](https://docs.microsoft.com/powershell/module/az.compute/new-azdiskconfig) | 创建用于磁盘创建的磁盘配置。 包括存储类型、位置、存储父 VHD 的存储帐户的资源 ID 以及父 VHD 的 VHD URI。 |
| [New-AzDisk](https://docs.microsoft.com/powershell/module/az.compute/new-azdisk) | 使用磁盘配置、磁盘名称和作为参数传递的资源组名称创建磁盘。 |

## <a name="next-steps"></a>后续步骤

[从快照创建托管磁盘](virtual-machines-linux-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fvirtual-machines%2flinux%2ftoc.json)

有关 Azure PowerShell 模块的详细信息，请参阅 [Azure PowerShell 文档](https://docs.microsoft.com/powershell/azure/)。

可以在 [Azure Linux VM 文档](../linux/powershell-samples.md?toc=%2fvirtual-machines%2flinux%2ftoc.json)中找到其他虚拟机 PowerShell 脚本示例。

<!-- Update_Description: update meta properties, wording update, update link -->