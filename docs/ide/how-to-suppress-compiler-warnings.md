---
title: Suprimir avisos do compilador para projetos e pacotes NuGet
ms.date: 01/24/2018
ms.technology: vs-ide-compile
ms.topic: how-to
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 53db72495b64236441b9ce517c0eb25dc09a207c
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283951"
---
# <a name="how-to-suppress-compiler-warnings"></a>Como suprimir avisos do compilador

Você pode organizar um log de build filtrando um ou mais tipos de avisos do compilador. Por exemplo, talvez você queira revisar apenas parte da saída gerada quando você define o detalhamento do log de compilação como **normal**, **detalhado**ou **diagnóstico**. Para saber mais sobre detalhamento, consulte [Como exibir, salvar e configurar arquivos de log de build](../ide/how-to-view-save-and-configure-build-log-files.md).

## <a name="suppress-specific-warnings-for-visual-c-or-f"></a>Suprimir avisos específicos para o Visual C# ou F\#

Use a página de propriedades **Build** para suprimir avisos específicos para projetos em C# e F#.

1. No **Gerenciador de Soluções**, escolha o projeto no qual você deseja suprimir avisos.

1. Na barra de menus, escolha **Exibir**  >  **páginas de propriedades**.

1. Escolha a página **Build**.

1. Na caixa **Suprimir avisos**, especifique os códigos de erro dos avisos que você quer suprimir, separados por ponto e vírgula.

1. Recriar a solução.

## <a name="suppress-specific-warnings-for-c"></a>Suprimir avisos específicos para C++

Use a página **Propriedades da Configuração** para suprimir avisos específicos para projetos em C++.

1. No **Gerenciador de Soluções**, escolha o projeto ou arquivo de origem no qual deseja suprimir avisos.

1. Na barra de menus, escolha **Exibir**  >  **páginas de propriedades**.

1. Escolha a categoria **Propriedades de Configuração**, escolha a categoria **C++** e escolha a página **Avançado**.

1. Execute uma das seguintes etapas:

    - Na caixa **Desabilita Avisos Específicos**, especifique os códigos de erro dos avisos que deseja suprimir, separados por ponto e vírgula.

    - Na caixa **Desabilita Avisos Específicos**, escolha **Editar** para exibir mais opções.

1. Escolha o botão **OK** e recompile a solução.

## <a name="suppress-warnings-for-visual-basic"></a>Suprimir avisos para o Visual Basic

Você pode ocultar avisos de compilador específicos para Visual Basic editando o arquivo *.vbproj* para o projeto. Para suprimir avisos por *categoria*, use a [página de propriedades de compilação](../ide/reference/compile-page-project-designer-visual-basic.md). Para obter mais informações, consulte [Configurar avisos no Visual Basic](../ide/configuring-warnings-in-visual-basic.md).

### <a name="to-suppress-specific-warnings-for-visual-basic"></a>Para suprimir avisos específicos para o Visual Basic

Este exemplo mostra como editar o arquivo *.vbproj* para suprimir avisos específicos ao compilador.

1. No **Gerenciador de Soluções**, escolha o projeto no qual você deseja suprimir avisos.

1. Na barra de menus, escolha **projeto**  >  **descarregar projeto**.

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse ou abra o menu de atalho do projeto e escolha **Editar \<ProjectName>.vbproj**.

    O arquivo XML do projeto é aberto no editor de códigos.

1. Localize o elemento `<NoWarn>` para a configuração de build com a qual você está compilando e adicione um ou mais números de aviso como o valor do elemento `<NoWarn>`. Se você especificar vários números de aviso, separe-os com uma vírgula.

     A exemplo a seguir mostra o elemento `<NoWarn>` para a configuração de build *Depuração* em uma plataforma x86, com dois avisos do compilador suprimidos:

    ```xml
    <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|x86' ">
        <PlatformTarget>x86</PlatformTarget>
        <DebugSymbols>true</DebugSymbols>
        <DebugType>full</DebugType>
        <Optimize>false</Optimize>
        <OutputPath>bin\Debug\</OutputPath>
        <DefineDebug>true</DefineDebug>
        <DefineTrace>true</DefineTrace>
        <ErrorReport>prompt</ErrorReport>
        <NoWarn>40059,42024</NoWarn>
        <WarningLevel>1</WarningLevel>
      </PropertyGroup>
    ```

   > [!NOTE]
   > Projetos em .NET Core não contêm grupos de propriedades de configuração de build por padrão. Para suprimir avisos em um projeto em .NET Core, adicione a seção de configuração de build ao arquivo manualmente. Por exemplo:
   >
   > ```xml
   > <Project Sdk="Microsoft.NET.Sdk">
   >   <PropertyGroup>
   >     <OutputType>Exe</OutputType>
   >     <TargetFramework>netcoreapp2.0</TargetFramework>
   >     <RootNamespace>VBDotNetCore_1</RootNamespace>
   >   </PropertyGroup>
   >   <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
   >     <NoWarn>42016,41999,42017</NoWarn>
   >   </PropertyGroup>
   > </Project>
   > ```

1. Salve as alterações no arquivo *.vbproj*.

1. Na barra de menus, escolha **projeto**  >  **recarregar projeto**.

1. Na barra de menus, escolha **Compilar**  >  **Recompilar solução**.

    A janela **Saída** não mostra mais os avisos especificados.

Para saber mais, consulte a [opção de compilador /nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn) para o compilador de linha de comando do Visual Basic.

## <a name="suppress-warnings-for-nuget-packages"></a>Suprimir avisos para pacotes NuGet

Em alguns casos, convém suprimir avisos do compilador NuGet para um único pacote NuGet, em vez de um projeto inteiro. O aviso atende a uma finalidade, portanto convém não suprimi-lo no nível do projeto. Por exemplo, um dos avisos NuGet informa que talvez o pacote não seja totalmente compatível com o seu projeto. Se você suprimi-lo no nível do projeto e depois adicionar outro pacote NuGet, você nunca saberá se ele estava gerando o aviso de compatibilidade.

### <a name="to-suppress-a-specific-warning-for-a-single-nuget-package"></a>Para suprimir um aviso específico para um único pacote NuGet

1. No **Gerenciador de Soluções**, selecione o pacote NuGet para o qual você deseja suprimir os avisos do compilador.

   ![Pacote NuGet no Gerenciador de Soluções](media/nuget-package-with-warning.png)

1. Ao clicar com o botão direito do mouse ou no menu de contexto, selecione **Propriedades**.

1. Na caixa **NoWarn** das propriedades do pacote, insira o número do aviso que você quer suprimir para esse pacote. Se você quiser suprimir mais de um aviso, use uma vírgula para separar os números de aviso.

   ![Propriedades do pacote NuGet](media/nuget-properties-nowarn.png)

   O aviso desaparece do **Gerenciador de Soluções** e da **Lista de Erros**.

## <a name="see-also"></a>Veja também

- [Passo a passo: Criar um aplicativo](../ide/walkthrough-building-an-application.md)
- [Como exibir, salvar e configurar arquivos de log de build](../ide/how-to-view-save-and-configure-build-log-files.md)
- [Compilação e construção](../ide/compiling-and-building-in-visual-studio.md)
