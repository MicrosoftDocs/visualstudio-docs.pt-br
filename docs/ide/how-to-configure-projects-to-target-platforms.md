---
title: Como configurar projetos para terem plataformas como destino
ms.date: 08/16/2019
ms.technology: vs-ide-compile
ms.topic: how-to
helpviewer_keywords:
- project settings [Visual Studio], targeting platforms
- platforms, targeting specific CPUs
- project properties [Visual Studio], targeting platforms
- projects [Visual Studio], targeting platforms
- 64-bit [Visual Studio]
- 64-bit programming [Visual Studio]
- CPUs, targeting specific
- 64-bit applications [Visual Studio]
ms.assetid: 845302fc-273d-4f81-820a-7296ce91bd76
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a58b60e23bf08fb86a8dd7bc09d760085b6ea25f
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284589"
---
# <a name="how-to-configure-projects-to-target-platforms"></a>Como configurar projetos para terem plataformas como destino

O Visual Studio permite que você configure seus aplicativos para direcionar as plataformas diferentes, incluindo plataformas de 64 bits. Para obter mais informações sobre o suporte à plataforma de 64 bits no Visual Studio, consulte [aplicativos de 64 bits](/dotnet/framework/64-bit-apps).

## <a name="target-platforms-with-the-configuration-manager"></a>Plataformas de destino com o Gerenciador de Configurações

O **Configuration Manager** oferece uma maneira de adicionar rapidamente uma nova plataforma de destino para seu projeto. Se você selecionar uma das plataformas incluídas com o Visual Studio, as propriedades do projeto serão modificadas para criar seu projeto para a plataforma selecionada.

### <a name="to-configure-a-project-to-target-a-64-bit-platform"></a>Para configurar um projeto para ter uma plataforma de 64 bits como destino

1. Na barra de menus, escolha **criar**  >  **Configuration Manager**.

2. Na lista **Plataforma da solução ativa**, escolha uma plataforma de 64 bits para a solução a ter como destino e, em seguida, escolha o botão **Fechar**.

    1. Se a plataforma que você deseja não aparecer na lista **plataforma de solução ativa** , escolha **novo**.

         A caixa de diálogo **Nova plataforma de solução** é exibida.

    2. Na lista **Digitar ou selecionar a nova plataforma**, escolha **x64**.

        > [!NOTE]
        > Se você der um novo nome à sua configuração, precisará modificar as configurações no **Designer de Projeto** para ter a plataforma correta como destino.

    3. Se você quiser copiar as configurações de uma configuração de plataforma atual, escolha-a e selecione o botão **OK**.

As propriedades de todos os projetos que têm a plataforma de 64 bits como destino são atualizadas e o próximo build do projeto será otimizado para plataformas de 64 bits.

> [!NOTE]
> O nome da plataforma **Win32** é usado para projetos C++ e significa **x86**. O Visual Studio considera as plataformas de nível de projeto e as plataformas de nível de solução, e as plataformas de projeto são provenientes dos sistemas de projeto específicos à linguagem. Os projetos C++ usam **Win32** e **x64**, mas as plataformas de solução usam **x86** e **x64**. Quando você escolhe **x86** como a configuração da solução, o Visual Studio seleciona a plataforma **Win32** para projetos C++. Para ver as configurações da plataforma no nível do projeto e da plataforma de nível de solução, abra **Configuration Manager** e observe as duas configurações de plataforma. A plataforma de nível de solução é mostrada na lista suspensa **plataforma de solução ativa** e a tabela mostra a plataforma de nível de projeto para cada projeto.
> ![Captura de tela mostrando plataforma de solução e plataforma de projeto](media/project-platform-win32.png)

## <a name="target-platforms-in-the-project-designer"></a>Plataformas de destino no Designer de Projeto

O **Designer de Projeto** também permite definir diferentes plataformas como destino para seu projeto. Se selecionar uma das plataformas incluídas na lista na caixa de diálogo **Nova Plataforma de Solução** não funcionar para sua solução, você poderá criar um nome de configuração personalizado e modificar as configurações no **Designer de Projeto** para ter a plataforma correta como destino.

