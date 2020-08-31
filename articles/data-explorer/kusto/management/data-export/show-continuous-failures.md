---
title: 显示连续数据导出失败 - Azure 数据资源管理器
description: 本文介绍了如何显示 Azure 数据资源管理器中的连续数据导出失败。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: yifats
ms.service: data-explorer
ms.topic: reference
origin.date: 08/03/2020
ms.date: 08/18/2020
ms.openlocfilehash: 2298d7b508344c9a8b07ecaa6c4957840bd32717
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88556490"
---
# <a name="show-continuous-export-failures"></a>显示连续导出失败

返回已记录为连续导出的一部分的所有失败。 可以在命令中按 Timestamp 列筛选结果，以仅查看感兴趣的时间范围。 

## <a name="syntax"></a>语法

`.show` `continuous-export` *ContinuousExportName* `failures`

## <a name="properties"></a>属性

| properties             | 类型   | 说明                |
|----------------------|--------|----------------------------|
| ContinuousExportName | String | 连续导出的名称  |

## <a name="output"></a>输出

| 输出参数 | 类型      | 说明                                         |
|------------------|-----------|-----------------------------------------------------|
| Timestamp        | datetime  | 失败时的时间戳。                           |
| OperationId      | String    | 失败的操作 ID。                    |
| 名称             | String    | 连续导出名称。                             |
| LastSuccessRun   | Timestamp | 连续导出的上次成功运行。   |
| FailureKind      | String    | Failure/PartialFailure。 PartialFailure 表示在失败之前已成功导出某些项目。 |
| 详细信息          | String    | 失败错误详细信息。                              |

## <a name="example"></a>示例 

```kusto
.show continuous-export MyExport failures 
```

| Timestamp                   | OperationId                          | 名称     | LastSuccessRun              | FailureKind | 详细信息    |
|-----------------------------|--------------------------------------|----------|-----------------------------|-------------|------------|
| 2019-01-01 11:07:41.1887304 | ec641435-2505-4532-ba19-d6ab88c96a9d | MyExport | 2019-01-01 11:06:35.6308140 | 失败     | 详细信息... |
