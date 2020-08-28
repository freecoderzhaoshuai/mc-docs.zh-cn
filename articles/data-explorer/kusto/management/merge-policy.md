---
title: 合并策略管理 - Azure 数据资源管理器 | Microsoft Docs
description: 本文介绍 Azure 数据资源管理器中的合并策略管理。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: rkarlin
ms.service: data-explorer
ms.topic: reference
origin.date: 02/13/2020
ms.date: 08/18/2020
ms.openlocfilehash: 5ceab6c8a0c553d0e7ec372a29550036ff3e3793
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88515650"
---
# <a name="merge-policy-command"></a>合并策略命令

## <a name="show-policy"></a>显示策略

```kusto
.show table [table_name] policy merge

.show table * policy merge

.show database [database_name] policy merge

.show database * policy merge
```

显示数据库或表的当前合并策略。
如果给定名称为“*”，则显示给定实体类型（数据库或表）的所有策略。

### <a name="output"></a>输出

|策略名称 | 实体名称 | 策略 | 子实体 | 实体类型
|---|---|---|---|---
|ExtentsMergePolicy | 数据库/表名称 | 一个表示策略的 JSON 格式字符串 | 表列表（对于数据库）|数据库 &#124; 表

## <a name="alter-policy"></a>更改策略

### <a name="examples"></a>示例

#### <a name="1-setting-all-properties-of-the-policy-explicitly-at-table-level"></a>1.在表级别显式设置策略的所有属性：

```kusto
.alter table [table_name] policy merge 
@'{'
    '"ExtentSizeTargetInMb": 1024,'
    '"OriginalSizeInMbUpperBoundForRebuild": 2048,'
    '"OriginalSizeInMbUpperBoundForMerge": 4096,'
    '"RowCountUpperBoundForRebuild": 750000,'
    '"RowCountUpperBoundForMerge": 0,'
    '"MaxExtentsToMerge": 100,'
    '"LoopPeriod": "01:00:00",'
    '"MaxRangeInHours": 8,'
    '"AllowRebuild": true,'
    '"AllowMerge": true '
'}'
```

#### <a name="2-setting-all-properties-of-the-policy-explicitly-at-database-level"></a>2.在数据库级别显式设置策略的所有属性：

```kusto
.alter database [database_name] policy merge 
@'{'
    '"ExtentSizeTargetInMb": 1024,'
    '"OriginalSizeInMbUpperBoundForRebuild": 2048,'
    '"OriginalSizeInMbUpperBoundForMerge": 4096,'
    '"RowCountUpperBoundForRebuild": 750000,'
    '"RowCountUpperBoundForMerge": 0,'
    '"MaxExtentsToMerge": 100,'
    '"LoopPeriod": "01:00:00",'
    '"MaxRangeInHours": 8,'
    '"AllowRebuild": true,'
    '"AllowMerge": true'
'}'
```

#### <a name="3-setting-the-default-merge-policy-at-database-level"></a>3.在数据库级别设置默认合并策略：

```kusto
.alter database [database_name] policy merge '{}'
```

#### <a name="4-altering-a-single-property-of-the-policy-at-database-level-keeping-all-other-properties-as-is"></a>4.在数据库级别更改策略的单个属性，按原样保留所有其他属性：

```kusto
.alter-merge database [database_name] policy merge
@'{'
    '"ExtentSizeTargetInMb": 1024'
'}'
```

#### <a name="5-altering-a-single-property-of-the-policy-at-table-level-keeping-all-other-properties-as-is"></a>5.在表级别更改策略的单个属性，按原样保留所有其他属性：

```kusto
.alter-merge table [table_name] policy merge
@'{'
    '"RowCountUpperBoundForRebuild": 750000'
'}'
```

以上所有示例都返回实体（指定为限定名称的数据库或表）的已更新盘区合并策略作为其输出。

对策略的更改可能需要长达 1 小时的时间才能生效。

## <a name="delete-policy-of-merge"></a>删除合并策略

```kusto
.delete table [table_name] policy merge

.delete database [database_name] policy merge

```

此命令删除给定实体的当前合并策略。
