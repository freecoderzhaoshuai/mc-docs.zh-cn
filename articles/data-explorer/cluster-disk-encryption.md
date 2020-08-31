---
title: 在 Azure 数据资源管理器中使用磁盘加密保护群集 - Azure 门户
description: 本文介绍如何通过 Azure 门户在 Azure 数据资源管理器中使用磁盘加密保护群集。
author: orspod
ms.author: v-tawe
ms.reviewer: gabil
ms.service: data-explorer
ms.topic: conceptual
origin.date: 08/02/2020
ms.date: 08/18/2020
ms.openlocfilehash: d2556cd625e023b1e25699df13f4d43a8f28b1d4
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88556477"
---
# <a name="secure-your-cluster-using-disk-encryption-in-azure-data-explorer---azure-portal"></a>在 Azure 数据资源管理器中使用磁盘加密保护群集 - Azure 门户

[Azure 磁盘加密](/security/azure-security-disk-encryption-overview)有助于保护数据，使组织能够信守在安全性与合规性方面作出的承诺。 它为群集虚拟机的 OS 和数据磁盘提供卷加密。 它还与 [Azure Key Vault](/key-vault/) 集成，使我们可以控制和管理磁盘加密密钥和机密，并确保 VM 磁盘上的所有数据已加密。 
  
## <a name="enable-encryption-at-rest-in-the-azure-portal"></a>在 Azure 门户中启用静态加密
  
通过群集安全设置可以在群集上启用磁盘加密。 在群集上启用[静态加密](/security/fundamentals/encryption-atrest)可为存储的数据（静态数据）提供数据保护。 

1. 在 Azure 门户中，转到 Azure 数据资源管理器群集资源。 在“设置”标题下，选择“安全性” 。 

    ![启用静态加密](media/manage-cluster-security/security-encryption-at-rest.png)

1. 在“安全性”窗口中，为“磁盘加密”安全设置选择“打开”。 

1. 选择“保存” 。
 
> [!NOTE]
> 启用加密后，选择“关闭”可禁用加密。

## <a name="azure-data-explorer-stores-data-within-a-region"></a>Azure 数据资源管理器将数据存储在区域中

每个 Azure 数据资源管理器群集都在单个区域中的专用资源上运行。 所有数据都存储在该区域中。 

## <a name="next-steps"></a>后续步骤

[检查群集运行状况](check-cluster-health.md)
