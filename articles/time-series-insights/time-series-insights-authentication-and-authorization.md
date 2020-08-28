---
title: API 身份验证和授权 - Azure 时序见解 | Microsoft Docs
description: 本文介绍如何为调用 Azure 时序见解 API 的自定义应用程序配置身份验证和授权。
ms.service: time-series-insights
services: time-series-insights
author: deepakpalled
ms.author: v-junlch
manager: dpalled
ms.reviewer: v-mamcge, jasonh, kfile
ms.devlang: csharp
ms.workload: big-data
ms.topic: conceptual
ms.date: 08/20/2020
ms.custom: seodec18, has-adal-ref
ms.openlocfilehash: 0acbc9b60402462f6cdc7a86cd557cd280c95c0d
ms.sourcegitcommit: 2e9b16f155455cd5f0641234cfcb304a568765a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88715173"
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a>Azure 时序见解 API 的身份验证和授权

本文档介绍如何使用新的 Azure Active Directory 边栏选项卡在 Azure Active Directory 中注册应用。 在 Azure Active Directory 中注册的应用可让用户进行身份验证，并有权使用与 Azure 时序见解环境关联的 Azure 时序见解 API。

## <a name="service-principal"></a>服务主体

以下部分介绍如何配置一个应用程序，以代表某个应用访问 Azure 时序见解 API。 然后，该应用程序可以通过 Azure Active Directory 使用自身的应用程序凭据在 Azure 时序见解环境中查询或发布参考数据。

## <a name="summary-and-best-practices"></a>摘要和最佳做法

Azure Active Directory 应用注册流程涉及三个主要步骤。

