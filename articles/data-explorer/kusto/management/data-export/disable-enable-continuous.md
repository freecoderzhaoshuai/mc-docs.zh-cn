---
title: 启用或禁用连续数据导出 - Azure 数据资源管理器
description: 本文介绍了如何禁用或启用 Azure 数据资源管理器中的连续数据导出。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: yifats
ms.service: data-explorer
ms.topic: reference
origin.date: 08/03/2020
ms.date: 08/18/2020
ms.openlocfilehash: 3b50b645e37050d11e550375789156fd7053c92a
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88556497"
---
# <a name="disable-or-enable-continuous-export"></a>禁用或启用连续导出

禁用或启用连续导出作业。 不会执行禁用的连续导出，但其当前状态将保留，并且可以在启用连续导出后恢复。 

当启用已长时间禁用的连续导出时，导出将从上次禁用导出时停止的位置继续进行。 如果没有足够的群集容量来为所有进程提供服务，此继续操作可能会导致导出长时间运行，阻止其他导出运行。 连续导出将按上次运行时间升序执行（最早的导出将首先运行，直到赶上进度）。 

## <a name="syntax"></a>语法

`.enable` `continuous-export` *ContinuousExportName* 

`.disable` `continuous-export` *ContinuousExportName* 

## <a name="properties"></a>属性

| properties             | 类型   | 说明                |
|----------------------|--------|----------------------------|
| ContinuousExportName | String | 连续导出的名称 |

## <a name="output"></a>输出

对更改后的连续导出执行[显示连续导出命令](show-continuous-export.md)的结果。 
