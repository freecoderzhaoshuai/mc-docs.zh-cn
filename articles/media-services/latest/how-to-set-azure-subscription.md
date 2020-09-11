---
title: 如何查找 Azure 订阅
description: 查找 Azure 订阅，以便设置环境。
services: media-services
documentationcenter: ''
author: WenJason
manager: digimobile
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to
origin.date: 03/15/2020
ms.date: 09/07/2020
ms.author: v-jay
ms.custom: cli,portal
ms.openlocfilehash: a3f7da5bfb15343d6ef769b61b9bd17b8e07e8d9
ms.sourcegitcommit: 2eb5a2f53b4b73b88877e962689a47d903482c18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89414090"
---
# <a name="find-your-azure-subscription"></a>查找你的 Azure 订阅

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="portal"></a>[Portal](#tab/portal/)

## <a name="use-the-azure-portal"></a>使用 Azure 门户

1. 登录到 [Azure 门户](https://portal.azure.cn)。
1. 在“Azure 服务”标题下，选择“订阅”。 （如果未列出任何订阅，可能需要切换 Azure AD 租户。）订阅 ID 在第二列中列出。
1. 复制订阅 ID 并将其粘贴到所选的文本文档中供稍后使用。

## <a name="cli"></a>[CLI](#tab/cli/)

## <a name="use-the-azure-cli"></a>使用 Azure CLI

<!-- NOTE: The following are in the includes file and are reused in other How To articles. All task based content should be in the includes folder with the "task-" prepended to the file name. -->

### <a name="list-your-azure-subscriptions-with-cli"></a>使用 CLI 列出 Azure 订阅

[!INCLUDE [List your Azure subscriptions with CLI](./includes/task-list-set-subscription-cli.md)]

### <a name="see-also"></a>另请参阅

* [Azure CLI](https://docs.microsoft.com/cli/azure/ams?view=azure-cli-latest)

---

## <a name="next-steps"></a>后续步骤

[流式传输文件](stream-files-dotnet-quickstart.md)
