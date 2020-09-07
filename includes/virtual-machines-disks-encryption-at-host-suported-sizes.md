---
title: 包含文件
description: 包含文件
services: virtual-machines
author: rockboyfor
ms.service: virtual-machines
ms.topic: include
origin.date: 07/08/2020
ms.date: 08/10/2020
ms.testscope: no
ms.testdate: 08/10/2020
ms.author: v-yeche
ms.custom: include file
ms.openlocfilehash: d67b44f06914a4798b50a77c025aa9037c06a710
ms.sourcegitcommit: ac70b12de243a9949bf86b81b2576e595e55b2a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "88946898"
---
<!--Verified successfully-->
所有最新一代的 VM，无论容量多大，都支持主机加密：

|类型  |不支持  |支持  |
|---------|---------|---------|
|常规用途     | Dv3, Dv2, Av2        | B, DSv2, Dsv3         |
|计算优化     |         | Fsv2        |
|内存优化     | Ev3        | DSv2, Esv3, M        |
|GPU     |        | NCv3        |
|前几代     | F, A, D       | DS, Fs       |

<!--Not Available on  |General purpose    | Dav4 | DC, DCv2, Dasv4 |-->
<!--Not Available on  |Memory optimized | Eav4 | Mv2, Easv4 |-->
<!--Not Available on  |Storage optimized     |         | Ls, Lsv2 (NVMe disks not encrypted)        |-->
<!--Not Available on  |GPU     | NC, NV        | NCv2, ND, NVv3, NVv4, NDv2 (preview)        |-->
<!--Not Available on  |High performance compute     | H        | HB, HC, HBv2        |-->
<!--Not Available on  |Previous generations     |  L, G        | GS, NVv2        |-->

升级 VM 大小将导致进行验证，以检查新 VM 大小是否支持 EncryptionAtHost 功能。

<!-- Update_Description: new article about virtual machines disks encryption at host suported sizes -->
<!--NEW.date: 08/10/2020-->