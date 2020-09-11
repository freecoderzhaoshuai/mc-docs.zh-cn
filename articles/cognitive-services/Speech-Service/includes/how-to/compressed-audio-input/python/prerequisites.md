---
author: amitkumarshukla
ms.service: cognitive-services
ms.topic: include
origin.date: 03/09/2020
ms.date: 08/03/2020
ms.author: v-tawe
ms.openlocfilehash: e7f297ac3453bb01ba8ff4b30a23b502953857f8
ms.sourcegitcommit: 3821704fee67315badba49cf628af2aa68d98f28
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2020
ms.locfileid: "89317428"
---
处理压缩音频是使用 [`GStreamer`](https://gstreamer.freedesktop.org) 实现的。 出于许可原因，`GStreamer` 二进制文件未编译，也未与语音 SDK 链接。 开发人员需要安装几个依赖项和插件，请参阅[在 Windows 上安装](https://gstreamer.freedesktop.org/documentation/installing/on-windows.html?gi-language=c)。 `GStreamer` 二进制文件需要在系统路径中，以便语音 SDK 可以在运行时加载二进制文件。 如果语音 SDK 能够在运行时找到 `libgstreamer-1.0-0.dll`，这意味着二进制文件在系统路径中。

