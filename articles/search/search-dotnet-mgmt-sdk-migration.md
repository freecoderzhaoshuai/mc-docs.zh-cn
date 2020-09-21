---
title: 升级到 Azure 搜索 .NET 管理 SDK
titleSuffix: Azure Cognitive Search
description: 从以前的版本升级到 Azure 搜索 .NET 管理 SDK。 了解执行迁移所需的新功能和代码更改。
manager: nitinme
author: brjohnstmsft
ms.author: v-tawe
ms.service: cognitive-search
ms.devlang: dotnet
ms.topic: conceptual
origin.date: 07/08/2020
ms.date: 09/10/2020
ms.openlocfilehash: 56e617c77c91c42019ee8d3d2ee67e0a3cadfcf6
ms.sourcegitcommit: 78c71698daffee3a6b316e794f5bdcf6d160f326
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90021574"
---
# <a name="upgrading-versions-of-the-azure-search-net-management-sdk"></a>升级 Azure 搜索 .NET 管理 SDK 的版本

本文介绍了如何迁移到 Azure 搜索 .NET 管理 SDK（用于预配或取消预配搜索服务、调整容量以及管理 API 密钥）的各个连续版本。

管理 SDK 面向管理 REST API 的某个特定版本。 有关概念和操作的详细信息，请参阅[搜索管理 (REST)](https://docs.microsoft.com/rest/api/searchmanagement/)。

## <a name="versions"></a>版本

| SDK 版本 | 相应的 REST API 版本 | 功能添加或行为变更 |
|-------------|--------------------------------|-------------------------------------|
| [2.0](https://www.nuget.org/packages/Microsoft.Azure.Management.Search/2.0.0) | api-version=2019-10-01 | 可用性改进。 针对[列出查询密钥](https://docs.microsoft.com/rest/api/searchmanagement/querykeys/listbysearchservice)的中断性变更（GET 已停用）。 |
| [1.0](https://www.nuget.org/packages/Microsoft.Azure.Management.Search/1.0.1) | api-version=2015-08-19  | 第一个版本 |

## <a name="how-to-upgrade"></a>如何升级

1. 按以下方式更新 `Microsoft.Azure.Management.Search` 的 NuGet 引用：使用 NuGet 包管理器控制台，或者在 Visual Studio 中右键单击项目引用，然后选择“管理 NuGet 程序包...”。

1. 在 NuGet 已下载新的程序包及其依赖项后，请重新生成项目。 根据代码结构的不同，重新生成该项目可能会成功，如果成功则操作完成。

1. 如果生成失败，则可能是因为已实现某些已更改的 SDK 接口（如出于单元测试目）。 若要解决此问题，需要实现 `BeginCreateOrUpdateWithHttpMessagesAsync` 等更新的方法。

1. 在修复了任何生成错误后，可以对应用程序进行更改，以利用新功能。 

<!-- 3.0 need private link not support in mc
## Upgrade to 3.0

Version 3.0 adds private endpoint protection by restricting access to IP ranges, and by optionally integrating with Azure Private Link for search services that should not be visible on the public internet.

### New APIs

| API | Category| Details |
|-----|--------|------------------|
| [NetworkRuleSet](https://docs.microsoft.com/rest/api/searchmanagement/services/createorupdate#networkruleset) | IP firewall | Restrict access to a service endpoint to a list of allowed IP addresses. See [Configure IP firewall](service-configure-firewall.md) for concepts and portal instructions. |
| [Shared Private Link Resource](https://docs.microsoft.com/rest/api/searchmanagement/sharedprivatelinkresources) | Private Link | Create a shared private link resource to be used by a search service.  |
| [Private Endpoint Connections](https://docs.microsoft.com/rest/api/searchmanagement/privateendpointconnections) | Private Link | Establish and manage connections to a search service through private endpoint. See [Create a private endpoint](service-create-private-endpoint.md) for concepts and portal instructions.|
| [Private Link Resources](https://docs.microsoft.com/rest/api/searchmanagement/privatelinkresources/) | Private Link | For a search service that has a private endpoint connection, get a list of all services used in the same virtual network. If your search solution includes indexers that pull from Azure data sources (Azure Storage, Cosmos DB, Azure SQL), or uses Cognitive Services or Key Vault, then all of those resources should have endpoints in the virtual network, and this API should return a list. |
| [PublicNetworkAccess](https://docs.microsoft.com/rest/api/searchmanagement/services/createorupdate#publicnetworkaccess)| Private Link | This is a property on Create or Update Service requests. When disabled, private link is the only access modality. |

### Breaking changes

You can no longer use GET on a [List Query Keys](https://docs.microsoft.com/rest/api/searchmanagement/querykeys/listbysearchservice) request. In previous releases you could use either GET or POST, in this release and in all releases moving forward, only POST is supported. 
-->

## <a name="upgrade-to-20"></a>升级到 2.0

Azure 搜索 .NET 管理 SDK 的版本 2 是一个次要升级，因此更改代码所需要的工作量应该极少。SDK 的更改在严格意义上而言是为改进 SDK 本身可用性而做出的客户端更改。 包括以下更改：

* `Services.CreateOrUpdate` 及其异步版本现在会自动轮询预配 `SearchService`，且在服务预配完成后才返回。 因此，无需自己编写此类轮询代码。

* 如果仍想手动轮询服务预配，可使用新的 `Services.BeginCreateOrUpdate` 方法或其异步版本之一。

* 新方法 `Services.Update` 及其异步版本已添加到 SDK。 这些方法使用 HTTP PATCH 来支持服务的增量更新。 例如，现在可以通过将 `SearchService` 实例传递到仅包含所需 `partitionCount` 和 `replicaCount` 属性的方法来缩放服务。 仍支持调用 `Services.Get`、修改返回的 `SearchService` 并将其传递给 `Services.CreateOrUpdate` 这一旧方法，但该方法不再是必要的。 

## <a name="next-steps"></a>后续步骤

如果遇到问题，最适合发布问题的论坛是 [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-cognitive-search?tab=Newest)。 如果找到 Bug，可以在 [Azure .NET SDK GitHub 存储库](https://github.com/Azure/azure-sdk-for-net/issues)中提出问题。 请务必使用“[search]”来标记问题标题。