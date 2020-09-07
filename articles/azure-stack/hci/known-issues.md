---
title: Azure Stack HCI 的已知问题
description: 本主题详细介绍 Azure Stack HCI 的已知问题。
author: WenJason
ms.author: v-jay
ms.topic: troubleshooting
origin.date: 07/21/2020
ms.date: 08/31/2020
ms.openlocfilehash: 548dbe291688779c53f7b2848259e041eba0d1fd
ms.sourcegitcommit: 4e2d781466e54e228fd1dbb3c0b80a1564c2bf7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88871714"
---
# <a name="known-issues-for-azure-stack-hci"></a>Azure Stack HCI 的已知问题

>适用于：Azure Stack HCI，版本 20H2

本主题详细介绍 Azure Stack HCI 的已知问题

- Azure Stack HCI 云服务当前仅在选定区域可用。
- Azure Stack HCI 于 2020 年 7 月 21 日公布。 其 Azure 门户用户界面扩展可能需要几天的时间才能在全球范围内可见。 在此期间，你可能会看到你的群集被表示为 Azure 门户中的默认资源页。 感谢你的耐心等待。
- 以交互方式登录到操作系统时，欢迎屏幕会显示“欢迎使用 Azure Stack HCI”。 此外，在除英语以外的所有其他语言中，“[Y]es/[N]o”这类输入提示仅接受值“Y”和“N”。
- 如果使用嵌套虚拟化评估 Azure Stack HCI，你可能会遇到类似于“由于未启用虚拟化支持而无法安装 Hyper-V”的错误，因为 Azure Stack HCI 依赖于基于虚拟化的安全性。 有两种可能的解决方法：(1) 改为使用 Hyper-V 第 1 代虚拟机；或者 (2) 将 Hyper-V 功能脱机插入到 VM 的 VHDX。 从主机处，在当 Azure Stack HCI 节点关闭时充当其节点的 VM 上运行以下 PowerShell 命令：Install-WindowsFeature -Vhd <path> -Name Hyper-V, RSAT-Hyper-V-Tools, Hyper-V-Powershell。
