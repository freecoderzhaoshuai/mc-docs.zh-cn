---
title: 创建 UI 定义日期函数
description: 介绍在使用日期值时要使用的函数。
ms.topic: conceptual
origin.date: 07/13/2020
author: rockboyfor
ms.date: 08/24/2020
ms.testscope: no
ms.testdate: ''
ms.author: v-yeche
ms.openlocfilehash: caa4e71efa004b6980dbb01b3f792ca58e0e2c2a
ms.sourcegitcommit: 2e9b16f155455cd5f0641234cfcb304a568765a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88715659"
---
<!--Verify Successfully-->
# <a name="createuidefinition-date-functions"></a>创建 UI 定义日期函数

在使用日期值时要使用的函数。

## <a name="addhours"></a>addHours

向指定时间戳添加整小时数。

以下示例返回 `"1991-01-01T00:59:59.000Z"`：

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="addminutes"></a>addMinutes

向指定时间戳添加整分钟数。

以下示例返回 `"1991-01-01T00:00:59.000Z"`：

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

## <a name="addseconds"></a>addSeconds
向指定时间戳添加整秒数。

以下示例返回 `"1991-01-01T00:00:00.000Z"`：

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

## <a name="utcnow"></a>utcNow

返回本地计算机上以 ISO 8601 格式显示的当前日期和时间的字符串。

以下示例可能返回 `"1990-12-31T23:59:59.000Z"`：

```json
"[utcNow()]"
```

## <a name="next-steps"></a>后续步骤

* 有关 Azure 资源管理器的简介，请参阅 [Azure 资源管理器概述](../management/overview.md)。

<!-- Update_Description: new article about create ui definition date functions -->
<!--NEW.date: 08/24/2020-->