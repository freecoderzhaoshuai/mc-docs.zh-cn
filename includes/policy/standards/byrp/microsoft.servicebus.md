---
ms.service: azure-policy
ms.topic: include
origin.date: 07/22/2020
author: rockboyfor
ms.date: 08/31/2020
ms.testscope: yes
ms.testdate: 08/17/2020
ms.author: v-yeche
ms.custom: generated
ms.openlocfilehash: 7c94da4369bb073b2f31e78e8e96f3b94504f255
ms.sourcegitcommit: b5ea35dcd86ff81a003ac9a7a2c6f373204d111d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88947616"
---
<!--Verify Successfully-->
## <a name="azure-security-benchmark"></a>Azure 安全基准

[Azure 安全基准](../../../../articles/security/benchmarks/overview.md)提供有关如何在 Azure 上保护云解决方案的建议。 若要查看此服务如何完全映射到 Azure 安全基准，请参阅 [Azure 安全基准映射文件](https://github.com/MicrosoftDocs/SecurityBenchmarks/tree/master/Azure%20Offer%20Security%20Baselines)。

<!--Not Avaialble on [Azure Policy Regulatory Compliance - Azure Security Benchmark](../../../../articles/governance/policy/samples/azure-security-benchmark.md)-->

|域 |控制 ID |控制标题 |策略<br /><sub>（Azure 门户）</sub> |Policy 版本<br /><sub>(GitHub)</sub>  |
|---|---|---|---|---|
|网络安全 |1.1 |在虚拟网络上使用网络安全组或 Azure 防火墙来保护资源 |[服务总线应使用虚拟网络服务终结点](https://portal.azure.cn/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F235359c5-7c52-4b82-9055-01c75cf9f60e) |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Network/VirtualNetworkServiceEndpoint_ServiceBus_AuditIfNotExists.json) |
|日志记录和监视 |2.3 |为 Azure 资源启用审核日志记录 |[应启用服务总线的诊断日志](https://portal.azure.cn/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff8d36e2f-389b-4ee4-898d-21aeb69a0f45) |[3.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Service%20Bus/ServiceBus_AuditDiagnosticLog_Audit.json) |

<!-- Update_Description: new article about microsoft.servicebus -->
<!--NEW.date: 08/17/2020-->