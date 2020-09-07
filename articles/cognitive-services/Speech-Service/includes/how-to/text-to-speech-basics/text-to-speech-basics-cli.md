---
author: trevorbye
ms.service: cognitive-services
ms.topic: include
origin.date: 08/11/2020
ms.date: 09/02/2020
ms.author: v-tawe
ms.openlocfilehash: 174143cf9fe96ca577e0f28237b917a80baab433
ms.sourcegitcommit: 4db9853370c9d4c7e5d54f1e1cfadf40efcc12a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89323282"
---
[!INCLUDE [SPX Setup](../../spx-setup.md)]

## <a name="synthesize-speech-to-a-speaker"></a>将语音合成到扬声器

现在，可以运行语音 CLI，以从文本合成语音。 在命令行中，更改为包含语音 CLI 二进制文件的目录。 然后，运行以下命令。

```bash
spx synthesize --text "The speech synthesizer greets you!"
```

语音 CLI 将通过计算机扬声器生成英语的自然语言。

## <a name="synthesize-speech-to-a-file"></a>将语音合成到文件中

运行以下命令，将扬声器的输出更改为 `.wav` 文件。

```bash
spx synthesize --text "The speech synthesizer greets you!" --audio output greetings.wav
```

语音 CLI 将采用英文向 `greetings.wav` 音频文件生成自然语言。
在 Windows 中，输入 `start greetings.wav` 可以播放音频文件。