---
title: 显示连续数据导出 - Azure 数据资源管理器
description: 本文介绍了如何显示 Azure 数据资源管理器中的连续数据导出属性。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: yifats
ms.service: data-explorer
ms.topic: reference
origin.date: 08/03/2020
ms.date: 08/18/2020
ms.openlocfilehash: c6e4c9c1d4a01f0699b4338098e1a16077f3d778
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88556492"
---
# <a name="show-continuous-export"></a>显示连续导出

返回 ContinuousExportName 的连续导出属性。

## <a name="syntax"></a>语法

`.show` `continuous-export` *ContinuousExportName*

## <a name="properties"></a>属性

| properties             | 类型   | 说明                |
|----------------------|--------|----------------------------|
| ContinuousExportName | String | 连续导出的名称。 |

`.show` `continuous-exports`

返回数据库中的所有连续导出。

## <a name="output"></a>输出

| 输出参数    | 类型     | 说明                                                             |
|---------------------|----------|-------------------------------------------------------------------------|
| CursorScopedTables  | String   | 显式限定了作用域的（事实数据）表的列表（序列化的 JSON）               |
| ExportProperties    | String   | 导出属性（序列化的 JSON）                                     |
| ExportedTo          | DateTime | 上次成功导出的日期时间（引入时间）       |
| ExternalTableName   | String   | 外部表的名称                                              |
| ForcedLatency       | TimeSpan | 强制延迟（如果未提供，则为 null）                                   |
| IntervalBetweenRuns | TimeSpan | 两次运行之间的间隔                                                   |
| IsDisabled          | 布尔  | 如果连续导出已禁用，则为 true                               |
| IsRunning           | 布尔  | 如果连续导出当前正在运行，则为 true                      |
| LastRunResult       | String   | 上次连续导出运行的结果（`Completed` 或 `Failed`） |
| LastRunTime         | DateTime | 上次执行连续导出的时间（开始时间）           |
| 名称                | String   | 连续导出的名称                                           |
| 查询               | String   | 导出查询                                                            |
| StartCursor         | String   | 此连续导出的首次执行的起点         |

