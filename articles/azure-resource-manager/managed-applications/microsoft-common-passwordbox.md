---
title: PasswordBox UI 元素
description: 介绍了 Azure 门户的 Microsoft.Common.PasswordBox UI 元素。 使用户能够在部署托管应用程序时提供机密值。
ms.topic: conceptual
origin.date: 06/27/2018
author: rockboyfor
ms.date: 08/24/2020
ms.testscope: no
ms.testdate: ''
ms.author: v-yeche
ms.openlocfilehash: 5c2594c7ac39ab727567325a80c20fd09785bd75
ms.sourcegitcommit: 601f2251c86aa11658903cab5c529d3e9845d2e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88807800"
---
# <a name="microsoftcommonpasswordbox-ui-element"></a>Microsoft.Common.PasswordBox UI 元素

一个可以用来提供和确认密码的控件。

## <a name="ui-sample"></a>UI 示例

:::image type="content" source="./media/managed-application-elements/microsoft-common-passwordbox.png" alt-text="Microsoft.Common.PasswordBox":::

## <a name="schema"></a>架构

```json
{
  "name": "element1",
  "type": "Microsoft.Common.PasswordBox",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "^[a-zA-Z0-9]{8,}$",
    "validationMessage": "Password must be at least 8 characters long, contain only numbers and letters"
  },
  "options": {
    "hideConfirmation": false
  },
  "visible": true
}
```

## <a name="sample-output"></a>示例输出

```json
"p4ssw0rd"
```

## <a name="remarks"></a>备注

- 此元素不支持 `defaultValue` 属性。
- 有关 `constraints` 的实现详细信息，请参阅 [Microsoft.Common.TextBox](microsoft-common-textbox.md)。
- 如果 `options.hideConfirmation` 设置为 **true**，则用于确认用户密码的第二个文本框会被隐藏。 默认值是 **false**秒。

## <a name="next-steps"></a>后续步骤

* 有关创建 UI 定义的简介，请参阅 [CreateUiDefinition 入门](create-uidefinition-overview.md)。
* 有关 UI 元素中的公用属性的说明，请参阅 [CreateUiDefinition 元素](create-uidefinition-elements.md)。

<!-- Update_Description: update meta properties, wording update, update link -->