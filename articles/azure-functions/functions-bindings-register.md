---
title: 注册 Azure Functions 绑定扩展
description: 了解如何根据你的环境注册 Azure Functions 绑定扩展。
author: craigshoemaker
ms.topic: reference
ms.date: 08/24/2020
ms.author: v-junlch
ms.openlocfilehash: 74683005b0fd1a8e7e0bb7d23076760a193e2691
ms.sourcegitcommit: b5ea35dcd86ff81a003ac9a7a2c6f373204d111d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88947138"
---
# <a name="register-azure-functions-binding-extensions"></a>注册 Azure Functions 绑定扩展

从 Azure Functions 版本 2.x 开始，[绑定](./functions-triggers-bindings.md)以独立于 Functions 运行时的包的形式提供。 虽然 .NET 函数通过 NuGet 包访问绑定，但扩展捆绑包允许其他函数通过配置设置访问所有绑定。

请考虑以下与绑定扩展相关的项：

- 除非[使用 Visual Studio 创建 C# 类库](#local-csharp)，否则绑定扩展不会在 Functions 1.x 中显式注册。

- 默认情况下支持 HTTP 和计时器触发器，不需要扩展。

下表指明了何时以及如何注册绑定。

| 开发环境 |在<br/> Functions 1.x 中注册  |在<br/> Functions 3.x/2.x 中注册  |
|-------------------------|------------------------------------|------------------------------------|
|Azure 门户|自动|自动<sup>*</sup>|
|非 .NET 语言或本地 Azure Core Tools 开发|自动|[使用 Azure Functions Core Tools 和扩展捆绑包](#extension-bundles)|
|使用 Visual Studio 的 C# 类库|[使用 NuGet 工具](#vs)|[使用 NuGet 工具](#vs)|
|使用 Visual Studio Code 的 C# 类库|不适用|[使用 .NET Core CLI](#vs-code)|

<sup>*</sup> 门户使用扩展捆绑包。

## <a name="extension-bundles"></a><a name="extension-bundles"></a>扩展捆绑包

使用扩展捆绑包可将一组兼容的 Functions 绑定扩展添加到函数应用。 如果使用捆绑包，则在生成应用时会添加一组预定义的扩展。 捆绑包中定义的扩展包已经过验证，可以彼此兼容，这有助于避免包之间发生冲突。 有了扩展捆绑包，就不需使用非 .NET 函数项目发布 .NET 项目代码。 可以在应用的 host.json 文件中启用扩展捆绑。  

可以将扩展捆绑与 2.x 版和更高版本的 Functions 运行时一起使用。 

对于使用 Azure Functions Core Tools、Visual Studio Code 进行的本地开发，以及在远程生成时，请使用扩展捆绑。 进行本地开发时，请确保使用最新版本的 [Azure Functions Core Tools](functions-run-local.md#v2)。 在 Azure 门户中开发函数时，也可使用扩展捆绑包。 

如果不使用扩展捆绑包，则必须先在本地计算机上安装 .NET Core 2.x SDK，然后才能[显式安装任何绑定扩展](#explicitly-install-extensions)。 将向你的项目添加一个可显式定义所需扩展的 extensions.csproj 文件。 扩展捆绑包消除了本地开发的这些要求。 

若要使用扩展捆绑，请更新 *host json*文件以包含 `extensionBundle` 的以下条目：
 
[!INCLUDE [functions-extension-bundles-json](../../includes/functions-extension-bundles-json.md)]

## <a name="explicitly-install-extensions"></a>显式安装扩展

[!INCLUDE [functions-extension-register-core-tools](../../includes/functions-extension-register-core-tools.md)]

## <a name="nuget-packages"></a><a name="local-csharp"></a>NuGet 包

对于基于 C# 类库的函数项目，应直接安装扩展。 扩展捆绑包专用于不基于 C# 类库的项目。

### <a name="c-class-library-with-visual-studio"></a><a name="vs"></a>使用 Visual Studio 的 C\# 类库

在 **Visual Studio** 中，可以使用 [Install-Package](https://docs.microsoft.com/nuget/tools/ps-ref-install-package) 命令从包管理器控制台安装包，如以下示例所示：

```powershell
Install-Package Microsoft.Azure.WebJobs.Extensions.ServiceBus -Version <TARGET_VERSION>
```

用于给定绑定的包的名称在该绑定的参考文章中提供。 有关示例，请参阅[服务总线绑定参考文章的“包”部分](functions-bindings-service-bus.md#functions-1x)。

将示例中的 `<TARGET_VERSION>` 替换为特定包版本，例如 `3.0.0-beta5`。 在 [NuGet.org](https://nuget.org) 上的单个包页上列出了有效版本。与 Functions 运行时 1.x 或 2.x 对应的主版本在绑定的参考文章中指定。

如果使用 `Install-Package` 来引用绑定，则无需使用[扩展捆绑](#extension-bundles)。 此方法特定于在 Visual Studio 中生成的类库。

## <a name="c-class-library-with-visual-studio-code"></a><a name="vs-code"></a> 使用 Visual Studio Code 的 C# 类库

在 **Visual Studio Code** 中，请使用 .NET Core CLI 中的 [dotnet add package](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package) 命令通过命令提示符安装 C# 类库项目的包。 以下示例演示如何添加绑定：

```terminal
dotnet add package Microsoft.Azure.WebJobs.Extensions.<BINDING_TYPE_NAME> --version <TARGET_VERSION>
```

.NET Core CLI 只能用于 Azure Functions 2.x 开发。

将 `<BINDING_TYPE_NAME>` 替换为包含所需绑定的包的名称。 可以在[支持的绑定列表](./functions-triggers-bindings.md#supported-bindings)中找到所需的绑定参考文章。

将示例中的 `<TARGET_VERSION>` 替换为特定包版本，例如 `3.0.0-beta5`。 在 [NuGet.org](https://nuget.org) 上的单个包页上列出了有效版本。与 Functions 运行时 1.x 或 2.x 对应的主版本在绑定的参考文章中指定。

## <a name="next-steps"></a>后续步骤
> [!div class="nextstepaction"]
> [Azure Functions 触发器和绑定示例](./functions-bindings-example.md)

