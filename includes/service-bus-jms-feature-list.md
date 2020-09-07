---
title: 包含文件
description: 包含文件
services: service-bus-messaging
author: rockboyfor
ms.service: service-bus-messaging
ms.topic: include
origin.date: 06/09/2020
ms.date: 08/31/2020
ms.testscope: yes|no
ms.testdate: 08/24/2020null
ms.author: v-yeche
ms.custom: include file
ms.openlocfilehash: 7871ade616fc4e5eb6419740445bd3edf79662ab
ms.sourcegitcommit: b5ea35dcd86ff81a003ac9a7a2c6f373204d111d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88947555"
---
<!--Verified for charactors only-->
下表列出了 Azure 服务总线当前支持的 Java 消息服务 (JMS) 功能。 它还展示了不支持的功能。

| 功能 | API |状态 |
|---|---|---|
| 队列   | <ul> <li> JMSContext.createQueue(String queueName) </li> </ul>| **支持** |
| 主题   | <ul> <li> JMSContext.createTopic(String topicName) </li> </ul>| **支持** |
| 临时队列 |<ul> <li> JMSContext.createTemporaryQueue() </li> </ul>| **支持** |
| 临时主题 |<ul> <li> JMSContext.createTemporaryTopic() </li> </ul>| **支持** |
| 消息生成者/<br/> JMSProducer |<ul> <li> JMSContext.createProducer() </li> </ul>| **支持** |
| 队列浏览器 |<ul> <li> JMSContext.createBrowser(Queue queue) </li> <li> JMSContext.createBrowser(Queue queue, String messageSelector) </li> </ul> | **支持** |
| 消息使用者/ <br/> JMSConsumer | <ul> <li> JMSContext.createConsumer(Destination destination) </li> <li> JMSContext.createConsumer(Destination destination, String messageSelector) </li> <li> JMSContext.createConsumer(Destination destination, String messageSelector, boolean noLocal)</li> </ul>  <br/> 目前不支持 noLocal | **支持** |
| 共享持久订阅 | <ul> <li> JMSContext.createSharedDurableConsumer(Topic topic, String name) </li> <li> JMSContext.createSharedDurableConsumer(Topic topic, String name, String messageSelector) </li> </ul>| **支持**|
| 非共享持久订阅 | <ul> <li> JMSContext.createDurableConsumer(Topic topic, String name) </li> <li> createDurableConsumer(Topic topic, String name, String messageSelector, boolean noLocal) </li> </ul> <br/> 目前不支持 noLocal，应将其设置为 false | **支持** |
| 共享非持久订阅 |<ul> <li> JMSContext.createSharedConsumer(Topic topic, String sharedSubscriptionName) </li> <li> JMSContext.createSharedConsumer(Topic topic, String sharedSubscriptionName, String messageSelector) </li> </ul> | **支持** |
| 非共享非持久订阅 |<ul> <li> JMSContext.createConsumer(Destination destination) </li> <li> JMSContext.createConsumer(Destination destination, String messageSelector) </li> <li> JMSContext.createConsumer(Destination destination, String messageSelector, boolean noLocal) </li> </ul> <br/> 目前不支持 noLocal，应将其设置为 false | **支持** |
| 消息选择器 | 取决于创建的使用者 | **支持** |
| 交付延迟（计划的消息） | <ul> <li> JMSProducer.setDeliveryDelay(long deliveryDelay) </li> </ul>|**支持**|
| 创建的消息 |<ul> <li> JMSContext.createMessage() </li> <li> JMSContext.createBytesMessage() </li> <li> JMSContext.createMapMessage() </li> <li> JMSContext.createObjectMessage(Serializable object) </li> <li> JMSContext.createStreamMessage() </li> <li> JMSContext.createTextMessage() </li> <li> JMSContext.createTextMessage(String text) </li> </ul>| **支持** |
| 分布式事务 || 不支持 |

<!-- Update_Description: new article about service bus jms feature list -->
<!--NEW.date: 08/17/2020-->