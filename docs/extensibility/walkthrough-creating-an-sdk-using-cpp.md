---
title: 'Passo a passo: criando um SDK usando C++ | Microsoft Docs'
description: Saiba como criar um SDK nativo da biblioteca matemática do C++, empacotar o SDK como uma Extensão Visual Studio e, em seguida, usá-lo para criar um aplicativo usando este passo a passo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 36ea793b-3832-41a1-b906-69e680ad5e1d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6a52322e575dc201a6bf1648af93d813828e0b17
ms.sourcegitcommit: 8b75524dc544e34d09ef428c3ebbc9b09f14982d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2021
ms.locfileid: "113223001"
---
# <a name="walkthrough-create-an-sdk-using-c"></a>Passo a passo: criar um SDK usando C++
Este passo a passo mostra como criar um SDK de biblioteca matemática C++ nativo, empacotar o SDK como uma VSIX (extensão Visual Studio) e, em seguida, usá-lo para criar um aplicativo. O passo a passo é dividido nestas etapas:

- [Para criar as bibliotecas nativas e Windows Runtime](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createClassLibrary)

- [Para criar o projeto de extensão NativeMathVSIX](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createVSIX)

- [Para criar um aplicativo de exemplo que usa a biblioteca de classes](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createSample)

## <a name="prerequisites"></a>Pré-requisitos
 Para seguir este passo a passo, você deve instalar o Visual Studio SDK. Para obter mais informações, [consulte Visual Studio SDK](../extensibility/visual-studio-sdk.md).

## <a name="to-create-the-native-and-windows-runtime-libraries"></a><a name="createClassLibrary"></a>Para criar as bibliotecas nativas e Windows Runtime

1. Na barra de menus, escolha **Arquivo**  >    >  **Novo Project**.

2. Na lista de modelos, expanda Visual C++ Windows Universal e selecione o modelo  >   **DLL (Windows Aplicativos Universais).** Na caixa **Nome,** especifique `NativeMath` e, em seguida, escolha o **botão OK.**

3. Atualize *NativeMath.h* para corresponder ao código a seguir.

     :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemath/nativemath.h" id="Snippet1":::

4. Atualize *NativeMath.cpp* para corresponder a este código:

     :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemath/nativemath.cpp" id="Snippet2":::

5. No **Gerenciador de Soluções**, abra o menu de atalho **da Solução 'NativeMath'** e escolha **Adicionar**  >  **Novo Project**.

6. Na lista de modelos, expanda **Visual C++** e selecione o modelo **Windows Componente de Runtime.** Na caixa **Nome,** especifique `NativeMathWRT` e, em seguida, escolha o **botão OK.**

7. Atualize *Class1.h* para corresponder a este código:

     :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathwrt/class1.h" id="Snippet3":::

8. Atualize *Class1.cpp* para corresponder a este código:

     :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathwrt/class1.cpp" id="Snippet4":::

9. Na barra de menus, escolha **Criar Solução**  >  **de Build**.

## <a name="to-create-the-nativemathvsix-extension-project"></a><a name="createVSIX"></a> Para criar o projeto de extensão NativeMathVSIX

1. No **Gerenciador de Soluções**, abra o menu de atalho **da Solução 'NativeMath'** e escolha **Adicionar**  >  **Novo Project**.

2. Na lista de modelos, expanda Extensibilidade do **Visual C#** e  >  selecione **VSIX Project**. Na caixa **Nome,** **especifique NativeMathVSIX** e, em seguida, escolha o **botão OK.**

3. No **Gerenciador de Soluções**, abra o menu de atalho para **source.extension.vsixmanifest** e escolha **Exibir Código**.

