---
title: 包含文件
description: 包含文件
services: virtual-machines
author: rockboyfor
ms.service: virtual-machines
ms.topic: include
origin.date: 07/10/2020
ms.date: 08/31/2020
ms.testscope: yes
ms.testdate: 08/24/2020
ms.author: v-yeche
ms.custom: include file
ms.openlocfilehash: 62b26a4feb606e519e4830fb65d777d1edba7c31
ms.sourcegitcommit: b5ea35dcd86ff81a003ac9a7a2c6f373204d111d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88946903"
---
<!--Verify Successfully-->
<!--Not Available on ultra disks-->

- 如果在你的 VM/虚拟机规模集上启用了 Azure 磁盘加密（使用 bitlocker/VM-Decrypt 的来宾 VM 加密），则无法启用。
- 无法在启用了主机加密的磁盘上启用 Azure 磁盘加密。
- 可以在现有的虚拟机规模集上启用加密。 但是，只有启用加密后新建的 VM 才会自动加密。
- 现有 VM 只有在经过释放和重新分配后才能加密。

<!-- Update_Description: update meta properties, wording update -->