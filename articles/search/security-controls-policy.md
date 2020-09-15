---
title: Azure 认知搜索的 Azure Policy 法规遵从性控制
description: 列出可用于 Azure 认知搜索的 Azure Policy 法规遵从性控制。 这些内置的策略定义提供了管理 Azure 资源符合性的常用方法。
ms.date: 09/10/2020
origin.date: 07/30/2020
ms.topic: sample
author: HeidiSteen
ms.author: v-tawe
ms.service: search
ms.custom: subject-policy-compliancecontrols
ms.openlocfilehash: ac3557d481a1006df1ce467bce84ef011b414f04
ms.sourcegitcommit: 78c71698daffee3a6b316e794f5bdcf6d160f326
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90021696"
---
# <a name="azure-policy-regulatory-compliance-controls-for-azure-cognitive-search"></a>Azure 认知搜索的 Azure Policy 法规遵从性控制

如果你使用 [Azure Policy](../governance/policy/overview.md) 强制实施 [Azure 安全基准](../security/benchmarks/introduction.md)中的建议，则可能已知道可以创建用于标识和修复不符合服务的策略。 这些策略可以是自定义的，也可以基于内置定义，这些定义针对易于理解的最佳做法提供符合性条件和合适的解决方案。

对于 Azure 认知搜索，当前有一个可以在策略分配中使用的生成定义（在下面列出）。 该内置定义用于日志记录和监视。 通过在[创建的策略](../governance/policy/assign-policy-portal.md)中使用此内置定义，系统将扫描没有[诊断日志记录](search-monitor-logs.md)的搜索服务，然后相应地进行启用。

<!-- [Regulatory Compliance in Azure Policy](../governance/policy/concepts/regulatory-compliance.md)
provides Microsoft-created and managed initiative definitions, known as _built-ins_, for the
**compliance domains** and **security controls** related to different compliance standards. This
page lists the **compliance domains** and **security controls** for Azure Cognitive Search. You can
assign the built-ins for a **security control** individually to help make your Azure resources
compliant with the specific standard. -->

[!INCLUDE [azure-policy-compliancecontrols-introwarning](../../includes/policy/standards/intro-warning.md)]

[!INCLUDE [azure-policy-compliancecontrols-search](../../includes/policy/standards/byrp/microsoft.search.md)]

## <a name="next-steps"></a>后续步骤

<!-- - Learn more about [Azure Policy Regulatory Compliance](../governance/policy/concepts/regulatory-compliance.md). -->

- 在 [Azure Policy GitHub 存储库](https://github.com/Azure/azure-policy)中查看这些内置项。