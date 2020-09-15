---
title: Azure CLI：将 Azure SQL 数据库中的数据库复制到新服务器
description: 用于将 Azure SQL 数据库中的数据库复制到新服务器的 Azure CLI 示例脚本
services: sql-database
ms.service: sql-database
ms.subservice: data-movement
ms.custom: devx-track-azurecli
ms.devlang: azurecli
ms.topic: sample
author: WenJason
ms.author: v-jay
ms.reviewer: carlrab
origin.date: 03/12/2019
ms.date: 09/14/2020
ms.openlocfilehash: 2f0caa478d5eaadd4b2dd70b0b1fe6324c071085
ms.sourcegitcommit: d5cdaec8050631bb59419508d0470cb44868be1a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90014244"
---
# <a name="use-cli-to-copy-a-database-in-azure-sql-database-to-a-new-server"></a>使用 CLI 将 Azure SQL 数据库中的数据库复制到新服务器

以下 Azure CLI 脚本示例在新服务器中创建现有数据库的副本。

本文要求运行 Azure CLI 2.0 或更高版本。 运行 `az --version` 即可查找版本。 如需进行安装或升级，请参阅[安装 Azure CLI](/cli/install-azure-cli)。

## <a name="sample-script"></a>示例脚本

### <a name="sign-in-to-azure"></a>登录 Azure

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

```azurecli
$subscription = "<subscriptionId>" # add subscription here

az account set -s $subscription # ...or use 'az login'
```

### <a name="run-the-script"></a>运行脚本

```azurecli
#!/bin/bash
location="China East"
randomIdentifier=random123

resource="resource-$randomIdentifier"
server="server-$randomIdentifier"
database="database-$randomIdentifier"

targetResource="targetResource-$randomIdentifier"
targetLocation="China North"
targetServer="targetServer-$randomIdentifier"
targetDatabase="targetDatabase-$randomIdentifier"

login="sampleLogin"
password="samplePassword123!"

echo "Using resource group $resourceGroup with login: $login, password: $password..."

echo "Creating $resource and $targetResource..."
az group create --name $resource --location "$location"
az group create --name $targetResource --location "$targetLocation"

echo "Creating $server in $location and $targetServer in $targetLocation..."
az sql server create --name $server --resource-group $resource --location "$location" --admin-user $login --admin-password $password
az sql server create --name $targetServer --resource-group $targetResource --location "$targetLocation" --admin-user $login --admin-password $password

echo "Creating $database on $server..."
az sql db create --name $database --resource-group $resource --server $server --service-objective S0

echo "Copying $database on $server to $targetDatabase on $targetServer..."
az sql db copy --dest-name $targetDatabase --dest-resource-group $targetResource --dest-server $targetServer --name $database --resource-group $resource --server $server
```

### <a name="clean-up-deployment"></a>清理部署

使用以下命令删除资源组及其相关的所有资源。

```azurecli
az group delete --name $resource
az group delete --name $targetResource
```

## <a name="sample-reference"></a>示例参考

此脚本使用以下命令。 表中的每条命令均链接到特定于命令的文档。

| Command | 描述 |
|---|---|
| [az sql db copy](/cli/sql/db#az-sql-db-copy) | 创建当前使用快照的数据库副本。 |

## <a name="next-steps"></a>后续步骤

有关 Azure CLI 的详细信息，请参阅 [Azure CLI 文档](/cli/)。

其他 SQL 数据库 CLI 脚本示例可以在 [Azure SQL 数据库文档](../../azure-sql/database/az-cli-script-samples-content-guide.md)中找到。
