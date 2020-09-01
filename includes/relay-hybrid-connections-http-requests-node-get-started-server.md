---
title: include 文件
description: include 文件
services: service-bus-relay
author: rockboyfor
ms.service: service-bus-relay
ms.topic: include
origin.date: 05/02/2018
ms.date: 07/27/2020
ms.testscope: yes
ms.testdate: 07/27/2020
ms.author: v-yeche
ms.custom: include file
ms.openlocfilehash: fd68a48386fd0060cb6c1714a75c60fd7e4f6f8a
ms.sourcegitcommit: 091c672fa448b556f4c2c3979e006102d423e9d7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2020
ms.locfileid: "88947120"
---
<!--Verified successfully-->
### <a name="create-a-nodejs-application"></a>创建 Node.js 应用程序

创建一个名为 `listener.js` 的新 JavaScript 文件。

### <a name="add-the-relay-npm-package"></a>添加中继 NPM 包

从项目文件夹中的 Node 命令提示符运行 `npm install hyco-https`。

### <a name="write-some-code-to-handle-requests"></a>编写一些代码以处理请求

1. 将下面的常量添加到 `listener.js` 文件顶部。

    ```js
    const https = require('hyco-https');
    ```
2. 将以下常量添加到 `listener.js` 文件，用于保存混合连接详细信息。 将括号中的占位符替换为在创建混合连接时获得的值。

    1. `const ns` - 中继命名空间。 请务必使用完全限定的命名空间名称，例如 `{namespace}.servicebus.chinacloudapi.cn`。
    2. `const path` - 混合连接的名称。
    3. `const keyrule` - SAS 密钥的名称。
    4. `const key` - SAS 密钥值。

3. 将以下代码添加到 `listener.js` 文件。 解码的字符：

    可以发现，该代码与 Node.js 入门教程中提供的任何简单 HTTP 服务器示例并无太大不同，只是使用的是 `createRelayedServer` 而不是典型的 `createServer` 函数。

    ```js
    var uri = https.createRelayListenUri(ns, path);
    var server = https.createRelayedServer(
        {
            server : uri,
            token : () => https.createRelayToken(uri, keyrule, key)
        },
        (req, res) => {
            console.log('request accepted: ' + req.method + ' on ' + req.url);
            res.setHeader('Content-Type', 'text/html');
            res.end('<html><head><title>Hey!</title></head><body>Relayed Node.js Server!</body></html>');
        });

    server.listen( (err) => {
            if (err) {
              return console.log('something bad happened', err)
            }
            console.log(`server is listening on ${port}`)
          });

    server.on('error', (err) => {
        console.log('error: ' + err);
    });
    ```
    listener.js 文件的内容应如下所示：
   
    ```js
    const https = require('hyco-https');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var uri = https.createRelayListenUri(ns, path);
    var server = https.createRelayedServer(
        {
            server : uri,
            token : () => https.createRelayToken(uri, keyrule, key)
        },
        (req, res) => {
            console.log('request accepted: ' + req.method + ' on ' + req.url);
            res.setHeader('Content-Type', 'text/html');
            res.end('<html><head><title>Hey!</title></head><body>Relayed Node.js Server!</body></html>');
        });

    server.listen( (err) => {
            if (err) {
              return console.log('something bad happened', err)
            }
            console.log(`server is listening on ${port}`)
          });

    server.on('error', (err) => {
        console.log('error: ' + err);
    });
    ```

