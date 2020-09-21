---
author: msmbaldwin
ms.service: key-vault
ms.topic: include
origin.date: 07/20/2020
ms.date: 09/16/2020
ms.author: v-tawe
ms.openlocfilehash: 76caa54b5bd53ec3c9d64118e9301b596e2cfeb5
ms.sourcegitcommit: 39410f3ed7bdeafa1099ba5e9ec314b4255766df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2020
ms.locfileid: "90678526"
---
本快速入门使用预先创建的 Azure Key Vault。 可以遵循 [Azure CLI 快速入门](/key-vault/general/quick-create-cli)、[Azure PowerShell 快速入门](/key-vault/general/quick-create-powershell)或 [Azure 门户快速入门](/key-vault/general/quick-create-portal)中的步骤创建 Key Vault。 

或者，只需运行以下 Azure CLI 或 Azure PowerShell 命令。

> [!Important]
> 每个密钥保管库必须具有唯一的名称。 在以下示例中，将 <your-unique-keyvault-name> 替换为密钥保管库的名称。

```azurecli
az group create --name "myResourceGroup" -l "ChinaEast"

az keyvault create --name "<your-unique-keyvault-name>" -g "myResourceGroup"
```

```azurepowershell
New-AzResourceGroup -Name myResourceGroup -Location ChinaEast

New-AzKeyVault -Name "<your-unique-keyvault-name>" -ResourceGroupName "myResourceGroup" -Location "ChinaEast"
```