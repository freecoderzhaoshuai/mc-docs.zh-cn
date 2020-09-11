---
title: 将托管磁盘快照复制到订阅 - CLI 示例
description: Azure CLI 脚本示例 - 使用 CLI 将托管磁盘的快照复制（或移动）到同一订阅或不同订阅
documentationcenter: storage
manager: kavithag
ms.service: virtual-machines
ms.subservice: disks
ms.topic: sample
ms.workload: infrastructure
origin.date: 05/19/2017
author: rockboyfor
ms.date: 09/07/2020
ms.testscope: no
ms.testdate: ''
ms.author: v-yeche
ms.custom: mvc
ms.openlocfilehash: 6ddc923d81bf9781033195888ca150d647aaef07
ms.sourcegitcommit: 2eb5a2f53b4b73b88877e962689a47d903482c18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89413843"
---
<!--Verified successfully from renamed articles-->
# <a name="copy-snapshot-of-a-managed-disk-to-same-or-different-subscription-with-cli"></a>使用 CLI 将托管磁盘的快照复制到相同或不同的订阅

此脚本会将托管磁盘的快照复制到相同或不同的订阅。 将此脚本用于以下方案：

1. 将高级存储 (Premium_LRS) 中的快照迁移到标准存储 (Standard_LRS) 以降低成本。

<!--Not Available on or Standard_ZRS(THIS FEATURE IS NOT AVAILABLE ON AZURE CHINA CLOUD)-->

<!--Not Available on to zone redundant storage (Standard_ZRS(THIS FEATURE IS NOT AVAILABLE ON AZURE CHINA CLOUD))-->

1. 将快照移到同一区域中的不同订阅，以延长保留时间。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>示例脚本

```azurecli
#Provide the subscription Id of the subscription where snapshot exists
sourceSubscriptionId=dd80b94e-0463-4a65-8d04-c94f403879dc

#Provide the name of your resource group where snapshot exists
sourceResourceGroupName=mySourceResourceGroupName

#Provide the name of the snapshot
snapshotName=mySnapshotName

#Set the context to the subscription Id where snapshot exists
az account set --subscription $sourceSubscriptionId

#Get the snapshot Id 
snapshotId=$(az snapshot show --name $snapshotName --resource-group $sourceResourceGroupName --query [id] -o tsv)

#If snapshotId is blank then it means that snapshot does not exist.
echo 'source snapshot Id is: ' $snapshotId

#Provide the subscription Id of the subscription where snapshot will be copied to
#If snapshot is copied to the same subscription then you can skip this step
targetSubscriptionId=6492b1f7-f219-446b-b509-314e17e1efb0

#Name of the resource group where snapshot will be copied to
targetResourceGroupName=mytargetResourceGroupName

#Set the context to the subscription Id where snapshot will be copied to
#If snapshot is copied to the same subscription then you can skip this step
az account set --subscription $targetSubscriptionId

#Copy snapshot to different subscription using the snapshot Id
#We recommend you to store your snapshots in Standard storage to reduce cost. 

az snapshot create --resource-group $targetResourceGroupName --name $snapshotName --source $snapshotId --sku Standard_LRS

```

<!--Not Available on Line 69 Please use Standard_ZRS(THIS FEATURE IS NOT AVAILABLE ON AZURE CHINA CLOUD) in regions where zone redundant storage (ZRS) is available, otherwise use Standard_LRS-->
<!--Not Available on Line 69 + 1 #Please check out the availability of ZRS here: https://docs.azure.cn/storage/common/storage-redundancy-zrs#support-coverage-and-regional-availability-->
## <a name="script-explanation"></a>脚本说明

此脚本使用以下命令，通过源快照的 ID 在目标订阅中创建快照。 表中的每条命令均链接到特定于命令的文档。

| 命令 | 说明 |
|---|---|
| [az snapshot show](https://docs.azure.cn/cli/snapshot?view=azure-cli-latest#az-snapshot-show) | 使用快照的名称和资源组属性获取该快照的所有属性。 使用 ID 属性将快照复制到其他订阅。  |
| [az snapshot create](https://docs.azure.cn/cli/snapshot?view=azure-cli-latest#az-snapshot-create) | 通过使用父快照的 ID 和名称在不同订阅中创建快照来复制快照。  |

## <a name="next-steps"></a>后续步骤

[从快照创建虚拟机](./virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fvirtual-machines%2flinux%2ftoc.json)

有关 Azure CLI 的详细信息，请参阅 [Azure CLI 文档](https://docs.azure.cn/cli/index?view=azure-cli-latest)。

可以在 [Azure Linux VM 文档](../linux/cli-samples.md?toc=%2fvirtual-machines%2flinux%2ftoc.json)中找到其他虚拟机和托管磁盘 CLI 脚本示例。

<!-- Update_Description: new article about virtual machines cli sample copy snapshot to same or different subscription -->
<!--NEW.date: 09/07/2020-->