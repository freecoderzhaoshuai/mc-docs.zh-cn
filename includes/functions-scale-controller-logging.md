---
author: ggailey777
ms.service: azure-functions
ms.topic: include
ms.date: 08/12/2020
ms.author: v-junlch
ms.openlocfilehash: 61197abece63f81bf328b6ebe96903c7de127795
ms.sourcegitcommit: 84606cd16dd026fd66c1ac4afbc89906de0709ad
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "89413804"
---
| | |
|--|--|
|**`<DESTINATION>`**| 日志发送到的目标。 有效值为 `AppInsights` 和 `Blob`。<br/>使用 `AppInsights` 时，请确保[在函数应用中启用 Application Insights](../articles/azure-functions/functions-monitoring.md#enable-application-insights-integration)。<br/>将目标设置为 `Blob` 时，将在名为 `azure-functions-scale-controller` 的 blob 容器中创建日志，该容器位于 `AzureWebJobsStorage` 应用程序设置中设置的默认存储帐户中。 |
|**`<VERBOSITY>`** | 指定日志记录级别。 支持的值为 `None`、`Warning` 和 `Verbose`。<br/>设置为 `Verbose` 时，缩放控制器将记录辅助角色计数每次更改的原因，以及有关将这些因素纳入决策的触发器的信息。 详细日志包含触发器警告和缩放控制器运行前后触发器使用的哈希。 |

> [!CAUTION]
> 请勿让缩放控制器日志记录处于启用状态。 启用日志记录，直到收集到的数据足以了解缩放控制器的行为方式，然后将其禁用。

