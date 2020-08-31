---
title: anyif()（聚合函数） - Azure 数据资源管理器 | Microsoft Docs
description: 本文介绍 Azure 数据资源管理器中的 anyif()（聚合函数）。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: rkarlin
ms.service: data-explorer
ms.topic: reference
origin.date: 02/13/2020
ms.date: 08/18/2020
ms.openlocfilehash: 9104aba239ccd07f29022235916843bac31ad648
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88515786"
---
# <a name="anyif-aggregation-function"></a>anyif()（聚合函数）

为 [summarize 运算符](summarizeoperator.md)中的每个组任意选择一条记录，其谓词为“true”。 该函数返回每个此类记录的表达式值。

> [!NOTE]
> 若要根据复合组键的值获取一个列的示例值，则可使用此函数，前提是某些谓词为“true”。
> 如果存在这样的值，该函数会尝试返回非 null/非空值。

## <a name="syntax"></a>语法

`summarize` `anyif` `(` *Expr*, *Predicate* `)`

## <a name="arguments"></a>参数

* Expr：从要返回的输入中选择的每条记录的表达式。
* *谓词*：指示可考虑对哪些记录进行计算的谓词。

## <a name="returns"></a>返回

`anyif` 聚合函数返回为每条记录计算的表达式的值，这些记录是从每个 summarize 运算符的组中随机选择而来。 只能选择 Predicate 返回“true”的记录。 如果 Predicate 不返回“true”，则生成 null 值。

## <a name="examples"></a>示例

显示一个拥有 3 亿到 6 亿人口的随机大陆。

```kusto
Continents | summarize anyif(Continent, Population between (300000000 .. 600000000))
```

:::image type="content" source="images/aggfunction/any1.png" alt-text="Any 1":::
