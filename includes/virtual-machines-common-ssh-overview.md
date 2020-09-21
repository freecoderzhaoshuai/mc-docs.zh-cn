---
title: include 文件
description: include 文件
services: virtual-machines-linux
author: rockboyfor
ms.service: virtual-machines-linux
ms.topic: include
origin.date: 07/09/2020
ms.date: 08/10/2020
ms.testscope: yes|no
ms.testdate: 11/11/2019
ms.author: v-yeche
ms.custom: include file
ms.openlocfilehash: 4d1ef38fd4601133edb345a62dc94b858bad4fc6
ms.sourcegitcommit: ac70b12de243a9949bf86b81b2576e595e55b2a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "90057697"
---
## <a name="overview-of-ssh-and-keys"></a>SSH 和密钥概述

[SSH](https://www.ssh.com/ssh/) 是一种加密的连接协议，利用该协议可以通过未受保护的连接进行安全登录。 SSH 是在 Azure 中托管的 Linux VM 的默认连接协议。 虽然 SSH 提供加密连接，但是将密码用于 SSH 连接仍会使 VM 易受到暴力攻击。 建议使用公钥-私钥对（也称为“SSH 密钥”）通过 SSH 连接到 VM。 

- 公钥放置在 Linux VM 上。

- *私钥*仍保留在本地系统上。 请保护好私钥， 不要透露给其他人。

当你使用 SSH 客户端连接到 Linux VM（具有公钥）时，远程 VM 会测试客户端以确保其具有正确的私钥。 如果客户端具有私钥，则授予其访问 VM 的权限。 

根据组织的安全策略，可重复使用单个公钥-私钥对来访问多个 Azure VM 和服务。 无需对要访问的每个 VM 或服务使用单独的密钥对。 

可与任何人共享公钥；但只有你（或本地安全基础结构）才应具有对私钥的访问权限。

<!-- Update_Description: update meta properties, wording update, update link -->