---
author: msmbaldwin
ms.service: key-vault
ms.topic: include
origin.date: 09/03/2020
ms.date: 09/16/2020
ms.author: v-tawe
ms.openlocfilehash: cb9381f750f4e8f36aaefcc40240d27b08b1a1a7
ms.sourcegitcommit: 39410f3ed7bdeafa1099ba5e9ec314b4255766df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2020
ms.locfileid: "90678362"
---
1. 请确保你具有[活动订阅的 Azure 帐户](https://wd.azure.cn/pricing/1rmb-trial/)。

1. 安装 [Python 2.7+ 或 3.5.3+](https://www.python.org/downloads)。

1. 安装 [Azure CLI](/cli/install-azure-cli)。

1. 按照[为本地开发配置身份验证](https://docs.microsoft.com/azure/developer/python/configure-local-development-environment?tabs=cmd#configure-authentication)的说明操作，使用该说明创建本地服务主体，并通过环境变量将其提供给 Python 的 Azure Key Vault 客户端。 

    直接在 Azure 上运行代码时，如果应用使用托管标识，则不需要单独的服务主体。

1. 在终端或命令提示符中，创建合适的项目文件夹，然后创建并激活 Python 虚拟环境，如[使用 Python 虚拟环境](https://docs.microsoft.com/azure/developer/python/configure-local-development-environment?tabs=cmd#use-python-virtual-environments)中所述

1. 安装 Azure Active Directory 标识库：

    ```terminal
    pip install azure.identity
    ```
