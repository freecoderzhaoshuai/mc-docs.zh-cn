---
title: include 文件
description: include 文件
services: service-bus-messaging
author: rockboyfor
ms.service: service-bus-messaging
ms.topic: include
origin.date: 02/20/2019
ms.date: 07/27/2020
ms.testscope: no
ms.testdate: ''
ms.author: v-yeche
ms.custom: include file
ms.openlocfilehash: 16536b16f52b8980a8b51c941ad4107c59f16c92
ms.sourcegitcommit: 091c672fa448b556f4c2c3979e006102d423e9d7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2020
ms.locfileid: "88946996"
---
## <a name="create-a-topic-using-the-azure-portal"></a>使用 Azure 门户创建主题
1. 在“服务总线命名空间”  页面上，选择左侧菜单中的“主题”  。
2. 在工具栏中选择“+ 主题”。  
4. 输入主题名称  。 将其他选项保留默认值。
5. 选择“创建”  。

    ![创建主题](./media/service-bus-create-topics-subscriptions-portal/create-topic.png)

## <a name="create-subscriptions-to-the-topic"></a>创建对主题的订阅
1. 选择在上一部分创建的主题  。 
    
    ![选择主题](./media/service-bus-create-topics-subscriptions-portal/select-topic.png)
2. 在“服务总线主题”  页面上，从左侧菜单中选择“订阅”  ，然后工具栏上选择“+ 订阅”  。 
    
    ![添加订阅按钮](./media/service-bus-create-topics-subscriptions-portal/add-subscription-button.png)
3. 在“创建订阅”  页面上，输入 **S1** 作为订阅名称  ，然后选择“创建”  。 

    ![创建订阅页面](./media/service-bus-create-topics-subscriptions-portal/create-subscription-page.png)
4. 重复上述步骤两次，创建名为 **S2** 和 **S3** 的订阅。

<!-- Update_Description: update meta properties, wording update, update link -->