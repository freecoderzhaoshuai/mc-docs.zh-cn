---
title: 使用 Azure 门户配置客户管理的密钥
titleSuffix: Azure Storage
description: 了解如何使用 Azure 门户通过 Azure Key Vault 来配置客户管理的密钥用于 Azure 存储加密。
services: storage
author: WenJason
ms.service: storage
ms.topic: how-to
origin.date: 07/13/2020
ms.date: 08/24/2020
ms.author: v-jay
ms.reviewer: ozgun
ms.subservice: common
ms.openlocfilehash: 00fa5ed1a4747eab99b7f9902586a85674c2c5bd
ms.sourcegitcommit: ecd6bf9cfec695c4e8d47befade8c462b1917cf0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2020
ms.locfileid: "88753412"
---
# <a name="configure-customer-managed-keys-with-azure-key-vault-by-using-the-azure-portal"></a>通过 Azure 门户使用 Azure Key Vault 配置客户管理的密钥

[!INCLUDE [storage-encryption-configure-keys-include](../../../includes/storage-encryption-configure-keys-include.md)]

本文介绍如何使用 [Azure 门户](https://portal.azure.cn/)配置包含客户管理的密钥的 Azure 密钥保管库。 若要了解如何使用 Azure 门户创建 Key Vault，请参阅[快速入门：使用 Azure 门户在 Azure Key Vault 中设置和检索机密](../../key-vault/secrets/quick-create-portal.md)。

## <a name="configure-azure-key-vault"></a>配置 Azure Key Vault

使用带有 Azure 存储加密的客户管理密钥需要在密钥保管库上设置两个属性：“软删除”和“不要清除”。 默认不会启用这些属性，但可以使用 PowerShell 或 Azure CLI 对新的或现有的 Key Vault 启用。

若要了解如何在现有密钥保管库上启用这些属性，请参阅以下文章之一中标题为“启用软删除”和“启用清除保护”的部分： 

- [如何通过 PowerShell 使用软删除](../../key-vault/general/soft-delete-powershell.md)。
- [如何通过 CLI 使用软删除](../../key-vault/general/soft-delete-cli.md)。

Azure 存储加密支持 2048、3072 和 4096 大小的 RSA 密钥。 有关密钥的详细信息，请参阅[关于 Azure Key Vault 密钥、机密和证书](../../key-vault/about-keys-secrets-and-certificates.md#key-vault-keys)中的“Key Vault 密钥”。

## <a name="enable-customer-managed-keys"></a>启用客户管理的密钥

若要在 Azure 门户中启用客户管理的密钥，请执行以下步骤：

1. 导航到存储帐户。
1. 在存储帐户的“设置”边栏选项卡上，单击“加密”。 选择“客户托管密钥”选项，如下图所示。

    ![显示加密选项的门户屏幕截图](./media/storage-encryption-keys-portal/portal-configure-encryption-keys.png)

## <a name="specify-a-key"></a>指定密钥

启用客户管理的密钥后，可以指定要与存储帐户关联的密钥。 你也可以指示 Azure 存储是否应该自动轮换客户管理的密钥，或者你是否将会手动轮换密钥。

### <a name="specify-a-key-from-a-key-vault"></a>从 Key Vault 指定密钥

从密钥保管库中选择客户管理的密钥时，会自动启用密钥自动轮换。 若要手动管理密钥版本，请改为指定密钥 URI，并包含密钥版本。 有关详细信息，请参阅[将密钥指定为 URI](#specify-a-key-as-a-uri)。

若要指定 Key Vault 中的密钥，请执行以下步骤：

1. 选择“从 Key Vault 中选择”选项。
1. 选择“选择密钥保管库和密钥”。
1. 选择包含要使用的密钥的密钥保管库。
1. 从密钥保管库中选择密钥。

   ![屏幕截图，显示如何选择密钥保管库和密钥](./media/storage-encryption-keys-portal/portal-select-key-from-key-vault.png)

1. 保存所做更改。

### <a name="specify-a-key-as-a-uri"></a>将密钥指定为 URI

指定密钥 URI 时，请省略密钥版本，以启用自动轮换客户管理的密钥。 如果密钥 URI 中包含密钥版本，则不启用自动轮换，你必须自行管理密钥版本。 若要详细了解如何更新密钥版本，请参阅[手动更新密钥版本](#manually-update-the-key-version)。

若要将某个密钥指定为 URI，请执行下列步骤：

1. 若要在 Azure 门户中查找密钥 URI，请导航到 Key Vault，然后选择“密钥”设置。 选择所需的密钥，然后单击该密钥以查看其版本。 选择一个密钥版本，查看该版本的设置。
1. 复制“密钥标识符”字段的值（提供 URI）。

    ![显示 Key Vault 密钥 URI 的屏幕截图](media/storage-encryption-keys-portal/portal-copy-key-identifier.png)

1. 在存储帐户的“加密密钥”设置中，选择“输入密钥 URI”选项。 
1. 将复制的 URI 粘贴到“密钥 URI”字段中。 从 URI 中省略密钥版本以启用自动轮换。

   ![显示如何输入密钥 URI 的屏幕截图](./media/storage-encryption-keys-portal/portal-specify-key-uri.png)

1. 指定包含密钥保管库的订阅。
1. 保存所做更改。

指定密钥后，Azure 门户会指示是否已启用自动密钥轮换，并显示当前用于加密的密钥版本。

:::image type="content" source="media/storage-encryption-keys-portal/portal-auto-rotation-enabled.png" alt-text="屏幕截图，显示已启用自动轮换客户管理的密钥":::

## <a name="manually-update-the-key-version"></a>手动更新密钥版本

默认情况下，Azure 存储会为你自动轮换客户管理的密钥（如前几节中所述）。 如果选择自行管理密钥版本，则每次创建密钥的新版本时都必须更新为存储帐户指定的密钥版本。

若要更新存储帐户以使用新的密钥版本，请执行以下步骤：

1. 导航到你的存储帐户，并显示“加密”设置。
1. 输入新密钥版本的 URI。 或者，可以再次选择 Key Vault 和密钥以更新版本。
1. 保存所做更改。

## <a name="switch-to-a-different-key"></a>切换到其他密钥

若要更改用于 Azure 存储加密的密钥，请执行以下步骤：

1. 导航到你的存储帐户，并显示“加密”设置。
1. 输入新密钥的 URI。 也可选择密钥保管库并选择一个新密钥。
1. 保存所做更改。

## <a name="disable-customer-managed-keys"></a>禁用客户托管密钥

禁用客户托管密钥时，将再次使用 Microsoft 托管密钥对存储帐户进行加密。 若要禁用客户托管密钥，请执行以下步骤：

1. 导航到你的存储帐户，并显示“加密”设置。
1. 取消选中“使用自己的密钥”设置旁边的复选框。

## <a name="next-steps"></a>后续步骤

- [静态数据的 Azure 存储加密](storage-service-encryption.md)
- [什么是 Azure Key Vault？](/key-vault/key-vault-overview)
