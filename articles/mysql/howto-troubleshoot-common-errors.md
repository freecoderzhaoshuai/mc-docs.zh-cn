---
title: 排查常见错误 - Azure Database for MySQL
description: 了解如何排查 Azure Database for MySQL 服务的新用户遇到的常见迁移错误
author: WenJason
ms.service: mysql
ms.author: v-jay
ms.custom: mvc
ms.topic: overview
origin.date: 8/20/2020
ms.date: 09/14/2020
ms.openlocfilehash: ebd12490ee79b3642c53f30df0161e267343e799
ms.sourcegitcommit: 5116a603d3cac3cbc2e2370ff857f871f8f51a5f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89512978"
---
# <a name="common-errors"></a>常见错误

Azure Database for MySQL 是由 MySQL 社区版本提供支持的完全托管的服务。 托管服务环境中的 MySQL 体验可能与在你自己的环境中运行 MySQL 时不同。 在本文中，你将了解用户首次迁移到 Azure Database for MySQL 服务或在该服务上开发时可能遇到的一些常见错误。

## <a name="errors-due-to-lack-of-super-privilege-and-dba-role"></a>由于缺少 SUPER 权限和 DBA 角色而引发的错误

该服务不支持 SUPER 权限和 DBA 角色。 因此，你可能会遇到下列的一些常见错误：

#### <a name="error-1419-you-do-not-have-the-super-privilege-and-binary-logging-is-enabled-you-might-want-to-use-the-less-safe-log_bin_trust_function_creators-variable"></a>错误 1419：你没有 SUPER 权限且二进制文件日志记录已启用（你可能需要使用安全性更低的 log_bin_trust_function_creators 变量）

创建函数（如下所示触发）或导入架构时，可能会出现上述错误。 诸如 CREATE FUNCTION 或 CREATE TRIGGER 这样的 DDL 语句会写入二进制日志，因此次要副本可执行它们。 副本 SQL 线程具有完全权限，你可利用它来提升权限。 为了帮助启用了二进制日志记录的服务器防范这一危险，除了所需的惯例 CREATE ROUTINE 权限外，MySQL 引擎还要求存储函数创建者必须具有 SUPER 权限。 

```sql
CREATE FUNCTION f1(i INT)
RETURNS INT
DETERMINISTIC
READS SQL DATA
BEGIN
  RETURN i;
END;
```

**解决方法**：要解决此错误，请从门户中的[服务器参数](howto-server-parameters.md)边栏选项卡将 log_bin_trust_function_creators 设置为 1，执行 DDL 语句或导入架构来创建所需的对象，并在创建后将 log_bin_trust_function_creators parameter 参数恢复到它之前的值。

#### <a name="error-1227-42000-at-line-101-access-denied-you-need-at-least-one-of-the-super-privileges-for-this-operation-operation-failed-with-exitcode-1"></a>第 101 行出现错误 1227 (42000)：访问被拒绝；需要（至少一项）SUPER 权限才能执行此操作。 操作失败，退出代码为 1

导入转储文件或创建包含[定义程序](https://dev.mysql.com/doc/refman/5.7/en/create-procedure.html)的过程时，可能会出现上述错误。 

**解决方法**：要解决此错误，管理员用户可通过运行 GRANT 命令来授予创建或执行过程的权限，如下例所示：

```sql
GRANT CREATE ROUTINE ON mydb.* TO 'someuser'@'somehost';
GRANT EXECUTE ON PROCEDURE mydb.myproc TO 'someuser'@'somehost';
```
或者，可将定义程序替换为正在运行导入过程的管理员用户的姓名，如下所示。

```sql
DELIMITER;;
/*!50003 CREATE*/ /*!50017 DEFINER=`root`@`127.0.0.1`*/ /*!50003
DELIMITER;;

/* Modified to */

DELIMITER ;;
/*!50003 CREATE*/ /*!50017 DEFINER=`AdminUserName`@`ServerName`*/ /*!50003
DELIMITER ;
```

