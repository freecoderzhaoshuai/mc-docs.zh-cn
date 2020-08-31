---
title: .create tables - Azure 数据资源管理器 | Microsoft Docs
description: 本文介绍 Azure 数据资源管理器中的 .create tables。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: alexans
ms.service: data-explorer
ms.topic: reference
origin.date: 07/05/2020
ms.date: 08/18/2020
ms.openlocfilehash: 44db0254d285bc7d5b44831d1cc745965e41ad52
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88515903"
---
# <a name="create-tables"></a>.create tables

创建新的空表作为批量操作。

该命令必须在特定数据库的上下文中运行。

需要[数据库用户权限](../management/access-control/role-based-authorization.md)。

**语法**

`.create` `tables` *TableName1* ([columnName:columnType], ...) [`,` *TableName2* ([columnName:columnType], ...) ... ] [`with` `(` `folder` `=` *FolderName*] `)`]

如果已经存在任何表，命令将返回成功。
 
**示例** 

```kusto
.create tables 
  MyLogs (Level:string, Timestamp:datetime, UserId:string, TraceId:string, Message:string, ProcessId:int32),
  MyUsers (UserId:string, Name:string)
```
