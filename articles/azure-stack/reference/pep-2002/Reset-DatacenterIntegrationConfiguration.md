---
title: Azure Stack Hub 的 Reset-DatacenterIntegrationConfiguration 特权终结点
description: PowerShell Azure Stack 特权终结点 - Reset-DatacenterIntegrationConfiguration 参考信息
author: WenJason
ms.topic: reference
origin.date: 04/27/2020
ms.date: 08/31/2020
ms.author: v-jay
ms.reviewer: fiseraci
ms.lastreviewed: 04/27/2020
ms.openlocfilehash: be119c99ccf1afd571107f02749e73c47c30f36a
ms.sourcegitcommit: 4e2d781466e54e228fd1dbb3c0b80a1564c2bf7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88867989"
---
# <a name="reset-datacenterintegrationconfiguration"></a>Reset-DatacenterIntegrationConfiguration

## <a name="synopsis"></a>摘要
用于重置数据中心集成更改的脚本。

## <a name="syntax"></a>语法

```
Reset-DatacenterIntegrationConfiguration [[-TimeoutInSecs] <Object>] [-AsJob]
```

## <a name="description"></a>说明
用于重置数据中心集成更改的脚本。

## <a name="examples"></a>示例

### <a name="example-1"></a>示例 1
```
Reset-DatacenterIntegrationConfiguration -TimeoutInSecs 2000
```

## <a name="parameters"></a>parameters

### <a name="-timeoutinsecs"></a>-TimeoutInSecs
 

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: 1
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
