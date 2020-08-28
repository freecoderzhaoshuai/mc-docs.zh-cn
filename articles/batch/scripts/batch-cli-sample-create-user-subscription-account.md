---
title: Azure CLI 脚本示例 - 创建 Batch 帐户 - 用户订阅
description: 此脚本在用户订阅模式下创建 Azure Batch 帐户。 此帐户将计算节点分配到你的订阅。
ms.topic: sample
author: rockboyfor
origin.date: 01/29/2018
ms.date: 08/24/2020
ms.testscope: no
ms.testdate: ''
ms.author: v-yeche
ms.custom: devx-track-azurecli
ms.openlocfilehash: 9df6fcfc3577701a87254731a8c899b6faca3d5b
ms.sourcegitcommit: e633c458126612223fbf7a8853dbf19acc7f0fa5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88654925"
---
# <a name="cli-example-create-a-batch-account-in-user-subscription-mode"></a>CLI 示例：在用户订阅模式下创建 Batch 帐户

此脚本在用户订阅模式下创建 Azure Batch 帐户。 必须通过 Azure Active Directory 令牌对那些将计算节点分配到订阅中的帐户进行身份验证。 计算节点将计数分配到订阅的 vCPU（核心）配额。 

[!INCLUDE [azure-cli-2-azurechinacloud-environment-parameter](../../../includes/azure-cli-2-azurechinacloud-environment-parameter.md)]

如果选择在本地安装并使用 CLI，本文要求运行 Azure CLI 2.0.20 或更高版本。 运行 `az --version` 即可查找版本。 如果需要进行安装或升级，请参阅[安装 Azure CLI](https://docs.azure.cn/cli/install-azure-cli?view=azure-cli-latest)。 

## <a name="example-script"></a>示例脚本

```azurecli
#!/bin/bash

# Allow Azure Batch to access the subscription (one-time operation).
az role assignment create \
    --assignee MicrosoftAzureBatch \
    --role contributor

# Create a resource group.
az group create --name myResourceGroup --location chinanorth

# Create an Azure Key Vault. A Batch account that allocates pools in the user's subscription 
# must be configured with a Key Vault located in the same region. 
az keyvault create \
    --resource-group myResourceGroup \
    --name mykevault \
    --location chinanorth \
    --enabled-for-deployment true \
    --enabled-for-disk-encryption true \
    --enabled-for-template-deployment true

# Add an access policy to the Key Vault to allow access by the Batch Service.
az keyvault set-policy \
    --resource-group myResourceGroup \
    --name mykevault \
    --spn ddbf3205-c6bd-46ae-8127-60eb93363864 \
    --key-permissions all \
    --secret-permissions all

# Create the Batch account, referencing the Key Vault either by name (if they
# exist in the same resource group) or by its full resource ID.
az batch account create \
    --resource-group myResourceGroup \
    --name mybatchaccount \
    --location chinanorth \
    --keyvault mykevault

# Authenticate directly against the account for further CLI interaction.
# Batch accounts that allocate pools in the user's subscription must be
# authenticated via an Azure Active Directory token.
az batch account login -g myResourceGroup -n mybatchaccount

```

## <a name="clean-up-deployment"></a>清理部署

运行以下命令以删除资源组及其相关的所有资源。

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>脚本说明

此脚本使用以下命令。 表中的每条命令均链接到特定于命令的文档。

| Command | 说明 |
|---|---|
| [az role assignment create](https://docs.azure.cn/cli/role?view=azure-cli-latest#az-role-assignment-create) | 为用户、组或服务主体创建新的角色分配。 |
| [az group create](https://docs.azure.cn/cli/group?view=azure-cli-latest#az-group-create) | 创建用于存储所有资源的资源组。 |
| [az keyvault create](https://docs.azure.cn/cli/keyvault?view=azure-cli-latest#az-keyvault-create) | 创建密钥保管库。 |
| [az keyvault set-policy](https://docs.azure.cn/cli/keyvault?view=azure-cli-latest#az-keyvault-set-policy) | 更新指定 Key Vault 的安全策略。 |
| [az batch account create](https://docs.azure.cn/cli/batch/account?view=azure-cli-latest#az-batch-account-create) | 创建批处理帐户。  |
| [az batch account login](https://docs.azure.cn/cli/batch/account?view=azure-cli-latest#az-batch-account-login) | 针对指定的批处理帐户进行身份验证，以便进一步进行 CLI 交互。  |
| [az group delete](https://docs.azure.cn/cli/group?view=azure-cli-latest#az-group-delete) | 删除资源组，包括所有嵌套的资源。 |

## <a name="next-steps"></a>后续步骤

有关 Azure CLI 的详细信息，请参阅 [Azure CLI 文档](https://docs.azure.cn/cli/index?view=azure-cli-latest)。

<!-- Update_Description: update meta properties, wording update, update link -->