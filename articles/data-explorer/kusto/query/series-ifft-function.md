---
title: series_ifft() - Azure 数据资源管理器
description: 本文介绍 Azure 数据资源管理器中的 series_ifft() 函数。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: adieldar
ms.service: data-explorer
ms.topic: reference
origin.date: 08/13/2020
ms.date: 08/18/2020
ms.openlocfilehash: 1709429220167790d162abc8f7aa6f6965a64c3b
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88556465"
---
# <a name="series_ifft"></a>series_ifft()

对系列应用快速傅立叶逆变换 (IFFT)。  

series_ifft() 函数接受频域中的一系列复数，使用快速傅立叶变换将其变换回时间/空间域。 此函数是 [series_fft](series-fft-function.md) 的互补函数。 通常，原始序列会变换为用于频谱处理的频域，然后再变换回时间/空间域。

## <a name="syntax"></a>语法

`series_ifft(`*fft_real* [`,` *fft_imaginary*]`)`

## <a name="arguments"></a>参数

* fft_real：数值的动态数组，表示要变换的序列的实数部分。
* fft_imaginary：一个类似的动态数组，表示序列的虚数部分。 此参数是可选参数，仅当输入序列包含复数时才应指定它。

## <a name="returns"></a>返回

此函数以两个序列返回复合反向 fft。 第一个序列表示实数部分，第二个序列表示虚数部分。

## <a name="example"></a>示例

请参阅 [series_fft](series-fft-function.md#example)
