---
author: trevorbye
ms.service: cognitive-services
ms.topic: include
origin.date: 04/03/2020
ms.date: 07/29/2020
ms.author: v-tawe
ms.openlocfilehash: 6580145593ff78b956bd0f5a33a4664dabd524d1
ms.sourcegitcommit: 5d167ad5411b018522a0fac9f5435a48f4ceb3a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "89317456"
---
## <a name="prerequisites"></a>先决条件

准备工作：

> [!div class="checklist"]
> * <a href="https://portal.azure.cn/#create/Microsoft.CognitiveServicesSpeechServices" target="_blank">创建 Azure 语音资源<span class="docon docon-navigate-external x-hidden-focus"></span></a>
> * [设置开发环境并创建空项目](../../../../quickstarts/setup-platform.md?pivots=programming-language-python)
> * 请确保你有权访问麦克风，以便进行音频捕获
> * 需要语音 SDK 1.11.0 或更高版本。

## <a name="source-code"></a>源代码

创建名为“quickstart.py”的文件并在其中粘贴以下 Python 代码。

```
import azure.cognitiveservices.speech as speechsdk

# Creates an instance of a speech config with specified subscription key and service region.
# Replace with your own subscription key and service region (e.g., "chinaeast2").
speech_key, service_region = "YourSubscriptionKey", "YourServiceRegion"
speech_config = speechsdk.SpeechConfig(subscription=speech_key, region=service_region)

# Creates a recognizer with the given settings
speech_recognizer = speechsdk.SpeechRecognizer(speech_config=speech_config)

print("Say something...")


# Starts speech recognition, and returns after a single utterance is recognized. The end of a
# single utterance is determined by listening for silence at the end or until a maximum of 15
# seconds of audio is processed.  The task returns the recognition text as result. 
# Note: Since recognize_once() returns only a single utterance, it is suitable only for single
# shot recognition like command or query. 
# For long-running multi-utterance recognition, use start_continuous_recognition() instead.
result = speech_recognizer.recognize_once()

# Checks result.
if result.reason == speechsdk.ResultReason.RecognizedSpeech:
    print("Recognized: {}".format(result.text))
elif result.reason == speechsdk.ResultReason.NoMatch:
    print("No speech could be recognized: {}".format(result.no_match_details))
elif result.reason == speechsdk.ResultReason.Canceled:
    cancellation_details = result.cancellation_details
    print("Speech Recognition canceled: {}".format(cancellation_details.reason))
    if cancellation_details.reason == speechsdk.CancellationReason.Error:
        print("Error details: {}".format(cancellation_details.error_details))
```

[!INCLUDE [replace key and region](../replace-key-and-region.md)]

## <a name="code-explanation"></a>代码说明

[!INCLUDE [code explanation](../code-explanation.md)]

## <a name="build-and-run-app"></a>生成并运行应用

现在，可以使用语音服务测试语音识别。 

如果在 macOS 上运行此程序，并且它是使用麦克风构建的第一个 Python 应用，则可能需要为该麦克风指定终端访问权限。 打开“系统设置”并选择“安全与隐私” 。 接下来，选择“隐私”并在列表中找到“麦克风” 。 最后，选择“终端”并保存。 

1. **启动应用** - 在命令行中键入：
    ```bash
    python quickstart.py
    ```
2. **开始识别** - 它会提示你说英语短语。 语音将发送到语音服务，转录为文本，并在控制台中呈现。

## <a name="next-steps"></a>后续步骤

[!INCLUDE [Speech recognition basics](../../speech-to-text-next-steps.md)]
