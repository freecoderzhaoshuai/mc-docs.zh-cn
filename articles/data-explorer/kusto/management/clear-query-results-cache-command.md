---
title: 清除查询结果缓存 - Azure 数据资源管理器
description: 本文介绍用于在 Azure 数据资源管理器中清除缓存的数据库架构的管理命令。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: amitof
ms.service: data-explorer
ms.topic: reference
origin.date: 06/16/2020
ms.date: 08/18/2020
ms.openlocfilehash: 54aa99a1b4ae56d07d56b27798ef65344d5aa94a
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88515917"
---
# <a name="clear-query-results-cache"></a>清除查询结果缓存

清除针对上下文数据库所获得的所有[缓存的查询结果](../query/query-results-cache.md)。

**语法**

`.clear` `database` `cache` `query_results`

**返回**

此命令返回包含以下列的表：

|列    |类型    |说明
|---|---|---
|NodeId|`string`|群集节点的标识符。
|计数|`long`|节点删除的项数。

**示例**

```kusto
.clear database cache queryresults
```

|NodeId|项|
|---|---|
|Node1|42
|Node2|0
