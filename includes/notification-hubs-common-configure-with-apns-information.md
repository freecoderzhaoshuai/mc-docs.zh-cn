---
author: mikeparker104
ms.author: v-tawe
origin.date: 06/02/2020
ms.date: 06/02/2020
ms.service: notification-hubs
ms.topic: include
ms.openlocfilehash: 988772043a843f7e47e0b9a18302c1d6d6981861
ms.sourcegitcommit: 5656c18d7d2faa09329b1a15e352d1622e252d5f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "89316497"
---
### <a name="configure-your-notification-hub-with-apns-information"></a>使用 APNS 信息配置通知中心

在“Notification Services”下，选择“Apple”，然后根据以前在[为通知中心创建证书](#creating-a-certificate-for-notification-hubs)部分中选择的方法，执行相应的步骤。  

> [!NOTE]
> 仅当希望将推送通知发送给已从应用商店购买应用的用户时，才应当对“应用程序模式”使用“生产”。

### <a name="option-1-using-a-p12-push-certificate"></a>选项 1：使用 .p12 推送证书

1. 选择“证书”。

1. 选择文件图标。

1. 选择前面导出的 .p12 文件，然后选择“Open”（打开）。

1. 如有必要，请指定正确的密码。

1. 选择“沙盒”模式。

1. 选择“保存”。

### <a name="option-2-using-token-based-authentication"></a>选项 2：使用基于令牌的身份验证

1. 选择“令牌”。
1. 输入前面获取的以下值：

    - 密钥 ID
    - 捆绑包 ID
    - 团队 ID
    - 令牌

1. 选择“沙盒”。
1. 选择“保存”。
