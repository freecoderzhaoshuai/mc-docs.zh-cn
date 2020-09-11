---
title: include 文件
description: include 文件
services: vpn-gateway
author: WenJason
ms.service: vpn-gateway
ms.topic: include
origin.date: 08/14/2019
ms.date: 09/07/2020
ms.author: v-jay
ms.custom: include file
ms.openlocfilehash: 061e5bad2fd0f0c7de277116d316204e05cca4d7
ms.sourcegitcommit: 22e1da9309795e74a91b7241ac5987a802231a8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2020
ms.locfileid: "89464251"
---
以下配置用于执行下面的步骤：

- 计算机：Ubuntu Server 18.04
- 依赖项：strongSwan


使用以下命令安装所需的 strongSwan 配置：

```
sudo apt install strongswan
```

```
sudo apt install strongswan-pki
```

```
sudo apt install libstrongswan-extra-plugins
```

使用以下命令安装 Azure 命令行接口：

```
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

[有关如何安装 Azure CLI 的其他说明](/cli/install-azure-cli-apt?view=azure-cli-latest)
