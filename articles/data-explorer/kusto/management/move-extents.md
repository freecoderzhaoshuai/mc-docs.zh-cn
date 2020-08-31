---
title: .move extents - Azure 数据资源管理器
description: 本文介绍 Azure 数据资源管理器中的 move extents 命令。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: rkarlin
ms.service: data-explorer
ms.topic: reference
origin.date: 07/02/2020
ms.date: 08/18/2020
ms.openlocfilehash: 1f2e1651262f8769e11abdf48e05548246b2669e
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88556469"
---
# <a name="move-extents"></a>.move 盘区

此命令在特定数据库的上下文中运行。 它将指定的区从源表移到目标表。

此命令需要源表和目标表的[表管理员权限](../management/access-control/role-based-authorization.md)。

> [!NOTE]
> 在 Kusto 中，数据分片被称为“盘区”，所有命令都将“extent”或“extents”作为同义词使用。
> 若要详细了解区，请参阅[区（数据分片）概述](extents-overview.md)。

## <a name="syntax"></a>语法

`.move` [`async`] `extents` `all` `from` `table` *SourceTableName* `to` `table` *DestinationTableName*

`.move` [`async`] `extents` `(` *GUID1* [`,` *GUID2* ...] `)` `from` `table` *SourceTableName* `to` `table` *DestinationTableName* 

`.move` [`async`] `extents` `to` `table` *DestinationTableName* <| *query*

`async`（可选）。 以异步方式执行命令。 
   * 返回操作 ID (Guid)。
   * 可以监视操作的状态。 使用 [.show operations](operations.md#show-operations) 命令。
   * 可以检索成功执行的结果。 使用 [.show operation details](operations.md#show-operation-details) 命令。

有三种方法可以指定要移动的盘区：
* 移动特定表的所有区。
* 在源表中显式指定区 ID。
* 提供一个查询，其结果指定源表中的区 ID。

## <a name="restrictions"></a>限制

* 源表和目标表都必须位于上下文数据库中。
* 源表中的所有列均应以相同的名称和数据类型存在于目标表中。

## <a name="specify-extents-with-a-query"></a>使用查询指定区

```kusto
.move extents to table TableName <| ...query...
```

使用 Kusto 查询指定区，该查询会返回一个包含名为“ExtentId”的列的记录集。

## <a name="return-output-for-sync-execution"></a>返回输出（对于同步执行）

输出参数 |类型 |说明
---|---|---
OriginalExtentId |string |源表中原始盘区的唯一标识符 (GUID)，该标识符已移至目标表。
ResultExtentId |string |已从源表移至目标表的结果区的唯一标识符 (GUID)。 失败时 -“已失败”。
详细信息 |string |包括失败详细信息（如果操作失败）。

## <a name="examples"></a>示例

### <a name="move-all-extents"></a>移动所有区 

将表 `MyTable` 中的所有区都移到表 `MyOtherTable`：

```kusto
.move extents all from table MyTable to table MyOtherTable
```

### <a name="move-two-specific-extents"></a>移动两个特定区 

将两个特定区（通过其区 ID）从表 `MyTable` 移到表 `MyOtherTable`：

```kusto
.move extents (AE6CD250-BE62-4978-90F2-5CB7A10D16D7,399F9254-4751-49E3-8192-C1CA78020706) from table MyTable to table MyOtherTable
```

### <a name="move-all-extents-from-specific-tables"></a>移动特定表中的所有区 

将特定表（`MyTable1`、`MyTable2`）中的所有区移到表 `MyOtherTable`：

```kusto
.move extents to table MyOtherTable <| .show tables (MyTable1,MyTable2) extents
```

## <a name="sample-output"></a>示例输出

|OriginalExtentId |ResultExtentId| 详细信息
|---|---|---
|e133f050-a1e2-4dad-8552-1f5cf47cab69 |0d96ab2d-9dd2-4d2c-a45e-b24c65aa6687| 
|cdbeb35b-87ea-499f-b545-defbae091b57 |a90a303c-8a14-4207-8f35-d8ea94ca45be| 
|4fcb4598-9a31-4614-903c-0c67c286da8c |97aafea1-59ff-4312-b06b-08f42187872f| 
|2dfdef64-62a3-4950-a130-96b5b1083b5a |0fb7f3da-5e28-4f09-a000-e62eb41592df| 
