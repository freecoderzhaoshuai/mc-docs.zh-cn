---
author: trevorbye
ms.service: cognitive-services
ms.topic: include
origin.date: 03/09/2020
ms.date: 09/02/2020
ms.author: v-tawe
ms.custom: devx-track-csharp
ms.openlocfilehash: d7454eb8a2a6b6d76b56f83919d95a82da418e45
ms.sourcegitcommit: 4db9853370c9d4c7e5d54f1e1cfadf40efcc12a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89317429"
---
若要以压缩音频格式流式传输到语音服务，请创建 `PullAudioInputStream` 或 `PushAudioInputStream`。 然后，从流类的实例创建 `AudioConfig`，并指定流的压缩格式。

让我们假设你有一个名为 `pushStream` 的输入流类，并且使用 OPUS/OGG。 你的代码可能如下所示：

```csharp
using Microsoft.CognitiveServices.Speech;
using Microsoft.CognitiveServices.Speech.Audio;

// ... omitted for brevity

var speechConfig =
    SpeechConfig.FromSubscription(
        "YourSubscriptionKey",
        "YourServiceRegion");

// Create an audio config specifying the compressed
// audio format and the instance of your input stream class.
var audioFormat =
    AudioStreamFormat.GetCompressedFormat(
        AudioStreamContainerFormat.OGG_OPUS);
var audioConfig =
    AudioConfig.FromStreamInput(
        pushStream,
        audioFormat);

using var recognizer = new SpeechRecognizer(speechConfig, audioConfig);
var result = await recognizer.RecognizeOnceAsync();

var text = result.Text;
```