---
title: .alter 盘区标记 - Azure 数据资源管理器
description: 本文介绍 Azure 数据资源管理器中的 alter extent 命令。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: rkarlin
ms.service: data-explorer
ms.topic: reference
origin.date: 07/02/2020
ms.date: 08/18/2020
ms.openlocfilehash: f2a2056de4a9433b59a6db6841f168e8416dff66
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88556525"
---
# <a name="alter-extent-tags"></a>.alter 盘区标记

此命令在特定数据库的上下文中运行。 它将更改查询返回的所有盘区指定的[标记](extents-overview.md#extent-tagging)。

使用 Kusto 查询指定要更改的盘区和标记，该查询将返回一个包含名为“ExtentId”的列的记录集。

需要所有涉及的表的[表管理员权限](../management/access-control/role-based-authorization.md)。

> [!NOTE]
> 在 Kusto 中，数据分片被称为“盘区”，所有命令都将“extent”或“extents”作为同义词使用。
> 有关盘区的详细信息，请参阅[盘区（数据分片）概述](extents-overview.md)。

## <a name="syntax"></a>语法

`.alter` [`async`] `extent` `tags` `(`'*Tag1*'[`,`'*Tag2*'`,`...`,`'*TagN*']`)` <| *query*

`async`（可选）：以异步方式执行命令。
   * 返回操作 ID (Guid)。 
   * 可以监视操作的状态。 使用 [.show operations](operations.md#show-operations) 命令。
   * 可以检索成功执行的结果。 使用 [.show operation details](operations.md#show-operation-details) 命令。

## <a name="restrictions"></a>限制

所有盘区都必须在上下文数据库中，并且必须属于同一个表。

## <a name="return-output"></a>返回输出

|输出参数 |类型 |说明|
|---|---|---|
|OriginalExtentId |string |原始盘区的唯一标识符 (GUID)，其标记已修改。 此盘区在操作过程中被删除。|
|ResultExtentId |string |结果盘区的唯一标识符 (GUID)，其标记已修改。 此盘区在操作过程中创建和添加。 失败时 -“已失败”。|
|ResultExtentTags |string |结果盘区的标记的集合，如果操作失败，则为“null”。|
|详细信息 |string |包括失败详细信息（如果操作失败）。|

## <a name="examples"></a>示例

### <a name="alter-tags"></a>更改标记 

将表 `MyTable` 中所有盘区的标记更改为 `MyTag`

```kusto
.alter extent tags ('MyTag') <| .show table MyTable extents
```

### <a name="alter-tags-of-all-extents"></a>更改所有盘区的标记

将表 `MyTable` 中所有标记为 `drop-by:MyTag` 的盘区的标记更改为 `drop-by:MyNewTag` 和 `MyOtherNewTag`

```kusto
.alter extent tags ('drop-by:MyNewTag','MyOtherNewTag') <| .show table MyTable extents where tags has 'drop-by:MyTag'
```

## <a name="sample-output"></a>示例输出

|OriginalExtentId |ResultExtentId | ResultExtentTags | 详细信息
|---|---|---|---
|e133f050-a1e2-4dad-8552-1f5cf47cab69 |0d96ab2d-9dd2-4d2c-a45e-b24c65aa6687 | drop-by:MyNewTag MyOtherNewTag| 
|cdbeb35b-87ea-499f-b545-defbae091b57 |a90a303c-8a14-4207-8f35-d8ea94ca45be | drop-by:MyNewTag MyOtherNewTag| 
|4fcb4598-9a31-4614-903c-0c67c286da8c |97aafea1-59ff-4312-b06b-08f42187872f | drop-by:MyNewTag MyOtherNewTag| 
|2dfdef64-62a3-4950-a130-96b5b1083b5a |0fb7f3da-5e28-4f09-a000-e62eb41592df | drop-by:MyNewTag MyOtherNewTag| 
