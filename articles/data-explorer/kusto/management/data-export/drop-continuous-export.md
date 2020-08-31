---
title: 删除连续数据导出 - Azure 数据资源管理器
description: 本文介绍了如何删除 Azure 数据资源管理器中的连续数据导出。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: yifats
ms.service: data-explorer
ms.topic: reference
origin.date: 08/03/2020
ms.date: 08/18/2020
ms.openlocfilehash: 8626ca76ac640a5363d5bd3144384547a1269a62
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88556494"
---
# <a name="drop-continuous-export"></a>删除连续导出

删除连续导出作业。

## <a name="syntax"></a>语法

`.drop` `continuous-export` *ContinuousExportName*

## <a name="properties"></a>属性

| properties             | 类型   | 说明                |
|----------------------|--------|----------------------------|
| ContinuousExportName | String | 连续导出的名称 |

## <a name="output"></a>输出

数据库中的其余连续导出（删除后）。 输出架构，与[显示连续导出命令](show-continuous-export.md)中显示的相同。
