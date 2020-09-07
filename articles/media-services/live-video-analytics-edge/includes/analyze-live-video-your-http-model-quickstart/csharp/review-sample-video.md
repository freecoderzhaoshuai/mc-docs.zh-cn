---
ms.openlocfilehash: 2a983431fa2cf538a1e556146cc4f96601be6edf
ms.sourcegitcommit: 2eb5a2f53b4b73b88877e962689a47d903482c18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89413601"
---
设置 Azure 资源时，一个高速公路车流量短视频被复制到 Azure 中用作 IoT Edge 设备的 Linux VM 上。 此快速入门使用视频文件来模拟实时流。

打开一个应用程序，例如 [VLC 媒体播放器](https://www.videolan.org/vlc/)。 选择 `Ctrl+N`，然后粘贴指向[高速公路交叉口示例视频](https://lvamedia.blob.core.windows.net/public/camera-300s.mkv)的链接以开始播放。 可以看到许多车辆在高速公路上行驶的镜头。

在本快速入门中，你在 IoT Edge 上使用实时视频分析来检测车辆和人员等对象。 将关联的推理事件发布到 IoT Edge 中心。
