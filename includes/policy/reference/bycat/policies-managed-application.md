---
ms.service: azure-policy
ms.topic: include
origin.date: 09/10/2020
author: rockboyfor
ms.date: 09/21/2020
ms.testscope: yes|no
ms.testdate: 09/21/2020null
ms.author: v-yeche
ms.custom: generated
ms.openlocfilehash: 9c97b4c8496bdefe6750e71a6b16e4ae8435fd4f
ms.sourcegitcommit: 41e986cd4a2879d8767dc6fc815c805e782dc7e6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2020
ms.locfileid: "90822440"
---
<!--Verified successfully-->

|名称<br /><sub>（Azure 门户）</sub> |说明 |效果 |版本<br /><sub>(GitHub)</sub> |
|---|---|---|---|
|[托管应用程序的应用程序定义应使用客户提供的存储帐户](https://portal.azure.cn/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F9db7917b-1607-4e7d-a689-bca978dd0633) |如果这是法规或合规性要求，请使用自己的存储帐户来控制应用程序定义数据。 可以选择将托管应用程序定义存储在创建过程中提供的存储帐户中，以便你能够对其位置和访问权限进行完全管理，以符合法规或合规性要求。 |审核、拒绝、已禁用 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Managed%20Application/ApplicationDefinition_Missing_StorageAccount_Deny.json) |

<!--Not Available on 09/17/2020 |[Deploy associations for a managed application](https://portal.azure.cn/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F17763ad9-70c0-4794-9397-53d765932634) |Deploys an association resource that associates selected resource types to the specified managed application.  This policy deployment does not support nested resource types. |deployIfNotExists |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Managed%20Application/AssociationForManagedApplication_Deploy.json)-->

<!-- Update_Description: new article about policies managed application -->
<!--NEW.date: 09/21/2020-->