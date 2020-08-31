---
title: binary_not() - Azure 数据资源管理器 | Microsoft Docs
description: 本文介绍 Azure 数据资源管理器中的 binary_not()。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: rkarlin
ms.service: data-explorer
ms.topic: reference
origin.date: 02/13/2020
ms.date: 08/18/2020
ms.openlocfilehash: ac5af92934167ae66617674d521330941dd6c232
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88515740"
---
# <a name="binary_not"></a>binary_not()

返回输入值的“按位求反”结果。

```kusto
binary_not(x)
```

## <a name="syntax"></a>语法

`binary_not(`*num1*`)`

## <a name="arguments"></a>参数

* num1：数字 

## <a name="returns"></a>返回

返回对一个数字 (num1) 的逻辑 NOT 运算。