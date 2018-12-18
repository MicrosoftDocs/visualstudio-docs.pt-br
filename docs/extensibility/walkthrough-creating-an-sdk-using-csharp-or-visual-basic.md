---
title: 'Passo a passo: Criando um SDK usando c# ou Visual Basic | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: ef96a249-5eef-402a-a8d5-d74cb49239bd
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3c65f827af864a32bb13a90a0ba9818467298527
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49835144"
---
# <a name="walkthrough-create-an-sdk-using-c-or-visual-basic"></a>Passo a passo: Criar um SDK usando c# ou Visual Basic
Neste passo a passo, você aprenderá como criar um SDK de biblioteca de matemática simples usando o Visual c# e, em seguida, o SDK como um Visual Studio VSIX (extensão) do pacote. Você concluirá os procedimentos a seguir:  
  
-   [Para criar o componente de tempo de execução SimpleMath Windows](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createClassLibrary)  
  
-   [Para criar o projeto de extensão SimpleMathVSIX](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createVSIX)  
-   [Para criar um aplicativo de exemplo que usa a biblioteca de classes](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createSample)  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para seguir este passo a passo, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  
  
##  <a name="createClassLibrary"></a> Para criar o componente de tempo de execução SimpleMath Windows  
  
1. Na barra de menus, escolha **arquivo** > **New** > **novo projeto**.  
  
2. Na lista de modelos, expanda **Visual c#** ou **Visual Basic**, escolha o **Windows Store** nó e, em seguida, escolha o **componente de tempo de execução do Windows** modelo.  
  
3. No **nome** , especifique **SimpleMath**e, em seguida, escolha o **Okey** botão.  
  
4. Na **Gerenciador de soluções**, abra o menu de atalho para o **SimpleMath** nó do projeto e, em seguida, escolha **propriedades**.  
  
