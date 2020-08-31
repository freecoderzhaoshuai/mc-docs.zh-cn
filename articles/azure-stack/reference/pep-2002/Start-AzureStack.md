---
title: Azure Stack Hub 的 Start-AzureStack 特权终结点
description: PowerShell Azure Stack 特权终结点 - Start-AzureStack 参考
author: WenJason
ms.topic: reference
origin.date: 04/27/2020
ms.date: 08/31/2020
ms.author: v-jay
ms.reviewer: fiseraci
ms.lastreviewed: 04/27/2020
ms.openlocfilehash: 81f1ea8a66dc2c671c3f34bb3d5780c9a17f31f5
ms.sourcegitcommit: 4e2d781466e54e228fd1dbb3c0b80a1564c2bf7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88867980"
---
# <a name="start-azurestack"></a>Start-AzureStack

## <a name="synopsis"></a>摘要
启动所有 Azure Stack Hub 服务。

## <a name="syntax"></a>语法

```
Start-AzureStack [[-TimeoutInSecs] <Object>] [-AsJob]
```

## <a name="description"></a>说明
启动所有 Azure Stack Hub 服务。

## <a name="examples"></a>示例

### <a name="example-1"></a>示例 1
```powershell
PS C:\> 
```



## <a name="parameters"></a>parameters

### <a name="-timeoutinsecs"></a>-TimeoutInSecs
最长时间，超过后即停止执行。

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
Default value: 2400
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
