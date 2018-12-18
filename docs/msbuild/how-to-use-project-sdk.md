---
title: Como fazer referência a um SDK de Projeto do MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 01/25/2018
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, SDKs, SDK
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: abc61f0e07ed1e22d0ec3b2c8fb15d66c9eea3cd
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220437"
---
# <a name="how-to-use-msbuild-project-sdks"></a>Como usar SDKs de projeto do MSBuild

O [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 15.0 introduziu o conceito de "SDK de projeto," que simplifica o uso de kits de desenvolvimento de software que exigem que propriedades e destinos sejam importados.

```xml
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
        <TargetFramework>net46</TargetFramework>
    </PropertyGroup>
</Project>
```

Durante a avaliação do projeto, o [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] adiciona importações implícitas nas partes superior e inferior do projeto:

```xml
<Project>
    <!-- Implicit top import -->
    <Import Project="Sdk.props" Sdk="Microsoft.NET.Sdk" />

    <PropertyGroup>
        <TargetFramework>net46</TargetFramework>
    </PropertyGroup>

    <!-- Implicit bottom import -->
    <Import Project="Sdk.targets" Sdk="Microsoft.NET.Sdk" />
</Project>
```

## <a name="reference-a-project-sdk"></a>Referenciar um SDK de projeto

 Há três maneiras de referenciar um SDK de projeto:

1. Use o atributo `Sdk` no elemento `<Project/>`:

    ```xml
    <Project Sdk="My.Custom.Sdk">
        ...
    </Project>
    ```

    Uma importação implícita é adicionada às partes superior e inferior do projeto, conforme descrito acima.  O formato do atributo `Sdk` é `Name[/Version]`, em que Versão é opcional.  Por exemplo, você pode especificar `My.Custom.Sdk/1.2.3`.

    > [!NOTE]
    > Isso atualmente é a única maneira com suporte para fazer referência a um projeto do SDK no Visual Studio para Mac.

2. Use o elemento `<Sdk/>` de nível superior:

    ```xml
    <Project>
        <Sdk Name="My.Custom.Sdk" Version="1.2.3" />
        ...
    </Project>
   ```

   Uma importação implícita é adicionada às partes superior e inferior do projeto, conforme descrito acima.  O atributo `Version` não é necessário.

3. Use o elemento `<Import/>` em qualquer lugar no projeto:

    ```xml
    <Project>
        <PropertyGroup>
            <MyProperty>Value</MyProperty>
        </PropertyGroup>
        <Import Project="Sdk.props" Sdk="My.Custom.Sdk" />
        ...
        <Import Project="Sdk.targets" Sdk="My.Custom.Sdk" />
    </Project>
   ```

   Incluir explicitamente as importações no projeto permite que você tenha controle total sobre a ordem.

   Ao usar o elemento `<Import/>`, você também pode especificar um atributo `Version` opcional.  Por exemplo, você pode especificar `<Import Project="Sdk.props" Sdk="My.Custom.Sdk" Version="1.2.3" />`.

## <a name="how-project-sdks-are-resolved"></a>Como os SDKs de projeto são resolvidos

Ao avaliar a importação, o [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] resolve dinamicamente o caminho para o SDK de projeto com base no nome e na versão especificados.  O [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] também tem uma lista de resolvedores de SDK registrados, que são plug-ins que localizam SDKs de projeto no computador.  Os plug-ins incluem:

1. Um resolvedor baseado em NuGet que consulta os feeds de pacotes configurados para pacotes do NuGet que correspondem à ID e à versão do SDK que você especificou.<br/>
   Esse resolvedor só estará ativo se você tiver especificado uma versão opcional e poderá ser usado para qualquer SDK de projeto personalizado.  
2. Um resolvedor de CLI do .NET que resolve SDKs instalados com a CLI do .NET.<br/>
   Esse resolvedor localiza SDKs de projeto, como `Microsoft.NET.Sdk` e `Microsoft.NET.Sdk.Web`, que fazem parte do produto.
3. Um resolvedor padrão que resolve SDKs instalados com o MSBuild.

O resolvedor de SDK baseado em NuGet dá suporte à especificação de uma versão em [global.json](https://docs.microsoft.com/dotnet/core/tools/global-json) que permite que você controle a versão do SDK do projeto em um único local, em vez de em cada projeto:

```json
{
    "msbuild-sdks": {
        "My.Custom.Sdk": "5.0.0",
        "My.Other.Sdk": "1.0.0-beta"
    }
}
```

Somente uma versão de cada SDK de projeto pode ser usada durante uma compilação.  Se você estiver fazendo referência a duas versões diferentes do mesmo SDK de projeto, o MSBuild emitirá um aviso.  É recomendável **não** especificar uma versão nos projetos caso uma versão seja especificada no *global.json*.  

## <a name="see-also"></a>Consulte também

 [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)   
 [Personalizar o build](../msbuild/customize-your-build.md)   
 [Pacotes, metadados e estruturas](/dotnet/core/packages)   
 [Adições ao formato csproj para o .NET Core](/dotnet/core/tools/csproj)
