---
title: API 版本
titleSuffix: Azure Cognitive Search
description: 适用于 .NET SDK 中的 Azure 认知搜索 REST API 和客户端库的版本策略。
manager: nitinme
author: HeidiSteen
ms.author: v-tawe
ms.service: cognitive-search
ms.topic: conceptual
origin.date: 08/26/2020
ms.date: 09/10/2020
ms.openlocfilehash: d0b3457f49ac8db61e4e4ffda359e7e7910eff17
ms.sourcegitcommit: 78c71698daffee3a6b316e794f5bdcf6d160f326
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90020942"
---
# <a name="api-versions-in-azure-cognitive-search"></a>Azure 认知搜索中的 API 版本

Azure 认知搜索会定期发布功能更新。 这些更新有时（但并非总是）需要发布 API 的新版本，以保持后向兼容性。 发布新版本使你可以控制何时以及如何在代码中集成搜索服务更新。

通常，Azure 认知搜索团队仅在必要时发布新版本，因为它可能会促使你必须升级代码才能使用新版本 API。 仅在 API 的某些方面以破坏后向兼容性的方式发生更改时，才需要新版本。 此类更改可能会因以下情况而发生：现有功能修复，或更改现有 API 外围功能的新功能。

相同规则适用于 SDK 更新。 Azure 认知搜索 SDK 遵循[语义版本控制](https://semver.org/)规则，这意味着其版本分为三个部分：主要版本号、次要版本号和内部版本号（例如，1.1.0）。 仅在更改破坏了后向兼容性时，才会发布新的 SDK 主版本。 非破坏功能更新会增大次要版本号，Bug 修复仅增大内部版本号。

> [!Important]
> 用于 .NET、Java、Python 和 JavaScript 的 Azure SDK 正在推出用于 Azure 认知搜索的新客户端库。 目前，尚无任何 Azure SDK 库完全支持最新的搜索 REST API (2020-06-30) 或管理 REST API (2020-03-13)，但这种情况以后将会发生改变。 可以定期查看此页面或[新增功能](whats-new.md)，以获取有关功能性增强的公告。

<a name="unsupported-versions"></a>

## <a name="unsupported-versions"></a>不支持的版本

请在 2020 年 10 月 15 日前将现有搜索解决方案升级到 REST API 的最新版本。 届时，Azure 认知搜索 REST API 的以下版本将会被停用，不再受支持：

+ **2015-02-28**
+ **2015-02-28-Preview**
+ **2014-07-31-Preview**
+ **2014-10-20-Preview**

另外，早于 [3.0.0-rc](https://www.nuget.org/packages/Microsoft.Azure.Search/3.0.0-rc) 的 Azure 认知搜索 .NET SDK 版本也将停用，因为它们面向这些 REST API 版本之一。 

在此日期之后，使用任何弃用的 REST API 或 SDK 版本的应用程序将不再能够正常运行，必须进行升级。 对于这种类型的任何更改，我们会提前 12 个月进行通知，以便你有足够的时间进行调整。

若要继续使用 Azure 认知搜索，请在 2020 年 10 月 15 日之前将面向 [REST API](search-api-migration.md) 的现有节点迁移到 [REST API 版本 2020-06-30](https://docs.microsoft.com/rest/api/searchservice/) 或较新的 SDK。  若有关于更新到最新版本的任何问题，请在 2020 年 5 月 15 日之前发送邮件到 azuresearch_contact@microsoft.com，确保有足够的时间更新代码。

## <a name="rest-apis"></a>REST API

Azure 认知搜索服务实例支持几个 REST API 版本，包括最新版本。 某个版本不再是最新版本时，仍可继续使用，但我们建议[迁移代码](search-api-migration.md)以使用最新版本。 使用 REST API 时，必须在每个请求中通过 api-version 参数指定 API 版本。 使用 .NET SDK 时，使用的 SDK 版本确定对应的 REST API 版本。 如果使用较旧的 SDK，即使已升级服务以支持较新的 API 版本，也可以继续运行代码，而不进行任何更改。

下表提供搜索服务 REST API 的当前版本和以前发布的版本的版本历史记录。 文档仅为最新的稳定版本和预览版本发布。

### <a name="search-service-apis"></a>搜索服务 API

创建和管理有关搜索服务的内容。

| 版本&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   | 状态 | 向后兼容性问题 |
|-------------------------|--------|------------------------------|
| [搜索 2020-06-30](https://docs.microsoft.com/rest/api/searchservice/index)| Stable | 搜索 REST API 的最新稳定版本，在相关性评分方面有改进。 |
| [搜索 2020-06-30-Preview](https://docs.microsoft.com/rest/api/searchservice/index-preview)| 预览 | 与稳定版本关联的预览版本。 |
| 搜索 2019-05-06 | Stable  | 添加了[复杂类型](search-howto-complex-data-types.md)。 |
| 搜索 2019-05-06-Preview | 预览 | 与稳定版本关联的预览版本。 |
| 搜索 2017-11-11 | Stable | 添加了技能集和 [AI 扩充](cognitive-search-concept-intro.md)。 |
| 搜索 2017-11-11-Preview | 预览 | 与稳定版本关联的预览版本。 |
| 搜索 2016-09-01 |Stable | 添加了[索引器](search-indexer-overview.md)。 |
| 搜索 2016-09-01-Preview | 预览 | 与稳定版本关联的预览版本。|
| 搜索 2015-02-28 | 在 2020 年 10 月 10 日之后不再受支持   | 第一个正式发布版本。  |
| 搜索 2015-02-28-Preview | 在 2020 年 10 月 10 日之后不再受支持  | 与稳定版本关联的预览版本。 |
| 搜索 2014-10-20-Preview | 在 2020 年 10 月 10 日之后不再受支持 | 第二个公共预览版。 |
| 搜索 2014-07-31-Preview | 在 2020 年 10 月 10 日之后不再受支持  | 第一个公共预览版。 |

### <a name="management-rest-apis"></a>管理 REST API

创建和配置搜索服务，并管理 API 密钥。

| 版本&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   | 状态 | 向后兼容性问题 |
|-------------------------|--------|------------------------------|
| [管理 2020-03-13](https://docs.microsoft.com/rest/api/searchmanagement/) | Stable | 管理 REST API 的最新稳定版本，在终结点保护方面有改进。 为新服务添加[网络 IP 规则](service-configure-firewall.md)。 |
| [管理 2019-10-01-Preview](https://docs.microsoft.com/rest/api/searchmanagement/index-2019-10-01-preview) | 预览  | 尽管具有版本号，但它仍是管理 REST API 的当前预览版。 目前没有预览功能。 所有预览功能最近已转换为正式发布版本。 |
| 管理 2015-08-19  | Stable | 管理 REST API 的第一个正式发布版本。 提供服务预配、纵向扩展和 API 密钥管理。 |
| 管理 2015-08-19-Preview | 预览 | 管理 REST API 的第一个预览版本。 |

## <a name="azure-sdk-for-net"></a>用于 .NET 的 Azure SDK

下表提供了最新 SDK 版本的链接。 

| SDK 版本 | 状态 | 描述 |
|-------------|--------|------------------------------|
| [Azure.Search.Documents 11.0](https://www.nuget.org/packages/Azure.Search.Documents/1.0.0-preview.4) | Stable | Azure .NET SDK 中的新客户端库，2020 年 7 月发布。 面向搜索 REST api-version=2020-06-30 REST API，但尚不支持地理位置筛选器或 [FieldBuilder](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.fieldbuilder)。 |
| [Microsoft.Azure.Search 10.0](https://www.nuget.org/packages/Microsoft.Azure.Search/) | Stable | 2019 年 5 月发布。 面向搜索 REST api-version=2019-05-06。|
| [Microsoft.Azure.Search 8.0-preview](https://www.nuget.org/packages/Microsoft.Azure.Search/8.0.0-preview) | 预览 | 2019 年 4 月发布。 面向搜索 REST api-version=2019-05-06-Preview。|
| [Microsoft.Azure.Management.Search 3.0.0](https://docs.microsoft.com/dotnet/api/overview/azure/search/management?view=azure-dotnet) | Stable | 针对管理 REST api-version=2015-08-19。  |

若要详细了解 Microsoft.Azure.Search 的早期版本，请访问 [NuGet 包页面](https://www.nuget.org/packages/Microsoft.Azure.Search/)以找到任意版本，向下滚动到“版本历史记录”并展开这部分以查看版本的完整列表。

## <a name="azure-sdk-for-java"></a>用于 Java 的 Azure SDK

| SDK 版本 | 状态 | 描述  |
|-------------|--------|------------------------------|
| [Java azure-search-documents 11](https://azuresdkdocs.blob.core.chinacloudapi.cn/$web/java/azure-search-documents/11.0.0/index.html) | Stable | Azure .NET SDK 中的新客户端库，2020 年 7 月发布。 面向搜索 REST api-version=2019-05-06。 |
| [Java 管理客户端 1.35.0](https://docs.microsoft.com/java/api/overview/azure/search/management?view=azure-java-stable) | Stable | 针对管理 REST api-version=2015-08-19。 |

## <a name="azure-sdk-for-javascript"></a>用于 JavaScript 的 Azure SDK

| SDK 版本 | 状态 | 描述  |
|-------------|--------|------------------------------|
| [JavaScript azure-search 11.0](https://azure.github.io/azure-sdk-for-node/azure-search/latest/) | Stable | Azure .NET SDK 中的新客户端库，2020 年 7 月发布。 面向搜索 REST api-version=2016-09-01。 |
| [JavaScript azure-arm-search](https://azure.github.io/azure-sdk-for-node/azure-arm-search/latest/) | Stable | 针对管理 REST api-version=2015-08-19。 |

## <a name="azure-sdk-for-python"></a>用于 Python 的 Azure SDK

| SDK 版本 | 状态 | 描述  |
|-------------|--------|------------------------------|
| [Python azure-search-documents 11.0](https://azuresdkdocs.blob.core.chinacloudapi.cn/$web/python/azure-search-documents/11.0.0/index.html) | Stable | Azure .NET SDK 中的新客户端库，2020 年 7 月发布。 面向搜索 REST api-version=2019-05-06。 |
| [Python azure-mgmt-search 1.0](https://docs.microsoft.com/python/api/overview/azure/search?view=azure-python) | Stable | 针对管理 REST api-version=2015-08-19。 |