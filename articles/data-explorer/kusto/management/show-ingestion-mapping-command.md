---
title: .show ingestion mappings - Azure 数据资源管理器
description: 本文介绍 Azure 数据资源管理器中的 .show ingestion mappings。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: rkarlin
ms.service: data-explorer
ms.topic: reference
origin.date: 02/04/2020
ms.date: 08/18/2020
ms.openlocfilehash: 6ebc7e76d6b119a4eacc331766399ddbd5b6d614
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88516117"
---
# <a name="show-ingestion-mapping"></a>.show ingestion mapping

显示引入映射（所有引入映射或按名称指定的某个引入映射）。

* `.show` `table` *TableName* `ingestion` *MappingKind*  `mappings`

* `.show` `table` *TableName* `ingestion` *MappingKind*  `mapping` *MappingName* 

显示所有映射类型的所有引入映射：

* `.show` `table` *TableName* `ingestion`  `mapping`
 
**示例** 
 
```kusto
.show table MyTable ingestion csv mapping "Mapping1" 

.show table MyTable ingestion csv mappings 

.show table MyTable ingestion mappings 
```

**示例输出**

| 名称     | 种类 | 映射     |
|----------|------|-------------|
| mapping1 | CSV  | `[{"Name":"rownumber","DataType":"int","CsvDataType":null,"Ordinal":0,"ConstValue":null},{"Name":"rowguid","DataType":"string","CsvDataType":null,"Ordinal":1,"ConstValue":null}]` |
