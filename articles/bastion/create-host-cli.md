---
title: 使用 Azure CLI 创建 Bastion 主机 | Azure Bastion
description: 本文介绍如何创建和删除 Bastion 主机
services: bastion
author: rockboyfor
ms.service: bastion
ms.topic: how-to
origin.date: 03/26/2020
ms.date: 09/14/2020
ms.testscope: yes
ms.testdate: 07/27/2020
ms.author: v-yeche
Customer intent: As someone with a networking background, I want to create an Azure Bastion host.
ms.openlocfilehash: 77137b0e9f1e1f8268a1458a96b81a7e9bb3bef3
ms.sourcegitcommit: e1cd3a0b88d3ad962891cf90bac47fee04d5baf5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2020
ms.locfileid: "89655554"
---
<!--Verified successfully on 09/07/2020->
# Create an Azure Bastion host using Azure CLI

This article shows you how to create an Azure Bastion host using Azure CLI. Once you provision the Azure Bastion service in your virtual network, the seamless RDP/SSH experience is available to all of the VMs in the same virtual network. Azure Bastion deployment is per virtual network, not per subscription/account or virtual machine.

Optionally, you can create an Azure Bastion host by using the [Azure portal](bastion-create-host-portal.md), or using [Azure PowerShell](bastion-create-host-powershell.md).

## Before you begin

Verify that you have an Azure subscription. If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://www.azure.cn/offers/ms-mc-arz-msdn/index.html) or sign up for a [trial account](https://www.azure.cn/pricing/1rmb-trial).

<!--Not Available on [!INCLUDE [cloudshell cli](../../includes/vpn-gateway-cloud-shell-cli.md)]-->

<a name="createhost"></a>
##创建 Bastion 主机

本部分帮助你使用 Azure CLI 创建新的 Azure Bastion 资源。

1. 创建虚拟网络和 Azure Bastion 子网。 必须使用名称值 AzureBastionSubnet 创建 Azure Bastion 子网。 此值告知 Azure 要将 Bastion 资源部署到哪个子网。 这不同于网关子网。 必须使用至少为 /27 或更大（/27、/26 等）的子网。 创建不包含任何路由表或委托的 AzureBastionSubnet。 如果使用 AzureBastionSubnet 上的网络安全组，请参阅[使用 NSG](bastion-nsg.md) 一文。

   ```azurecli
   az network vnet create -g MyResourceGroup -n MyVnet --address-prefix 10.0.0.0/16 --subnet-name AzureBastionSubnet  --subnet-prefix 10.0.0.0/24
   ```

2. 为 Azure Bastion 创建一个公共 IP 地址。 此公共 IP 是将在其上访问 RDP/SSH（通过端口 443）的 Bastion 资源的公共 IP 地址。 公共 IP 地址必须与要创建的 Bastion 资源位于同一区域。

   ```azurecli
   az network public-ip create -g MyResourceGroup -n MyIp --sku Standard
   ```

3. 在虚拟网络的 AzureBastionSubnet 中创建新的 Azure Bastion 资源。 创建和部署 Bastion 资源大约需要 5 分钟。

   ```azurecli
   az network bastion create --name $name --public-ip-address $publicip --resource-group $RgName --vnet-name $VNetName --location $location

   ```

## <a name="next-steps"></a>后续步骤

* 有关其他信息，请参阅 [Bastion 常见问题解答](bastion-faq.md)。

* 若要在 Azure Bastion 子网中使用网络安全组，请参阅[使用 NSG](bastion-nsg.md)。

<!-- Update_Description: new article about create host cli -->
<!--NEW.date: 07/27/2020-->