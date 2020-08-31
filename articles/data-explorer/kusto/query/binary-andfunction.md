---
title: binary_and() - Azure 数据资源管理器 | Microsoft Docs
description: 本文介绍 Azure 数据资源管理器中的 binary_and()。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: rkarlin
ms.service: data-explorer
ms.topic: reference
origin.date: 02/13/2020
ms.date: 08/18/2020
ms.openlocfilehash: 63e44d62dcc194afb1c23f08f3b7e9b8c68d559a
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88515741"
---
# <a name="binary_and"></a>binary_and()

返回两个值的“按位 `and`”运算的结果。

```kusto
binary_and(x,y) 
```

## <a name="syntax"></a>语法

`binary_and(`*num1*`,` *num2* `)`

## <a name="arguments"></a>参数

* num1、num2：长整型数字 。

## <a name="returns"></a>返回

返回对一对数字（num1 和 num2）的逻辑 AND 运算。