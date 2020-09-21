---
title: 适用于虚拟机的 Azure 专用主机概述
description: 详细了解如何使用 Azure 专用主机部署虚拟机。
author: Johnnytechn
ms.service: virtual-machines
ms.topic: article
origin.date: 01/09/2020
ms.date: 09/03/2020
ms.author: v-johya
ms.openlocfilehash: 12d2367cac9584010b7c3080387c7e3eff06d934
ms.sourcegitcommit: f45809a2120ac7a77abe501221944c4482673287
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2020
ms.locfileid: "90057603"
---
<!--Verified successfully-->
# <a name="azure-dedicated-hosts-for-virtual-machines"></a>适用于虚拟机的 Azure 专用主机

Azure 专用主机是一种提供物理服务器（能够托管一个或多个虚拟机）的服务，专用于一个 Azure 订阅。 专用主机是数据中心中使用的相同物理服务器，作为资源提供。 你可以在区域和容错域中预配专用主机。 然后，可以按照最能满足你的需要的配置将 VM 直接放入预配的主机中。

<!--Not Available on  availability zone-->

[!INCLUDE [virtual-machines-common-dedicated-hosts](../../../includes/virtual-machines-common-dedicated-hosts.md)]


## <a name="next-steps"></a>后续步骤

- 可以使用 [Azure CLI](dedicated-hosts-cli.md)、[门户](dedicated-hosts-portal.md)和 [PowerShell](../windows/dedicated-hosts-powershell.md) 来部署专用主机。

- 有关详细信息，请参阅[专用主机](dedicated-hosts.md)概述。

<!--Not Available on [here](https://github.com/Azure/azure-quickstart-templates/blob/master/201-vm-dedicated-hosts/README.md)-->

<!--Not Available on [Reserved Instance of Azure Dedicated Hosts](../prepay-dedicated-hosts-reserved-instances.md)-->
