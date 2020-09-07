---
title: 管理 Azure 媒体服务 v3 帐户 | Microsoft Docs
description: 若要开始管理、加密、编码和流式处理 Azure 中的媒体内容，需要创建媒体服务帐户。 本文介绍如何管理 Azure 媒体服务 v3 帐户。
services: media-services
documentationcenter: ''
author: WenJason
manager: digimobile
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
origin.date: 07/08/2019
ms.date: 09/07/2020
ms.author: v-jay
ms.openlocfilehash: c18bbaab3ff6b53c2c92267b6da08bc806eb3070
ms.sourcegitcommit: 2eb5a2f53b4b73b88877e962689a47d903482c18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89413461"
---
# <a name="manage-azure-media-services-v3-accounts"></a>管理 Azure 媒体服务 v3 帐户

若要开始管理、加密、编码和流式处理 Azure 中的媒体内容，需要创建媒体服务帐户。 创建媒体服务帐户时，需要提供 Azure 存储帐户资源的名称。 指定存储帐户会附加到媒体服务帐户。 媒体服务帐户和所有关联的存储帐户必须位于同一 Azure 订阅中。 有关详细信息，请参阅[存储帐户](storage-account-concept.md)。

## <a name="moving-a-media-services-account-between-subscriptions"></a>在订阅之间移动媒体服务帐户 

如果需要将媒体服务帐户移到新订阅，需要先将包含媒体服务帐户的整个资源组移到新订阅。 必须移动所有附加资源：Azure 存储帐户等。有关详细信息，请参阅[将资源移到新资源组或订阅](../../azure-resource-manager/management/move-resource-group-and-subscription.md)。 与 Azure 中的任何资源一样，资源组移动可能需要一些时间才能完成。

> [!NOTE]
> 媒体服务 v3 支持多租户模型。

### <a name="considerations"></a>注意事项

* 在迁移到其他订阅之前，请创建帐户中所有数据的备份。
* 需要停止所有流式处理终结点和实时传送视频流资源。 在资源组移动期间，你的用户将无法访问你的内容。 

> [!IMPORTANT]
> 在移动成功完成之前，请勿启动流式处理终结点。

### <a name="troubleshoot"></a>故障排除 

如果媒体服务帐户或关联的 Azure 存储帐户在资源组移动后变为“已断开连接”状态，请尝试轮换存储帐户密钥。 如果轮换存储帐户密钥不能解决媒体服务帐户的“已断开连接”状态，请通过媒体服务帐户中的“支持 + 疑难解答”菜单来提交新的支持请求。  

## <a name="next-steps"></a>后续步骤

[创建帐户](./create-account-howto.md)
