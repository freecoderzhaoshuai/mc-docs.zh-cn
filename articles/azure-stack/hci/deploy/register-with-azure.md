---
title: 将 Azure Stack HCI 连接到 Azure
description: 如何使用 Azure 注册 Azure Stack HCI。
author: WenJason
ms.author: v-jay
ms.topic: how-to
origin.date: 07/27/2020
ms.date: 08/31/2020
ms.openlocfilehash: fe432a24af1c9019ffcaa003a9d646c7db133c4d
ms.sourcegitcommit: 4e2d781466e54e228fd1dbb3c0b80a1564c2bf7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88871640"
---
# <a name="connect-azure-stack-hci-to-azure"></a>将 Azure Stack HCI 连接到 Azure

> 适用于 Azure Stack HCI v20H2；Windows Server 2019

根据 Azure 在线服务条款，Azure Stack HCI 作为 Azure 服务提供，需要在安装后 30 天内进行注册。 本主题介绍如何向 [Azure Arc](https://azure.microsoft.com/services/azure-arc/) 注册 Azure Stack HCI 群集，以实现监视、支持、计费和混合服务。 注册后，将创建一个 Azure 资源管理器资源来表示每个本地 Azure Stack HCI 群集，从而有效地将 Azure 管理平面扩展到 Azure Stack HCI。 信息会定期在 Azure 资源和本地群集之间进行同步。 

## <a name="prerequisites-for-registration"></a>注册的先决条件

在创建 Azure Stack HCI 群集之前，将无法向 Azure 注册。 节点可以是物理计算机或虚拟机，但是它们必须具有统一可扩展固件接口 (UEFI)，这意味着不能使用 Hyper-V 第 1 代虚拟机。 Azure Arc 注册是 Azure Stack HCI 的本机功能，因此不需要代理。

### <a name="internet-access"></a>Internet 访问权限

Azure Stack HCI 节点需要连接到云才能连接到 Azure。 例如，出站 ping 应成功：

```PowerShell
C:\> ping bing.com
```

### <a name="azure-subscription"></a>Azure 订阅

如果还没有 Azure 帐户，请[创建一个](https://wd.azure.cn/zh-cn/pricing/1rmb-trial-full/?form-type=identityauth)。 

可以使用任何类型的现有订阅：
- [提前支付](https://www.azure.cn/offers/ms-mc-arz-33p/)订阅
- 通过企业协议 (EA) 获取的订阅
- 通过云解决方案提供商 (CSP) 计划获取的订阅

### <a name="azure-active-directory-permissions"></a>Azure Active Directory 权限

需要具有 Azure Active Directory 权限才能完成注册过程。 如果还没有这些权限，请让 Azure AD 管理员向你授予或委托这些权限。 有关详细信息，请参阅[管理 Azure 注册](../manage/manage-azure-registration.md#azure-active-directory-permissions)。

## <a name="register-using-powershell"></a>使用 PowerShell 注册

通过在运行 Azure Stack HCI 操作系统的群集中的一个或多个服务器上运行以下 PowerShell 命令，为 Azure Stack HCI 安装 PowerShell 模块：

```PowerShell
Install-WindowsFeature RSAT-Azure-Stack-HCI -ComputerName Server1
```

在群集节点或管理 PC 上安装所需的 cmdlet：

```PowerShell
Install-Module Az.StackHCI
```
   > [!NOTE]
   > 1. 你可能会看到一条提示，例如“是否希望 PowerShellGet 立即安装并导入 NuGet 提供程序?”， 你应该回答“是(Y)”。
   > 2. 系统可能还会提示“是否确定要从 'PSGallery' 安装模块?”，你应该回答“是(Y)”。
   > 3. 最后，你可能会假定安装整个 Az 模块将包括 StackHCI 子模块，从长远来看，这将是正确的 。 但是，按照标准 Azure PowerShell 约定，不会自动包括预览版中的子模块；你需要显式指定它们。 因此，目前需要显式要求安装 Az.StackHCI，如上所示。

为获得最简单的体验，请在 Azure Stack HCI 群集节点上运行以下命令（这将提示进行 Azure 登录）：

```PowerShell
Register-AzStackHCI  -SubscriptionId "e569b8af-6ecc-47fd-a7d5-2ac7f23d8bfe" [-ResourceName] [-ResourceGroupName]
```

最简语法仅需要 Azure 订阅 ID。 使用此语法，将在默认的 Azure 区域和云环境中，使用 Azure 资源和资源组的智能默认名称，以当前用户身份注册本地群集（本地服务器是其中的成员）。 

如果希望使用管理 PC 注册群集，请为 -ComputerName 参数提供群集中服务器的名称和凭据（如果需要）：

```PowerShell
Register-AzStackHCI  -SubscriptionId "e569b8af-6ecc-47fd-a7d5-2ac7f23d8bfe" -ComputerName Server1 [–Credential] [-ResourceName] [-ResourceGroupName]
```

默认情况下，创建用于表示 Azure Stack HCI 群集的 Azure 资源会继承群集名称，并放置在具有相同名称但添加了后缀“-rg”的新资源组中。 可以指定其他资源名称，也可以使用上面列出的可选参数将资源放入现有资源组中。

请记住，运行 `Register-AzStackHCI` cmdlet 的用户必须具有 [Azure Active Directory 权限](../manage/manage-azure-registration.md#azure-active-directory-permissions)，否则注册过程将不会完成；相反，它将退出并使注册挂起以等待管理员同意。 授权后，只需重新运行 `Register-AzStackHCI` 即可完成注册。

   > [!NOTE]
   > 如果注册后收到如下错误消息，请在 24-48 小时内再次尝试注册。 Azure 集成仍处于跨区域推出的过程中。 你仍然可以继续进行评估，并且不会影响任何功能。 请确保稍后回来注册！
   >
   > `Register-AzStackHCI : Azure Stack HCI is not yet available in region <regionName>`
   >
   > 若要检查 Azure Stack HCI 在 Azure 区域中是否可用，请[使用此工具](https://azure.microsoft.com/global-infrastructure/services/?regions=china-non-regional,china-east,china-east-2,china-north,china-north-2&products=all)并搜索“hci”。

## <a name="authenticate-with-azure"></a>使用 Azure 进行身份验证
安装依赖项并验证参数后，需要使用 Azure 帐户进行身份验证（登录）。 帐户需要有权访问指定的 Azure 订阅才能继续进行注册。

如果在无法呈现交互式 Azure 登录窗口的 Azure Stack HCI 操作系统上本地运行 `Register-AzStackHCI`，系统将提示你在另一台设备（如 PC 或手机）上访问 microsoft.com/deviceloginchina。请输入代码，然后在该处登录。 这与 Microsoft 用于输入方式受限的其他设备（例如 Xbox）的体验是相同的。

如果从具有桌面体验的管理 PC（如 Windows 10）远程运行 `Register-AzStackHCI`，则会弹出一个交互式 Azure 登录窗口。 显示的确切提示将因安全设置（例如双重身份验证）而异。 按照提示进行登录。

注册工作流将检测到你的登录并继续完成注册。 然后，你应该能够在 Azure 门户中看到你的群集。

## <a name="next-steps"></a>后续步骤

现在可以执行以下操作：

- [验证群集](validate.md)
- [创建卷](../manage/create-volumes.md)
