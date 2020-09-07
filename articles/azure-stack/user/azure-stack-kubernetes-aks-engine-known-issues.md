---
title: 在 Azure Stack Hub 上使用 AKS 引擎的已知问题
description: 了解在 Azure Stack Hub 上使用 AKS 引擎的已知问题。
author: WenJason
ms.topic: article
origin.date: 08/05/2020
ms.date: 08/31/2020
ms.author: v-jay
ms.reviewer: waltero
ms.lastreviewed: 08/05/2020
ms.openlocfilehash: 625a6ee3a99a1811fe8d863a37e829673946a827
ms.sourcegitcommit: 4e2d781466e54e228fd1dbb3c0b80a1564c2bf7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88867936"
---
# <a name="known-issues-with-the-aks-engine-on-azure-stack-hub"></a>在 Azure Stack Hub 上使用 AKS 引擎的已知问题

本主题介绍 Azure Stack Hub 上的 AKS 引擎的已知问题。

## <a name="upgrade-issues-in-aks-engine-0510"></a>AKS 引擎 0.51.0 中的升级问题

* 在将 Kubernetes 群集从 1.15.x 版升级到 1.16.x 版（aks 引擎升级）期间，以下 Kubernetes 组件的升级需要额外的手动步骤：kube-proxy、azure-cni-networkmonitor、csi-secrets-store、kubernetes-dashboard。 下面描述了你可能观察到的情况以及如何解决这些问题。

  * 在已连接的环境中，由于群集中没有迹象表明受影响的组件未升级，因此不会明显注意到此问题。 一切似乎都按预期进行。
  <!-- * In disconnected environments, you can see this problem when you run a query for the system pods status and see that the pods for the components mentioned below are not in "Ready" state: -->

    ```bash  
    kubectl get pods -n kube-system
    ```

  * 若要为上述每个组件解决此问题，请运行下表的“解决方法”列中的命令。

    |组件名称 |解决方法 |受影响方案|
    |---------------|-----------|------------------|
    |kube-proxy     | `kubectl delete ds kube-proxy -n kube-system` |已连接、离线 |
    |azure-cni-networkmonitor   | `kubectl delete ds azure-cni-networkmonitor -n kube-system`   | 已连接、离线 |
    |csi-secrets-store  |`sudo sed -i s/Always/IfNotPresent/g /etc/kubernetes/addons/secrets-store-csi-driver.yaml`<br>`kubectl delete ds csi-secrets-store -n kube-system` | 已断开连接 |
    |kubernetes-dashboard |在每个主节点上运行以下命令：<br>`sudo sed -i s/Always/IfNotPresent/g /etc/kubernetes/addons/kubernetes-dashboard.yaml` |已断开连接 |

* 此版本不支持 Kubernetes 1.17。 尽管有 GitHub 拉取请求 (PR) 引用 1.17，但它不受支持。

## <a name="aks-engine-get-versions-command-limitations"></a>aks-engine get-versions 命令限制

aks-engine `get-versions` 命令的输出仅与全局 Azure 相关，与 Azure Stack Hub 不相关。 有关不同升级路径的详细信息，请参阅[升级到更新 Kubernetes 版本的步骤](azure-stack-kubernetes-aks-engine-upgrade.md#steps-to-upgrade-to-a-newer-kubernetes-version)。

## <a name="next-steps"></a>后续步骤

[Azure Stack Hub 上的 AKS 引擎概述](azure-stack-kubernetes-aks-engine-overview.md)
