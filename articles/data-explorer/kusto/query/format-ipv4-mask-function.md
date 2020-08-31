---
title: format_ipv4_mask() - Azure 数据资源管理器
description: 本文介绍 Azure 数据资源管理器中的 format_ipv4_mask()。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: alexans
ms.service: data-explorer
ms.topic: reference
origin.date: 08/09/2020
ms.date: 08/18/2020
ms.openlocfilehash: 84eaba68f4381b77568a366a016218e439ec01b9
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88556483"
---
# <a name="format_ipv4_mask"></a>format_ipv4_mask()

使用网络掩码分析输入，并以 CIDR 表示法返回表示 IPv4 地址的字符串。

```kusto
print format_ipv4_mask('192.168.1.255', 24) == '192.168.1.0/24'
print format_ipv4_mask(3232236031, 24) == '192.168.1.0/24'
```

## <a name="syntax"></a>语法

`format_ipv4_mask(`*Expr* [`,` *PrefixMask*`])`

## <a name="arguments"></a>参数

* *`Expr`* ：以 CIDR 表示法表示的 IPv4 地址的字符串或数字表示形式。
* *`PrefixMask`* ：（可选）从 0 到 32 的整数，表示所考虑的最有效位的数目。 如果未指定参数，则使用所有位掩码 (32)。

## <a name="returns"></a>返回

如果转换成功，则结果将是以 CIDR 表示法表示 IPv4 地址的字符串。
如果转换不成功，则结果将为空字符串。

## <a name="see-also"></a>请参阅

- [format_ipv4()](format-ipv4-function.md)：适用于未以 CIDR 表示法设置格式的 IPv4 地址。
- [IPv4 和 IPv6 函数](scalarfunctions.md#ipv4ipv6-functions)

## <a name="examples"></a>示例

<!-- csl: https://help.kusto.chinacloudapi.cn/Samples -->
```kusto
datatable(address:string, mask:long)
[
 '192.168.1.1', 24,          
 '192.168.1.1', 32,          
 '192.168.1.1/24', 32,       
 '192.168.1.1/24', long(-1), 
]
| extend result = format_ipv4(address, mask), 
         result_mask = format_ipv4_mask(address, mask)
```

|address|掩码|result|result_mask|
|---|---|---|---|
|192.168.1.1|24|192.168.1.0|192.168.1.0/24|
|192.168.1.1|32|192.168.1.1|192.168.1.1/32|
|192.168.1.1/24|32|192.168.1.0|192.168.1.0/24|
|192.168.1.1/24|-1|||
