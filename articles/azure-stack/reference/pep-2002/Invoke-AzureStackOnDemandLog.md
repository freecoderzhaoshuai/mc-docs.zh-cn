---
title: Azure Stack Hub 的 Invoke-AzureStackOnDemandLog 终结点
description: PowerShell Azure Stack 特权终结点 - Invoke-AzureStackOnDemandLog 参考
author: WenJason
ms.topic: reference
origin.date: 04/27/2020
ms.date: 08/31/2020
ms.author: v-jay
ms.reviewer: fiseraci
ms.lastreviewed: 04/27/2020
ms.openlocfilehash: b532bf7f4cbfc17cb544d25f4ce900a30faa75c9
ms.sourcegitcommit: 4e2d781466e54e228fd1dbb3c0b80a1564c2bf7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88868086"
---
# <a name="invoke-azurestackondemandlog"></a>Invoke-AzureStackOnDemandLog

## <a name="synopsis"></a>摘要
按需生成 Azure Stack Hub 角色的日志（如果适用）。

## <a name="syntax"></a>语法

```
Invoke-AzureStackOnDemandLog [-OutputPath <Object>] [-SlbTimeOutInMinutes <Object>] [-Generate]
 [-FilterByRole <Object>] [-TimeOutInMinutes <Object>] [-AsJob]
```

## <a name="parameters"></a>parameters

### <a name="-outputpath"></a>-OutputPath

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <a name="-filterbyrole"></a>-FilterByRole
```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### <a name="-timeoutinminutes"></a>-TimeOutInMinutes
```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: 30
Accept pipeline input: False
Accept wildcard characters: False
```

### <a name="-slbtimeoutinminutes"></a>-SlbTimeOutInMinutes

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: 20
Accept pipeline input: False
Accept wildcard characters: False
```

### <a name="-generate"></a>-Generate

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: False
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
