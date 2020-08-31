---
author: ggailey777
ms.service: azure-functions
ms.topic: include
ms.date: 07/01/2020
ms.author: v-junlch
ms.openlocfilehash: 80c981d20345752d44eb84956c6767c2c780327a
ms.sourcegitcommit: 9d9795f8a5b50cd5ccc19d3a2773817836446912
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88947136"
---
Azure 存储可对存储帐户中的所有数据进行静态加密。 有关详细信息，请参阅[静态数据的 Azure 存储加密](../articles/storage/common/storage-service-encryption.md)。

默认情况下，数据使用 Microsoft 管理的密钥进行加密。 为了进一步控制加密密钥，可以提供客户管理的密钥，用于对 blob 和文件数据进行加密。 这些密钥必须存在于 Azure Key Vault 中，以便 Functions 能够访问存储帐户。

<!-- To learn more, see [Encryption at rest using customer-managed keys](../articles/azure-functions/configure-encrypt-at-rest-using-cmk.md).   -->

