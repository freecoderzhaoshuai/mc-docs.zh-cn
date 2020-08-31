---
title: .show functions - Azure 数据资源管理器 | Microsoft Docs
description: 本文介绍 Azure 数据资源管理器中的 .show functions。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: rkarlin
ms.service: data-explorer
ms.topic: reference
origin.date: 02/13/2020
ms.date: 08/18/2020
ms.openlocfilehash: c2dfd566ef0d316349fed9fb620c121aa6d351a9
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88516119"
---
# <a name="show-functions"></a>.show 函数

列出当前所选数据库中存储的所有函数。
若要仅返回一个特定函数，请参阅 [.show function](#show-function)。

## <a name="show-functions"></a>.show functions

```kusto
.show functions
```

需要[数据库用户权限](../management/access-control/role-based-authorization.md)。
 
|输出参数 |类型 |说明
|---|---|--- 
|名称  |String |函数的名称。 
|parameters  |String |函数所需的参数。
|正文  |String |（零个或多个）`let` 语句，后跟有效的 CSL 表达式，该表达式在函数调用时求值。
|文件夹|String|用于 UI 函数分类的文件夹。 此参数不会更改调用函数的方式。
|DocString|String|用于 UI 目的的函数说明。
 
**输出示例** 

|名称 |parameters|正文|文件夹|DocString
|---|---|---|---|---
|MyFunction1 |() | {StormEvents &#124; limit 100}|MyFolder|简单演示函数|
|MyFunction2 |(myLimit: long)| {StormEvents &#124; limit myLimit}|MyFolder|带参数的演示函数|
|MyFunction3 |() | { StormEvents(100) }|MyFolder|调用其他函数的函数||

## <a name="show-function"></a>.show function

```kusto
.show function MyFunc1
```

列出存储的某个特定函数的详细信息。 有关所有函数的列表，请参阅 [.show functions](#show-functions)。

**语法**

`.show` `function` FunctionName

**输出**

|输出参数 |类型 |说明
|---|---|--- 
|名称  |String |函数的名称。 
|parameters  |String |函数所需的参数。
|正文  |String |（零个或多个）`let` 语句，后跟有效的 CSL 表达式，该表达式在函数调用时求值。
|文件夹|String|用于 UI 函数分类的文件夹。 此参数不会更改调用函数的方式
|DocString|String|用于 UI 目的的函数说明。
 
> [!NOTE] 
> * 如果该函数不存在，将返回错误。
> * 需要[数据库用户权限](../management/access-control/role-based-authorization.md)。
 
**示例** 

```kusto
.show function MyFunction1 
```
    
|名称 |parameters |正文|文件夹|DocString
|---|---|---|---|---
|MyFunction1 |() | {StormEvents &#124; limit 100}|MyFolder|简单演示函数
