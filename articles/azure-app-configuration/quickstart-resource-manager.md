---
title: 有关自动完成使用 Azure 应用程序配置的 VM 部署的快速入门
description: 本快速入门演示如何使用 Azure PowerShell 模块和 Azure 资源管理器模板部署 Azure 应用程序配置存储。 然后使用该存储中的值来部署 VM。
author: lisaguthrie
ms.author: lcozzens
ms.date: 08/11/2020
ms.topic: quickstart
ms.service: azure-app-configuration
ms.custom:
- mvc
- subject-armqs
ms.openlocfilehash: 0409536d6829d215a3c2e14f8a0150cc9f2f8fd1
ms.sourcegitcommit: f9a819b7429a2cca868eba0d9241d4e6b3cf905a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88866748"
---
# <a name="quickstart-automated-vm-deployment-with-app-configuration-and-resource-manager-template-arm-template"></a>快速入门：使用应用程序配置和资源管理器模板（ARM 模板）自动部署 VM

了解如何使用 Azure 资源管理器模板和 Azure PowerShell 部署 Azure 应用程序配置存储，如何将键值添加到存储中，以及如何使用该存储中的键值来部署 Azure 资源（例如本例中的 Azure 虚拟机）。

[!INCLUDE [About Azure Resource Manager](../../includes/resource-manager-quickstart-introduction.md)]

如果你的环境满足先决条件，并且你熟悉如何使用 ARM 模板，请选择“部署到 Azure”按钮。 Azure 门户中会打开模板。

