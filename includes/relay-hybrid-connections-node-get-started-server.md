---
author: rockboyfor
ms.service: service-bus-relay
ms.topic: include
origin.date: 11/09/2018
ms.date: 07/27/2020
ms.testscope: yes
ms.testdate: 07/27/2020
ms.author: v-yeche
ms.openlocfilehash: 258214f8e2cff72c39687bcd68b03736550503c7
ms.sourcegitcommit: 091c672fa448b556f4c2c3979e006102d423e9d7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2020
ms.locfileid: "88947124"
---
<!--Verified successfully-->
### <a name="create-a-nodejs-application"></a>创建 Node.js 应用程序

创建一个名为 `listener.js` 的新 JavaScript 文件。

### <a name="add-the-relay-npm-package"></a>添加中继 NPM 包

从项目文件夹中的 Node 命令提示符运行 `npm install hyco-ws`。

### <a name="write-some-code-to-receive-messages"></a>编写一些代码来接收消息

1. 将下面的常量添加到 `listener.js` 文件顶部。
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. 将以下常量添加到 `listener.js` 文件，用于保存混合连接详细信息。 将括号中的占位符替换为在创建混合连接时获得的值。
   
   1. `const ns` - 中继命名空间。 请务必使用完全限定的命名空间名称，例如 `{namespace}.servicebus.chinacloudapi.cn`。
   2. `const path` - 混合连接的名称。
   3. `const keyrule` - SAS 密钥的名称。
   4. `const key` - SAS 密钥值。

3. 将以下代码添加到 `listener.js` 文件：
   
    ```js
    var wss = WebSocket.createRelayedServer(
    {
        server : WebSocket.createRelayListenUri(ns, path),
        token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(event.data);
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```
    listener.js 文件的内容应如下所示：
   
    ```js
    const WebSocket = require('hyco-ws');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(event.data);
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```

<!-- Update_Description: update meta properties, wording update, update link -->