---
title: include 文件
description: include 文件
services: storage
author: WenJason
ms.service: storage
ms.topic: include
origin.date: 12/20/2019
ms.date: 08/24/2020
ms.author: v-jay
ms.custom: include file
ms.openlocfilehash: 4c0d6892d82ffc87629daa69f38d97c8be79cf25
ms.sourcegitcommit: ecd6bf9cfec695c4e8d47befade8c462b1917cf0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2020
ms.locfileid: "88753339"
---
使用共享访问签名 (SAS)，可以授予对存储帐户中容器和 blob 的有限访问权限。 创建 SAS 时，需要指定其约束条件，包括允许客户端访问哪些 Azure 存储资源、它们对这些资源具有哪些权限，以及 SAS 的有效期。

每个 SAS 均使用密钥进行签名。 可通过以下两种方式之一对 SAS 进行签名：

- 使用 Azure Active Directory (Azure AD) 凭据创建的密钥。 使用 Azure AD 凭据签名的 SAS 是用户委托 SAS。
- 使用存储帐户密钥。 服务 SAS 和帐户 SAS 均使用存储帐户密钥进行签名。  

用户委托 SAS 为使用存储帐户密钥签名的 SAS 提供更高的安全性。 Microsoft 建议尽可能使用用户委托 SAS。 有关详细信息，请参阅[向具有共享访问签名的数据授予有限的访问权限 (SAS)](../articles/storage/common/storage-sas-overview.md)。
