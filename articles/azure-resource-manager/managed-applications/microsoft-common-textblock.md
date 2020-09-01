---
title: TextBlock UI 元素
description: 介绍了 Azure 门户的 Microsoft.Common.TextBlock UI 元素。 用于向界面添加文本。
ms.topic: conceptual
origin.date: 06/27/2018
author: rockboyfor
ms.date: 08/24/2020
ms.testscope: no
ms.testdate: ''
ms.author: v-yeche
ms.openlocfilehash: 56adde47215a6527b24e209c6b1cf5f2d7a1d632
ms.sourcegitcommit: 601f2251c86aa11658903cab5c529d3e9845d2e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88807911"
---
# <a name="microsoftcommontextblock-ui-element"></a>Microsoft.Common.TextBlock UI 元素

可用于向门户界面添加文本的控件。

## <a name="ui-sample"></a>UI 示例

:::image type="content" source="./media/managed-application-elements/microsoft-common-textblock.png" alt-text="Microsoft.Common.TextBox":::

## <a name="schema"></a>架构

```json
{
  "name": "text1",
  "type": "Microsoft.Common.TextBlock",
  "visible": true,
  "options": {
    "text": "Please provide the configuration values for your application.",
    "link": {
      "label": "Learn more",
      "uri": "https://www.microsoft.com"
    }
  }
}
```

## <a name="sample-output"></a>示例输出

```json
"Please provide the configuration values for your application. Learn more"
```

## <a name="next-steps"></a>后续步骤

* 有关创建 UI 定义的简介，请参阅 [CreateUiDefinition 入门](create-uidefinition-overview.md)。
* 有关 UI 元素中的公用属性的说明，请参阅 [CreateUiDefinition 元素](create-uidefinition-elements.md)。

<!-- Update_Description: update meta properties, wording update, update link -->