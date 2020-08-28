---
title: .merge 盘区 - Azure 数据资源管理器
description: 本文介绍 Azure 数据资源管理器中的 merge 盘区命令。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: rkarlin
ms.service: data-explorer
ms.topic: reference
origin.date: 07/02/2020
ms.date: 08/18/2020
ms.openlocfilehash: ffde2db4441152fcad1f805d4e38d8805b3bce91
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88556517"
---
# <a name="merge-extents"></a>.merge 盘区

该命令合并指定表中由其 ID 指示的盘区。 

> [!NOTE]
> 在 Kusto 中，数据分片被称为“盘区”，所有命令都将“extent”或“extents”作为同义词使用。
> 有关盘区的详细信息，请参阅[盘区（数据分片）概述](extents-overview.md)。

## <a name="syntax"></a>语法

`.merge` `[async | dryrun]` *TableName* `(` *GUID1* [`,` *GUID2* ...] `)` `[with(rebuild=true)]`

有两种类型的合并操作：
* “合并”，即重新构建索引
* “重新生成”，即完全重新引入数据

有三个可用选项：
* `async`：以异步方式执行命令。 
    * 返回操作 ID (Guid)。
    * 可以监视操作的状态。 将操作 ID 与 `.show operations <operation ID>` 命令一起使用。
* `dryrun`：该操作将仅列出应合并的盘区，但实际上不会合并它们。
* `with(rebuild=true)`：将重新生成这些盘区，并重新引入数据，而非合并。 将重新生成索引。

## <a name="return-output"></a>返回输出

输出参数 |类型 |说明
---|---|---
OriginalExtentId |string |源表中原始盘区的唯一标识符 (GUID)，该标识符已合并到目标盘区。
ResultExtentId |string |从源盘区创建的盘区的唯一标识符 (GUID)。 失败时：“失败”或“放弃”。
持续时间 |timespan |完成合并操作所需的时间段。

## <a name="examples"></a>示例

### <a name="rebuild-two-specific-extents-in-mytable-asynchronously"></a>重新生成 `MyTable` 中的两个特定盘区，以异步方式执行。

```kusto
.merge async MyTable (e133f050-a1e2-4dad-8552-1f5cf47cab69, 0d96ab2d-9dd2-4d2c-a45e-b24c65aa6687) with(rebuild=true)
```

### <a name="merge-two-specific-extents-in-mytable-synchronously"></a>合并 `MyTable` 中的两个特定盘区，以同步方式执行。

```kusto
.merge MyTable (12345050-a1e2-4dad-8552-1f5cf47cab69, 98765b2d-9dd2-4d2c-a45e-b24c65aa6687)
```

## <a name="notes"></a>备注

* 通常，不应手动运行 `.merge` 命令。 根据表和数据库的[合并策略](mergepolicy.md)，这些命令会在群集的后台连续自动运行。  
  * 有关将多个盘区合并为单个盘区的条件的详细信息，请参阅[合并策略](mergepolicy.md)。
* `.merge` 操作的最终状态可能为 `Abandoned`，可在使用操作 ID 运行 `.show operations` 时进行查看。 此状态表明源盘区未合并，因为某些源盘区不再存在于源表中。 发生以下情况时，会出现 `Abandoned` 状态：
   * 源盘区已在表保留过程中被删除。
   * 源盘区已移到另一个表中。
   * 已完全删除或重命名源表。
