---
title: 条件访问策略中的云应用或操作 - Azure Active Directory
description: Azure AD 条件访问策略中的云应用或操作是什么
services: active-directory
ms.service: active-directory
ms.subservice: conditional-access
ms.topic: conceptual
ms.date: 09/07/2020
ms.author: v-junlch
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: calebb
ms.collection: M365-identity-device-management
ms.openlocfilehash: c91fa5be8cad43993e6699bf9795b83e171ffe48
ms.sourcegitcommit: 25d542cf9c8c7bee51ec75a25e5077e867a9eb8b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89593697"
---
# <a name="conditional-access-cloud-apps-or-actions"></a>条件访问：云应用或操作

云应用或操作是条件访问策略中的一个关键信号。 管理员可以使用条件访问策略将控制措施分配给特定的应用程序或操作。

- 管理员可以从包含内置 Microsoft 应用程序和任何 Azure AD 集成应用程序的应用程序列表中进行选择。
- 管理员可以选择定义一个并非基于云应用程序，而是基于用户操作的策略。 唯一受支持的操作是注册安全信息（预览版），允许条件访问围绕组合的安全信息注册体验来强制实施控制。

![定义条件访问策略并指定云应用](./media/concept-conditional-access-cloud-apps/conditional-access-cloud-apps-or-actions.png)

## <a name="azure-cloud-applications"></a>Azure 云应用程序

许多现有的 Azure 云应用程序都包含在你可以从中进行选择的应用程序列表中。 

管理员可以向 Microsoft 提供的以下云应用分配条件访问策略。 某些应用（例如 Office 365（预览版）和 Azure 管理）包含多个相关的子应用或服务。 以下列表并不完整，且随时可能会更改。

- [Office 365（预览版）](#office-365-preview)
- Azure Analysis Services
- Azure DevOps
- Azure SQL 数据库和数据仓库
- Dynamics CRM Online
- Microsoft Application Insights Analytics
- [Azure 管理](#microsoft-azure-management)
- Azure 订阅管理
- Microsoft Cloud App Security
- Microsoft Commerce Tools 访问控制门户
- Microsoft Commerce Tools 身份验证服务
- Microsoft Flow
- Microsoft Forms
- Microsoft Intune
- [Microsoft Intune 注册](https://docs.microsoft.com/intune/enrollment/multi-factor-authentication)
- Microsoft Planner
- Microsoft PowerApps
- Microsoft 必应搜索
- Microsoft StaffHub
- Microsoft Stream
- Microsoft Teams
- Office 365 Exchange Online
- Office 365 SharePoint Online
- Office 365 Yammer
- Office Delve
- Office Sway
- Outlook Groups
- Power BI 服务
- Project Online
- Skype for Business Online
- 虚拟专用网络 (VPN)
- Windows Defender ATP

### <a name="office-365-preview"></a>Office 365（预览版）

Office 365 提供基于云的生产力和协作服务，如 Exchange、SharePoint 和 Microsoft Teams。 Office 365 云服务已深度集成，以确保提供顺利的协作体验。 在创建策略时，这种集成可能会造成混淆，因为某些应用（如 Microsoft Teams）依赖于 SharePoint 或 Exchange 等其他一些应用。

在 Office 365（预览版）应用中可以一次性将所有这些服务作为目标。 我们建议使用新的 Office 365（预览版）应用，而不要将单个云应用作为目标，以免[服务依赖关系](service-dependencies.md)出现问题。 将这一组应用程序作为目标有助于避免因策略和依赖关系不一致而导致的问题。

如果需要，管理员可以选择从策略中排除特定的应用，只需在策略中包含 Office 365（预览版）应用，并排除所选的特定应用即可。

Office 365（预览版）客户端应用中包含的关键应用程序：

   - Microsoft Flow
   - Microsoft Forms
   - Microsoft Stream
   - 微软待办
   - Microsoft Teams
   - Office 365 Exchange Online
   - Office 365 SharePoint Online
   - Office 365 Search Service
   - Office 365 Yammer
   - Office Delve
   - Office Online
   - Office.com
   - OneDrive
   - PowerApps
   - Skype for Business Online
   - Sway

### <a name="azure-management"></a>Azure 管理

Azure 管理应用程序包括多个基础服务。 

   - Azure 门户
   - Azure 资源管理器提供程序
   - 经典部署模型 API
   - Azure PowerShell
   - Visual Studio 订阅管理员门户
   - Azure DevOps
   - Azure 数据工厂门户

> [!NOTE]
> Azure 管理应用程序适用于调用 Azure 资源管理器 API 的 Azure PowerShell。 它不适用于 Azure AD PowerShell，后者调用 Microsoft Graph。

## <a name="other-applications"></a>其他应用程序

除 Microsoft 应用以外，管理员还可以将任何已在 Azure AD 中注册的应用程序添加到条件访问策略。 

> [!NOTE]
> 由于条件访问策略规定了有关访问服务的要求，因此你无法将其应用于客户端（公共/本机）应用程序。 换句话说，该策略不是直接在客户端（公共/本机）应用程序上设置的，而是在客户端调用服务时应用的。 例如，在 SharePoint 服务上设置的策略将应用于调用 SharePoint 的客户端。 在 Exchange 上设置的策略将应用于使用 Outlook 客户端访问电子邮件的尝试。 正因如此，云应用选取器没有客户端（公共/本机）应用程序可供选择，并且在租户中注册的客户端（公共/本机）应用程序的应用程序设置中未提供条件访问选项。 


## <a name="user-actions"></a>用户操作

用户操作是可由用户执行的任务。 目前唯一支持的操作是“注册安全信息”。当启用了组合注册功能的用户尝试注册其安全信息时，此操作允许条件访问策略来强制实施。

## <a name="next-steps"></a>后续步骤

- [条件访问：条件](concept-conditional-access-conditions.md)

- [条件访问常见策略](concept-conditional-access-policy-common.md)
- [客户端应用程序依赖关系](service-dependencies.md)

