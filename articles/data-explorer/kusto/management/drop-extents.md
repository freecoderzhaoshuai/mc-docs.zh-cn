---
title: .drop extents - Azure 数据资源管理器
description: 本文介绍 Azure 数据资源管理器中的 drop extents 命令。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: rkarlin
ms.service: data-explorer
ms.topic: reference
origin.date: 07/02/2020
ms.date: 08/18/2020
ms.openlocfilehash: 233bb95636939feaa97767f622dc42e7716f3c1e
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88556503"
---
# <a name="drop-extents"></a>.drop 盘区

从指定的数据库或表中删除区。

该命令有多个变体：在一个变体中，要删除的区由 Kusto 查询指定。 在其他变体中，区是通过使用下面所述的迷你语言指定的。

对于每个包含由提供的查询所返回的区的表，需要[表管理员权限](../management/access-control/role-based-authorization.md)。

> [!NOTE]
> 在 Kusto 中，数据分片被称为“盘区”，所有命令都将“extent”或“extents”作为同义词使用。
> 若要详细了解区，请参阅[区（数据分片）概述](extents-overview.md)。

## <a name="drop-extents-with-a-query"></a>使用查询删除区

删除使用 Kusto 查询指定的区。
将会返回一个包含名为“ExtentId”的列的记录集。

如果使用 `whatif`，则只会报告它们，而不会实际删除。

### <a name="syntax"></a>语法

`.drop` `extents` [`whatif`] <| *query*

## <a name="drop-a-specific-extent"></a>删除特定区

如果已指定表名，则需要[表管理员权限](../management/access-control/role-based-authorization.md)。

如果未指定表名，则需要[数据库管理员权限](../management/access-control/role-based-authorization.md)。

### <a name="syntax"></a>语法

`.drop` `extent` *ExtentId* [`from` *TableName*]

## <a name="drop-specific-multiple-extents"></a>删除特定的多个区

如果已指定表名，则需要[表管理员权限](../management/access-control/role-based-authorization.md)。

如果未指定表名，则需要[数据库管理员权限](../management/access-control/role-based-authorization.md)。

### <a name="syntax"></a>语法

`.drop` `extents` `(`*ExtentId1*`,`...*ExtentIdN*`)` [`from` *TableName*]

## <a name="drop-extents-by-specified-properties"></a>按指定的属性删除区

此命令支持仿真模式，该模式生成输出，就好像该命令已运行，但实际上并没有执行。 请使用 `.drop-pretend`，而不是 `.drop`。

如果已指定表名，则需要[表管理员权限](../management/access-control/role-based-authorization.md)。

如果未指定表名，则需要[数据库管理员权限](../management/access-control/role-based-authorization.md)。

### <a name="syntax"></a>语法

`.drop` `extents` [`older` *N* (`days` | `hours`)] `from` (*TableName* | `all` `tables`) [`trim` `by` (`extentsize` | `datasize`) *N* (`MB` | `GB` | `bytes`)] [`limit` *LimitCount*]

* `older`：仅会删除早于 N 天/小时的盘区。
* `trim`：该操作将修整数据库中的数据，直到区总数与所需大小 (MaxSize) 相匹配。
* `limit`：该操作将应用于前 LimitCount 个区。

## <a name="examples"></a>示例

### <a name="remove-all-extents-by-time-created"></a>按创建时间删除所有区

从数据库 `MyDatabase` 的所有表中删除创建时间早于 10 天前的所有区

```kusto
.drop extents <| .show database MyDatabase extents | where CreatedOn < now() - time(10d)
```

### <a name="remove-some-extents-by-time-created"></a>按创建时间删除某些区

删除表 `Table1` 和 `Table2` 中创建时间早于 10 天前的所有区

```kusto
.drop extents older 10 days from tables (Table1, Table2)
```

### <a name="emulation-mode-show-which-extents-would-be-removed-by-the-command"></a>仿真模式：显示哪些区会由该命令删除

>[!NOTE]
>区 ID 参数不适用于此命令。

```kusto
.drop-pretend extents older 10 days from all tables
```

### <a name="remove-all-extents-from-testtable"></a>从“TestTable”中删除所有区

```kusto
.drop extents from TestTable
```

## <a name="return-output"></a>返回输出

|输出参数 |类型 |说明 
|---|---|---
|ExtentId |String |由于该命令而删除的 ExtentId
|TableName |字符串 |盘区所属的表名  
|CreatedOn |DateTime |时间戳，它保留有关最初创建该区的时间的信息
 
## <a name="sample-output"></a>示例输出

|区 ID |表名称 |创建时间 
|---|---|---
|43c6e03f-1713-4ca7-a52a-5db8a4e8b87d |TestTable |2015-01-12 12:48:49.4298178
