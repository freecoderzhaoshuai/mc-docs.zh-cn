---
title: .show 盘区 - Azure 数据资源管理器
description: 本文介绍 Azure 数据资源管理器中的 show 盘区命令。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: rkarlin
ms.service: data-explorer
ms.topic: reference
origin.date: 07/02/2020
ms.date: 08/18/2020
ms.openlocfilehash: 000a76e388b7f5199d881b6587f478ccab5391c6
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88556526"
---
# <a name="show-extents"></a>.show 盘区

从指定的数据库或表中显示盘区。

> [!NOTE]
> 在 Kusto 中，数据分片被称为“盘区”，所有命令都将“extent”或“extents”作为同义词使用。
> 若要详细了解盘区，请参阅[盘区（数据分片）概述](extents-overview.md)。

## <a name="cluster-level"></a>群集级别

`.show` `cluster` `extents` [`hot`]

显示有关群集中存在的盘区（数据分片）的信息。
如果指定了 `hot` - 仅显示应位于热缓存中的盘区。

## <a name="database-level"></a>数据库级别

`.show` `database` *DatabaseName* `extents` [`(`*ExtentId1*`,`...`,`*ExtentIdN*`)`] [`hot`] [`where` `tags` (`has`|`contains`|`!has`|`!contains`) *Tag1* [`and` `tags` (`has`|`contains`|`!has`|`!contains`) *Tag2*...]]

显示有关指定数据库中存在的盘区（数据分片）的信息。
如果指定了 `hot` - 仅显示应位于热缓存中的盘区。

## <a name="table-level"></a>表级别

`.show` `table` *TableName* `extents` [`(`*ExtentId1*`,`...`,`*ExtentIdN*`)`] [`hot`] [`where` `tags` (`has`|`contains`|`!has`|`!contains`) *Tag1* [`and` `tags` (`has`|`contains`|`!has`|`!contains`) *Tag2*...]]

`.show` `tables` `(`*TableName1*`,`...`,`*TableNameN*`)` `extents` [`(`*ExtentId1*`,`...`,`*ExtentIdN*`)`] [`hot`] [`where` `tags` (`has`|`contains`|`!has`|`!contains`) *Tag1* [`and` `tags` (`has`|`contains`|`!has`|`!contains`) *Tag2*...]]

显示有关指定表中存在的盘区（数据分片）的信息。 数据库取自命令的上下文。
如果指定了 `hot`则仅显示应位于热缓存中的盘区。

## <a name="notes"></a>备注

* 使用数据库或表级别命令比筛选（添加 `| where DatabaseName == '...' and TableName == '...'`）群集级别命令的结果要快得多。
* 如果提供了盘区 ID 的可选列表，则返回的数据集仅限于这些盘区。
    * 此方法比筛选（将 `| where ExtentId in(...)` 添加到）“bare”命令的结果要快得多。
* 如果指定了 `tags` 筛选器：
    * 返回的列表仅限于标记集合遵循所有提供的标记筛选条件的盘区。
    * 此方法比筛选（将 `| where Tags has '...' and Tags contains '...'` 添加到）“bare”命令的结果要快得多。
    * `has` 筛选器是相等性筛选器。 将筛选出未使用任何指定标记标记的盘区。
    * `!has` 筛选器是相等负筛选器。 将筛选出使用任何指定标记标记的盘区。
    * `contains` 筛选器是不区分大小写的子字符串筛选器。 将筛选出未将指定字符串作为其任何标记的子字符串的盘区。
    * `!contains` 筛选器是不区分大小写的子字符串负筛选器。 将筛选出其所带的任何标记的包含指定字符串的盘区。
  
## <a name="output-parameters"></a>输出参数

|输出参数 |类型 |说明 |
|---|---|---|
|ExtentId |Guid |盘区 ID 
|DatabaseName |String |盘区所属的数据库
|TableName |字符串 |盘区所属的表
|MaxCreatedOn |DateTime |创建盘区时的日期时间。 对于合并的盘区，则是源盘区中创建时间的最大值
|OriginalSize |Double |盘区数据的原始大小（以字节为单位）
|ExtentSize |Double |内存中的盘区大小（已压缩 + 索引）
|CompressedSize |Double |内存中盘区数据的压缩大小
|IndexSize |Double |盘区数据的索引大小
|块 |Long |盘区中的数据块数
|段数 |Long |盘区中的数据段数
|AssignedDataNodes |String | 已弃用（空字符串）
|LoadedDataNodes |String |已弃用（空字符串）
|ExtentContainerId |String | 盘区所在的盘区容器的 ID
|RowCount |Long |盘区中的行数
|MinCreatedOn |DateTime |创建盘区时的日期时间。 对于合并的盘区，则是源盘区中创建时间的最小值
|Tags|String|为盘区定义的标记（如果有）
 
## <a name="examples"></a>示例

### <a name="tagged-extent"></a>标记的盘区

表 `T` 中的盘区 `E` 用标记 `aaa`、`BBB` 和 `ccc` 进行标记。

* 此查询将返回 `E`：
    
   ```kusto
    .show table T extents where tags has 'aaa' and tags contains 'bb'
   ```
   
* 此查询不会返回 `E`，因为它未标记 `aa`：
    
   ```kusto
    .show table T extents where tags has 'aa' and tags contains 'bb'
   ```
    
* 此查询将返回 `E`：
    
   ```kusto
    .show table T extents where tags contains 'aaa' and tags contains 'bb' 
   ```

### <a name="show-volume-of-extents-created"></a>显示创建的盘区量

显示每小时在特定数据库中创建的盘区量

```kusto 
.show database MyDatabase extents | summarize count(ExtentId) by MaxCreatedOn bin=time(1h) | render timechart  
```

### <a name="show-volume-of-data-arriving-by-table-per-hour"></a>显示每个表每小时到达的数据量

```kusto 
.show database MyDatabase extents  
| summarize sum(OriginalSize) by TableName, MaxCreatedOn bin=time(1h)  
| render timechart
```

### <a name="show-data-size-distribution-by-table"></a>显示每个表的数据大小分布

```kusto 
.show database MyDatabase extents | summarize sum(OriginalSize) by TableName
```

### <a name="show-all-extents-in-the-database-named-gamesdb"></a>显示名为“GamesDB”的数据库中的所有盘区

```kusto 
.show database GamesDB extents
```

### <a name="show-all-extents-in-the-table-named-games"></a>显示名为“Games”的表中的所有盘区

```kusto 
.show table Games extents
```

### <a name="show-all-extents-in-specific-tables"></a>显示特定表中的所有盘区

显示名为“TaggingGames1”和“TaggingGames2”并标记为“tag1”和“tag2”的表中的所有盘区

```kusto 
.show tables (TaggingGames1,TaggingGames2) extents where tags has 'tag1' and tags has 'tag2'
```
