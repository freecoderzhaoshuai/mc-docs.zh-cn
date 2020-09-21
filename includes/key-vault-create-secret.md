---
author: msmbaldwin
ms.service: key-vault
ms.topic: include
origin.date: 07/20/2020
ms.date: 09/16/2020
ms.author: v-tawe
ms.openlocfilehash: 7176472b145e57c55d8669b7238bad8e9b278597
ms.sourcegitcommit: 39410f3ed7bdeafa1099ba5e9ec314b4255766df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2020
ms.locfileid: "90678533"
---
让我们创建一个名为 mySecret 的机密，其值为 Success!。 机密可以是密码、SQL 连接字符串，或者需要安全保存的、可供应用程序使用的其他任何信息。 

若要将机密添加到新创建的 Key Vault，请使用 Azure CLI [az keyvault secret set](/cli/keyvault/secret?view=azure-cli-latest#az-keyvault-secret-set) 命令：

```azurecli
az keyvault secret set --vault-name "<your-unique-keyvault-name>" --name "mySecret" --value "Success!"
```