4. Use o XML a seguir para substituir o XML existente.

    ```xml
    <PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">
      <Metadata>
        <Identity Id="NativeMathVSIX..c6b3cae1-e7e2-4e71-90f6-21017ea0dff7" Version="1.0" Language="en-US" Publisher="MyName" />
        <DisplayName>Native Math SDK</DisplayName>
        <Description>Native Math Library w/ Windows Runtime Additions</Description>
      </Metadata>
      <Installation Scope="Global" AllUsers="true">
        <InstallationTarget Id="Microsoft.ExtensionSDK" TargetPlatformIdentifier="Windows" TargetPlatformVersion="v8.0" SdkName="NativeMathSDK" SdkVersion="1.0" />
      </Installation>
      <Dependencies>
      </Dependencies>
      <Assets>
        <Asset Type="Microsoft.ExtensionSDK" d:Source="File" Path="SDKManifest.xml" />
      </Assets>
    </PackageManifest>
    ```

5. No **Gerenciador de Soluções**, abra o menu de atalho do **projeto NativeMathVSIX** e escolha **Adicionar**  >  **Novo Item**.

6. Na lista de Itens **do Visual C#,** expanda **Dados** e, em seguida, selecione **Arquivo XML.** Na caixa **Nome,** especifique `SDKManifest.xml` e, em seguida, escolha o **botão OK.**

7. Use este XML para substituir o conteúdo do arquivo:

    :::code language="xml" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathvsix/sdkmanifest.xml" id="Snippet5":::

8. No **Gerenciador de Soluções**, no projeto **NativeMathVSIX,** crie esta estrutura de pastas:

    ```xml
    \DesignTime
          \CommonConfiguration
                \Neutral
                      \Include
          \Debug
                \x86
    \Redist
          \Debug
                \x86
    \References
          \CommonConfiguration
                \Neutral
    ```

9. No **Gerenciador de Soluções**, abra o menu de atalho da **Solução 'NativeMath'** e escolha **Abrir Pasta no Explorador de Arquivos**.

10. No **Explorador de Arquivos**, copie *$SolutionRoot$\NativeMath\NativeMath.h* e, em **seguida,** no Gerenciador de Soluções , no projeto **NativeMathVSIX,** copie-o na pasta *\\ $SolutionRoot$\NativeMathVSIX\DesignTime\CommonConfiguration\Neutral\Include.*

     Copie *$SolutionRoot$\Debug\NativeMath\NativeMath.lib* e, em seguida, copie-o na pasta *\\ $SolutionRoot$\NativeMathVSIX\DesignTime\Debug\x86.*

     Copie *$SolutionRoot$\Debug\NativeMath\NativeMath.dll* e colá-lo na *pasta $SolutionRoot$\NativeMathVSIX\Redist\Debug\x86. \\*

     Copie *$SolutionRoot$\Debug\NativeMathWRT\NativeMathWRT.dll* e colá-lo na *pasta $SolutionRoot$\NativeMathVSIX\Redist\Debug\x86.*
     Copie *$SolutionRoot$\Debug\NativeMathWRT\NativeMathWRT.winmd* e copie-o na pasta *$SolutionRoot$\NativeMathVSIX\References\CommonConfiguration\Neutral.*

     Copie *$SolutionRoot$\Debug\NativeMathWRT\NativeMathWRT.pri* e copie-o na pasta *$SolutionRoot$\NativeMathVSIX\References\CommonConfiguration\Neutral.*

11. Na pasta *$SolutionRoot$\NativeMathVSIX\DesignTime\Debug\x86, \\* crie um arquivo de texto chamado *NativeMathSDK.props* e, em seguida, colar o seguinte conteúdo nele:
   
    ```xml
    <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <PropertyGroup>
        <NativeMathSDKPath>$(FrameworkSDKRoot)\..\..\UAP\v0.8.0.0\ExtensionSDKs\NativeMathSDK\1.0\</NativeMathSDKPath>
        <IncludePath>$(NativeMathSDKPath)DesignTime\CommonConfiguration\Neutral\Include;$(IncludePath)</IncludePath>
        <LibraryPath>$(NativeMathSDKPath)DesignTime\Debug\x86;$(LibraryPath)</LibraryPath>
      </PropertyGroup>
      <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Debug|Win32'">
         <Link>
           <AdditionalDependencies>NativeMath.lib;%(AdditionalDependencies)</AdditionalDependencies>
         </Link>
      </ItemDefinitionGroup>
    </Project>
    ```