A execução dessa tarefa varia de acordo com a linguagem de programação que você está usando. Para obter mais informações, consulte os links a seguir:

- Para projetos [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)], consulte [/platform (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/platform).

- Para projetos [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)], consulte [Página de Build, Designer de Projeto (C#)](../ide/reference/build-page-project-designer-csharp.md).

- Para projetos [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)], consulte [/clr (Compilação do Common Language Runtime)](/cpp/build/reference/clr-common-language-runtime-compilation).

## <a name="manually-editing-the-project-file"></a>Edição manual do arquivo de projeto

Às vezes, você precisa editar manualmente o arquivo de projeto para algumas configurações personalizadas. Um exemplo disso é quando existem condições que não podem ser especificadas no IDE, como uma referência que é diferente para duas plataformas distintas, conforme o exemplo a seguir.

### <a name="example-referencing-x86-and-x64-assemblies-and-dlls"></a>Exemplo: Referenciando assemblies e DLLs x86 e x64

Você pode ter um assembly ou uma DLL .NET com as versões x86 e x64. Para configurar o projeto para usar essas referências, primeiro adicione a referência e, em seguida, abra o arquivo de projeto e edite-o para adicionar um `ItemGroup` com uma condição que referencie a configuração e a plataforma de destino.  Por exemplo, suponha que o binário que você está referenciando seja o ClassLibrary1 e que haja caminhos diferentes para as Configurações de Depuração e Versão, bem como para as versões x86 e x64.  Em seguida, use quatro elementos `ItemGroup` com todas as combinações de configurações, da seguinte maneira:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.0</TargetFramework>
    <Platforms>AnyCPU;x64;x86</Platforms>
  </PropertyGroup>

  <ItemGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|x64'">
    <Reference Include="ClassLibrary1">
      <HintPath>..\..\ClassLibrary1\ClassLibrary1\bin\x64\Debug\netstandard2.0\ClassLibrary1.dll</HintPath>
    </Reference>
  </ItemGroup>

  <ItemGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|x64'">
    <Reference Include="ClassLibrary1">
      <HintPath>..\..\ClassLibrary1\ClassLibrary1\bin\x64\Release\netstandard2.0\ClassLibrary1.dll</HintPath>
    </Reference>
  </ItemGroup>

  <ItemGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|x86'">
    <Reference Include="ClassLibrary1">
      <HintPath>..\..\ClassLibrary1\ClassLibrary1\bin\x86\Debug\netstandard2.0\ClassLibrary1.dll</HintPath>
    </Reference>
  </ItemGroup>
  
  <ItemGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|x86'">
    <Reference Include="ClassLibrary1">
      <HintPath>..\..\ClassLibrary1\ClassLibrary1\bin\x86\Release\netstandard2.0\ClassLibrary1.dll</HintPath>
    </Reference>
  </ItemGroup>
</Project>
```

::: moniker range="vs-2017"
> [!NOTE]
> No Visual Studio 2017, você precisa descarregar o projeto antes de editar o arquivo de projeto. Para descarregar o projeto, clique com o botão direito do mouse sobre o nó do projeto e escolha **Descarregar projeto**. Ao terminar de editar, salve as alterações e recarregue o projeto clicando com o botão direito do mouse sobre o nó do projeto e escolhendo **Recarregar projeto**.
::: moniker-end

Para obter mais informações sobre o arquivo de projeto, confira [Referência de esquema do arquivo de projeto do MSBuild](../msbuild/msbuild-project-file-schema-reference.md).

## <a name="see-also"></a>Veja também

- [Noções básicas sobre plataformas de build](../ide/understanding-build-platforms.md)
- [/platform (opções do compilador de C#)](/dotnet/csharp/language-reference/compiler-options/platform-compiler-option)
- [Aplicativos de 64 bits](/dotnet/framework/64-bit-apps)
- [Suporte ao IDE do Visual Studio de 64 bits](../ide/visual-studio-ide-64-bit-support.md)
- [Noções básicas sobre o arquivo de projeto](/aspnet/web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file)
