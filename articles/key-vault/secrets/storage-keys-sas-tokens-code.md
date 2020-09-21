---
title: 通过编写代码提取共享访问签名令牌 | Azure Key Vault
description: 托管存储帐户功能在 Azure Key Vault 与 Azure 存储帐户之间提供无缝集成。 此示例使用 Azure SDK for .NET 管理 SAS 令牌。
ms.topic: tutorial
ms.service: key-vault
ms.subservice: secrets
author: msmbaldwin
ms.author: v-tawe
manager: rkarlin
origin.date: 09/10/2019
ms.date: 09/15/2020
ms.custom: devx-track-csharp
ms.openlocfilehash: 587ac3843b0087dfc38fa2f6e994d04e4b0f44f6
ms.sourcegitcommit: 39410f3ed7bdeafa1099ba5e9ec314b4255766df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2020
ms.locfileid: "90678513"
---
# <a name="fetch-shared-access-signature-tokens-in-code"></a>通过编写代码提取共享访问签名令牌

你可以使用存储在密钥保险库中的共享访问签名 (SAS) 令牌来管理存储帐户。 有关详细信息，请参阅[使用 SAS 授予对 Azure 存储资源的有限访问权限](../../storage/common/storage-sas-overview.md)。

> [!NOTE]
> 建议使用[基于角色的访问控制(RBAC)](../../storage/common/storage-auth-aad.md) 来保护存储帐户，以获得比“共享密钥”授权更高的安全性和易用性。

本文展示了用于创建 SAS 定义和获取 SAS 令牌的 .NET 代码的示例。 请参阅我们的 [ShareLink](https://docs.microsoft.com/samples/azure/azure-sdk-for-net/share-link/) 示例，获取完整详细信息，包括为密钥保管库托管的存储帐户生成的客户端的信息。 有关如何创建和存储 SAS 令牌的信息，请参阅[使用密钥保管库和 Azure CLI 管理存储帐户密钥](overview-storage-keys.md)或[使用密钥保管库和 Azure PowerShell 管理存储帐户密钥](overview-storage-keys-powershell.md)。

## <a name="code-samples"></a>代码示例

在以下示例中，将创建 SAS 模板：

```csharp
private static string BuildSasDefinitionTemplate(bool readOnly) =>
    new StringBuilder("sv=2018-03-28")  // service version
        .Append("&spr=https")           // HTTPS only
        .Append("&ss=bf")               // blobs and files only
        .Append("&srt=o")               // applies to objects only
        .Append(readOnly ? "&sp=r" : "&sp=rw")  // read-only or read-write
        .ToString();
```

使用此模板，可以通过使用...创建 SAS 定义 

```csharp
string sasDefinitionName = BuildSasDefinitionName(Tag, readOnly, duration);
SasDefinitionAttributes sasDefinitionAttributes = new SasDefinitionAttributes
{
    Enabled = true,
};

Dictionary<string, string> tags = new Dictionary<string, string>
{
    [Tag] = "1",
};

SasDefinitionBundle createdSasDefinition = await storageClient.SetSasDefinitionAsync(
    storageAccountName,
    sasDefinitionName,
    sasTemplate,
    SasTokenType.Account,
    duration,
    sasDefinitionAttributes,
    tags,
    s_cancellationTokenSource.Token);
```

创建 SAS 定义后，就可以使用 `SecretClient` 检索 SAS 令牌，比如机密。 需要在机密名称前面加上存储帐户名称，后跟短划线：

```csharp
// Build our SAS template, get an existing SAS definition, or create a new one.
string sasTemplate = BuildSasDefinitionTemplate(readOnly);
string sasDefinitionName = await GetOrCreateSasDefinitionAsync(storageClient, storageAccountName, sasTemplate, days, readOnly);

// Now we can create a SecretClient and generate a new SAS token from the storage account and SAS definition names.
SecretClient secretClient = new SecretClient(vaultUri, credential, options);
KeyVaultSecret sasToken = await secretClient.GetSecretAsync($"{storageAccountName}-{sasDefinitionName}", cancellationToken: s_cancellationTokenSource.Token);
```

如果共享访问签名令牌即将过期，可以再次获取相同的机密并生成新的令牌。

## <a name="next-steps"></a>后续步骤
- 了解如何[使用 SAS 授予对 Azure 存储资源的有限访问权限](../../storage/common/storage-sas-overview.md)。
- 了解如何[使用密钥保管库和 Azure CLI 管理存储帐户密钥](overview-storage-keys.md)或 [Azure PowerShell](overview-storage-keys-powershell.md)。
- 请参阅完整的[共享链接](https://docs.microsoft.com/samples/azure/azure-sdk-for-net/share-link/)示例。
- 更多 [Key Vault 示例](https://docs.microsoft.com/samples/browse/?expanded=azure&products=azure-key-vault)
- 请参阅[托管存储帐户密钥示例](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=key+vault+storage&type=&language=)
