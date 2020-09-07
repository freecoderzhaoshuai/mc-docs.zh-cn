---
title: 包含文件
description: 包含文件
services: functions
author: ggailey777
ms.service: azure-functions
ms.topic: include
ms.date: 08/11/2020
ms.author: v-junlch
ms.custom: include file
ms.openlocfilehash: cfc9bdb1460b02b763c9e80694babb669bce71f8
ms.sourcegitcommit: 84606cd16dd026fd66c1ac4afbc89906de0709ad
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88946890"
---
可以通过 Azure Functions 轻松地将 Application Insights 集成从 [Azure 门户]添加到某个函数应用。

1. 在 [Azure 门户][Azure 门户]中，搜索并选择“函数应用”，然后选择你的函数应用。 

1. 选择窗口顶部的“未配置 Application Insights”横幅。 如果看不到此横幅，则应用可能已启用 Application Insights。

    :::image type="content" source="media/functions-connect-new-app-insights/enable-application-insights.png" alt-text="从门户启用 Application Insights":::

1. 展开“更改资源”，使用下表中指定的设置创建 Application Insights 资源。  

    | 设置      | 建议的值  | 描述                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | **新资源名称** | 唯一的应用名称 | 使用与函数应用相同的名称是最方便的，该名称在订阅中必须独一无二。 | 
    | **位置** | 中国北部 | 尽可能使用函数应用所在的同一[区域](https://azure.microsoft.com/regions/)，或与该区域接近的区域。 |

    :::image type="content" source="media/functions-connect-new-app-insights/ai-general.png" alt-text="创建 Application Insights 资源":::

1. 选择“应用”。 

   Application Insights 资源在与函数应用相同的资源组和订阅中创建。 创建资源后，关闭 Application Insights 窗口。

1. 在函数应用中，选择“设置”下的“配置”，然后选择“应用程序设置”。   如果看到名为 `APPINSIGHTS_INSTRUMENTATIONKEY` 的设置，则表明已为在 Azure 中运行的函数应用启用 Application Insights 集成。

[Azure 门户]: https://portal.azure.cn

