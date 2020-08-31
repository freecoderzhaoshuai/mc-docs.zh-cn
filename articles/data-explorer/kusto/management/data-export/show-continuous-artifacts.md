---
title: 显示连续数据导出项目 - Azure 数据资源管理器
description: 本文介绍了如何显示 Azure 数据资源管理器中的连续数据导出项目。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: yifats
ms.service: data-explorer
ms.topic: reference
origin.date: 08/03/2020
ms.date: 08/18/2020
ms.openlocfilehash: 6e4f2296186be8835815ce383b4d5c6ae1f857ca
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88556493"
---
# <a name="show-continuous-export-artifacts"></a>显示连续导出项目

返回连续导出在所有运行中导出的所有项目。 可以在命令中按 Timestamp 列筛选结果，以仅查看感兴趣的记录。 导出的项目的历史记录将保留 14 天。 

## <a name="syntax"></a>语法

`.show` `continuous-export` *ContinuousExportName* `exported-artifacts`

## <a name="properties"></a>属性

| properties             | 类型   | 说明                |
|----------------------|--------|----------------------------|
| ContinuousExportName | String | 连续导出的名称。 |

## <a name="output"></a>输出

| 输出参数  | 类型     | 说明                            |
|-------------------|----------|----------------------------------------|
| Timestamp         | datetime | 连续导出运行的时间戳 |
| ExternalTableName | String   | 外部表的名称             |
| `Path`              | String   | 输出路径                            |
| NumRecords        | long     | 导出到路径的记录数     |

## <a name="example"></a>示例

```kusto
.show continuous-export MyExport exported-artifacts | where Timestamp > ago(1h)
```

| Timestamp                   | ExternalTableName | `Path`             | NumRecords | SizeInBytes |
|-----------------------------|-------------------|------------------|------------|-------------|
| 2018-12-20 07:31:30.2634216 | ExternalBlob      | `http://storageaccount.blob.core.chinacloudapi.cn/container1/1_6ca073fd4c8740ec9a2f574eaa98f579.csv` | 10                          | 1024              |
