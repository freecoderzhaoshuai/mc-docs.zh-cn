---
author: rockboyfor
ms.service: service-bus-relay
ms.topic: include
origin.date: 11/09/2018
ms.date: 07/27/2020
ms.testscope: yes
ms.testdate: 07/27/2020
ms.author: v-yeche
ms.openlocfilehash: a6d2d311f6b981210a0779fc0d5f79d4d42473b3
ms.sourcegitcommit: 091c672fa448b556f4c2c3979e006102d423e9d7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2020
ms.locfileid: "88947122"
---
<!--Verified successfully-->
确保已[创建中继命名空间][namespace-how-to]。

1. 登录到 [Azure 门户](https://portal.azure.cn)。
2. 在左侧菜单中，选择“所有资源”  。
3. 选择要在其中创建混合连接的命名空间。 在本示例中，该命名空间为 **mynewns**。  
4. 在“中继命名空间”下选择“混合连接”。  

    ![创建混合连接](./media/relay-create-hybrid-connection-portal/create-hc-1.png)

5. 在命名空间概览窗口中，选择“+ 混合连接” 
   
    ![选择混合连接](./media/relay-create-hybrid-connection-portal/create-hc-2.png)
    
6. 在“创建混合连接”下输入一个值，作为混合连接名称。  保留其他默认值。
   
    ![选择“新建”](./media/relay-create-hybrid-connection-portal/create-hc-3.png)
    
7. 选择“创建”  。

[namespace-how-to]: ../articles/service-bus-relay/relay-create-namespace-portal.md

<!-- Update_Description: update meta properties, wording update, update link -->