---
title: include 文件
description: 机密客户端方案登陆页的 include 文件（守护程序、Web 应用、Web API）
services: active-directory
documentationcenter: dev-center-name
author: jmprieur
manager: CelesteDG
editor: ''
ms.service: active-directory
ms.devlang: na
ms.topic: include
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2020
ms.author: v-junlch
ms.custom: include file
ms.openlocfilehash: edb4a833f0ef8b43e55a21bbbdbd305321cdee16
ms.sourcegitcommit: 7646936d018c4392e1c138d7e541681c4dfd9041
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88655060"
---
## <a name="register-secrets-or-certificates"></a>注册机密或证书

与任何机密客户端应用程序一样，你需要注册机密或证书。 可以通过 [Azure 门户](https://portal.azure.cn/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview)中的交互体验或使用命令行工具（如 PowerShell）注册应用程序机密。

### <a name="register-client-secrets-by-using-the-portal"></a>使用门户注册客户端机密

在应用程序的“证书和机密”  页上管理客户端凭据：

![“证书和机密”页](../articles/active-directory/develop/media/quickstart-update-azure-ad-app-preview/credentials-certificates-secrets.png)

- 可以通过在 Azure 门户的应用注册中选择”新建客户端机密”来创建客户端机密。 创建客户端机密时，必须在记录机密的字符串后再从“证书和机密”窗格中离开。 不会再次显示该机密的字符串。
- 在应用程序注册过程中，请使用“上传证书”**** 按钮来上传证书。 Azure AD 仅支持在应用程序上直接注册的证书，而不遵循证书链。

有关详细信息，请参阅[快速入门：将客户端应用程序配置为访问 Web API | 将凭据添加到应用程序](../articles/active-directory/develop/quickstart-configure-app-access-web-apis.md#add-credentials-to-your-web-application)。

### <a name="register-client-secrets-by-using-powershell"></a>使用 PowerShell 注册客户端机密

或者，可以使用命令行工具向 Azure AD 注册应用程序。 [active-directory-dotnetcore-daemon-v2](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2) 示例显示如何向 Azure AD 应用程序注册应用程序机密或证书：

- 有关如何注册应用程序机密的详细信息，请参阅 [AppCreationScripts/Configure.ps1](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/blob/5199032b352a912e7cc0fce143f81664ba1a8c26/AppCreationScripts/Configure.ps1#L190)。
- 有关如何向应用程序注册证书的详细信息，请参阅 [AppCreationScripts-withCert/Configure.ps1](https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/blob/5199032b352a912e7cc0fce143f81664ba1a8c26/AppCreationScripts-withCert/Configure.ps1#L162-L178)。

