---
title: Azure 启动诊断
description: Azure 启动诊断和托管启动诊断概述
services: virtual-machines
ms.service: virtual-machines
author: rockboyfor
ms.topic: conceptual
origin.date: 08/04/2020
ms.date: 08/31/2020
ms.testscope: no
ms.testdate: ''
ms.author: v-yeche
ms.openlocfilehash: 4beceb05c944bc554e29b7f7ec603d3a548d7160
ms.sourcegitcommit: 63a4bc7c501fb6dd54a31d39c87c0e8692ac2eb0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89052426"
---
# <a name="azure-boot-diagnostics"></a>Azure 启动诊断

启动诊断是 Azure 虚拟机 (VM) 的一项调试功能，可用于诊断 VM 启动故障。 启动诊断使用户能够通过收集串行日志信息和屏幕截图来观察其 VM 在启动时的状态。

## <a name="boot-diagnostics-view"></a>启动诊断视图
虚拟机边栏选项卡中的启动诊断选项位于 Azure 门户的“支持和故障排除”部分。 选择启动诊断会显示屏幕截图和串行日志信息。 串行日志包含内核消息，屏幕快照是 VM 当前状态的快照。 Windows 或 Linux 会根据 VM 是否正在运行来确定预期的屏幕快照会是什么样子。 Windows 用户会看到桌面背景，Linux 用户会看到登录提示。

:::image type="content" source="./media/boot-diagnostics/boot-diagnostics-linux.png" alt-text="Linux 启动诊断的屏幕截图":::
:::image type="content" source="./media/boot-diagnostics/boot-diagnostics-windows.png" alt-text="Windows 启动诊断的屏幕截图":::

## <a name="limitations"></a>限制
- 启动诊断仅适用于 Azure 资源管理器 VM。 
- 启动诊断不支持高级存储帐户。如果将高级存储帐户用于启动诊断，则在启动 VM 时，用户会收到 `StorageAccountTypeNotSupported` 错误。 

## <a name="next-steps"></a>后续步骤

详细了解如何使用启动诊断功能来[排查 Azure 中虚拟机的问题](/virtual-machines/troubleshooting/boot-diagnostics)。

<!--Not Available on the [Azure Serial Console](/virtual-machines/troubleshooting/serial-console-overview)-->
<!-- Update_Description: update meta properties, wording update, update link -->
