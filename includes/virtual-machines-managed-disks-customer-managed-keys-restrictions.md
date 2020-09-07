---
title: 包含文件
description: 包含文件
services: virtual-machines
author: rockboyfor
ms.service: virtual-machines
ms.topic: include
origin.date: 07/10/2020
ms.date: 08/24/2020
ms.testscope: yes
ms.testdate: 08/24/2020
ms.author: v-yeche
ms.custom: include file
ms.openlocfilehash: 1cb22c744da3fe9709c7815d84a7b74b0731a132
ms.sourcegitcommit: b5ea35dcd86ff81a003ac9a7a2c6f373204d111d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88946901"
---
<!--Verify Successfully-->
- 仅支持大小为 2048 位、3,072 位和 4,096 位的[软件密钥](../articles/key-vault/keys/about-keys.md)，不支持其他密钥或其他大小。

    <!--Not Available on and HSM RSA keys-->
    <!--Not Available on - [HSM](../articles/key-vault/keys/hsm-protected-keys.md) keys require the **premium** tier of Azure Key vaults.-->
    
- 从使用服务器端加密和客户托管密钥加密的自定义映像创建的磁盘必须使用相同的客户托管密钥进行加密，且必须位于同一订阅中。
- 从使用服务器端加密和客户托管密钥加密的磁盘创建的快照必须使用相同的客户托管密钥进行加密。
- 与客户托管密钥相关的所有资源（Azure Key Vault、磁盘加密集、VM、磁盘和快照）都必须位于同一订阅和区域中。
- 使用客户托管密钥加密的磁盘、快照和映像不能移至另一个订阅。
- 使用客户托管密钥加密的托管磁盘也不能使用 Azure 磁盘加密进行加密。
- 每个区域、每个订阅最多只能创建 50 个磁盘加密集。

<!--Not Available on [Preview: Use customer-managed keys for encrypting images](../image-version-encryption.md)-->
<!-- Update_Description: new article about virtual machines managed disks customer managed keys restrictions -->
<!--NEW.date: 08/10/2020-->

