---
title: 查询结果缓存命令 - Azure 数据资源管理器
description: 本文介绍了 Azure 数据资源管理器中的查询结果缓存。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: amitof
ms.service: data-explorer
ms.topic: reference
origin.date: 06/16/2020
ms.date: 08/18/2020
ms.openlocfilehash: ed0f061d2c0b41654c9a0717e8cd0f2303314a54
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88516103"
---
# <a name="query-results-cache-commands"></a>查询结果缓存命令

查询结果缓存是专用于存储查询结果的缓存。 有关详细信息，请参阅[查询结果缓存](../query/query-results-cache.md)。

**查询结果缓存命令**

Kusto 提供了两个用于缓存管理和可观测性的命令：

* [`Show cache`](show-query-results-cache-command.md)：使用此命令显示结果缓存公开的统计信息。

* [`Clear cache(rhs:string)`](clear-query-results-cache-command.md)：使用此命令可清除缓存的结果。
