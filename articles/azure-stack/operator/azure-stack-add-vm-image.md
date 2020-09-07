---
title: 将自定义 VM 映像添加到 Azure Stack Hub
description: 了解如何在 Azure Stack Hub 中添加或删除自定义 VM 映像。
author: WenJason
ms.topic: conceptual
origin.date: 07/14/2020
ms.date: 08/31/2020
ms.author: v-jay
ms.reviewer: kivenkat
ms.lastreviewed: 07/10/2020
ms.openlocfilehash: 577ff4426afeeb268b18f34c65a2e5c1610892b7
ms.sourcegitcommit: 4e2d781466e54e228fd1dbb3c0b80a1564c2bf7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88867891"
---
# <a name="add-a-custom-vm-image-to-azure-stack-hub"></a>将自定义 VM 映像添加到 Azure Stack Hub

在 Azure Stack Hub 中，作为操作员，你可以将虚拟机 (VM) 自定义映像添加到市场供用户使用。 可以通过管理员门户或 Windows PowerShell 将 VM 映像添加到 Azure Stack Hub 市场。 使用 Azure 市场中的映像作为自定义映像的基础，或使用 Hyper-V 创建自己的映像。

Azure Stack Hub 的租户门户中的用户还可以按照步骤 1 中的指南添加自定义虚拟机 (VM) 映像。 用户可以创建其自定义映像作为虚拟硬盘 (VHD)，并将映像上传到 Azure Stack Hub 上的存储帐户。 然后，他们可以从 VHD 创建 VM。

自定义映像有两种形式：通用和专用 。

- **通用映像**

  通用磁盘映像是使用 Sysprep 准备的用于删除任何唯一信息（如用户帐户）的映像，从而使它能够重复用于创建多个 VM。 对于市场项，这是一个不错的选择。

- **专用映像**

  专用磁盘映像是包含原始 VM 中的用户帐户、应用程序和其他状态数据的现有 VM 中虚拟硬盘 (VHD) 的副本。 将 VM 迁移到 Azure Stack Hub 时通常采用此格式。

## <a name="step-1-create-the-custom-vm-image"></a>步骤 1：创建自定义 VM 映像

### <a name="windows---create-a-custom-generalized-vhd"></a>Windows - 创建自定义的通用 VHD

#### <a name="vhd-is-from-outside-azure"></a>VHD 来自 Azure 外部

按照[准备好要上传到 Azure 的 Windows VHD 或 VHDX](/virtual-machines/windows/prepare-for-upload-vhd-image)中的步骤，在上传之前正确通用化 VHD。

#### <a name="vhd-is-from-azure"></a>VHD 来自 Azure

请在用化 VM 之前确保：

在 Azure Stack 1910 版本之前：

- 在 Azure 上预配 VM 时，使用 PowerShell 并在不使用 `-ProvisionVMAgent` 标志的情况下对其进行预配。
- 通用化 Azure 中的 VM 之前，先在该 VM 中使用 **Remove-AzureRmVMExtension** cmdlet 删除所有 VM 扩展。 可以转到 `Windows (C:) > WindowsAzure > Logs > Plugins` 查找已安装的 VM 扩展。

```powershell
Remove-AzureRmVMExtension -ResourceGroupName winvmrg1 -VMName windowsvm -Name "CustomScriptExtension"
```

使用 Azure Stack 1910 版本或更高版本：

- 上述步骤不适用于从 Azure 引入到 Azure Stack Hub（使用 Azure Stack 1910 版本或更高版本）的 VHD。

按照[此文](/virtual-machines/windows/download-vhd)中的说明正确通用化并下载 VHD，然后将其移植到 Azure Stack Hub。

### <a name="windows---specialized"></a>Windows - 专用

