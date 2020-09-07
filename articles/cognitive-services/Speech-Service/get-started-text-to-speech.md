---
title: 语音合成快速入门 - 语音服务
titleSuffix: Azure Cognitive Services
description: 了解如何使用语音 SDK 将文本转换为语音。 本快速入门介绍有关语音合成的对象构造和设计模式、支持的音频输出格式、语音 CLI 以及自定义配置选项。
services: cognitive-services
author: trevorbye
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: quickstart
origin.date: 08/11/2020
ms.date: 09/02/2020
ms.author: v-tawe
ms.custom: devx-track-python, devx-track-javascript, devx-track-csharp
zone_pivot_groups: speech-full-stack
ms.openlocfilehash: 14e9c9bf5544d892c0d7fb1d82c06965e79d7225
ms.sourcegitcommit: 4db9853370c9d4c7e5d54f1e1cfadf40efcc12a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89323285"
---
# <a name="get-started-with-speech-synthesis"></a>语音合成入门

本快速入门介绍使用语音 SDK 进行文本到语音合成的常见设计模式。 首先，请进行基本的配置和合成，然后通过更高级的示例来了解自定义应用程序开发，其中包括：

* 获取内存中流形式的响应
* 自定义输出采样率和比特率
* 使用 SSML（语音合成标记语言）提交合成请求
* 使用神经语音

> [!TIP]
> 如果要直接跳到示例代码，请参阅 GitHub 上的[快速入门示例](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/quickstart)。

::: zone pivot="programming-language-csharp"
[!INCLUDE [C# Basics include](includes/how-to/text-to-speech-basics/text-to-speech-basics-csharp.md)]
::: zone-end

::: zone pivot="programming-language-cpp"
[!INCLUDE [C++ Basics include](includes/how-to/text-to-speech-basics/text-to-speech-basics-cpp.md)]
::: zone-end

::: zone pivot="programming-language-java"
[!INCLUDE [Java Basics include](includes/how-to/text-to-speech-basics/text-to-speech-basics-java.md)]
::: zone-end

::: zone pivot="programming-language-javascript"
[!INCLUDE [JavaScript Basics include](includes/how-to/text-to-speech-basics/text-to-speech-basics-javascript.md)]
::: zone-end

::: zone pivot="programming-language-python"
[!INCLUDE [Python Basics include](includes/how-to/text-to-speech-basics/text-to-speech-basics-python.md)]
::: zone-end

::: zone pivot="programming-language-spx"
[!INCLUDE [CLI include](includes/how-to/text-to-speech-basics/text-to-speech-basics-cli.md)]
::: zone-end

## <a name="next-steps"></a>后续步骤

* [自定义语音入门](how-to-custom-voice.md)
* [通过 SSML 改进合成](speech-synthesis-markup.md)
* 了解如何使用[长音频 API](long-audio-api.md) 来获取大型文本示例，例如书籍和新闻文章
* 请参阅 GitHub 上的[快速入门示例](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/quickstart)
