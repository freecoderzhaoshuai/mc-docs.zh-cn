---
title: InfoBox UI 元素
description: 介绍 Azure 门户的 Microsoft.Common.InfoBox UI 元素。 用于在部署托管应用程序时添加文本或警告。
ms.topic: conceptual
origin.date: 06/15/2018
author: rockboyfor
ms.date: 08/24/2020
ms.testscope: no
ms.testdate: ''
ms.author: v-yeche
ms.openlocfilehash: 4c2a47de9cdff6f5f0021b37ef20a63ec4a78abd
ms.sourcegitcommit: 601f2251c86aa11658903cab5c529d3e9845d2e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88807862"
---
# <a name="microsoftcommoninfobox-ui-element"></a>Microsoft.Common.InfoBox UI 元素

可添加信息框的控件。 该框包含重要文本或警告，可帮助用户了解他们提供的值。 它还可以链接到详细信息的 URI。

## <a name="ui-sample"></a>UI 示例

:::image type="content" source="./media/managed-application-elements/microsoft-common-infobox.png" alt-text="Microsoft.Common.InfoBox":::

## <a name="schema"></a>架构

```json
{
  "name": "text1",
  "type": "Microsoft.Common.InfoBox",
  "visible": true,
  "options": {
    "icon": "None",
    "text": "Nullam eros mi, mollis in sollicitudin non, tincidunt sed enim. Sed et felis metus, rhoncus ornare nibh. Ut at magna leo.",
    "uri": "https://www.microsoft.com"
  }
}
```

## <a name="sample-output"></a>示例输出

```json
"Nullam eros mi, mollis in sollicitudin non, tincidunt sed enim. Sed et felis metus, rhoncus ornare nibh. Ut at magna leo."
```

## <a name="remarks"></a>备注

* 对于 `icon`，请使用“无”、“信息”、“警告”或“错误”     。
* `uri` 属性为可选。

## <a name="next-steps"></a>后续步骤

* 有关创建 UI 定义的简介，请参阅 [CreateUiDefinition 入门](create-uidefinition-overview.md)。
* 有关 UI 元素中的公用属性的说明，请参阅 [CreateUiDefinition 元素](create-uidefinition-elements.md)。

<!-- Update_Description: update meta properties, wording update, update link -->