---
title: include 文件
description: include 文件
services: storage
author: WenJason
ms.service: storage
ms.topic: include
origin.date: 12/27/2019
ms.date: 07/20/2020
ms.author: v-jay
ms.custom: include file
ms.openlocfilehash: b60377b711abe113a5a97cca0290acdf44acf15a
ms.sourcegitcommit: 31da682a32dbb41c2da3afb80d39c69b9f9c1bc6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "88753582"
---
Azure 文件存储提供了两种不同的存储层（高级和标准），可让你根据方案的性能和价格要求定制共享：

- 高级文件共享：高级文件共享由固态硬盘 (SSD) 支持，并部署在 FileStorage 存储帐户类型中。 高级文件共享提供稳定的高性能和低延迟，对于大多数 IO 操作和 IO 密集型工作负荷，延迟不到 10 毫秒。 这使得它们适合于各种各样的工作负荷，例如数据库、网站托管和开发环境。 高级文件共享只能在预配的计费模型下使用。 有关高级文件共享的预配计费模型的详细信息，请参阅[了解预配高级文件共享](../articles/storage/files/storage-files-planning.md#understanding-provisioning-for-premium-file-shares)。
- 标准文件共享：标准文件共享由硬盘驱动器 (HDD) 提供支持，部署在**常规用途版本2 (GPv2) 存储帐户**类型中。 标准文件共享为对性能波动不太敏感的 IO 工作负荷（例如，常规用途文件共享和开发/测试环境）提供可靠的性能。