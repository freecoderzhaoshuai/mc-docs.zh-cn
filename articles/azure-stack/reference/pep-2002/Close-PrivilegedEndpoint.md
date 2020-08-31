---
title: Azure Stack Hub 的 Close-PrivilegedEndpoint 特权终结点
description: PowerShell Azure Stack 特权终结点 - Close-PrivilegedEndpoint 参考
author: WenJason
ms.topic: reference
origin.date: 04/27/2020
ms.date: 08/31/2020
ms.author: v-jay
ms.reviewer: fiseraci
ms.lastreviewed: 04/27/2020
ms.openlocfilehash: e7b2972324f3cb1178a719719fd1209b8d40abb6
ms.sourcegitcommit: 4e2d781466e54e228fd1dbb3c0b80a1564c2bf7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88867853"
---
# <a name="close-privilegedendpoint"></a>Close-PrivilegedEndpoint

## <a name="syntax"></a>语法

```
Close-PrivilegedEndpoint [[-TranscriptsPathDestination] <Object>] [[-Credential] <Object>] [-AsJob]
```

## <a name="parameters"></a>parameters

### <a name="-credential"></a>-Credential


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

### <a name="-transcriptspathdestination"></a>-TranscriptsPathDestination
 

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: 0
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
