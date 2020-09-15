---
title: 使用 PowerShell 生成连接字符串 - Azure Database for MySQL
description: 本文提供一个 Azure PowerShell 示例，用于生成连接到 Azure Database for MySQL 所用的连接字符串。
author: WenJason
ms.author: v-jay
ms.service: mysql
ms.custom: mvc, devx-track-azurepowershell
ms.topic: quickstart
origin.date: 8/5/2020
ms.date: 09/14/2020
ms.openlocfilehash: e4140911822aab788c53536f9ac1d5f02e44238b
ms.sourcegitcommit: 5116a603d3cac3cbc2e2370ff857f871f8f51a5f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89512976"
---
# <a name="how-to-generate-an-azure-database-for-mysql-connection-string-with-powershell"></a>如何使用 PowerShell 生成 Azure Database for MySQL 连接字符串

> [!NOTE]
> 将要查看的是 Azure Database for MySQL 的新服务。 若要查看经典 MySQL Database for Azure 的文档，请访问[此页](https://docs.azure.cn/zh-cn/mysql-database-on-azure/)。

本文演示如何为 Azure Database for MySQL 服务器生成连接字符串。 可以使用连接字符串从许多不同的应用程序连接到 Azure Database for MySQL。

## <a name="requirements"></a>要求

本文使用以下指南中创建的资源作为起点：

* [快速入门：使用 PowerShell 创建 Azure Database for MySQL 服务器](quickstart-create-mysql-server-database-using-azure-powershell.md)

## <a name="get-the-connection-string"></a>获取连接字符串

`Get-AzMySqlConnectionString` cmdlet 用于生成连接字符串，以便将应用程序连接到 Azure Database for MySQL。 下面的示例从 mydemoserver 返回 PHP 客户端的连接字符串。

```azurepowershell
Get-AzMySqlConnectionString -Client PHP -Name mydemoserver -ResourceGroupName myresourcegroup
```

```Output
$con=mysqli_init();mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL); mysqli_real_connect($con, "mydemoserver.mysql.database.chinacloudapi.cn", "myadmin@mydemoserver", {your_password}, {your_database}, 3306);
```

`Client` 参数的有效值包括：

* ADO&#46;NET
* JDBC
* Node.js
* PHP
* Python
* Ruby
* WebApp

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 PowerShell 自定义 Azure Database for MySQL 服务器参数](howto-configure-server-parameters-using-powershell.md)
