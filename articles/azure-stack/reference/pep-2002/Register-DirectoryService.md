---
title: Azure Stack Hub 的 Register-DirectoryService 特权终结点
description: PowerShell Azure Stack 特权终结点参考 - Register-DirectoryService
author: WenJason
ms.topic: reference
origin.date: 04/27/2020
ms.date: 08/31/2020
ms.author: v-jay
ms.reviewer: fiseraci
ms.lastreviewed: 04/27/2020
ms.openlocfilehash: c6bc169c2edcc1d26022d91ccbab727c48eb844e
ms.sourcegitcommit: 4e2d781466e54e228fd1dbb3c0b80a1564c2bf7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88867997"
---
# <a name="register-directoryservice"></a>Register-DirectoryService

## <a name="synopsis"></a>摘要
用于将客户 Active Directory (Azure AD) 注册到 Graph 服务的脚本。
CustomADGlobalCatalog**** 是自定义 Active Directory 的全局编录。
这将是 Get-ADForest**** cmdlet 的输出中的 `RootDomain` 值。

## <a name="syntax"></a>语法

```
Register-DirectoryService [-Force] [[-TimeoutInSecs] <Object>] [-SkipRootDomainValidation]
 [[-CustomADAdminCredential] <Object>] [-ValidateParameters] [[-CustomADGlobalCatalog] <Object>] [-AsJob]
```

## <a name="description"></a>说明
用于将客户 Active Directory 注册到 Graph 服务的脚本。
CustomADGlobalCatalog**** 是自定义 Active Directory 的全局编录。
这将是 Get-ADForest**** cmdlet 的输出中的 `RootDomain` 值。

## <a name="examples"></a>示例

### <a name="example-1"></a>示例 1
```
Register-DirectoryService -CustomADGlobalCatalog "contoso.com" -CustomADAdminCredential (Get-Credential) -TimeoutInSecs 1000
```

## <a name="parameters"></a>parameters

### <a name="-customadglobalcatalog"></a>-CustomADGlobalCatalog
 

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

### <a name="-customadadmincredential"></a>-CustomADAdminCredential
 

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

### <a name="-validateparameters"></a>-ValidateParameters
 

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

### <a name="-skiprootdomainvalidation"></a>-SkipRootDomainValidation
 

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

### <a name="-force"></a>-Force
 

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

### <a name="-timeoutinsecs"></a>-TimeoutInSecs
 

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: False
Position: 3
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

若要了解如何访问和使用特权终结点，请参阅[使用 Azure Stack Hub 中的特权终结点](../../operator/azure-stack-privileged-endpoint.md)。
