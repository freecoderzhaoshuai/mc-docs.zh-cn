---
title: Azure Stack Hub 的 New-AzureStackActivation 特权终结点
description: PowerShell Azure Stack 特权终结点 - New-AzureStackActivation 参考
author: WenJason
ms.topic: reference
origin.date: 04/27/2020
ms.date: 08/31/2020
ms.author: v-jay
ms.reviewer: fiseraci
ms.lastreviewed: 04/27/2020
ms.openlocfilehash: 4f28d3bad3dca6361a2bcdf15801900ec419235d
ms.sourcegitcommit: 4e2d781466e54e228fd1dbb3c0b80a1564c2bf7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88868001"
---
# <a name="new-azurestackactivation"></a>New-AzureStackActivation

## <a name="synopsis"></a>摘要
激活 Azure Stack Hub。

## <a name="syntax"></a>语法

```
New-AzureStackActivation [[-TimeoutInSeconds] <Object>] [[-ActivationKey] <Object>] [-AsJob]
```

## <a name="parameters"></a>parameters

### <a name="-activationkey"></a>-ActivationKey
 

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

### <a name="-timeoutinseconds"></a>-TimeoutInSeconds
 

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: 2
Default value: 1000
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
