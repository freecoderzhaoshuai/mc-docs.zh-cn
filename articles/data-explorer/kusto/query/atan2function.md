---
title: atan2() - Azure 数据资源管理器 | Microsoft Docs
description: 本文介绍 Azure 数据资源管理器中的 atan2()。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: rkarlin
ms.service: data-explorer
ms.topic: reference
origin.date: 02/13/2020
ms.date: 08/18/2020
ms.openlocfilehash: dd908834e0f941ada3aff433a1ce5d165c95becf
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88515769"
---
# <a name="atan2"></a>atan2()

计算正 x 轴与从原点到点 (y, x) 的射线之间的角度（以弧度表示）。

## <a name="syntax"></a>语法

`atan2(`*y*`,`*x*`)`

## <a name="arguments"></a>参数

* x：X 坐标（实数）。
* y：Y 坐标（实数）。

## <a name="returns"></a>返回

* 正 x 轴与从原点到点 (y, x) 的射线之间的角度（以弧度表示）。

## <a name="examples"></a>示例

```kusto
print atan2_0 = atan2(1,1) // Pi / 4 radians (45 degrees)
| extend atan2_1 = atan2(0,-1) // Pi radians (180 degrees)
| extend atan2_2 = atan2(-1,0) // - Pi / 2 radians (-90 degrees)
```

|atan2_0|atan2_1|atan2_2|
|---|---|---|
|0.785398163397448|3.14159265358979|-1.5707963267949|