---
title: ARM 模板测试工具包
description: 描述如何在模板上运行 ARM 模板测试工具包。 使用该工具包可以查看是否已实现了建议的做法。
ms.topic: conceptual
origin.date: 06/19/2020
ms.date: 08/31/2020
ms.testscope: yes|no
ms.testdate: 08/31/2020null
ms.author: v-yeche
author: rockboyfor
ms.openlocfilehash: eead2f3fc6310c26572604c44d69fd293962aa7a
ms.sourcegitcommit: 601f2251c86aa11658903cab5c529d3e9845d2e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88807925"
---
<!--Verified successfully-->
# <a name="use-arm-template-test-toolkit"></a>使用 ARM 模板测试工具包

[ARM 模板测试工具包](https://aka.ms/arm-ttk)检查模板是否使用建议的做法。 如果模板不符合建议的做法，它将返回包含建议的更改的警告列表。 通过使用测试工具包，可以了解如何避免模板开发中的常见问题。

测试工具包提供[一组默认测试](test-cases.md)。 这些测试是建议，而不是要求。 你可以确定哪些测试与目标相关，并自定义要运行哪些测试。

本文介绍如何运行测试工具包以及如何添加或删除测试。 有关默认测试的说明，请参阅[工具包测试用例](test-cases.md)。

工具包是一组可从 PowerShell 或 CLI 中的命令运行的 PowerShell 脚本。

## <a name="download-test-toolkit"></a>下载测试工具包

若要使用测试工具包，可以分叉并克隆包含脚本的[存储库](https://aka.ms/arm-ttk)，或[下载最新的 .zip 文件](https://aka.ms/arm-ttk-latest)。

根据运行脚本的计算机的执行策略，你可能会收到有关从 Internet 运行脚本的错误消息。 必须更改[执行策略](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies)或[取消阻止脚本文件](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/unblock-file)。

## <a name="run-on-powershell"></a>在 PowerShell 上运行

在运行测试之前，导入模块。

```powershell
Import-Module .\arm-ttk.psd1 # from the same directory as .\arm-ttk.psd1
```

若要在“PowerShell”中运行测试，请使用以下命令：

```powershell
Test-AzTemplate -TemplatePath $TemplateFolder
```

## <a name="run-on-linux"></a>在 Linux 上运行

在运行测试之前，安装 [PowerShell Core](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux)。

若要在 Bash 的“Linux”上运行测试，请使用以下命令：

```bash
Test-AzTemplate.sh -TemplatePath $TemplateFolder
```

还可以在 pwsh.exe 上运行测试。

## <a name="run-on-macos"></a>在 macOS 上运行

在运行测试之前，安装 [PowerShell Core](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos)。 

安装 `coreutils`：

```bash
brew install coreutils
```

若要在“macOS”上运行测试，请使用以下命令：

```bash
Test-AzTemplate.sh -TemplatePath $TemplateFolder
```

## <a name="result-format"></a>结果格式

顺利通过的测试显示为“绿色”，并以“[+]”开头 。

失败的测试显示为“红色”，并以“[-]”开头 。

:::image type="content" source="./media/template-test-toolkit/view-results.png" alt-text="查看测试结果":::

文本结果为：

```powershell
[+] adminUsername Should Not Be A Literal (24 ms)
[+] apiVersions Should Be Recent (18 ms)
[+] artifacts parameter (16 ms)
[+] DeploymentTemplate Schema Is Correct (17 ms)
[+] IDs Should Be Derived From ResourceIDs (15 ms)
[-] Location Should Not Be Hardcoded (41 ms)
     azuredeploy.json must use the location parameter, not resourceGroup().location (except when used as a default value in the main template)
```

## <a name="test-parameters"></a>测试参数

提供“-TemplatePath”参数时，工具箱将在该文件夹中查找名为 azuredeploy.json 或 maintemplate.json 的模板。 它首先测试此模板，然后测试该文件夹及其子文件夹中的所有其他模板。 其他模板将作为链接模板进行测试。 如果路径包含名为 [CreateUiDefinition.json](../managed-applications/create-uidefinition-overview.md) 的文件，则它将运行与 UI 定义相关的测试。

```powershell
Test-AzTemplate -TemplatePath $TemplateFolder
```

若要测试该文件夹中的某个文件，请添加“-File”参数。 但是，该文件夹仍然必须具有名为 azuredeploy.json 或 maintemplate.json 的主模板。

```powershell
Test-AzTemplate -TemplatePath $TemplateFolder -File cdn.json
```

默认情况下，会运行所有测试。 若要指定要运行的各个测试，请使用“-Test”参数。 提供测试的名称。 有关名称，请参阅[工具包的测试用例](test-cases.md)。

```powershell
Test-AzTemplate -TemplatePath $TemplateFolder -Test "Resources Should Have Location"
```

## <a name="customize-tests"></a>自定义测试

对于 ARM 模板，工具包将运行“\arm-ttk\testcases\deploymentTemplate”文件夹中的所有测试。 如果要永久删除测试，请从文件夹中删除该文件。

对于 [CreateUiDefinition](../managed-applications/create-uidefinition-overview.md) 文件，工具包将运行“\arm-ttk\testcases\CreateUiDefinition”文件夹中的所有测试。

若要添加自己的测试，请使用以下命名约定创建文件：Your-Custom-Test-Name.test.ps1。

测试可以获取模板作为对象参数或字符串参数。 通常使用其中一种参数，但也可以同时使用两种。

需要获取模板的一部分并循环访问其属性时，请使用 object 参数。 使用 object 参数的测试采用以下格式：

```powershell
param(
    [Parameter(Mandatory=$true,Position=0)]
    [PSObject]
    $TemplateObject
)

# Implement test logic that evaluates parts of the template.
# Output error with: Write-Error -Message
```

模板对象具有以下属性：

* $schema
* contentVersion
* parameters
* variables
* resources
* outputs

例如，可以通过 `$TemplateObject.parameters` 获取参数的集合。

如果需要对整个模板执行字符串操作，请使用 string 参数。 使用 string 参数的测试采用以下格式：

```powershell
param(
    [Parameter(Mandatory)]
    [string]
    $TemplateText
)

# Implement test logic that performs string operations.
# Output error with: Write-Error -Message
```

例如，可以运行字符串参数的正则表达式，以查看是否使用了特定语法。

若要了解有关实施测试的更多信息，请查看该文件夹中的其他测试。

## <a name="integrate-with-azure-pipelines"></a>与 Azure Pipelines 集成

可以将测试工具包添加到 Azure Pipelines。 使用管道，可以在每次更新模板时运行测试，也可以在部署过程中运行测试。

将测试工具包添加到管道的最简单的方法是利用第三方扩展。 提供以下两个扩展：

* [运行 ARM TTK 测试](https://marketplace.visualstudio.com/items?itemName=Sam-Cogan.ARMTTKExtension)
* [ARM 模板测试程序](https://marketplace.visualstudio.com/items?itemName=maikvandergaag.maikvandergaag-arm-ttk)

或者，你可以执行自己的任务。 以下示例演示如何下载测试工具包。

```json
{
    "environment": {},
    "enabled": true,
    "continueOnError": false,
    "alwaysRun": false,
    "displayName": "Download TTK",
    "timeoutInMinutes": 0,
    "condition": "succeeded()",
    "task": {
        "id": "e213ff0f-5d5c-4791-802d-52ea3e7be1f1",
        "versionSpec": "2.*",
        "definitionType": "task"
    },
    "inputs": {
        "targetType": "inline",
        "filePath": "",
        "arguments": "",
        "script": "New-Item '$(ttk.folder)' -ItemType Directory\nInvoke-WebRequest -uri '$(ttk.uri)' -OutFile \"$(ttk.folder)/$(ttk.asset.filename)\" -Verbose\nGet-ChildItem '$(ttk.folder)' -Recurse\n\nWrite-Host \"Expanding files...\"\nExpand-Archive -Path '$(ttk.folder)/*.zip' -DestinationPath '$(ttk.folder)' -Verbose\n\nWrite-Host \"Expanded files found:\"\nGet-ChildItem '$(ttk.folder)' -Recurse",
        "errorActionPreference": "stop",
        "failOnStderr": "false",
        "ignoreLASTEXITCODE": "false",
        "pwsh": "true",
        "workingDirectory": ""
    }
}
```

下一个示例演示如何运行测试。

```json
{
    "environment": {},
    "enabled": true,
    "continueOnError": true,
    "alwaysRun": false,
    "displayName": "Run Best Practices Tests",
    "timeoutInMinutes": 0,
    "condition": "succeeded()",
    "task": {
        "id": "e213ff0f-5d5c-4791-802d-52ea3e7be1f1",
        "versionSpec": "2.*",
        "definitionType": "task"
    },
    "inputs": {
        "targetType": "inline",
        "filePath": "",
        "arguments": "",
        "script": "Import-Module $(ttk.folder)/arm-ttk/arm-ttk.psd1 -Verbose\n$testOutput = @(Test-AzTemplate -TemplatePath \"$(sample.folder)\")\n$testOutput\n\nif ($testOutput | ? {$_.Errors }) {\n   exit 1 \n} else {\n    Write-Host \"##vso[task.setvariable variable=result.best.practice]$true\"\n    exit 0\n} \n",
        "errorActionPreference": "continue",
        "failOnStderr": "true",
        "ignoreLASTEXITCODE": "false",
        "pwsh": "true",
        "workingDirectory": ""
    }
}
```

## <a name="next-steps"></a>后续步骤

若要了解默认测试，请参阅[工具包的测试用例](test-cases.md)。

<!-- Update_Description: new article about test toolkit -->
<!--NEW.date: 08/31/2020-->