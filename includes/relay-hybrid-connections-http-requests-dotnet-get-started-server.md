---
title: include 文件
description: include 文件
services: service-bus-relay
author: rockboyfor
ms.service: service-bus-relay
ms.topic: include
origin.date: 05/02/2018
ms.date: 07/27/2020
ms.testscope: yes|no
ms.testdate: 07/27/2020Null
ms.author: v-yeche
ms.custom: include file
ms.openlocfilehash: 87b717ad7d97da2f7f6058bdc0e1a9b12a0867ca
ms.sourcegitcommit: 091c672fa448b556f4c2c3979e006102d423e9d7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2020
ms.locfileid: "88947128"
---
<!--Verified successfully-->
### <a name="create-a-console-application"></a>创建控制台应用程序

在 Visual Studio 中创建新的**控制台应用 (.NET Framework)** 项目。

### <a name="add-the-relay-nuget-package"></a>添加中继 NuGet 包

1. 右键单击新创建的项目，然后选择“管理 NuGet 包”。
2. 选择“包括预发行版”选项。 
3. 选择“浏览”，然后搜索 **Microsoft.Azure.Relay**。 在搜索结果中，选择“Microsoft Azure 中继”。

    <!--CORRECT ON Microsoft Azure Relay-->

4. 对于版本，选择 **2.0.0-preview1-20180523**。 
5. 选择“安装”即可完成安装。 关闭对话框。

### <a name="write-code-to-receive-messages"></a>编写接收消息的代码

1. 将 Program.cs 文件顶部的现有 `using` 语句替换为以下 `using` 语句：
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
    using System.Net;
    ```
2. 将常量添加到 `Program` 类，用于保存混合连接的连接详细信息。 将括号中的占位符替换为在创建混合连接时获得的值。 请务必使用完全限定的命名空间名称。
   
    ```csharp
    // replace {RelayNamespace} with the name of your namespace
    private const string RelayNamespace = "{RelayNamespace}.servicebus.chinacloudapi.cn";

    // replace {HybridConnectionName} with the name of your hybrid connection
    private const string ConnectionName = "{HybridConnectionName}";

    // replace {SAKKeyName} with the name of your Shared Access Policies key, which is RootManageSharedAccessKey by default
    private const string KeyName = "{SASKeyName}";

    // replace {SASKey} with the primary key of the namespace you saved earlier
    private const string Key = "{SASKey}";
    ```

3. 将 `RunAsync` 方法添加到 `Program` 类：
   
    ```csharp
    private static async Task RunAsync()
    {
        var cts = new CancellationTokenSource();
   
        var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
        var listener = new HybridConnectionListener(new Uri(string.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
        // Subscribe to the status events.
        listener.Connecting += (o, e) => { Console.WriteLine("Connecting"); };
        listener.Offline += (o, e) => { Console.WriteLine("Offline"); };
        listener.Online += (o, e) => { Console.WriteLine("Online"); };

        // Provide an HTTP request handler
        listener.RequestHandler = (context) =>
        {
            // Do something with context.Request.Url, HttpMethod, Headers, InputStream...
            context.Response.StatusCode = HttpStatusCode.OK;
            context.Response.StatusDescription = "OK, This is pretty neat";
            using (var sw = new StreamWriter(context.Response.OutputStream))
            {
                sw.WriteLine("hello!");
            }
            
            // The context MUST be closed here
            context.Response.Close();
        };
            
        // Opening the listener establishes the control channel to
        // the Azure Relay service. The control channel is continuously 
        // maintained, and is reestablished when connectivity is disrupted.
        await listener.OpenAsync();
        Console.WriteLine("Server listening");
    
        // Start a new thread that will continuously read the console.
        await Console.In.ReadLineAsync();
        
        // Close the listener after you exit the processing loop.
        await listener.CloseAsync();
    }
    ```
5. 在 `Program` 类的 `Main` 方法中添加以下代码行：
   
    ```csharp
    RunAsync().GetAwaiter().GetResult();
    ```
   
    完成的 Program.cs 文件应如下所示：
   
    ```csharp
    namespace Server
    {
        using System;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.Azure.Relay;
   
        public class Program
        {
            private const string RelayNamespace = "{RelayNamespace}.servicebus.chinacloudapi.cn";
            private const string ConnectionName = "{HybridConnectionName}";
            private const string KeyName = "{SASKeyName}";
            private const string Key = "{SASKey}";
   
            public static void Main(string[] args)
            {
                RunAsync().GetAwaiter().GetResult();
            }
   
            private static async Task RunAsync()
            {
                var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
                var listener = new HybridConnectionListener(new Uri(string.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
           
                // Subscribe to the status events.
                listener.Connecting += (o, e) => { Console.WriteLine("Connecting"); };
                listener.Offline += (o, e) => { Console.WriteLine("Offline"); };
                listener.Online += (o, e) => { Console.WriteLine("Online"); };
        
                // Provide an HTTP request handler
                listener.RequestHandler = (context) =>
                {
                    // Do something with context.Request.Url, HttpMethod, Headers, InputStream...
                    context.Response.StatusCode = HttpStatusCode.OK;
                    context.Response.StatusDescription = "OK";
                    using (var sw = new StreamWriter(context.Response.OutputStream))
                    {
                        sw.WriteLine("hello!");
                    }
                    
                    // The context MUST be closed here
                    context.Response.Close();
                };
           
                // Opening the listener establishes the control channel to
                // the Azure Relay service. The control channel is continuously 
                // maintained, and is reestablished when connectivity is disrupted.
                await listener.OpenAsync();
                Console.WriteLine("Server listening");
           
                // Start a new thread that will continuously read the console.
                await Console.In.ReadLineAsync();
               
                // Close the listener after you exit the processing loop.
                await listener.CloseAsync();
            }
        }
    }
    ```

<!-- Update_Description: update meta properties, wording update, update link -->