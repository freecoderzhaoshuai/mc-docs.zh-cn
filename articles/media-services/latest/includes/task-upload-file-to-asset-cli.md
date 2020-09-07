---
author: WenJason
ms.service: media-services
ms.topic: include
origin.date: 08/17/2020
ms.date: 09/07/2020
ms.author: v-jay
ms.custom: CLI
ms.openlocfilehash: 45a804f3f19b9ed3043d716ad8627f89436e4838
ms.sourcegitcommit: 2eb5a2f53b4b73b88877e962689a47d903482c18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89414089"
---
<!-- ### Upload files with the CLI -->

以下命令上传单个文件。  

更改以下值：

1. 将 `/path/to/file` 更改为文件的本地路径。  
1. 将 `MyContainer` 更改为先前使用资产 ID（而非名称）创建的资产。
1. 将 `MyBlob` 更改为想要用于已上传的文件的名称。
1. 将 `MyStorageAccountName` 更改为正在使用的存储帐户的名称。
1. 将 `MyStorageAccountKey` 更改为存储帐户的访问密钥。

    ```azurecli
    az storage blob upload -f /path/to/file -c MyContainer -n MyBlob --acount-name MyStorageAccountName --account-key MyStorageAccountKey
    ```
