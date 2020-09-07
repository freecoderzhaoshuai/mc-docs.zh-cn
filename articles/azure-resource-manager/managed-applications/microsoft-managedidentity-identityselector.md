---
title: IdentitySelector UI 元素
description: 介绍了 Azure 门户的 Microsoft.ManagedIdentity.IdentitySelector UI 元素。 用于将托管标识分配给资源。
ms.topic: conceptual
origin.date: 02/06/2020
author: rockboyfor
ms.date: 08/24/2020
ms.testscope: no
ms.testdate: ''
ms.author: v-yeche
ms.openlocfilehash: 2b165e1d4b95f017ad28daedd0abf582e7b11507
ms.sourcegitcommit: 601f2251c86aa11658903cab5c529d3e9845d2e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88807903"
---
<!--Verified successfully-->
# <a name="microsoftmanagedidentityidentityselector-ui-element"></a>Microsoft.ManagedIdentity.IdentitySelector UI 元素

用于为部署中的资源分配[托管标识](../../active-directory/managed-identities-azure-resources/overview.md)的控件。

## <a name="ui-sample"></a>UI 示例

此控件由以下元素组成：

:::image type="content" source="./media/managed-application-elements/microsoft-managedidentity-identityselector-1.png" alt-text="Microsoft.ManagedIdentity.IdentitySelector 第一步":::

当用户选择“添加”  时，将打开以下窗体。 用户可以为资源选择一个或多个用户分配的标识。

:::image type="content" source="./media/managed-application-elements/microsoft-managedidentity-identityselector-2.png" alt-text="Microsoft.ManagedIdentity.IdentitySelector 第二步":::

所选的标识将显示在表中。 用户可以从此表中添加或删除项。

:::image type="content" source="./media/managed-application-elements/microsoft-managedidentity-identityselector-3.png" alt-text="Microsoft.ManagedIdentity.IdentitySelector 第三步":::

## <a name="schema"></a>架构

```json
{
  "name": "identity",
  "type": "Microsoft.ManagedIdentity.IdentitySelector",
  "label": "Managed Identity Configuration",
  "toolTip": {
    "systemAssignedIdentity": "Enable system assigned identity to grant the resource access to other existing resources.",
    "userAssignedIdentity": "Add user assigned identities to grant the resource access to other existing resources."
  },
  "defaultValue": {
    "systemAssignedIdentity": "Off"
  },
  "options": {
    "hideSystemAssignedIdentity": false,
    "hideUserAssignedIdentity": false
  },
  "visible": true
}
```

## <a name="sample-output"></a>示例输出

```json
{
  "identity": {
    "value": {
      "type": "UserAssigned",
      "userAssignedIdentities": {
        "/subscriptions/xxxx/resourceGroups/TestResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/TestUserIdentity1": {}
      }
    }
  }
}
```

## <a name="remarks"></a>备注

- 使用 **defaultValue.systemAssignedIdentity** 为系统分配的标识选项控件设置初始值。 默认值为 **Off**。 允许以下值：
    - **On** - 系统分配的标识将分配给资源。
    - **Off** - 不会将系统分配的标识分配给资源。
    - **OnOnly** - 系统分配的标识将分配给资源。 在部署期间，用户无法编辑此值。
    - **OffOnly** - 不会将系统分配的标识分配给资源。 在部署期间，用户无法编辑此值。

- 如果 **options.hideSystemAssignedIdentity** 设为 **true**，则不会显示用于配置系统分配标识的 UI。 此选项的默认值为 **false**。
- 如果 **options.hideUserAssignedIdentity** 设为 **true**，则不会显示用于配置用户分配标识的 UI。 没有为资源分配用户分配的标识。 此选项的默认值为 **false**。

## <a name="next-steps"></a>后续步骤

- 有关创建 UI 定义的简介，请参阅 [CreateUiDefinition 入门](create-uidefinition-overview.md)。
- 有关 UI 元素中的公用属性的说明，请参阅 [CreateUiDefinition 元素](create-uidefinition-elements.md)。

<!-- Update_Description: update meta properties, wording update, update link -->