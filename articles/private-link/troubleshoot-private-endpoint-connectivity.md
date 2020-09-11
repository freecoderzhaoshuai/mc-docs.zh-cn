---
title: 排查 Azure 专用终结点连接问题
description: 有关诊断专用终结点连接的分步指导
services: private-endpoint
documentationcenter: na
manager: narayan
editor: ''
ms.service: private-link
ms.devlang: na
ms.topic: troubleshooting
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
origin.date: 01/31/2020
author: rockboyfor
ms.date: 09/07/2020
ms.testscope: no
ms.testdate: 06/15/2020
ms.author: v-yeche
ms.openlocfilehash: a00503dacb40f828aadc328640e3dc288f428c8b
ms.sourcegitcommit: 6e88e0e41b35d160a09f7a906ca3b7e837f51803
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89412104"
---
<!--Verified successfully-->
# <a name="troubleshoot-azure-private-endpoint-connectivity-problems"></a>排查 Azure 专用终结点连接问题

本文提供了有关验证和诊断 Azure 专用终结点连接设置的分步指导。

Azure 专用终结点是一个网络接口，可以通过私密且安全的方式连接到专用链接服务。 此解决方案提供从虚拟网络到 Azure 服务资源的专用连接，帮助保护 Azure 中的工作负荷。 此解决方案可以有效地将这些服务接入虚拟网络。

下面是专用终结点可用的连接方案：

- 同一区域中的虚拟网络
- 区域对等互连的虚拟网络
- 全球对等互连的虚拟网络
- 基于 VPN 或 Azure ExpressRoute 线路的客户本地连接

## <a name="diagnose-connectivity-problems"></a>诊断连接问题 

查看下面的步骤，确保所有一般配置都符合预期，以解决专用终结点的连接问题。

1. 通过浏览资源来查看专用终结点配置。

    a. 在门户的搜索框中键入 `Private Link`，在服务列表中选择 `Private Link`。 转到“专用链接中心”****。


    :::image type="content" source="./media/private-endpoint-tsg/private-endpoints.png" alt-text="专用链接中心":::

    b. 在左侧窗格中，选择“专用终结点”。****

    ![专用终结点](./media/private-endpoint-tsg/private-endpoints.png)

    c. 筛选并选择要诊断的专用终结点。

    d. 查看虚拟网络和 DNS 信息。
    - 验证连接状态是否为“已批准”。
    - 确保 VM 已连接到托管专用终结点的虚拟网络。
    - 检查是否分配了 FQDN 信息（复制）和专用 IP 地址。

       :::image type="content" source="./media/private-endpoint-tsg/vnet-dns-configuration.png" alt-text="虚拟网络和 DNS 配置":::

1. 使用 [Azure Monitor](/azure-monitor/overview) 查看是否有数据在流动。

    a. 在“专用终结点”资源中，选择“监视”****。
    - 选择“传入数据”或“传出数据” 。 
    - 查看在尝试连接到专用终结点时是否有数据在流动。 预计延迟大约为 10 分钟。

       :::image type="content" source="./media/private-endpoint-tsg/private-endpoint-monitor.png" alt-text="验证专用终结点遥测":::

1. 使用 Azure 网络观察程序中的“VM 连接故障排除”****。

    a. 选择客户端 VM。

    b. 选择“连接故障排除”****，然后选择“出站连接”**** 选项卡。

    :::image type="content" source="./media/private-endpoint-tsg/network-watcher-outbound-connection.png" alt-text="网络观察程序 - 测试出站连接":::

    c. 选择“使用网络观察程序进行详细的连接跟踪”****。

    :::image type="content" source="./media/private-endpoint-tsg/network-watcher-connection-troubleshoot.png" alt-text="网络观察程序 - 连接故障排除":::

    d. 选择“按 FQDN 进行测试”****。
     - 从专用终结点资源粘贴 FQDN。
     - 提供一个端口。 通常，对于 Azure 存储或 Azure Cosmos DB，请使用 443；对于 SQL，请使用 1336。

    e. 选择“测试”，验证测试结果****。

    :::image type="content" source="./media/private-endpoint-tsg/network-watcher-test-results.png" alt-text="网络观察程序 - 测试结果":::

1. 测试结果中的 DNS 解析必须包含分配给专用终结点的同一专用 IP 地址。

    a. 如果 DNS 设置不正确，请执行以下步骤：
    - 如果使用专用区域： 
        - 确保客户端 VM 虚拟网络与专用区域相关联。
        - 检查是否存在专用 DNS 区域记录。 如果不存在，请创建它。
    - 如果使用自定义 DNS：
        - 检查你的自定义 DNS 设置，并验证 DNS 配置是否正确。
        有关指南，请参阅[专用终结点概述：DNS 配置](/private-link/private-endpoint-overview#dns-configuration)。

    b. 如果连接由于网络安全组 (NSG) 或用户定义的路由而失败：
    - 检查 NSG 出站规则，并创建相应的出站规则来允许流量。

        :::image type="content" source="./media/private-endpoint-tsg/nsg-outbound-rules.png" alt-text="NSG 出站规则":::

1. 如果连接的验证结果符合预期，则连接问题可能与应用层的其他方面（例如机密、令牌和密码）相关。
    - 在这种情况下，请检查与专用终结点关联的专用链接资源的配置。 有关详细信息，请参阅 [Azure 专用链接故障排除指南](troubleshoot-private-link-connectivity.md)。

1. 如果问题仍未解决，并且连接问题仍然存在，请联系 [Azure 支持](https://support.azure.cn/support/support-azure/)团队。

## <a name="next-steps"></a>后续步骤

 * [在更新的子网上创建专用终结点（Azure 门户）](/private-link/create-private-endpoint-portal)
 * [Azure 专用链接故障排除指南](troubleshoot-private-link-connectivity.md)

<!-- Update_Description: update meta properties, wording update, update link -->