[![部署到 Azure](../media/template-deployments/deploy-to-azure.svg)](https://portal.azure.cn/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-app-configuration-store%2Fazuredeploy.json)

## <a name="prerequisites"></a>先决条件

如果没有 Azure 订阅，可在开始前创建一个[试用帐户](https://www.azure.cn/pricing/1rmb-trial)。

## <a name="review-the-templates"></a>查看模板

本快速入门中使用的模板来自 [Azure 快速入门模板](https://azure.microsoft.com/resources/templates/)。 [第一个模板](https://azure.microsoft.comresources/templates/101-app-configuration-store/)创建应用程序配置存储：

```JSON
{
 "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
 "contentVersion": "1.0.0.0",
 "parameters": {
   "configStoreName": {
     "type": "string",
     "metadata": {
       "description": "Specifies the name of the app configuration store."
     }
   },
   "location": {
     "type": "string",
     "defaultValue": "[resourceGroup().location]",
     "metadata": {
       "description": "Specifies the Azure location where the app configuration store should be created."
     }
   },
   "skuName": {
     "type": "string",
     "defaultValue": "standard",
     "metadata": {
       "description": "Specifies the SKU of the app configuration store."
     }
   }
 },
 "resources": [
   {
     "type": "Microsoft.AppConfiguration/configurationStores",
     "apiVersion": "2019-10-01",
     "name": "[parameters('configStoreName')]",
     "location": "[parameters('location')]",
     "sku": {
       "name": "[parameters('skuName')]"
     }
   }
 ]
}
```

模板中定义了一个 Azure 资源：

- [Microsoft.AppConfiguration/configurationStores](https://docs.microsoft.com/azure/templates/microsoft.appconfiguration/2019-10-01/configurationstores)：创建应用程序配置存储。

[第二个模板](https://azure.microsoft.com/resources/templates/101-app-configuration/)使用存储中的键值创建虚拟机。 在执行此步骤之前，需要使用门户或 Azure CLI 添加键值。

```JSON
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "location": {
      "type": "string",
      "defaultValue": "[resourceGroup().location]",
      "metadata": {
        "description": "Specify the locations for all resources."
      }
    },
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Specify the virtual machine admin user name."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Specify the virtual machine admin password."
      }
    },
    "domainNameLabel": {
      "type": "string",
      "metadata": {
        "description": "Specify the DNS label for the virtual machine public IP address. It must be lowercase. It should match the following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$."
      }
    },
    "vmSize": {
      "type": "string",
      "defaultValue": "Standard_D2_v3",
      "metadata": {
        "description": "Specify the size of the VM."
      }
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Specify the storage account name."
      }
    },
      "appConfigStoreResourceGroup": {
      "type": "string",
      "metadata": {
        "description": "Name of the resource group for the app config store."
      }
    },
    "appConfigStoreName": {
      "type": "string",
      "metadata": {
        "description": "App configuration store name."
      }
    },
    "vmSkuKey": {
      "type": "string",
      "metadata": {
        "description": "Specify the name of the key in the app config store for the VM windows sku."
      }
    },
    "diskSizeKey": {
      "type": "string",
      "metadata": {
        "description": "Specify the name of the key in the app config store for the VM disk size"
      }
    }
  },
  "variables": {
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "publicIPAddressName": "myPublicIP",
    "vmName": "SimpleWinVM",
    "virtualNetworkName": "MyVNET",
    "subnetRef": "[resourceId('Microsoft.Network/virtualNetworks/subnets', variables('virtualNetworkName'), variables('subnetName'))]",
    "appConfigRef": "[resourceId(parameters('appConfigStoreResourceGroup'), 'Microsoft.AppConfiguration/configurationStores', parameters('appConfigStoreName'))]",
    "windowsOSVersionParameters": {
      "key": "[parameters('vmSkuKey')]",
      "label": "template"
    },
    "diskSizeGBParameters": {
      "key": "[parameters('diskSizeKey')]",
      "label": "template"
    }
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2019-06-01",
      "name": "[parameters('storageAccountName')]",
      "location": "[parameters('location')]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": {
      }
    },
    {
      "type": "Microsoft.Network/publicIPAddresses",
      "apiVersion": "2020-05-01",
      "name": "[variables('publicIPAddressName')]",
      "location": "[parameters('location')]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[parameters('domainNameLabel')]"
        }
      }
    },
    {
      "type": "Microsoft.Network/virtualNetworks",
      "apiVersion": "2020-05-01",
      "name": "[variables('virtualNetworkName')]",
      "location": "[parameters('location')]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[variables('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "type": "Microsoft.Network/networkInterfaces",
      "apiVersion": "2020-05-01",
      "name": "[variables('nicName')]",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[resourceId('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[resourceId('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
              },
              "subnet": {
                "id": "[variables('subnetRef')]"
              }
            }
          }
        ]
      }
    },
    {
      "type": "Microsoft.Compute/virtualMachines",
      "apiVersion": "2019-12-01",
      "name": "[variables('vmName')]",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "[parameters('vmSize')]"
        },
        "osProfile": {
          "computerName": "[variables('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "[listKeyValue(variables('appConfigRef'), '2019-10-01', variables('windowsOSVersionParameters')).value]",
            "version": "latest"
          },
          "osDisk": {
            "createOption": "FromImage"
          },
          "dataDisks": [
            {
              "diskSizeGB": "[listKeyValue(variables('appConfigRef'), '2019-10-01', variables('diskSizeGBParameters')).value]",
              "lun": 0,
              "createOption": "Empty"
            }
          ]
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        },
        "diagnosticsProfile": {
          "bootDiagnostics": {
            "enabled": true,
            "storageUri": "[reference(resourceId('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))).primaryEndpoints.blob]"
          }
        }
      }
    }
  ],
  "outputs": {
    "hostname": {
      "type": "string",
      "value": "[reference(variables('publicIPAddressName')).dnsSettings.fqdn]"
    }
  }
}
```

## <a name="deploy-the-templates"></a>部署模板

### <a name="create-an-app-configuration-store"></a>创建应用配置存储区

1. 选择下图登录到 Azure 并打开一个模板。 该模板会创建应用程序配置存储。

    [![部署到 Azure](../media/template-deployments/deploy-to-azure.svg)](https://portal.azure.cn/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-app-configuration-store%2Fazuredeploy.json)

1. 选择或输入以下值。

    - 订阅：选择用于创建应用程序配置存储的 Azure 订阅。
    - 资源组：选择“新建”以创建新的资源组，除非你想使用现有资源组。
    - 区域：选择资源组的位置。  例如，“中国东部 2”。
    - 配置存储名称：输入新的应用程序配置存储名称。
    - 位置：指定应用程序配置存储的位置。  使用默认值。
    - SKU 名称：指定应用程序配置存储的 SKU 名称。 使用默认值。

1. 选择“查看 + 创建”。
1. 验证该页是否显示“通过验证”，然后选择“创建” 。

记下资源组名称和应用程序配置存储名称。  部署虚拟机时需要这些值
### <a name="add-vm-configuration-key-values"></a>添加 VM 配置键-值

创建应用程序配置存储后，可以使用 Azure 门户或 Azure CLI 将键值添加到该存储。

1. 登录到 [Azure 门户](https://portal.azure.cn)，然后导航到新创建的应用程序配置存储。
1. 从左侧菜单中选择“配置资源管理器”。
1. 选择“创建”以添加以下键值对：

   |密钥|值|Label|
   |-|-|-|
   |windowsOsVersion|2019-Datacenter|template|
   |diskSizeGB|1023|template|

   将“内容类型”保留为空。

若要使用 Azure CLI，请参阅[使用 Azure 应用程序配置存储中的键值](./scripts/cli-work-with-keys.md)。

### <a name="deploy-vm-using-stored-key-values"></a>使用存储的键-值部署 VM

将键-值添加到存储后，接下来可以使用 Azure 资源管理器模板部署 VM。 该模板引用创建的 **windowsOsVersion** 和 **diskSizeGB** 键。

1. 选择下图登录到 Azure 并打开一个模板。 该模板使用应用程序配置存储中存储的键值创建虚拟机。

    [![部署到 Azure](../media/template-deployments/deploy-to-azure.svg)](https://portal.azure.cn/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-app-configuration%2Fazuredeploy.json)

1. 选择或输入以下值。

    - 订阅：选择用于创建虚拟机的 Azure 订阅。
    - 资源组：指定与应用程序配置存储相同的资源组，或选择“新建”以创建新的资源组。
    - 区域：选择资源组的位置。  例如，“中国东部 2”。
    - 位置：指定虚拟机的位置。 使用默认值。
    - 管理员用户名：指定虚拟机的管理员用户名。
    - 管理员密码：指定虚拟机的管理员密码。
    - 域名标签：指定唯一的域名。
    - 存储帐户名称：为与虚拟机关联的存储帐户指定唯一的名称。
    - 应用程序配置存储资源组：指定包含应用程序配置存储的资源组。
    - 应用程序配置存储名称：指定 Azure 应用程序配置存储的名称。
    - VM SKU 密钥：指定 windowsOsVersion。  这是你添加到存储的密钥值名称。
    - 磁盘大小密钥：指定 diskSizeGB。 这是你添加到存储的密钥值名称。

1. 选择“查看 + 创建”。
1. 验证该页是否显示“通过验证”，然后选择“创建” 。

## <a name="review-deployed-resources"></a>查看已部署的资源

1. 登录到 [Azure 门户](https://portal.azure.cn)，然后导航到新创建的虚拟机。
1. 从左侧菜单中选择“概述”，并验证“SKU”是否为“2019-Datacenter”  。
1. 从左侧菜单中选择“磁盘”，并验证数据磁盘的大小是否为“2013” 。

## <a name="clean-up-resources"></a>清理资源

如果不再需要本教程中所述的资源组、应用程序配置存储、VM 和所有相关资源，请将其删除。 如果你打算将来还要使用该应用程序配置存储或 VM，可以保留这些资源。 如果不打算继续使用该作业，请运行以下 cmdlet，删除本快速入门创建的所有资源：

```azurepowershell
Remove-AzResourceGroup `
  -Name $resourceGroup
```

## <a name="next-steps"></a>后续步骤

在本快速入门中，你已使用 Azure 资源管理器模板和 Azure 应用程序配置中的键-值部署了一个 VM。

若要了解如何创建使用 Azure 应用程序配置的其他应用程序，请继续阅读以下文章：

> [!div class="nextstepaction"]
> [快速入门：创建使用 Azure 应用程序配置的 ASP.NET Core 应用](quickstart-aspnet-core-app.md)
