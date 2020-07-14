---
title: 'Walkthrough: Criando um SDK usando C# ou Visual Basic | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: ef96a249-5eef-402a-a8d5-d74cb49239bd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CSharp
- VB
ms.openlocfilehash: 73cd76445adb798be078461e5b209e35f8b8163c
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904970"
---
# <a name="walkthrough-create-an-sdk-using-c-or-visual-basic"></a>Walkthrough: criar um SDK usando C# ou Visual Basic
Neste tutorial, você aprenderá a criar um SDK de biblioteca de matemática simples usando o Visual C# e, em seguida, empacotará o SDK como uma extensão do Visual Studio (VSIX). Você concluirá os seguintes procedimentos:

- [Para criar o componente de Windows Runtime SimpleMath](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createClassLibrary)

- [Para criar o projeto de extensão SimpleMathVSIX](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createVSIX)
- [Para criar um aplicativo de exemplo que usa a biblioteca de classes](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createSample)

## <a name="prerequisites"></a>Pré-requisitos
 Para seguir este passo a passos, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [Visual Studio SDK](../extensibility/visual-studio-sdk.md).

## <a name="to-create-the-simplemath-windows-runtime-component"></a><a name="createClassLibrary"></a>Para criar o componente de Windows Runtime SimpleMath

1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

2. Na lista de modelos, expanda **Visual C#** ou **Visual Basic**, escolha o nó **Windows Store** e, em seguida, escolha o modelo de **componente de Windows Runtime** .

3. Na caixa **nome** , especifique **SimpleMath**e, em seguida, escolha o botão **OK** .

4. No **Gerenciador de soluções**, abra o menu de atalho para o nó do projeto **SimpleMath** e escolha **Propriedades**.