5. Renomeie **Class1.cs** à **Arithmetic.cs** e atualizá-lo de acordo com o código a seguir:  
  
    [!code-csharp[CreatingAnSDKUsingWinRT#3](../extensibility/codesnippet/CSharp/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_1.cs)]
    [!code-vb[CreatingAnSDKUsingWinRT#3](../extensibility/codesnippet/VisualBasic/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_1.vb)]  
  
6. Na **Gerenciador de soluções**, abra o menu de atalho para o **solução 'SimpleMath'** nó e, em seguida, escolha **Configuration Manager**.  
  
    O **Configuration Manager** caixa de diálogo é aberta.  
  
7. No **configuração da solução ativa** , escolha **versão**.  
  
8. No **Configuration** coluna, verifique **SimpleMath** linha é definida como **versão**e, em seguida, escolha o **fechar** botão para aceitar o Altere.  
  
   > [!IMPORTANT]
   >  O SDK para o componente SimpleMath inclui apenas uma configuração. Essa configuração deve ser o build de versão, ou aplicativos que usam o componente não passam na certificação o[!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)].  
  
9. Na **Gerenciador de soluções**, abra o menu de atalho para o **SimpleMath** nó do projeto e, em seguida, escolha **Build**.  
  
##  <a name="createVSIX"></a> Para criar o projeto de extensão SimpleMathVSIX  
  
1.  No menu de atalho para o **solução 'SimpleMath'** nó, escolha **Add** > **novo projeto**.  
  
2.  Na lista de modelos, expanda **Visual c#** ou **Visual Basic**, escolha o **extensibilidade** nó e, em seguida, escolha o **projeto VSIX** modelo.  
  
3.  No **nome** , especifique **SimpleMathVSIX**e, em seguida, escolha o **Okey** botão.  
  
4.  Na **Gerenciador de soluções**, escolha o **vsixmanifest** item.  
  
5.  Na barra de menus, escolha **Exibir** > **Código**.  
  
6.  Substitua o XML existente com o seguinte XML:  
  
     [!code-xml[CreatingAnSDKUsingWinRT#1](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_2.xml)]
  
7.  Na **Gerenciador de soluções**, escolha o **SimpleMathVSIX** projeto.  
  
8.  Na barra de menus, escolha **Projeto** > **Adicionar Novo Item**.  
  
9. Na lista de **itens comuns**, expanda **dados**e, em seguida, escolha **arquivo XML**.  
  
10. No **nome** , especifique `SDKManifest.xml`e, em seguida, escolha o **Add** botão.  
  
11. Na **Gerenciador de soluções**, abra o menu de atalho `SDKManifest.xml`, escolha **propriedades**e, em seguida, altere o valor da **incluir em VSIX** propriedade para **Verdadeiro**.  
  
12. Substitua o conteúdo do arquivo pelo XML a seguir:  

    **C#**
    ```xml
    <FileList
      DisplayName="WinRT Math Library (CS)"
      MinVSVersion="11.0"
      TargetFramework=".NETCore,version=v4.5"
      AppliesTo="WindowsAppContainer"
      SupportsMultipleVersions="Error"
      MoreInfo="https://msdn.microsoft.com/">
    </FileList>
    ```

    **Visual Basic**
    ```xml
    <FileList
      DisplayName="WinRT Math Library (VB)"
      MinVSVersion="11.0"
      TargetFramework=".NETCore,version=v4.5"
      AppliesTo="WindowsAppContainer"
      SupportsMultipleVersions="Error"
      MoreInfo="https://msdn.microsoft.com/">
    </FileList>
    ```  
  
13. Na **Gerenciador de soluções**, abra o menu de atalho para o **SimpleMathVSIX** do projeto, escolha **Add**e, em seguida, escolha **nova pasta**.  
  
14. Renomear a pasta para `references`.  
  
15. Abra o menu de atalho para o **referências** pasta, escolha **Add**e, em seguida, escolha **nova pasta**.  
  
16. Renomeie a subpasta `commonconfiguration`, crie uma subpasta dentro dele e nomear a subpasta `neutral`.  
  
17. Repita as quatro etapas anteriores, desta vez, a primeira pasta para a renomeação `redist`.  
  
     O projeto agora contém a seguinte estrutura de pasta:  
  
    ```xml
    references\commonconfiguration\neutral  
    redist\commonconfiguration\neutral  
    ```  
  
18. Na **Gerenciador de soluções**, abra o menu de atalho para o **SimpleMath** do projeto e, em seguida, escolha **Abrir pasta no Explorador de arquivos**.  
  
19. Na **Explorador de arquivos**, navegue até a *bin\Release* pasta, abra o menu de atalho para o **SimpleMath.winmd** file e, em seguida, escolha **copiar**.  
  
20. Na **Gerenciador de soluções**, cole o arquivo na *references\commonconfiguration\neutral* pasta o **SimpleMathVSIX** projeto.  
  
21. Repita a etapa anterior, colando as **SimpleMath.pri** o arquivo na *redist\commonconfiguration\neutral* pasta no **SimpleMathVSIX** projeto.  
  
22. Na **Gerenciador de soluções**, escolha **SimpleMath.winmd**.  
  
23. Na barra de menus, escolha **modo de exibição** > **as propriedades** (teclado: escolha a **F4** chave).  
  
24. No **propriedades** janela, altere o **Build Action** propriedade a ser **conteúdo**e, em seguida, altere o **incluir em VSIX** propriedade  **True**.  
  
25. Na **Gerenciador de soluções**, repita esse processo para **SimpleMath.pri**.  
  
26. Na **Gerenciador de soluções**, escolha o **SimpleMathVSIX** projeto.  
  
27. Na barra de menus, escolha **construir** > **Build SimpleMathVSIX**.  
  
28. Na **Gerenciador de soluções**, abra o menu de atalho para o **SimpleMathVSIX** do projeto e, em seguida, escolha **Abrir pasta no Explorador de arquivos**.  
  
29. Na **Explorador de arquivos**, navegue até *\bin\Release* pasta e, em seguida, execute *SimpleMathVSIX.vsix* para instalá-lo.  
  
30. Escolha o **instalar** botão, aguarde a conclusão da instalação e, em seguida, reinicie o Visual Studio.  
  
##  <a name="createSample"></a> Para criar um aplicativo de exemplo que usa a biblioteca de classes  
  
1. Na barra de menus, escolha **arquivo** > **New** > **novo projeto**.  
  
2. Na lista de modelos, expanda **Visual c#** ou **Visual Basic**e, em seguida, escolha o **Windows Store** nó.  
  
3. Escolha o **aplicativo em branco** modelo, o nome do projeto **ArithmeticUI**e, em seguida, escolha o **Okey** botão.  
  
4. Na **Gerenciador de soluções**, abra o menu de atalho para o **ArithmeticUI** do projeto e, em seguida, escolha **Add** > **referência**.  
  
5. Na lista de tipos de referência, expanda **Windows**e, em seguida, escolha **extensões**.  
  
6. No painel de detalhes, escolha o **SDK de matemática simples** extensão.  
  
    Informações adicionais sobre o SDK é exibida. Você pode escolher o **mais informações** link para abrir https://msdn.microsoft.com/, conforme especificado no arquivo Sdkmanifest no início deste passo a passo.  
  
7. No **Gerenciador de referências** caixa de diálogo, selecione o **SDK de matemática simples** caixa de seleção e, em seguida, escolha o **Okey** botão.  
  
8. Na barra de menus, escolha **modo de exibição** > **Pesquisador de objetos**.  
  
9. No **navegue** , escolha **matemática simples**.  
  
     Agora você pode explorar o que há no SDK.  
  
10. Na **Gerenciador de soluções**, abra **MainPage. XAML**e substitua seu conteúdo com o XAML a seguir:  

    **C#**
    ```xml
    <Page
        x:Class="WinRTMathTestCS.MainPage"
        IsTabStop="False"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:WinRTMathTestCS"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        mc:Ignorable="d">

        <Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
            <TextBox x:Name="_firstNumber" HorizontalAlignment="Left" Margin="414,370,0,0" TextWrapping="Wrap" Text="First Number" VerticalAlignment="Top" Height="32" Width="135" TextAlignment="Center"/>
            <TextBox x:Name="_secondNumber" HorizontalAlignment="Left" Margin="613,370,0,0" TextWrapping="Wrap" Text="Second Number" VerticalAlignment="Top" Height="32" Width="135" TextAlignment="Center"/>
            <Button Content="+" HorizontalAlignment="Left" Margin="557,301,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="-" HorizontalAlignment="Left" Margin="557,345,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="*" HorizontalAlignment="Left" Margin="557,389,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="/" HorizontalAlignment="Left" Margin="557,433,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="=" HorizontalAlignment="Left" Margin="755,367,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnResultsClick"/>
            <TextBox x:Name="_result" HorizontalAlignment="Left" Margin="809,370,0,0" TextWrapping="Wrap" Text="Result" VerticalAlignment="Top" Height="32" Width="163" TextAlignment="Center" IsReadOnly="True"/>
        </Grid>
    </Page>
    ```
    
    **Visual Basic**
    ```xml
    <Page
        x:Class="WinRTMathTest.MainPage"
        IsTabStop="False"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:WinRTMathTest"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        mc:Ignorable="d">

        <Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
            <TextBox x:Name="_firstNumber" HorizontalAlignment="Left" Margin="414,370,0,0" TextWrapping="Wrap" Text="First Number" VerticalAlignment="Top" Height="32" Width="135" TextAlignment="Center"/>
            <TextBox x:Name="_secondNumber" HorizontalAlignment="Left" Margin="613,370,0,0" TextWrapping="Wrap" Text="Second Number" VerticalAlignment="Top" Height="32" Width="135" TextAlignment="Center"/>
            <Button Content="+" HorizontalAlignment="Left" Margin="557,301,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="-" HorizontalAlignment="Left" Margin="557,345,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="*" HorizontalAlignment="Left" Margin="557,389,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="/" HorizontalAlignment="Left" Margin="557,433,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnOperatorClick"/>
            <Button Content="=" HorizontalAlignment="Left" Margin="755,367,0,0" VerticalAlignment="Top" Height="39" Width="49" Click="OnResultsClick"/>
            <TextBox x:Name="_result" HorizontalAlignment="Left" Margin="809,370,0,0" TextWrapping="Wrap" Text="Result" VerticalAlignment="Top" Height="32" Width="163" TextAlignment="Center" IsReadOnly="True"/>
        </Grid>
    </Page>
    ```
  
11. Atualização **MainPage.xaml.cs** para coincidir com o código a seguir:  
  
     [!code-csharp[CreatingAnSDKUsingWinRTDemoApp#2](../extensibility/codesnippet/CSharp/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_5.cs)]
     [!code-vb[CreatingAnSDKUsingWinRTDemoApp#2](../extensibility/codesnippet/VisualBasic/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_5.vb)]  
  
12. Escolha o **F5** chave para executar o aplicativo.  
  
13. No aplicativo, insira quaisquer dois números, escolha uma operação e, em seguida, escolha o **=** botão.  
  
     O resultado correto é exibido.  
  
    Você criou e usado um SDK de extensão com êxito.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Criar um SDK usando C++](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)   
 [Passo a passo: Criar um SDK usando JavaScript](../extensibility/walkthrough-creating-an-sdk-using-javascript.md)   
 [Criar um Kit de desenvolvimento de Software](../extensibility/creating-a-software-development-kit.md)