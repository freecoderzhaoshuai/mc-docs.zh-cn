---
title: 参考：Data Science Virtual Machine 映像停用
titleSuffix: Azure Data Science Virtual Machine
description: 有关影响 Azure Data Science Virtual Machine 的停用的详细信息
author: lobrien
ms.service: machine-learning
ms.subservice: data-science-vm
ms.author: laobri
ms.date: 07/17/2020
ms.topic: reference
ms.openlocfilehash: bffbcc76faf2a8ef331063f0bcf2c519e377e48f
ms.sourcegitcommit: 78c71698daffee3a6b316e794f5bdcf6d160f326
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90021176"
---
# <a name="reference-retirements-of-dsvm-images"></a>参考：DSVM 映像的停用

下文讨论了映像的停用（弃用），并提供了建议以用于处理即将到来的有关 Azure Data Science Virtual Machine 的停用。

## <a name="why-we-retire-dsvm-images"></a>停用 DSVM 映像的原因

Data Science Virtual Machine 当前有两个版本：

* Ubuntu
* Windows Server

这些版本的 DSVM 映像是基于特定操作系统版本（例如 Ubuntu 18.04 LTS）构建的。 随着时间的推移，操作系统版本的维护时段将会结束，并且/或者数据科学工具将不再支持较早的操作系统版本。 为了使 DSVM 映像时时能够与最新的操作系统和数据科学工具保持一致，我们会根据更新的操作系统版本发布新的 DSVM 映像。

## <a name="how-we-retire-dsvm-images"></a>如何停用 DSVM 映像

我们会发布停用公告，通过电子邮件通知现有的 DSVM 用户即将停用 DSVM 映像。 停用公告将详细说明停用日期（此日期之后不再提供该映像）和缓和处理建议（例如，升级到较新的 DSVM 映像）。

在公告日当天，我们将在市场中隐藏该映像，以便：

1. 防止新用户无意中预配已停用的 DSVM 映像。
2. 现有用户在停用日期之前可以继续使用 ARM 部署。

隐藏的映像在停用日期之前将会继续接收操作系统补丁，但不会接收对数据科学工具和框架的更新。 在停用日当天，该映像将无法用于 ARM 部署。

你的订阅中任何预配的 DSVM 映像在停用日期之后将会继续正常工作。 但我们还是建议升级到最新 DSVM 映像，以便你使用最新的操作系统和数据科学工具。

## <a name="impact"></a>影响

你的订阅中现有的已预配 DSVM 映像在停用日期之后将会继续正常工作。 但我们还是建议用户使用 Azure 门户或 ARM 模板将其 DSVM 映像升级到较新的版本。

> [!WARNING]
> 在停用日期之后，已停用的使用虚拟机规模集预配的 DSVM 映像将无法纵向扩展。
>
> 在停用日期之后，尚未使用新 DSVM 映像详细信息更新的 ARM 模板将无法部署。

