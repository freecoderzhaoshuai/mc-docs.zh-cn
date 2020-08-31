---
title: Azure Stack Hub 的 Get-ActionStatus 特权终结点
description: PowerShell Azure Stack 特权终结点 - Get-ActionStatus 参考
author: WenJason
ms.topic: reference
origin.date: 04/27/2020
ms.date: 08/31/2020
ms.author: v-jay
ms.reviewer: fiseraci
ms.lastreviewed: 04/27/2020
ms.openlocfilehash: 9b2283c15e0c0470c885f66d6d4ceabf44f95bce
ms.sourcegitcommit: 4e2d781466e54e228fd1dbb3c0b80a1564c2bf7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88867850"
---
# <a name="get-actionstatus"></a>Get-ActionStatus

## <a name="synopsis"></a>摘要
为具有指定函数名称的操作获取最新动作的状态。

## <a name="syntax"></a>语法

```
Get-ActionStatus [[-ActionType] <Object>] [[-FunctionName] <Object>] [-AsJob]
```

## <a name="description"></a>说明
为具有指定函数名称的操作获取最新动作的状态。

## <a name="examples"></a>示例

### <a name="example-1"></a>示例 1
```
Get-ActionStatus -FunctionName "Start-SecretRotation"
```

## <a name="parameters"></a>parameters

### <a name="-functionname"></a>-FunctionName
正在为其查询状态的函数的名称。

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <a name="-actiontype"></a>-ActionType
操作动作的类型名称。

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <a name="-asjob"></a>-AsJob


```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

## <a name="next-steps"></a>后续步骤

有关如何访问和使用特权终结点的信息，请参阅[使用 Azure Stack Hub 中的特权终结点](../../operator/azure-stack-privileged-endpoint.md)。
