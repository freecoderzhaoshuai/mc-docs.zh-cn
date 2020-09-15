---
author: rockboyfor
ms.service: azure-policy
ms.topic: include
origin.date: 07/10/2020
ms.date: 09/14/2020
ms.testscope: no
ms.testdate: 09/14/2020
ms.author: v-yeche
ms.custom: generated
ms.openlocfilehash: 455c0864b8d0af75f2d7bc4f41d59b88931da731
ms.sourcegitcommit: 78c71698daffee3a6b316e794f5bdcf6d160f326
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90021340"
---
<!--Verified successfully-->
|名称<br /><sub>（Azure 门户）</sub> |说明 |效果 |版本<br /><sub>(GitHub)</sub> |
|---|---|---|---|
|[容器注册表应使用客户托管密钥 (CMK) 进行加密](https://portal.azure.cn/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5b9159ae-1701-4a6f-9a7a-aa9c8ddd0580) |审核未通过客户托管密钥 (CMK) 启用加密的容器注册表。 有关 CMK 加密的详细信息，请访问：[https://aka.ms/acr/CMK](https://docs.azure.cn/container-registry/container-registry-customer-managed-keys)。 |Audit、Disabled |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Container%20Registry/ACR_CMKEncryptionEnabled_Audit.json) |
|[容器注册表不得允许无限制的网络访问](https://portal.azure.cn/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd0793b48-0edc-4296-a390-4c75d1bdfd71) |审核容器注册表，这些注册表默认情况下未配置任何网络（IP 或 VNET）规则，因此允许所有网络访问。 如果容器注册表至少有一个 IP/防火墙规则或配置了虚拟网络，则会将其视为合规。 有关容器注册表网络规则的详细信息，请访问：[https://aka.ms/acr/vnet](https://docs.azure.cn/container-registry/container-registry-vnet)。 |Audit、Disabled |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Container%20Registry/ACR_NetworkRulesExist_Audit.json) |
|[容器注册表应使用专用链接](https://portal.azure.cn/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe8eef0a8-67cf-4eb4-9386-14b0e78733d4) |审核没有达到“至少有一个已批准的专用终结点连接”标准的容器注册表。 虚拟网络中的客户端可以安全地访问通过专用链接获得专用终结点连接的资源。 有关详细信息，请访问：[https://aka.ms/acr/private-link](https://docs.azure.cn/container-registry/container-registry-private-link)。 |Audit、Disabled |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Container%20Registry/ACR_PrivateEndpointEnabled_Audit.json) |
|[容器注册表应使用虚拟网络服务终结点](https://portal.azure.cn/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc4857be7-912a-4c75-87e6-e30292bcdf78) |此策略审核任何未配置为使用虚拟网络服务终结点的容器注册表。 |Audit、Disabled |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Network/VirtualNetworkServiceEndpoint_ContainerRegistry_Audit.json) |

<!--MOONCAKE CUSTOMIZATION: Redirect from https://aka.ms/acr/ to http://docs.azure.cn-->
<!-- Update_Description: update meta properties, wording update, update link -->