1. 在 Azure Active Directory 中[注册应用程序](#azure-active-directory-app-registration)。
1. 授权应用程序[对 Azure 时序见解环境进行数据访问](#granting-data-access)。
1. 使用应用程序 ID 和客户端密码从[客户端应用](#client-app-initialization)中的 `https://api.timeseries.azure.cn/` 获取令牌。 然后可使用该令牌调用 Azure 时序见解 API。

根据步骤 3，将应用程序凭据和用户凭据隔离可以：

* 将权限分配给应用标识，这些权限不同于你自己的权限。 通常情况下，这些权限仅限于应用需要的权限。 例如，可仅允许应用读取特定 Azure 时序见解环境中的数据。
* 使用客户端密码或安全证书，将应用安全性与创建用户身份验证凭据的过程相隔离。 因此，应用程序的凭据不依赖于特定用户的凭据。 如果用户的角色发生更改，应用程序不一定需要新的凭据或进一步的配置。 如果用户更改了其密码，对应用程序的所有访问都不需要新的凭据或密钥。
* 使用客户端密码或安全证书而不是特定用户的凭据（这需要出示这些凭据）来运行无人参与的脚本。
* 使用安全证书而不是密码来保护对 Azure 时序见解 API 的访问。

> [!IMPORTANT]
> 配置 Azure 时序见解安全策略时，请遵循“关注点分离”的原则（在上述方案中已介绍）。

> [!NOTE]

> * 文中重点介绍了单租户应用程序，其中应用程序只应在一个组织内运行。
> * 通常会将单租户应用程序作为在组织中运行的业务线应用程序使用。

## <a name="detailed-setup"></a>详细设置

### <a name="azure-active-directory-app-registration"></a>Azure Active Directory 应用注册

[!INCLUDE [Azure Active Directory app registration](../../includes/time-series-insights-aad-registration.md)]

### <a name="granting-data-access"></a>授予数据访问权限

1. 对于 Azure 时序见解环境，请选择“数据访问策略”，然后选择“添加” 。

   [![将新的数据访问策略添加到 Azure 时序见解环境](./media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)](./media/authentication-and-authorization/time-series-insights-data-access-policies-add.png#lightbox)

1. 在“选择用户”对话框中，粘贴来自 Azure Active Directory 应用注册部分的“应用程序名称”或“应用程序 ID” 。

   [![在“选择用户”对话框中查找应用程序](./media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)](./media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png#lightbox)

1. 选择角色。 选择“读取者”以查询数据，或选择“参与者”以查询数据和更改参考数据。 选择“确定”。

   [![在“选择角色”对话框中选择“读取者”或“参与者”](./media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)](./media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png#lightbox)

1. 通过选择“确定”来保存策略。

   > [!TIP]
   > 对于高级数据访问选项，请阅读[授予数据访问权限](./time-series-insights-data-access.md)。

### <a name="client-app-initialization"></a>客户端应用初始化

* 开发人员可以使用 Microsoft 身份验证库 (MSAL) 通过 Azure 时序见解进行身份验证。

* 使用 MSAL 进行身份验证：

   1. 使用来自 Azure Active Directory 应用注册部分的“应用程序 ID”和“客户端密码”（应用程序密钥）来代表应用程序获取令牌。

   1. 在 C# 中，以下代码可以代表应用程序获取令牌。 有关如何从 Gen1 环境查询数据的完整示例，请参阅[使用 C# 查询数据](time-series-insights-query-data-csharp.md)。

        ```csharp
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.Linq;
        using System.Net;
        using System.Net.WebSockets;
        using System.Text;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Newtonsoft.Json;
        using Newtonsoft.Json.Linq;
    
        namespace TimeSeriesInsightsQuerySample
        {
            class Program
            {
                // For automated execution under application identity,
                // use application created in Active Directory.
                // To create the application in AAD, follow the steps provided here:
                // /time-series-insights/time-series-insights-authentication-and-authorization
    
                // SET the application ID of application registered in your Azure Active Directory
                private static string ApplicationClientId = "#DUMMY#";
    
                // SET the application key of the application registered in your Azure Active Directory
                private static string ApplicationClientSecret = "#DUMMY#";
    
                // SET the Azure Active Directory tenant.
                private static string Tenant = "#DUMMY#.partner.onmschina.cn";
    
                public static async Task SampleAsync()
                {
                    // Acquire an access token.
                    string accessToken = await AcquireAccessTokenAsync();
    
                    // Obtain list of environments and get environment FQDN for the environment of interest.
                    string environmentFqdn;
                    {
                        HttpWebRequest request = CreateHttpsWebRequest("api.timeseries.azure.cn", "GET", "environments", accessToken);
                        JToken responseContent = await GetResponseAsync(request);
    
                        JArray environmentsList = (JArray)responseContent["environments"];
                        if (environmentsList.Count == 0)
                        {
                            // List of user environments is empty, fallback to sample environment.
                            environmentFqdn = "10000000-0000-0000-0000-100000000108.env.timeseries.azure.com";
                        }
                        else
                        {
                            // Assume the first environment is the environment of interest.
                            JObject firstEnvironment = (JObject)environmentsList[0];
                            environmentFqdn = firstEnvironment["environmentFqdn"].Value<string>();
                        }
                    }
                    Console.WriteLine("Using environment FQDN '{0}'", environmentFqdn);
                    Console.WriteLine();
    
                    // Obtain availability data for the environment and get availability range.
                    DateTime fromAvailabilityTimestamp;
                    DateTime toAvailabilityTimestamp;
                    {
                        HttpWebRequest request = CreateHttpsWebRequest(environmentFqdn, "GET", "availability", accessToken);
                        JToken responseContent = await GetResponseAsync(request);
    
                        JObject range = (JObject)responseContent["range"];
                        fromAvailabilityTimestamp = range["from"].Value<DateTime>();
                        toAvailabilityTimestamp = range["to"].Value<DateTime>();
                    }
                    Console.WriteLine(
                        "Obtained availability range [{0}, {1}]",
                        fromAvailabilityTimestamp,
                        toAvailabilityTimestamp);
                    Console.WriteLine();
    
                    // Assume data for the whole availablility range is requested.
                    DateTime from = fromAvailabilityTimestamp;
                    DateTime to = toAvailabilityTimestamp;
    
                    // Obtain metadata for the environment.
                    {
                        JObject inputPayload = new JObject(
                            new JProperty("searchSpan", new JObject(
                                new JProperty("from", from),
                                new JProperty("to", to))));
    
                        HttpWebRequest request = CreateHttpsWebRequest(environmentFqdn, "POST", "metadata", accessToken);
                        await WriteRequestStreamAsync(request, inputPayload);
                        JToken responseContent = await GetResponseAsync(request);
    
                        DumpMetadata(responseContent);
                        Console.WriteLine();
                    }
    
                    // Get events for the environment.
                    {
                        int requestedEventCount = 10;
    
                        JObject contentInputPayload = new JObject(
                            new JProperty("take", requestedEventCount),
                            new JProperty("searchSpan", new JObject(
                                new JProperty("from", from),
                                new JProperty("to", to))));
    
                        // Use HTTP request.
                        HttpWebRequest request = CreateHttpsWebRequest(environmentFqdn, "POST", "events", accessToken, new[] { "timeout=PT20S" });
                        await WriteRequestStreamAsync(request, contentInputPayload);
                        JToken responseContent = await GetResponseAsync(request);
    
                        Console.WriteLine("Requested {0} events via HTTP request.", requestedEventCount);
                        DumpEvents(responseContent);
                        Console.WriteLine();
    
                        // Use WebSocket request.
                        JObject inputPayload = new JObject(
                            // Send HTTP headers as a part of the message since .NET WebSocket does not support
                            // sending custom headers on HTTP GET upgrade request to WebSocket protocol request.
                            new JProperty("headers", new JObject(
                                new JProperty("x-ms-client-application-name", "TimeSeriesInsightsQuerySample"),
                                new JProperty("Authorization", "Bearer " + accessToken))),
                            new JProperty("content", contentInputPayload));
                        IReadOnlyList<JToken> responseMessagesContent = await ReadWebSocketResponseAsync(environmentFqdn, "events", inputPayload);
    
                        Console.WriteLine("Requested {0} events via WebSocket request.", requestedEventCount);
                        DumpEventsStreamed(responseMessagesContent);
                        Console.WriteLine();
                    }
    
                    // Get aggregates for the environment: group by Event Source Name and calculate number of events in each group.
                    {
                        JObject contentInputPayload = new JObject(
                            new JProperty("aggregates", new JArray(new JObject(
                                new JProperty("dimension", new JObject(
                                    new JProperty("uniqueValues", new JObject(
                                        new JProperty("input", new JObject(
                                            new JProperty("builtInProperty", "$esn"))),
                                        new JProperty("take", 1000))))),
                                new JProperty("measures", new JArray(new JObject(
                                    new JProperty("count", new JObject()))))))),
                            new JProperty("searchSpan", new JObject(
                                new JProperty("from", from),
                                new JProperty("to", to))));
    
                        // Use HTTP request.
                        HttpWebRequest request = CreateHttpsWebRequest(environmentFqdn, "POST", "aggregates", accessToken, new[] { "timeout=PT20S" });
                        await WriteRequestStreamAsync(request, contentInputPayload);
                        JToken responseContent = await GetResponseAsync(request);
    
                        Console.WriteLine("Group by Event Source Name via HTTP request.");
                        DumpAggregates(responseContent);
                        Console.WriteLine();
    
                        // Use WebSocket request.
                        JObject inputPayload = new JObject(
                            // Send HTTP headers as a part of the message since .NET WebSocket does not support
                            // sending custom headers on HTTP GET upgrade request to WebSocket protocol request.
                            new JProperty("headers", new JObject(
                                new JProperty("x-ms-client-application-name", "TimeSeriesInsightsQuerySample"),
                                new JProperty("Authorization", "Bearer " + accessToken))),
                            new JProperty("content", contentInputPayload));
                        IReadOnlyList<JToken> responseMessagesContent = await ReadWebSocketResponseAsync(environmentFqdn, "aggregates", inputPayload);
    
                        Console.WriteLine("Group by Event Source Name via WebSocket request.");
                        DumpAggregatesStreamed(responseMessagesContent);
                        Console.WriteLine();
                    }
                }
    
                private static async Task<string> AcquireAccessTokenAsync()
                {
                    if (AadClientApplicationId == "#PLACEHOLDER#" || AadScopes.Length == 0 || AadRedirectUri == "#PLACEHOLDER#" || AadTenantName.StartsWith("#PLACEHOLDER#"))
                    {
                        throw new Exception($"Use the link {"/time-series-insights/time-series-insights-get-started"} to update the values of 'AadClientApplicationId', 'AadScopes', 'AadRedirectUri', and 'AadAuthenticationAuthority'.");
                    }
    
                    IPublicClientApplication app = PublicClientApplicationBuilder
                                .Create(AadClientApplicationId)
                                .WithRedirectUri(AadRedirectUri)
                                .WithAuthority(AadAuthenticationAuthority)
                                .Build();
    
                    AuthenticationResult result = await app
                                .AcquireTokenInteractive(AadScopes)
                                .ExecuteAsync();
    
                    // Show interactive logon dialog to acquire token on behalf of the user.
                    // Suitable for native apps, and not on server-side of a web application.
                    // AuthenticationResult result = await app
                    //          .AcquireTokenInteractive(AadScopes)
                    //          .ExecuteAsync();
                    //    
                    //    // Set redirect URI for Azure PowerShell
                    //    redirectUri: new Uri("urn:ietf:wg:oauth:2.0:oob"),
                    //    parameters: new PlatformParameters(PromptBehavior.Auto));
    
                    return result.AccessToken;
                }
    
                private static HttpWebRequest CreateHttpsWebRequest(string host, string method, string path, string accessToken, string[] queryArgs = null)
                {
                    string query = "api-version=2016-12-12";
                    if (queryArgs != null && queryArgs.Any())
                    {
                        query += "&" + String.Join("&", queryArgs);
                    }
    
                    Uri uri = new UriBuilder("https", host)
                    {
                        Path = path,
                        Query = query
                    }.Uri;
                    HttpWebRequest request = WebRequest.CreateHttp(uri);
                    request.Method = method;
                    request.Headers.Add("x-ms-client-application-name", "TimeSeriesInsightsQuerySample");
                    request.Headers.Add("Authorization", "Bearer " + accessToken);
                    return request;
                }
    
                private static async Task WriteRequestStreamAsync(HttpWebRequest request, JObject inputPayload)
                {
                    using (var stream = await request.GetRequestStreamAsync())
                    using (var streamWriter = new StreamWriter(stream))
                    {
                        await streamWriter.WriteAsync(inputPayload.ToString());
                        await streamWriter.FlushAsync();
                        streamWriter.Close();
                    }
                }
    
                private static async Task<JToken> GetResponseAsync(HttpWebRequest request)
                {
                    using (WebResponse webResponse = await request.GetResponseAsync())
                    using (var sr = new StreamReader(webResponse.GetResponseStream()))
                    {
                        string result = await sr.ReadToEndAsync();
                        return JsonConvert.DeserializeObject<JToken>(result);
                    }
                }
    
                private static async Task<IReadOnlyList<JToken>> ReadWebSocketResponseAsync(string environmentFqdn, string path, JObject inputPayload)
                {
                    var webSocket = new ClientWebSocket();
    
                    // Establish web socket connection.
                    Uri uri = new UriBuilder("wss", environmentFqdn)
                    {
                        Path = path,
                        Query = "api-version=2016-12-12"
                    }.Uri;
                    await webSocket.ConnectAsync(uri, CancellationToken.None);
    
                    // Send input payload.
                    byte[] inputPayloadBytes = Encoding.UTF8.GetBytes(inputPayload.ToString());
                    await webSocket.SendAsync(
                        new ArraySegment<byte>(inputPayloadBytes),
                        WebSocketMessageType.Text,
                        endOfMessage: true,
                        cancellationToken: CancellationToken.None);
    
                    // Read response messages from web socket.
                    List<JToken> responseMessagesContent = new List<JToken>();
                    using (webSocket)
                    {
                        while (true)
                        {
                            string message;
                            using (var ms = new MemoryStream())
                            {
                                // Write from socket to memory stream.
                                const int bufferSize = 16 * 1024;
                                var temporaryBuffer = new byte[bufferSize];
                                while (true)
                                {
                                    WebSocketReceiveResult response = await webSocket.ReceiveAsync(
                                        new ArraySegment<byte>(temporaryBuffer),
                                        CancellationToken.None);
    
                                    ms.Write(temporaryBuffer, 0, response.Count);
                                    if (response.EndOfMessage)
                                    {
                                        break;
                                    }
                                }
    
                                // Reset position to the beginning to allow reads.
                                ms.Position = 0;
    
                                using (var sr = new StreamReader(ms))
                                {
                                    message = sr.ReadToEnd();
                                }
                            }
    
                            JObject messageObj = JsonConvert.DeserializeObject<JObject>(message);
    
                            // Stop reading if error is emitted.
                            if (messageObj["error"] != null)
                            {
                                break;
                            }
    
                            // Actual response contents is wrapped into "content" object.
                            responseMessagesContent.Add(messageObj["content"]);
    
                            // Stop reading if 100% of completeness is reached.
                            if (messageObj["percentCompleted"] != null &&
                                Math.Abs((double)messageObj["percentCompleted"] - 100d) < 0.01)
                            {
                                break;
                            }
                        }
    
                        // Close web socket connection.
                        if (webSocket.State == WebSocketState.Open)
                        {
                            await webSocket.CloseAsync(
                                WebSocketCloseStatus.NormalClosure,
                                "CompletedByClient",
                                CancellationToken.None);
                        }
                    }
    
                    return responseMessagesContent;
                }
    
                private static void DumpMetadata(JToken responseContent)
                {
                    // Response content has a list of properties under "properties" property.
                    JArray properties = (JArray)responseContent["properties"];
                    int propertiesCount = properties.Count;
                    Console.WriteLine("Acquired {0} properties:", propertiesCount);
                    for (int i = 0; i < propertiesCount; i++)
                    {
                        JObject currentProperty = (JObject)properties[i];
                        Console.WriteLine("'{0}': {1}", currentProperty["name"], currentProperty["type"]);
                    }
                }
    
                private static void DumpEvents(JToken responseContent)
                {
                    // Response content has a list of events under "events" property for HTTP request.
                    JArray events = (JArray)responseContent["events"];
                    int eventCount = events.Count;
                    Console.WriteLine("Acquired {0} events:", eventCount);
                    for (int i = 0; i < eventCount; i++)
                    {
                        JObject currentEvent = (JObject)events[i];
                        JArray values = (JArray)currentEvent["values"];
                        Console.WriteLine("{{$ts: {0}, values: {1}}}", currentEvent["$ts"].ToString(), String.Join(",", values));
                    }
                }
    
                private static void DumpEventsStreamed(IReadOnlyList<JToken> responseMessagesContent)
                {
                    // For events stream next message always contains additional events, i.e. new message is additive to the previous one.
                    // New message contains new events that were not in the previous message.
                    // The previous message should be kept and accumulated with the new message.
                    // Response content has a list of events under "events" property both for HTTP and WebSocket requests.
                    JArray events = new JArray(responseMessagesContent.SelectMany(m => (JArray)m["events"]));
    
                    int eventCount = events.Count;
                    Console.WriteLine("Acquired {0} events:", eventCount);
                    for (int i = 0; i < eventCount; i++)
                    {
                        JObject currentEvent = (JObject)events[i];
                        JArray values = (JArray)currentEvent["values"];
                        Console.WriteLine("{{$ts: {0}, values: {1}}}", currentEvent["$ts"].ToString(), String.Join(",", values));
                    }
                }
    
                private static void DumpAggregates(JToken responseContent)
                {
                    // HTTP response content contains the list of aggregates under "aggregates" property.
                    JArray aggregates = (JArray)responseContent["aggregates"];
    
                    DumpAggregatesInternal(aggregates);
                }
    
                private static void DumpAggregatesStreamed(IReadOnlyList<JToken> responseMessagesContent)
                {
                    // For aggregates stream next message always contains a replacement (snapshot) of all the values.
                    // Previous message can be discarded by the client.
                    // WebSocket response represents the list of aggregates.
                    JArray aggregates = (JArray)responseMessagesContent.Last();
    
                    DumpAggregatesInternal(aggregates);
                }
    
                private static void DumpAggregatesInternal(JArray aggregates)
                {
                    // Number of items corresponds to number of aggregates in input payload.
                    // In this sample list of aggregates in input payload contains only 1 item since request contains 1 aggregate.
                    JObject aggregate = (JObject)aggregates[0];
                    JArray dimensionValues = (JArray)aggregate["dimension"];
                    JArray measures = (JArray)aggregate["measures"];
                    Debug.Assert(
                        dimensionValues.Count == measures.Count,
                        "Number of measures and dimensions should match.");
                    Console.WriteLine("Dimension Value\t\tCount");
                    for (int i = 0; i < dimensionValues.Count; i++)
                    {
                        string currentDimensionValue = (string)dimensionValues[i];
                        JArray currentMeasureValues = (JArray)measures[i];
                        double currentCount = (double)currentMeasureValues[0];
    
                        Console.WriteLine("{0}\t\t{1}", currentDimensionValue, currentCount);
                    }
                }
    
                static void Main(string[] args)
                {
                    ServicePointManager.SecurityProtocol = SecurityProtocolType.Tls12;
                    Task.Run(async () => await SampleAsync()).Wait();
                }
            }
        }
        ```

   1. 随后可在应用程序调用 Azure 时序见解 API 时，将令牌传入 `Authorization` 标头。

    > [!IMPORTANT]
    > 如果使用的是 [Active Directory 身份验证库 (ADAL)](/active-directory/azuread-dev/active-directory-authentication-libraries)，请阅读[迁移到 MSAL](/active-directory/develop/msal-net-migration)。

## <a name="common-headers-and-parameters"></a>常用标头和参数

本部分介绍用于对 Azure 时序见解 Gen1 和 Gen2 API 进行查询的常用 HTTP 请求标头和参数。 [Azure 时序见解 REST API 参考文档](https://docs.microsoft.com/rest/api/time-series-insights/)中更详细地介绍了特定于 API 的要求。

> [!TIP]
> 阅读 [Azure REST API 参考](https://docs.microsoft.com/rest/api/azure/)，了解有关如何使用 REST API、发出 HTTP 请求和处理 HTTP 响应的详细信息。

### <a name="authentication"></a>身份验证

若要对 [Azure 时序见解 REST API](https://docs.microsoft.com/rest/api/time-series-insights/) 执行经过身份验证的查询，必须使用所选的 REST 客户端（Postman、JavaScript、C#）将有效的 OAuth 2.0 持有者令牌传入[授权标头](https://docs.microsoft.com/rest/api/apimanagement/2019-12-01/authorizationserver/createorupdate)。

> [!TIP]
> 阅读托管的 Azure 时序见解[客户端 SDK 示例可视化](https://tsiclientsample.azurewebsites.net/)，了解如何使用 [JavaScript 客户端 SDK](https://github.com/microsoft/tsiclient/blob/master/docs/API.md) 以及图表和图以编程方式通过 Azure 时序见解 API 进行身份验证。

### <a name="http-headers"></a>HTTP 标头

必需的请求标头如下所述。

| 必需的请求标头 | 说明 |
| --- | --- |
| 授权 | 若要使用 Azure 时序见解进行身份验证，必须将有效的 OAuth 2.0 持有者令牌传入“授权”标头。 |

> [!IMPORTANT]
> 令牌必须严格颁发给 `https://api.timeseries.azure.cn/` 资源（也称为令牌的“受众”）。

> * 因此，[Postman](https://www.getpostman.com/) **AuthURL** 将为：`https://login.partner.microsoftonline.cn/microsoft.partner.onmschina.cn/oauth2/authorize?scope=https://api.timeseries.azure.cn/.default`
> * `https://api.timeseries.azure.cn/` 有效，但 `https://api.timeseries.azure.cn` 无效。

可选请求标头如下所述。

| 可选请求标头 | 说明 |
| --- | --- |
| Content-type | 仅支持 `application/json`。 |
| x-ms-client-request-id | 客户端请求 ID。 服务记录此值。 允许服务跨服务跟踪操作。 |
| x-ms-client-session-id | 客户端会话 ID。 服务记录此值。 允许服务跨服务跟踪一组相关操作。 |
| x-ms-client-application-name | 生成此请求的应用程序的名称。 服务记录此值。 |

可选但建议的响应标头如下所述。

| 响应标头 | 说明 |
| --- | --- |
| Content-type | 仅支持 `application/json`。 |
| x-ms-request-id | 服务器生成的请求 ID。 可用于与 Microsoft 联系以调查请求。 |
| x-ms-property-not-found-behavior | GA API 可选响应标头。 可能的值为 `ThrowError`（默认）或 `UseNull`。 |

### <a name="http-parameters"></a>HTTP 参数

> [!TIP]
> 如需查找有关必需和可选查询信息的详细信息，请参阅[参考文档](https://docs.microsoft.com/rest/api/time-series-insights/)。

必需的 URL 查询字符串参数依赖于 API 版本。

| 发布 | 可能的 API 版本值 |
| --- |  --- |
| Gen1 | `api-version=2016-12-12`|
| Gen2 | `api-version=2020-07-31` 和 `api-version=2018-11-01-preview`|

> [!IMPORTANT]
>
> `api-version=2018-11-01-preview` 版本很快就会被弃用。 建议用户切换到较新的版本。

可选 URL 查询字符串参数包括为 HTTP 请求执行时间设置超时。

| 可选查询参数 | 说明 | 版本 |
| --- |  --- | --- |
| `timeout=<timeout>` | 用于执行 HTTP 请求的服务器端超时。 仅适用于`Get Environment Events`和[获取环境聚合](https://docs.microsoft.com/rest/api/time-series-insights/gen1-query-api#get-environment-aggregates-api) API。 超时值应采用 ISO 8601 持续时间格式（例如 `"PT20S"`），并且应在 `1-30 s` 范围内。 默认值为 `30 s`。 | Gen1 |
| `storeType=<storeType>` | 对于启用了 Warm 存储的 Gen2 环境，可以对 `WarmStore` 或 `ColdStore` 执行查询。 查询中的此参数定义应对哪个存储执行查询。 如果未定义，将对 Cold 存储区执行查询。 若要查询 Warm 存储，需要将 storeType 设置为 `WarmStore`。 如果未定义，将对 Cold 存储区执行查询。 | Gen2 |

## <a name="next-steps"></a>后续步骤

* 有关调用 Gen1 Azure 时序见解 API 的示例代码，请参阅[使用 C# 查询 Gen1 数据](./time-series-insights-query-data-csharp.md)。

* 有关调用 Gen2 Azure 时序见解 API 示例代码的示例代码，请参阅[使用 C# 查询 Gen2 数据](./time-series-insights-update-query-data-csharp.md)。

* 有关 API 参考信息，请阅读[查询 API 参考](https://docs.microsoft.com/rest/api/time-series-insights/gen1-query-api)文档。

* 了解如何[创建服务主体](../active-directory/develop/howto-create-service-principal-portal.md)。

