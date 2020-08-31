---
title: series_fft() - Azure 数据资源管理器
description: 本文介绍 Azure 数据资源管理器中的 series_fft() 函数。
services: data-explorer
author: orspod
ms.author: v-tawe
ms.reviewer: adieldar
ms.service: data-explorer
ms.topic: reference
origin.date: 08/13/2020
ms.date: 08/18/2020
ms.openlocfilehash: 7fa3fb03e19083f1061ba6c462f9e9daa5afdc4b
ms.sourcegitcommit: f4bd97855236f11020f968cfd5fbb0a4e84f9576
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88556473"
---
# <a name="series_fft"></a>series_fft()

对系列应用快速傅立叶变换 (FFT)。  

series_fft() 函数接受时间/空间域中的一系列复数，使用快速傅立叶变换将其变换为频域。 变换后的复数序列表示原始序列中出现的频率的幅值和相位。 使用互补函数 [series_ifft](series-ifft-function.md) 从频域变换回时间/空间域。

## <a name="syntax"></a>语法

`series_fft(`*x_real* [`,` *x_imaginary*]`)`

## <a name="arguments"></a>参数

* x_real：数值的动态数组，表示要变换的序列的实数部分。
* x_imaginary：一个类似的动态数组，表示序列的虚数部分。 此参数是可选参数，仅当输入序列包含复数时才应指定它。

## <a name="returns"></a>返回

此函数以两个序列返回复合反向 fft。 第一个序列表示实数部分，第二个序列表示虚数部分。

## <a name="example"></a>示例

* 生成一个复杂的序列，其中的实数部分和虚数部分是不同频率的纯正弦波。 使用 FFT 将其变换为频域：

    <!-- csl: https://help.kusto.chinacloudapi.cn:443/Samples -->
    ```kusto
    let sinewave=(x:double, period:double, gain:double=1.0, phase:double=0.0)
    {
        gain*sin(2*pi()/period*(x+phase))
    }
    ;
    let n=128;      //  signal length
    range x from 0 to n-1 step 1 | extend yr=sinewave(x, 8), yi=sinewave(x, 32)
    | summarize x=make_list(x), y_real=make_list(yr), y_imag=make_list(yi)
    | extend (fft_y_real, fft_y_imag) = series_fft(y_real, y_imag)
    | render linechart with(ysplit=panels)
    ```
    
    此查询返回 fft_y_real 和 fft_y_imag：  
    
    :::image type="content" source="images/series-fft-function/series-fft.png" alt-text="序列 fft" border="false":::
    
* 将序列变换为频域，然后应用反向变换以返回原始序列：

    <!-- csl: https://help.kusto.chinacloudapi.cn:443/Samples -->
    ```kusto
    let sinewave=(x:double, period:double, gain:double=1.0, phase:double=0.0)
    {
        gain*sin(2*pi()/period*(x+phase))
    }
    ;
    let n=128;      //  signal length
    range x from 0 to n-1 step 1 | extend yr=sinewave(x, 8), yi=sinewave(x, 32)
    | summarize x=make_list(x), y_real=make_list(yr), y_imag=make_list(yi)
    | extend (fft_y_real, fft_y_imag) = series_fft(y_real, y_imag)
    | extend (y_real2, y_image2) = series_ifft(fft_y_real, fft_y_imag)
    | project-away fft_y_real, fft_y_imag   //  too many series for linechart with panels
    | render linechart with(ysplit=panels)
    ```
    
    此查询返回 y_real2 和 *y_imag2（与 y_real 和 y_imag 相同）：  
    
    :::image type="content" source="images/series-fft-function/series-ifft.png" alt-text="序列 ifft" border="false":::
    