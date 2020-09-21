---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
origin.date: 09/10/2020
ms.date: 09/15/2020
ms.author: v-tawe
ms.custom: generated
ms.openlocfilehash: bceae44290750d42b69b313d154224fc6b2b2215
ms.sourcegitcommit: f5d53d42d58c76bb41da4ea1ff71e204e92ab1a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90524010"
---
|名称<br /><sub>（Azure 门户）</sub> |说明 |效果 |版本<br /><sub>(GitHub)</sub> |
|---|---|---|---|
|[容器注册表应使用客户托管密钥 (CMK) 进行加密](https://portal.azure.cn/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5b9159ae-1701-4a6f-9a7a-aa9c8ddd0580) |审核未通过客户管理的密钥 (CMK) 启用加密的容器注册表。 Azure 会自动用服务管理的密钥来加密静态注册表内容。 可以使用在 Azure Key Vault 中创建和管理的密钥，通过一个附加的加密层来补充默认加密。 有关 CMK 加密的详细信息，请访问：[https://docs.azure.cn/container-registry/container-registry-customer-managed-keys](https://docs.azure.cn/container-registry/container-registry-customer-managed-keys)。 |Audit、Disabled |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Container%20Registry/ACR_CMKEncryptionEnabled_Audit.json) |
|[容器注册表不得允许无限制的网络访问](https://portal.azure.cn/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd0793b48-0edc-4296-a390-4c75d1bdfd71) |审核容器注册表，这些注册表默认情况下未配置任何网络或防火墙 (IP) 规则，因此允许所有网络访问。 限制网络访问可防止容器注册表出现潜在的威胁。 如果容器注册表至少有一个 IP/防火墙规则或配置了虚拟网络，则会将其视为合规。 有关 Azure 容器注册表网络规则的详细信息，请访问：[https://docs.azure.cn/container-registry/container-registry-access-selected-networks](https://docs.azure.cn/container-registry/container-registry-access-selected-networks) 和 [https://docs.azure.cn/container-registry/container-registry-vnet](https://docs.azure.cn/container-registry/container-registry-vnet) |Audit、Disabled |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Container%20Registry/ACR_NetworkRulesExist_Audit.json) |

<!-- |[Container registries should use private links](https://portal.azure.cn/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe8eef0a8-67cf-4eb4-9386-14b0e78733d4) |Audit container registries that do not have at least one approved private endpoint connection. Clients in a virtual network can securely access resources that have private endpoint connections through private links. Public access can then be disabled to ensure that only private links can be used to connect to the registry. For more information, visit: [https://aka.ms/acr/private-link](https://aka.ms/acr/private-link). |Audit, Disabled |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Container%20Registry/ACR_PrivateEndpointEnabled_Audit.json) | -->