按照[此处](/virtual-machines/windows/create-vm-specialized#prepare-the-vm)的步骤正确准备 VHD。
若要部署 VM 扩展，请确保在部署 VM 之前，已在该 VM 中安装[本文](/virtual-machines/extensions/agent-windows#manual-installation)提供的 VM 代理 .msi。 如果 VHD 中不存在 VM 代理，扩展部署将失败。 预配时无需设置 OS 配置文件或设置 `$vm.OSProfile.AllowExtensionOperations = $true`。

### <a name="linux---generalized"></a>Linux - 通用

#### <a name="vhd-from-outside-azure"></a>VHD 来自 Azure 外部

如果 VHD 来自 Azure 外部，请根据相应的说明将 VHD 通用化：

- [基于 CentOS 的分发版](/virtual-machines/linux/create-upload-centos?toc=%2fvirtual-machines%2flinux%2ftoc.json)
- [Debian Linux](/virtual-machines/linux/debian-create-upload-vhd?toc=%2fvirtual-machines%2flinux%2ftoc.json)
- [Red Hat Enterprise Linux](azure-stack-redhat-create-upload-vhd.md)
- [SLES 或 openSUSE](/virtual-machines/linux/suse-create-upload-vhd?toc=%2fvirtual-machines%2flinux%2ftoc.json)
- [Ubuntu Server](/virtual-machines/linux/create-upload-ubuntu?toc=%2fvirtual-machines%2flinux%2ftoc.json)

#### <a name="vhd-from-azure"></a>VHD 来自 Azure

如果 VHD 来自 Azure，请按照以下说明通用化并下载 VHD：

1. 停止 **waagent** 服务：

   ```bash
   sudo waagent -force -deprovision
   export HISTSIZE=0
   logout
   ```

   适用于 Azure Stack Hub 的 Azure Linux 代理版本[在此处记述](azure-stack-linux.md#azure-linux-agent)。 确保已执行 Sysprep 的映像包含与 Azure Stack Hub 兼容的 Azure Linux 代理版本。

2. 停止/解除分配 VM。

3. 下载 VHD。

   1. 若要下载 VHD 文件，请生成共享访问签名 (SAS) URL。 生成 URL 时，将为 URL 分配到期时间。

   1. 在 VM 的边栏选项卡菜单中选择“磁盘”。

   1. 为 VM 选择操作系统磁盘，然后选择“磁盘导出”。

   1. 将 URL 的过期时间设置为 36000。

   1. 选择“生成 URL”。

   1. 生成 URL。

   1. 在生成的 URL 下，选择“下载 VHD 文件”。

   1. 可能需要选择浏览器中的“保存”才能开始下载。 VHD 文件的默认名称为 **abcd**。

   1. 现在可以将此 VHD 移植到 Azure Stack Hub。

> [!IMPORTANT]  
> 可在[将 VHD 上传到 Azure 并创建新的 VM 的示例脚本](/virtual-machines/scripts/virtual-machines-windows-powershell-upload-generalized-script)一文中查找脚本，以将 VHD 上传到 Azure Stack Hub 用户存储帐户并创建 VM。 请确保提供 `$urlOfUploadedImageVhd` 作为 Azure Stack Hub 存储帐户和容器 URL。 对于通用 VHD，请确保在设置 `-CreateOption FromImage` 使用 `FromImage` 值。

### <a name="linux---specialized"></a>Linux - 专用

专用 VHD 不应用作市场项的基础 VHD。 对此使用专用 VHD。 但是，需要将 VM 从本地迁移到 Azure Stack Hub 时，专用 VHD 非常适合此操作

#### <a name="vhd-from-outside-azure"></a>VHD 来自 Azure 外部

步骤 1：按照相应的说明，使 VHD 适用于 Azure。 在执行到安装 Linux 代理的步骤之前都根据本文的步骤操作，然后在安装代理之前继续执行步骤 2：

- [基于 CentOS 的分发版](/virtual-machines/linux/create-upload-centos?toc=%2fvirtual-machines%2flinux%2ftoc.json)
- [Debian Linux](/virtual-machines/linux/debian-create-upload-vhd?toc=%2fvirtual-machines%2flinux%2ftoc.json)
- [Red Hat Enterprise Linux](azure-stack-redhat-create-upload-vhd.md)
- [SLES 或 openSUSE](/virtual-machines/linux/suse-create-upload-vhd?toc=%2fvirtual-machines%2flinux%2ftoc.json)
- [Ubuntu Server](/virtual-machines/linux/create-upload-ubuntu?toc=%2fvirtual-machines%2flinux%2ftoc.json)

> [!IMPORTANT]
> 请勿运行最后一步：(`sudo waagent -force -deprovision`)，因为这将通用化 VHD。

步骤 2：如果 Linux 专用 VHD 是从 Azure 外部引入到 Azure Stack Hub 的，那么若要运行 VM 扩展并禁用预配，请执行以下操作：

若要确定在源 VM 映像中安装的 Linux 代理版本，请运行以下命令。 描述预配代码的版本号是 `WALinuxAgent-`，而不是 `Goal state agent`：

```bash
waagent -version
```

例如：

```bash
waagent -version
WALinuxAgent-2.2.45 running on centos 7.7.1908
Python: 2.7.5
Goal state agent: 2.2.46
```

若要禁用 Linux 代理版本低于 2.2.4 的 Linux 代理，请在 /etc/waagent.conf 中设置以下参数：`Provisioning.Enabled=n, and Provisioning.UseCloudInit=n`。

需要运行扩展的情况：

1. 在 /etc/waagent.conf 中设置以下参数：

   - `Provisioning.Enabled=n`
   - `Provisioning.UseCloudInit=n`

2. 若要确保禁用 walinuxagent 预配，请运行：`mkdir -p /var/lib/waagent && touch /var/lib/waagent/provisioned`

3. 如果映像中有 cloud-init，请禁用云 init：

   ```bash
   touch /etc/cloud/cloud-init.disabled
   sudo sed -i '/azure_resource/d' /etc/fstab
   ```

4. 执行注销。

若要禁用 Linux 代理版本为 2.2.45 及更高版本的预配，请更改以下配置选项：

- 现在已忽略 `Provisioning.Enabled` 和 `Provisioning.UseCloudInit`。

在此版本中，当前没有完全禁用预配的 `Provisioning.Agent` 选项；但是，你可以添加预配标记文件，并进行以下设置来忽略预配：

1. 在 /etc/waagent.conf 中添加此配置选项：`Provisioning.Agent=Auto`。
2. 若要确保禁用 walinuxagent 预配，请运行：`mkdir -p /var/lib/waagent && touch /var/lib/waagent/provisioned`。
3. 运行以下命令，禁用 cloud-init 安装：

   ```bash
   touch /etc/cloud/cloud-init.disabled
   sudo sed -i '/azure_resource/d' /etc/fstab
   ```

4. 注销。

#### <a name="vhd-from-azure"></a>VHD 来自 Azure

可以使用[本指南](/virtual-machines/linux/upload-vhd#requirements)来准备 VHD。

> [!IMPORTANT]  
> 可以使用以下 PowerShell 示例将 VHD 上传到 Azure Stack Hub 用户存储帐户：

```powershell  
# Provide values for the variables
$resourceGroup = 'myResourceGroup'
$location = 'ChinaEast2'
$storageaccount = 'mystorageaccount'
$storageType = 'Standard_LRS'
$storageaccounturl = 'https://resourcegrpabc.blob.chinaeast2.azurestack.corp.microsoft.com/container'
$localPath = 'C:\Users\Public\Documents\Hyper-V\VHDs\generalized.vhd'
$vhdName = 'myUploadedVhd.vhd'

New-AzResourceGroup -Name $resourceGroup -Location $location
New-AzStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
  -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ($storageaccounturl + '/' + $vhdName)
Add-AzVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath
```

对于专用 VHD，请确保通过 `-CreateOption Attach`（[如本示例所示](/virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks)）使用“附加”语义从该 VHD 创建 VM。

### <a name="considerations"></a>注意事项

在上传映像之前，必须考虑以下因素：

- Azure Stack Hub 仅支持采用固定磁盘 VHD 格式的第 1 代 VM。 固定格式在文件中将逻辑磁盘以线性方式布局，使磁盘偏移量 **X** 存储在 Blob 偏移量 **X** 的位置。在 Blob 末尾有一小段脚注，描述了 VHD 的属性。 若要确认磁盘是否为固定格式，请使用 **Get-VHD** PowerShell cmdlet。

- Azure Stack Hub 不支持动态磁盘 VHD。

## <a name="step-2-upload-a-storage-account"></a>步骤 2：上传存储帐户

以 Azure Stack Hub 操作员身份将 VM 映像上传到存储帐户。

1. [安装适用于 Azure Stack Hub 的 PowerShell](azure-stack-powershell-install.md)。  

2. 以操作员身份登录到 Azure Stack Hub。 有关说明，请参阅[以操作员身份登录到 Azure Stack Hub](azure-stack-powershell-configure-admin.md)。

3. 映像必须通过 Blob 存储 URI 进行引用。 以 VHD（不是 VHDX）格式准备 Windows 或 Linux 操作系统映像，然后将映像上传到 Azure Stack Hub 中的存储帐户。

   - 如果 VHD 位于 Azure 中，且你在联网的 Azure Stack Hub 上运行，可以使用 [Azcopy](/storage/common/storage-use-azcopy) 等工具直接在 Azure 与 Azure Stack Hub 存储帐户之间传输 VHD。

   - 在离线的 Azure Stack Hub 上，如果 VHD 位于 Azure 中，则必须将 VHD 下载到可以同时连接 Azure 和 Azure Stack Hub 的计算机上。 然后，先从 Azure 将 VHD 复制到此计算机，再使用任何可跨 Azure 与 Azure Stack Hub 使用的通用[存储数据传输工具](../user/azure-stack-storage-transfer.md)，将 VHD 传输到 Azure Stack Hub。

     本示例中使用的一个此类工具是 Add-AzureRmVHD 命令，可将 VHD 上传到 Azure Stack Hub 管理员门户中的存储帐户：

     ```powershell
     Add-AzureRmVhd -Destination "https://bash.blob.redmond.azurestack.com/sample/vhdtestingmgd.vhd" -LocalFilePath "C:\vhd\vhdtestingmgd.vhd"
     ```

4. 记下在其中上传映像的 Blob 存储 URI。 blob 存储 URI 的格式如下： **&lt;storageAccount&gt;/&lt;blobContainer&gt;/&lt;targetVHDName&gt;*.vhd**。

5. 若要使 Blob 可供匿名访问，请转到已在其中上传了 VM 映像 VHD 的存储帐户 Blob 容器。 选择“Blob”，然后选择“访问策略”。 也可生成容器的共享访问签名 (SAS)，然后将其作为 blob URI 的一部分包括进去。 此步骤确保 blob 可用。 如果 blob 不可匿名访问，则 VM 映像创建将处于失败状态。

   ![转到存储帐户 Blob](./media/azure-stack-add-vm-image/tca1.png)

   ![将 Blob 访问权限设置为公共](./media/azure-stack-add-vm-image/tca2.png)

   ![将 Blob 访问权限设置为公共](./media/azure-stack-add-vm-image/tca3.png)

6. 还可以使用上述步骤将映像上传到用户门户（以用户身份登录）中的存储帐户，直接从中创建 VM。 在此情况下，它将是无法通过市场获取的自定义 VHD。 也不需要执行步骤 3。

## <a name="step-3-option-1-add-using-the-portal"></a>步骤 3，选项 1：使用门户添加

以 Azure Stack Hub 操作员的身份使用门户添加 VM 映像。

1. 以操作员身份登录到 Azure Stack Hub。 在菜单中选择“VM 映像” > “添加”下面的“所有服务” > “计算”。**** **** **** ****

   ![自定义映像旁加载 UI](./media/azure-stack-add-vm-image/tca4.png)

2. 在“创建映像”下，输入“发布者”、“套餐”、“SKU”、“版本”和 OS 磁盘 blob URI。 然后选择“创建”，开始创建 VM 映像。

   ![自定义映像旁加载 UI](./media/azure-stack-add-vm-image/tca5.png)

   成功创建映像后，VM 映像状态会更改为“已成功”。

3. 添加映像时，它仅适用于基于 Azure 资源管理器的模板和 PowerShell 部署。 若要将映像作为市场项提供给用户，请使用[创建和发布市场项](azure-stack-create-and-publish-marketplace-item.md)一文中的步骤发布市场项 请务必记下“发布者”、“套餐”、“SKU”和“版本”的值。**** **** **** **** 在自定义 .azpkg 中编辑资源管理器模板和 Manifest.json 时，需要用到这些值。

## <a name="step-3-option-2-add-using-powershell"></a>步骤 3，选项 2：使用 PowerShell 添加

 以 Azure Stack Hub 操作员的身份使用 PowerShell 添加 VM 映像。

1. [安装适用于 Azure Stack Hub 的 PowerShell](azure-stack-powershell-install.md)。  

2. 以操作员身份登录到 Azure Stack Hub。 有关说明，请参阅[以操作员身份登录到 Azure Stack Hub](azure-stack-powershell-configure-admin.md)。

3. 使用权限提升的提示符打开 PowerShell，并运行：

   ```powershell
    Add-AzsPlatformimage -publisher "<publisher>" `
      -offer "<Offer>" `
      -sku "<SKU>" `
      -version "<#.#.#>" `
      -OSType "<OS type>" `
      -OSUri "<OS URI>"
   ```

   **Add-AzsPlatformimage** cmdlet 指定 Azure 资源管理器模板用来引用 VM 映像的值。 这些值包括：
   - **publisher**  
     例如： `Canonical`  
     VM 映像的**发布者**名称段，供用户在部署映像时使用。 不要在此字段中包含空格或其他特殊字符。  
   - **offer**  
     例如： `UbuntuServer`  
     VM 映像的**套餐**名称段，供用户在部署 VM 映像时使用。 不要在此字段中包含空格或其他特殊字符。  
   - **sku**  
     例如： `14.04.3-LTS`  
     VM 映像的 SKU 名称段，供用户在部署 VM 映像时使用。 不要在此字段中包含空格或其他特殊字符。  
   - **version**  
     例如： `1.0.0`  
     VM 映像的版本，供用户在部署 VM 映像时使用。 此版本采用 **\#.\#.\#** 格式。 不要在此字段中包含空格或其他特殊字符。  
   - **osType**  
     例如： `Linux`  
     映像的 **osType** 必须为 **Windows** 或 **Linux**。  
   - **OSUri**  
     例如： `https://storageaccount.blob.core.chinacloudapi.cn/vhds/Ubuntu1404.vhd`  
     可以指定 `osDisk` 的 Blob 存储 URI。  

     有关详细信息，请参阅 [Add-AzsPlatformimage](https://docs.microsoft.com/powershell/module/azs.compute.admin/add-azsplatformimage) cmdlet 的 PowerShell 参考。

4. 添加映像时，它仅适用于基于 Azure 资源管理器的模板和 PowerShell 部署。 若要将映像作为市场项提供给用户，请使用[创建和发布市场项](azure-stack-create-and-publish-marketplace-item.md)一文中的步骤发布市场项 请务必记下“发布者”、“套餐”、“SKU”和“版本”的值。**** **** **** **** 在自定义 .azpkg 中编辑资源管理器模板和 Manifest.json 时，需要用到这些值。

## <a name="remove-using-the-portal"></a>使用门户删除

若要以 Azure Stack Hub 操作员的身份使用 Azure Stack Hub 门户删除 VM 映像，请执行以下步骤：

1. 打开 Azure Stack Hub [管理员门户](https://portal.azure.cn/signin/index)。

2. 如果 VM 映像有关联的市场项，请选择“市场管理”，然后选择要删除的 VM 市场项。

3. 如果 VM 映像没有关联的市场项，请导航到“所有服务”>“计算”>“VM 映像”，然后选择 VM 映像旁边的省略号 ( **...** )。

4. 选择“删除” 。

## <a name="remove-using-powershell"></a>使用 PowerShell 删除

若要以 Azure Stack Hub 操作员的身份使用 PowerShell 删除 VM 映像，请执行以下步骤：

1. [安装适用于 Azure Stack Hub 的 PowerShell](azure-stack-powershell-install.md)。

2. 以操作员身份登录到 Azure Stack Hub。

3. 使用权限提升的提示符打开 PowerShell，并运行：

   ```powershell  
   Remove-AzsPlatformImage `
    -publisher "<Publisher>" `
    -offer "<Offer>" `
    -sku "<SKU>" `
    -version "<Version>" `
   ```

   **Remove-AzsPlatformImage** cmdlet 指定 Azure 资源管理器模板用来引用 VM 映像的值。 这些值包括：
   - **publisher**  
     例如： `Canonical`  
     VM 映像的**发布者**名称段，供用户在部署映像时使用。 不要在此字段中包含空格或其他特殊字符。  
   - **offer**  
     例如： `UbuntuServer`  
     VM 映像的**套餐**名称段，供用户在部署 VM 映像时使用。 不要在此字段中包含空格或其他特殊字符。  
   - **sku**  
     例如： `14.04.3-LTS`  
     VM 映像的 SKU 名称段，供用户在部署 VM 映像时使用。 不要在此字段中包含空格或其他特殊字符。  
   - **version**  
     例如： `1.0.0`  
     VM 映像的版本，供用户在部署 VM 映像时使用。 此版本采用 **\#.\#.\#** 格式。 不要在此字段中包含空格或其他特殊字符。  

     有关 **Remove-AzsPlatformImage** cmdlet 的详细信息，请参阅 Azure PowerShell [Azure Stack Hub 操作员模块文档](https://docs.microsoft.com/powershell/azure/azure-stack/overview)。

## <a name="next-steps"></a>后续步骤

- [创建并发布自定义 Azure Stack Hub 市场项](azure-stack-create-and-publish-marketplace-item.md)
- [预配虚拟机](../user/azure-stack-create-vm-template.md)