12. Na barra de menus, escolha **Exibir**  >  **Windows**  >  **Janela Propriedades** (Teclado: Escolha a tecla **F4).**

13. No **Gerenciador de Soluções**, selecione o **arquivo NativeMathWRT.winmd.** Na janela **Propriedades,** altere a propriedade Ação de **Build** para **Conteúdo** e altere a propriedade Incluir no **VSIX** para **True.**

     Repita esse processo para o **arquivo NativeMath.h.**

     Repita esse processo para o **arquivo NativeMathWRT.pri.**

     Repita esse processo para o **arquivo NativeMath.Lib.**

     Repita esse processo para o **arquivo NativeMathSDK.props.**

14. No **Gerenciador de Soluções**, selecione o **arquivo NativeMath.h.** Na janela **Propriedades,** altere a **propriedade Incluir no VSIX** para **True.**

     Repita esse processo para o **NativeMath.dll** arquivo.

     Repita esse processo para o **NativeMathWRT.dll** arquivo.

     Repita esse processo para o **SDKManifest.xml** arquivo.

15. Na barra de menus, escolha **Criar Solução**  >  **de Build**.

16. No **Gerenciador de Soluções**, abra o menu de atalho do **projeto NativeMathVSIX** e escolha **Abrir Pasta no Explorador de Arquivos**.

17. No **Explorador de Arquivos**, navegue até a pasta *$SolutionRoot$\NativeMathVSIX\bin\Debug* e execute *NativeMathVSIX.vsix* para iniciar a instalação.

18. Escolha o **botão** Instalar, aguarde a instalação ser final e, em seguida, abra Visual Studio.

## <a name="to-create-a-sample-app-that-uses-the-class-library"></a><a name="createSample"></a> Para criar um aplicativo de exemplo que usa a biblioteca de classes

1. Na barra de menus, escolha **Arquivo**  >    >  **Novo Project**.

2. Na lista de modelos, **expanda** Visual C++  >  **Windows Universal** e selecione **Aplicativo em Branco.** Na caixa **Nome,** especifique **NativeMathSDKSample** e, em seguida, escolha o **botão OK.**

3. No **Gerenciador de Soluções**, abra o menu de atalho do **projeto NativeMathSDKSample** e escolha **Adicionar**  >  **Referência**.

4. Na caixa **de diálogo** Adicionar Referência, na lista de tipos de **referência,** expanda Universal Windows e, em seguida, selecione **Extensões**. Por fim, marque a caixa de **seleção SDK de** Matemática Nativa e, em seguida, escolha o **botão OK.**

5. Exibir as propriedades do projeto para NativeMathSDKSample.

    As propriedades que você definiu *em NativeMathSDK.props* foram aplicadas quando você adicionou a referência. Você pode verificar se as propriedades foram aplicadas examinando a **propriedade VC++ Diretórios** do projeto das Propriedades de **Configuração do projeto.**

6. No **Gerenciador de Soluções**, abra **MainPage.xaml** e, em seguida, use o seguinte XAML para substituir seu conteúdo:

    :::code language="xml" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml" id="Snippet1":::

7. Atualize *Mainpage.xaml.h* para corresponder a este código:

    :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml.h" id="Snippet2":::

8. Atualize *MainPage.xaml.cpp* para corresponder a este código:

    :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml.cpp" id="Snippet3":::

9. Escolha a **tecla F5** para executar o aplicativo.

10. No aplicativo, insira dois números, selecione uma operação e, em seguida, escolha o **=** botão.

     O resultado correto é exibido.

    Este passo a passo mostrou como criar e usar um SDK de Extensão para chamar uma biblioteca [!INCLUDE[wrt](../extensibility/includes/wrt_md.md)] e uma biblioteca [!INCLUDE[wrt](../extensibility/includes/wrt_md.md)] não.

## <a name="next-steps"></a>Próximas etapas

## <a name="see-also"></a>Confira também
- [Passo a passo: criar um SDK usando C# ou Visual Basic](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)
- [Criar um kit de desenvolvimento de software](../extensibility/creating-a-software-development-kit.md)