5. Renomeie **Class1.cs** para **Arithmetic.cs** e atualize-o para corresponder ao seguinte código:

    [!code-csharp[CreatingAnSDKUsingWinRT#3](../extensibility/codesnippet/CSharp/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_1.cs)]
    [!code-vb[CreatingAnSDKUsingWinRT#3](../extensibility/codesnippet/VisualBasic/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_1.vb)]

6. No **Gerenciador de soluções**, abra o menu de atalho do nó da **solução ' SimpleMath '** e escolha **Configuration Manager**.

    A caixa de diálogo **Configuration Manager** é aberta.

7. Na lista **configuração de solução ativa** , escolha **liberar**.

8. Na coluna **configuração** , verifique se **SimpleMath** linha está definida como **liberar**e, em seguida, escolha o botão **fechar** para aceitar a alteração.

   > [!IMPORTANT]
   > O SDK para o componente SimpleMath inclui apenas uma configuração. Essa configuração deve ser a compilação de versão ou os aplicativos que usam o componente não passarão na certificação para o [!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)] .

9. No **Gerenciador de soluções**, abra o menu de atalho para o nó do projeto **SimpleMath** e escolha **Compilar**.

## <a name="to-create-the-simplemathvsix-extension-project"></a><a name="createVSIX"></a>Para criar o projeto de extensão SimpleMathVSIX

1. No menu de atalho do nó da **solução ' SimpleMath '** , escolha **Adicionar**  >  **novo projeto**.

2. Na lista de modelos, expanda **Visual C#** ou **Visual Basic**, escolha o nó **extensibilidade** e, em seguida, escolha o modelo de **projeto VSIX** .

3. Na caixa **nome** , especifique **SimpleMathVSIX**e, em seguida, escolha o botão **OK** .

4. Em **Gerenciador de soluções**, escolha o item **origem. extensão. vsixmanifest** .

5. Na barra de menus, escolha **Exibir**  >  **código**.

6. Substitua o XML existente pelo seguinte XML:

     [!code-xml[CreatingAnSDKUsingWinRT#1](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_2.xml)]

7. Em **Gerenciador de soluções**, escolha o projeto **SimpleMathVSIX** .

8. Na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

9. Na lista de **itens comuns**, expanda **dados**e, em seguida, escolha **arquivo XML**.

10. Na caixa **nome** , especifique `SDKManifest.xml` e, em seguida, escolha o botão **Adicionar** .

11. No **Gerenciador de soluções**, abra o menu de atalho para `SDKManifest.xml` , escolha **Propriedades**e, em seguida, altere o valor da propriedade **include in VSIX** para **true**.

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

13. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **SimpleMathVSIX** , escolha **Adicionar**e, em seguida, escolha **nova pasta**.

14. Renomeie a pasta como `references` .

15. Abra o menu de atalho para a pasta **referências** , escolha **Adicionar**e, em seguida, escolha **nova pasta**.

16. Renomeie a subpasta para `commonconfiguration` , crie uma subpasta dentro dela e nomeie a subpasta `neutral` .

17. Repita as quatro etapas anteriores, desta vez renomeando a primeira pasta para `redist` .

     O projeto agora contém a seguinte estrutura de pastas:

    ```xml
    references\commonconfiguration\neutral
    redist\commonconfiguration\neutral
    ```

18. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **SimpleMath** e, em seguida, escolha **abrir pasta no explorador de arquivos**.

19. No **Explorador de arquivos**, navegue até a pasta *bin\Release* , abra o menu de atalho do arquivo **SimpleMath. winmd** e, em seguida, escolha **copiar**.

20. Em **Gerenciador de soluções**, Cole o arquivo na pasta *References\commonconfiguration\neutral* no projeto **SimpleMathVSIX** .

21. Repita a etapa anterior, colando o arquivo **SimpleMath. pri** na pasta *Redist\commonconfiguration\neutral* do projeto **SimpleMathVSIX** .

22. Em **Gerenciador de soluções**, escolha **SimpleMath. winmd**.

23. Na barra de menus, escolha **Exibir**  >  **Propriedades** (teclado: escolha a tecla **F4** ).

24. Na janela **Propriedades** , altere a propriedade **ação de compilação** para **conteúdo**e, em seguida, altere a propriedade **incluir na VSIX** para **true**.

25. Em **Gerenciador de soluções**, repita esse processo para **SimpleMath. pri**.

26. Em **Gerenciador de soluções**, escolha o projeto **SimpleMathVSIX** .

27. Na barra de menus, escolha **Build**  >  **Compilar SimpleMathVSIX**.

28. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **SimpleMathVSIX** e, em seguida, escolha **abrir pasta no explorador de arquivos**.

29. No **Explorador de arquivos**, navegue até a pasta *\Bin\Release* e execute *SimpleMathVSIX. vsix* para instalá-lo.

30. Escolha o botão **instalar** , aguarde a conclusão da instalação e reinicie o Visual Studio.

## <a name="to-create-a-sample-app-that-uses-the-class-library"></a><a name="createSample"></a>Para criar um aplicativo de exemplo que usa a biblioteca de classes

1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

2. Na lista de modelos, expanda **Visual C#** ou **Visual Basic**e, em seguida, escolha o nó **Windows Store** .

3. Escolha o modelo de **aplicativo em branco** , nomeie o projeto **ArithmeticUI**e escolha o botão **OK** .

4. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **ArithmeticUI** e escolha **Adicionar**  >  **referência**.

5. Na lista de tipos de referência, expanda **Windows**e, em seguida, escolha **extensões**.

6. No painel de detalhes, escolha a extensão de **biblioteca matemática do WinRT** .

    Informações adicionais sobre o SDK são exibidas. Você pode escolher o link **mais informações** a ser aberto https://msdn.microsoft.com/ , como você especificou no arquivo SDKManifest.xml anteriormente neste guia.

7. Na caixa de diálogo **Gerenciador de referências** , marque a caixa de seleção biblioteca de **matemática do WinRT** e escolha o botão **OK** .

8. Na barra de menus, escolha **Exibir**  >  **pesquisador de objetos**.

9. Na lista **procurar** , escolha **matemática simples**.

     Agora você pode explorar o que está no SDK.

10. No **Gerenciador de soluções**, abra **MainPage. XAML**e substitua seu conteúdo pelo XAML a seguir:

    **C#**

    ```xml
    <Page
        x:Class="ArithmeticUI.MainPage"
        IsTabStop="False"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:SimpleMath"
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
        x:Class="ArithmeticUI.MainPage"
        IsTabStop="False"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:local="using:SimpleMath"
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

11. Atualize **MainPage.XAML.cs** para corresponder ao seguinte código:

     [!code-csharp[CreatingAnSDKUsingWinRTDemoApp#2](../extensibility/codesnippet/CSharp/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_5.cs)]
     [!code-vb[CreatingAnSDKUsingWinRTDemoApp#2](../extensibility/codesnippet/VisualBasic/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_5.vb)]

12. Escolha a tecla **F5** para executar o aplicativo.

13. No aplicativo, insira dois números, escolha uma operação e, em seguida, escolha o **=** botão.

     O resultado correto é exibido.

    Você criou e usou com êxito um SDK de extensão.

## <a name="see-also"></a>Confira também
- [Walkthrough: criar um SDK usando C++](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)
- [Walkthrough: criar um SDK usando JavaScript](../extensibility/walkthrough-creating-an-sdk-using-javascript.md)
- [Criar um Software Development Kit](../extensibility/creating-a-software-development-kit.md)
