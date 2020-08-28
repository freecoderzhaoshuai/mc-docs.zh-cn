---
title: 字符串数据类型 - Azure 数据资源管理器
description: 本文介绍 Azure 数据资源管理器中的字符串数据类型。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: rkarlin
ms.service: data-explorer
ms.topic: reference
origin.date: 02/13/2020
ms.date: 07/31/2020
ms.openlocfilehash: f318ad6fad7a68690e12c5ae21d1a26af5b08964
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88515947"
---
# <a name="the-string-data-type"></a>字符串数据类型

`string` 数据类型表示 Unicode 字符串。 Kusto 字符串以 UTF-8 编码，默认情况下限制为 1MB。

## <a name="string-literals"></a>字符串文本

有多种方法可以对 `string` 数据类型的文本进行编码。

* 将字符串括在双引号中 (`"`)：`"This is a string literal. Single quote characters (') don't require escaping. Double quote characters (\") are escaped by a backslash (\\)"`
* 将字符串括在单引号中 (`'`)：`'Another string literal. Single quote characters (\') require escaping by a backslash (\\). Double quote characters (") do not require escaping.'`

在上面的两种表示形式中，反斜杠 (`\`) 字符表示转义。
它用于转义括起来的引号字符、制表符 (`\t`)、换行符 (`\n`) 和它自身 (`\\`)。

也支持逐字字符串文本。 在这种形式中，反斜杠字符 (`\`) 代表它自己，而不是转义字符。

* 括在双引号中 (`"`)：`@"This is a verbatim string literal that ends with a backslash\"`
* 括在单引号中 (`'`)：`@'This is a verbatim string literal that ends with a backslash\'`

如果查询中的两个字符串文本之间没有任何内容，或仅由空格和注释分隔，它们会自动联接，形成一个新的字符串文本。
例如，以下表达式均产生长度 `13`。

```kusto
print strlen("Hello"', '@"world!"); // Nothing between them

print strlen("Hello" ', ' @"world!"); // Separated by whitespace only

print strlen("Hello"
  // Comment
  ', '@"world!"); // Separated by whitespace and a comment
```

## <a name="examples"></a>示例

```kusto
// Simple string notation
print s1 = 'some string', s2 = "some other string"

// Strings that include single or double-quotes can be defined as follows
print s1 = 'string with " (double quotes)',
          s2 = "string with ' (single quotes)"

// Strings with '\' can be prefixed with '@' (as in c#)
print myPath1 = @'C:\Folder\filename.txt'

// Escaping using '\' notation
print s = '\\n.*(>|\'|=|\")[a-zA-Z0-9/+]{86}=='
```

可见，将字符串括在双引号 (`"`) 中时，单引号 (`'`) 字符不需要转义，反之亦然。 此方法可以更轻松地根据上下文引用字符串。

## <a name="obfuscated-string-literals"></a>经过模糊处理的字符串文本

系统跟踪查询并将其存储起来以用于遥测和分析。
例如，可能会向群集所有者提供查询文本的访问权限。 如果查询文本包含机密信息（例如密码），则可能会泄漏应保密的信息。 为了防止发生此类泄漏，查询作者可以将特定的字符串文本标记为经过模糊处理的字符串文本。
查询文本中的此类文本会自动替换为一些星号 (`*`) 字符，这样它们便不能用于稍后的分析。

> [!IMPORTANT]
> 将所有包含机密信息的字符串文本标记为经过模糊处理的字符串文本。

可以通过采用“常规”字符串文本并在其前面加上 `h` 或 `H` 字符来形成经过模糊处理的字符串文本。 

例如：

```kusto
h'hello'
h@'world'
h"hello"
```

> [!NOTE]
> 在许多情况下，只有一部分字符串文本是机密的。 在这些情况下，将文本拆分为非机密部分和机密部分。 然后，仅将机密部分标记为模糊处理。

例如：

```kusto
print x="https://contoso.blob.core.chinacloudapi.cn/container/blob.txt?"
  h'sv=2012-02-12&se=2013-04-13T0...'
```
