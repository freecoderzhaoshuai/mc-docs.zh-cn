---
title: 如何将用户分配给应用程序 | Microsoft Docs
description: 了解如何将用户分配给租户中的应用程序
services: active-directory
documentationcenter: ''
author: kenwith
manager: celestedg
ms.assetid: ''
ms.service: active-directory
ms.subservice: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 09/08/2020
ms.author: v-junlch
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5526e49a4039b113f8f7bf8529b4a91e40ab38d7
ms.sourcegitcommit: 25d542cf9c8c7bee51ec75a25e5077e867a9eb8b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89593816"
---
# <a name="how-to-assign-users-to-applications"></a>如何将用户分配给应用程序

本文介绍如何将用户分配给租户中的应用程序。

## <a name="how-do-users-get-assigned-to-an-application-in-azure-ad"></a>如何将用户分配给 Azure AD 中的应用程序？

用户要访问应用程序，必须先以某种方式将其分配给该应用程序。 可使用管理员、业务委托，或有时使用用户本身的身份执行分配。 下文介绍了可以将用户分配给应用程序的方式：

1.  管理员直接[将用户分配给](/active-directory/active-directory-coreapps-assign-user-azure-portal)应用程序

2.  管理员[将用户是其成员的组分配](/active-directory/active-directory-coreapps-assign-user-azure-portal)给应用程序，包括：

    * 已从本地同步的组

    * 在云中创建的静态安全组

    * 在云中创建的 Office 365 组

    * [所有用户](/active-directory/fundamentals/active-directory-groups-create-azure-portal)组

5.  管理员启用[自助服务组管理](../users-groups-roles/groups-self-service-management.md)以允许用户**无需业务批准**，即可加入已对其分配应用程序的组

6.  管理员启用[自助服务组管理](../users-groups-roles/groups-self-service-management.md)以允许用户在经过**选定业务批准者的事先批准**的情况下，加入已对其分配应用程序的组

7.  对于第一方应用程序，如 [ Microsoft Office 365](https://products.office.com/)，管理员直接为用户分配许可证

8.  对于第一方应用程序，如 [ Microsoft Office 365](https://products.office.com/)，管理员直接为用户是其成员的组分配许可证

9.  [管理员同意](/active-directory/develop/active-directory-devhowto-multi-tenant-overview)所有用户均可使用某个应用程序，然后用户登录该应用程序

10. 通过登录应用程序，用户自己[同意使用应用程序](/active-directory/develop/active-directory-devhowto-multi-tenant-overview)



