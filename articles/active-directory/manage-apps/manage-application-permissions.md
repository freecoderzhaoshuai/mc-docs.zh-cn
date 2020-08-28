---
title: 管理用户和管理员权限 - Azure Active Directory | Microsoft Docs
description: 了解如何在 Azure AD 上查看和管理应用程序的权限。 例如，如果要撤消授予应用程序的所有权限。
services: active-directory
author: mimart
manager: CelesteDG
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.topic: conceptual
ms.date: 08/14/2020
ms.author: v-junlch
ms.reviewer: luleonpla
ms.collection: M365-identity-device-management
ms.openlocfilehash: 012e0128df5b1dabe440f4f11dfc13e34fe67498
ms.sourcegitcommit: 7646936d018c4392e1c138d7e541681c4dfd9041
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88648081"
---
# <a name="take-action-on-overpriviledged-or-suspicious-application-in-azure-active-directory"></a>对 Azure Active Directory 中拥有过度特权的或可疑的应用程序采取措施

了解如何查看和管理应用程序权限。 根据方案，本文将提供可执行以保护应用程序安全的不同操作。 这适用于通过用户或管理员同意添加到 Azure Active Directory (Azure AD) 租户的所有应用程序。

有关许可应用程序的详细信息，请参阅 [Azure Active Directory 许可框架](../develop/consent-framework.md)。

## <a name="prerequisites"></a>先决条件

若要执行以下操作，需要以全局管理员、应用程序管理员或云应用程序管理员的身份登录。

若要限制对应用程序的访问，你需要要求用户分配，然后将用户或组分配到应用程序。  有关详细信息，请参阅[分配用户和组的方法](methods-for-assigning-users-and-groups.md)。

可以访问 Azure AD 门户，获取上下文 PowerShell 脚本来执行这些操作。
 
