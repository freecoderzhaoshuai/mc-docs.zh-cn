---
title: .replace extents - Azure 数据资源管理器
description: 本文介绍 Azure 数据资源管理器中的 replace extents 命令。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: rkarlin
ms.service: data-explorer
ms.topic: reference
origin.date: 07/02/2020
ms.date: 08/18/2020
ms.openlocfilehash: a737d69d935549f38364e816186f1aef8b26ee42
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88556468"
---
# <a name="replace-extents"></a>.replace 盘区

此命令在特定数据库的上下文中运行。
它将指定的区从其源表移至目标表，然后从目标表中删除指定的区。
所有删除和移动操作都在单个事务中完成。

需要源表和目标表的[表管理员权限](../management/access-control/role-based-authorization.md)。

> [!NOTE]
> 在 Kusto 中，数据分片被称为“盘区”，所有命令都将“extent”或“extents”作为同义词使用。
> 若要详细了解区，请参阅[区（数据分片）概述](extents-overview.md)。

## <a name="syntax"></a>语法

`.replace` [`async`] `extents` `in` `table` *DestinationTableName* `<| 
{`*查询要从表中删除的盘区*`},{`*查询要移动到表中的盘区*`}`

* `async`（可选）：以异步方式执行该命令。
    * 返回操作 ID (Guid)。
    * 可以监视操作的状态。 请使用 [.show operations](operations.md#show-operations) 命令。
    * 可以检索成功执行的结果。 请使用 [.show operation details](operations.md#show-operation-details) 命令。

若要指定应该删除或移动哪些区，请使用以下两个查询之一。
* 查询要从表中删除的区：此查询的结果指定应从目标表中删除的区 ID。
* 查询要移动到表的区：此查询的结果指定源表中应移至目标表的区 ID。

这两个查询都应返回一个包含名为“ExtentId”的列的记录集。

## <a name="restrictions"></a>限制

* 源表和目标表都必须位于上下文数据库中。
* 对要从表中删除的盘区的查询所指定的所有盘区应属于目标表。
* 源表中的所有列均应以相同的名称和数据类型存在于目标表中。

## <a name="return-output-for-sync-execution"></a>返回输出（对于同步执行）

输出参数 |类型 |说明
---|---|---
OriginalExtentId |string |源表中原始区（已移至目标表）或目标表中已被删除的区的唯一标识符。
ResultExtentId |string |已从源表移至目标表的结果区的唯一标识符 (GUID)。 如果已从目标表中删除该区，则为空。 失败时：“失败”。
详细信息 |string |包括失败详细信息（如果操作失败）。

> [!NOTE]
> 如果目标表中不存在要从表中删除的盘区的查询所返回的盘区，则该命令将失败。 如果在执行 replace 命令之前合并了盘区，则可能会发生这种情况。
> 为确保命令在缺失盘区时失败，请检查查询是否返回所需的盘区 ID。 如果表 MyOtherTable 中不存在要删除的区，下面的示例 #1 将会失败。 但是，即使要删除的区不存在，示例 #2 也会成功，因为用于执行删除操作的查询未返回任何区 ID。

## <a name="examples"></a>示例

### <a name="move-all-extents-from-two-tables"></a>移动两个表中所有的区 

从两个特定表（`MyTable1`、`MyTable2`）中将所有区移至表 `MyOtherTable`，并删除 `MyOtherTable` 中标有 `drop-by:MyTag` 的所有区：

```kusto
.replace extents in table MyOtherTable <|
    {
        .show table MyOtherTable extents where tags has 'drop-by:MyTag'
    },
    {
        .show tables (MyTable1,MyTable2) extents
    }
```

#### <a name="sample-output"></a>示例输出

|OriginalExtentId |ResultExtentId |详细信息
|---|---|---
|e133f050-a1e2-4dad-8552-1f5cf47cab69 |0d96ab2d-9dd2-4d2c-a45e-b24c65aa6687| 
|cdbeb35b-87ea-499f-b545-defbae091b57 |a90a303c-8a14-4207-8f35-d8ea94ca45be| 
|4fcb4598-9a31-4614-903c-0c67c286da8c |97aafea1-59ff-4312-b06b-08f42187872f| 
|2dfdef64-62a3-4950-a130-96b5b1083b5a |0fb7f3da-5e28-4f09-a000-e62eb41592df| 

### <a name="move-all-extents-from-one-table-to-another-drop-specific-extent"></a>将一个表中所有的区移至另一个表，删除特定区

从一个特定表 (`MyTable1`) 中将所有区移至表 `MyOtherTable`，并删除 `MyOtherTable` 中的特定区（按其 ID）：

```kusto
.replace extents in table MyOtherTable <|
    {
        print ExtentId = "2cca5844-8f0d-454e-bdad-299e978be5df"
    },
    {
        .show table MyTable1 extents 
    }
```

```kusto
.replace extents in table MyOtherTable  <|
    {
        .show table MyOtherTable extents
        | where ExtentId == guid(2cca5844-8f0d-454e-bdad-299e978be5df) 
    },
    {
        .show table MyTable1 extents 
    }
```

### <a name="implement-an-idempotent-logic"></a>实现幂等逻辑

实现幂等逻辑，以便 Kusto 仅在有区要从表 `t_source` 移至表 `t_dest` 的情况下才从表 `t_dest` 中删除区：

```kusto
.replace async extents in table t_dest <|
{
    let any_extents_to_move = toscalar( 
        t_source
        | where extent_tags() has 'drop-by:blue'
        | summarize count() > 0
    );
    let extents_to_drop =
        t_dest
        | where any_extents_to_move and extent_tags() has 'drop-by:blue'
        | summarize by ExtentId = extent_id()
    ;
    extents_to_drop
},
{
    let extents_to_move = 
        t_source
        | where extent_tags() has 'drop-by:blue'
        | summarize by ExtentId = extent_id()
    ;
    extents_to_move
}
```
