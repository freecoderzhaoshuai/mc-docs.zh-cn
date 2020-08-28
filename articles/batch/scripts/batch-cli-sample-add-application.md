---
title: Azure CLI 脚本示例 - 在 Batch 中添加应用程序
description: 此示例脚本演示如何添加要与 Azure Batch 池或任务配合使用的应用程序。
ms.topic: sample
author: rockboyfor
origin.date: 01/29/2018
ms.date: 08/24/2020
ms.testscope: no
ms.testdate: 09/07/2018
ms.author: v-yeche
ms.custom: devx-track-azurecli
ms.openlocfilehash: ac914b9e98a475525a90e284b4682b2b92154c70
ms.sourcegitcommit: e633c458126612223fbf7a8853dbf19acc7f0fa5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88654927"
---
<!--Verified successfully-->
# <a name="cli-example-add-an-application-to-an-azure-batch-account"></a>CLI 示例：向 Azure Batch 帐户添加应用程序

此脚本演示如何添加要与 Azure Batch 池或任务配合使用的应用程序。 若要设置添加到 Batch 帐户的应用程序，请将可执行文件与所有依赖文件一起打包为 zip 文件。 

[!INCLUDE [azure-cli-2-azurechinacloud-environment-parameter](../../../includes/azure-cli-2-azurechinacloud-environment-parameter.md)]

如果选择在本地安装并使用 CLI，本文要求运行 Azure CLI 2.0.20 或更高版本。 运行 `az --version` 即可查找版本。 如果需要进行安装或升级，请参阅[安装 Azure CLI](https://docs.azure.cn/cli/install-azure-cli?view=azure-cli-latest)。 

## <a name="example-script"></a>示例脚本

<!--MOONCAKE: --application-name MUST MATCH [A-Za-z-]-->
<!--MOONCAKE: KEEP ALIGN WITH CHINAEAST-->
```azurecli
#!/bin/bash

# Create a resource group.
az group create --name myResourceGroup --location chinaeast

# Create a general-purpose storage account in your resource group.
az storage account create \
    --resource-group myResourceGroup \
    --name mystorageaccount \
    --location chinaeast \
    --sku Standard_LRS

# Create a Batch account.
az batch account create \
    --name mybatchaccount \
    --storage-account mystorageaccount \
    --resource-group myResourceGroup \
    --location chinaeast

# Authenticate against the account directly for further CLI interaction.
az batch account login \
    --name mybatchaccount \
    --resource-group myResourceGroup \
    --shared-key-auth

# Create a new application.
az batch application create \
    --resource-group myResourceGroup \
    --name mybatchaccount \
    --application-name "My-Application"

# An application can reference multiple application executable packages
# of different versions. The executables and any dependencies need
# to be zipped up for the package. Once uploaded, the CLI attempts
# to activate the package so that it's ready for use.
az batch application package create \
    --resource-group myResourceGroup \
    --name mybatchaccount \
    --application-name "My-Application" \
    --package-file my-application-exe.zip \
    --version-name 1.0

# Update the application to assign the newly added application
# package as the default version.
az batch application set \
    --resource-group myResourceGroup \
    --name mybatchaccount \
    --application-name "My-Application" \
    --default-version 1.0
```

## <a name="clean-up-deployment"></a>清理部署

运行以下命令以删除资源组及其相关的所有资源。

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>脚本说明

此脚本使用以下命令。
表中的每条命令均链接到特定于命令的文档。

| Command | 说明 |
|---|---|
| [az group create](https://docs.azure.cn/cli/group?view=azure-cli-latest#az-group-create) | 创建用于存储所有资源的资源组。 |
| [az storage account create](https://docs.azure.cn/cli/storage/account?view=azure-cli-latest#az-storage-account-create) | 创建存储帐户。 |
| [az batch account create](https://docs.azure.cn/cli/batch/account?view=azure-cli-latest#az-batch-account-create) | 创建批处理帐户。 |
| [az batch account login](https://docs.azure.cn/cli/batch/account?view=azure-cli-latest#az-batch-account-login) | 针对指定的批处理帐户进行身份验证，以便进一步进行 CLI 交互。  |
| [az batch application create](https://docs.azure.cn/cli/batch/application?view=azure-cli-latest#az-batch-application-create) | 创建应用程序。  |
| [az batch application package create](https://docs.azure.cn/cli/batch/application/package?view=azure-cli-latest#az-batch-application-package-create) | 将应用程序包添加到指定的应用程序。  |
| [az batch application set](https://docs.azure.cn/cli/batch/application?view=azure-cli-latest#az-batch-application-set) | 更新应用程序的属性。  |
| [az group delete](https://docs.azure.cn/cli/group?view=azure-cli-latest#az-group-delete) | 删除资源组，包括所有嵌套的资源。 |

## <a name="next-steps"></a>后续步骤

有关 Azure CLI 的详细信息，请参阅 [Azure CLI 文档](https://docs.azure.cn/cli/index?view=azure-cli-latest)。

<!-- Update_Description: update meta properties, wording update, update link -->