1. 以全局管理员、应用程序管理员或云应用程序管理员的身份登录到 [Azure 门户](https://portal.azure.cn)。
2. 选择“Azure Active Directory” > “企业应用程序”。 
3. 选择要限制访问的应用程序。
4. 选择“权限”。 在命令栏中，选择“检查权限”。

![检查权限](./media/manage-application-permissions/review-permissions.png)

## <a name="i-want-to-control-access-to-an-application"></a>我想要控制对应用程序的访问

建议打开“用户分配”设置来限制对此应用程序的访问。

1. 以全局管理员、应用程序管理员或云应用程序管理员的身份登录到 [Azure 门户](https://portal.azure.cn)。
2. 选择“Azure Active Directory” > “企业应用程序”。 
3. 选择要限制访问的应用程序。
4. 选择“属性”，然后将用户要求所需设置为“是”。
5. 选择“用户和组”，然后删除分配给该应用程序的不需要的用户。
6. 将用户或组分配给应用程序。

（可选）你可以使用 PowerShell 删除分配给该应用程序的所有用户。

## <a name="i-want-to-revoke-all-permissions-for-an-application"></a>我想要撤销应用程序的所有权限

使用 PowerShell 将撤消授予此应用程序的所有权限。

（可选）你可以禁用应用程序以阻止用户访问应用并阻止应用程序访问数据。

1. 以全局管理员、应用程序管理员或云应用程序管理员的身份登录到 [Azure 门户](https://portal.azure.cn)。
2. 选择“Azure Active Directory” > “企业应用程序”。 
3. 选择要限制访问的应用程序。
4. 选择“属性”，然后将“启用以供用户登录?”设置为“否” 。

## <a name="application-is-suspicious-and-i-want-to-investigate"></a>应用程序可疑，我想要进行调查

建议你通过打开“用户分配”设置来限制对此应用程序的访问，并查看用户和管理员已授予该应用程序的权限。

1. 以全局管理员、应用程序管理员或云应用程序管理员的身份登录到 [Azure 门户](https://portal.azure.cn)。
3. 选择“Azure Active Directory” > “企业应用程序”。 
5. 选择要限制访问的应用程序。
6. 选择“属性”，然后将“需要进行用户分配?”设置为“是” 。
7. 选择“权限”并查看管理员和用户许可的权限。

可以选择执行以下操作：

- 使用 PowerShell，删除所有分配的用户，以阻止他们登录到应用程序。
- 使用 PowerShell，使有权访问应用程序的用户的刷新令牌失效。
- 使用 PowerShell，撤消此应用程序的所有权限
- 禁用应用程序以阻止用户访问并阻止此应用程序访问数据。


## <a name="application-is-malicious-and-im-compromised"></a>应用程序为恶意应用程序，我已遭到入侵

建议禁用此应用程序以阻止用户访问应用，并阻止此应用程序访问你的数据。 如果改为删除此应用程序，则最终用户将能够再次同意该应用程序并授予对你的数据的访问权限。

1. 以全局管理员、应用程序管理员或云应用程序管理员的身份登录到 [Azure 门户](https://portal.azure.cn)。
2. 选择“Azure Active Directory” > “企业应用程序”。 
3. 选择要限制访问的应用程序。
4. 选择“属性”，然后复制对象 ID。

### <a name="powershell-commands"></a>PowerShell 命令


检索服务主体对象 ID

1. 以全局管理员、应用程序管理员或云应用程序管理员的身份登录到 [Azure 门户](https://portal.azure.cn)。
2. 选择“Azure Active Directory” > “企业应用程序”。 
3. 选择要限制访问的应用程序。
4. 选择“属性”，然后复制对象 ID。

```powershell
    $sp = Get-AzureADServicePrincipal -Filter "displayName eq '$app_name'"
    $sp.ObjectId
```
删除分配给应用程序的所有用户。
 ```powershell
    Connect-AzureAD -AzureEnvironmentName AzureChinaCloud

    # Get Service Principal using objectId
    $sp = Get-AzureADServicePrincipal -ObjectId "<ServicePrincipal objectID>"

    # Get Azure AD App role assignments using objectId of the Service Principal
    $assignments = Get-AzureADServiceAppRoleAssignment -ObjectId $sp.ObjectId -All $true

    # Remove all users and groups assigned to the application
    $assignments | ForEach-Object {
        if ($_.PrincipalType -eq "User") {
            Remove-AzureADUserAppRoleAssignment -ObjectId $_.PrincipalId -AppRoleAssignmentId $_.ObjectId
        } elseif ($_.PrincipalType -eq "Group") {
            Remove-AzureADGroupAppRoleAssignment -ObjectId $_.PrincipalId -AppRoleAssignmentId $_.ObjectId
        }
    }
 ```

撤消授予应用程序的权限

```powershell
    Connect-AzureAD -AzureEnvironmentName AzureChinaCloud

    # Get Service Principal using objectId
    $sp = Get-AzureADServicePrincipal -ObjectId "<ServicePrincipal objectID>"

    # Get all delegated permissions for the service principal
    $spOAuth2PermissionsGrants = Get-AzureADOAuth2PermissionGrant -All $true| Where-Object { $_.clientId -eq $sp.ObjectId }

    # Remove all delegated permissions
    $spOAuth2PermissionsGrants | ForEach-Object {
        Remove-AzureADOAuth2PermissionGrant -ObjectId $_.ObjectId
    }

    # Get all application permissions for the service principal
    $spApplicationPermissions = Get-AzureADServiceAppRoleAssignedTo -ObjectId $sp.ObjectId -All $true | Where-Object { $_.PrincipalType -eq "ServicePrincipal" }

    # Remove all delegated permissions
    $spApplicationPermissions | ForEach-Object {
        Remove-AzureADServiceAppRoleAssignment -ObjectId $_.PrincipalId -AppRoleAssignmentId $_.objectId
    }
```
使刷新令牌失效
```powershell
        Connect-AzureAD -AzureEnvironmentName AzureChinaCloud

        # Get Service Principal using objectId
        $sp = Get-AzureADServicePrincipal -ObjectId "<ServicePrincipal objectID>"

        # Get Azure AD App role assignments using objectID of the Service Principal
        $assignments = Get-AzureADServiceAppRoleAssignment -ObjectId $sp.ObjectId -All $true | Where-Object {$_.PrincipalType -eq "User"}

        # Revoke refresh token for all users assigned to the application
        $assignments | ForEach-Object {
            Revoke-AzureADUserAllRefreshToken -ObjectId $_.PrincipalId
        }
```

