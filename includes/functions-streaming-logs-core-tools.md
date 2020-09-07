---
author: ggailey777
ms.author: v-junlch
origin.date: 07/24/2019
ms.date: 09/05/2019
ms.topic: include
ms.service: azure-functions
ms.openlocfilehash: e7f74fd89c1700399c19d8728ddc7edde8d85ca4
ms.sourcegitcommit: 4f1047b6848ca5dd96266150af74633b2e9c77a3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2019
ms.locfileid: "88946887"
---
#### <a name="built-in-log-streaming"></a>内置日志流式处理

使用 `logstream` 选项开始接收在 Azure 中运行的特定函数应用的流式处理日志，如以下示例所示：

```bash
func azure functionapp logstream <FunctionAppName>
```

#### <a name="live-metrics-stream"></a>实时指标流

也可通过包括 `--browser` 选项在新的浏览器窗口中查看函数应用的[实时指标流](../articles/azure-monitor/app/live-stream.md)，如以下示例所示：

```bash
func azure functionapp logstream <FunctionAppName> --browser
```

