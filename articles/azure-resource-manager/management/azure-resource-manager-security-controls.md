---
title: 安全控件
description: 用于评估 Azure 资源管理器服务的内置安全控制的清单。
ms.topic: conceptual
origin.date: 09/04/2019
author: rockboyfor
ms.date: 08/24/2020
ms.testscope: no
ms.testdate: ''
ms.author: v-yeche
ms.openlocfilehash: 6e02df5f571c390e385856c19c8e157a084466ac
ms.sourcegitcommit: 601f2251c86aa11658903cab5c529d3e9845d2e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88807703"
---
<!--Verify successfully-->
# <a name="security-controls-for-azure-resource-manager"></a>Azure 资源管理器的安全控制

本文介绍 Azure 资源管理器中内置的安全控制。

[!INCLUDE [Security controls Header](../../../includes/security-controls-header.md)]

## <a name="data-protection"></a>数据保护

| 安全控制 | Yes/No | 注释 |
|---|---|--|
| 服务器端静态加密：Azure 托管的密钥 | 是 |  |
| 传输中加密（例如 ExpressRoute 加密、VNet 中加密，以及 VNet-VNet 加密）| 是 | HTTPS/TLS。 |
| 服务器端静态加密：客户管理的密钥 (BYOK) | 空值 | Azure 资源管理器不存储客户内容，仅存储控制数据。 |
| 列级加密（Azure 数据服务）| 是 | |
| 加密的 API 调用| 是 | |

## <a name="network"></a>网络

| 安全控制 | Yes/No | 注释 |
|---|---|--|
| 服务终结点支持| 否 | |
| VNet 注入支持| 是 | |
| 网络隔离和防火墙支持| 否 |  |
| 强制隧道支持| 否 |  |

## <a name="monitoring--logging"></a>监视和日志记录

| 安全控制 | Yes/No | 注释|
|---|---|--|
| Azure 监视支持（Log Analytics、App Insights 等）| 否 | |
| 控制和管理平面日志记录和审核| 是 | 活动日志公开对资源执行的所有写入操作（PUT、POST、DELETE）；请参阅[查看活动日志来审核对资源的操作](view-activity-logs.md)。 |
| 数据平面日志记录和审核| 不适用 | |

## <a name="identity"></a>标识

| 安全控制 | Yes/No | 注释|
|---|---|--|
| 身份验证| 是 | 基于 [Azure Active Directory](../../active-directory/index.yml)。|
| 授权| 是 | |

## <a name="configuration-management"></a>配置管理

| 安全控制 | Yes/No | 注释|
|---|---|--|
| 配置管理支持（配置的版本控制等）| 是 |  |

## <a name="next-steps"></a>后续步骤

- 详细了解[跨 Azure 服务的内置安全控制](../../security/fundamentals/security-controls.md)。

<!-- Update_Description: update meta properties, wording update, update link -->