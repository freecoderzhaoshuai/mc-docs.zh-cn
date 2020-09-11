---
author: cephalin
ms.service: app-service-web
ms.topic: include
origin.date: 11/21/2018
ms.author: v-biyu
ms.date: 06/17/2019
ms.openlocfilehash: 432fff08c041d2a8793158516221273d1f52add8
ms.sourcegitcommit: 9d9795f8a5b50cd5ccc19d3a2773817836446912
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "89503341"
---
## <a name="clean-up-resources"></a>清理资源

在前面的步骤中，你在资源组中创建了 Azure 资源。 如果认为将来不需要这些资源，请在 Azure CLI 中运行以下命令以删除资源组：

```azurecli
az group delete --name myResourceGroup
```

此命令可能需要花费一点时间运行。