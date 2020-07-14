---
title: Adicionando controle de usuário à página inicial | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- start page dll
- custom start page
- start page assembly
ms.assetid: 5b7997db-af6f-4fa9-a128-bceb42bddaf1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 8000c6cc067f61a64c71b8c8ac4f5c0176504cd4
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903389"
---
# <a name="add-user-control-to-the-start-page"></a>Adicionar controle de usuário à página inicial

Este tutorial mostra como adicionar uma referência de DLL a uma página inicial personalizada. O exemplo adiciona um controle de usuário à solução, cria o controle de usuário e, em seguida, faz referência ao assembly compilado do arquivo Start Page *. XAML* . Uma nova guia hospeda o controle de usuário, que funciona como um navegador da Web básico.

Você pode usar o mesmo processo para adicionar qualquer assembly que possa ser chamado a partir de um arquivo *. XAML* .

## <a name="add-a-wpf-user-control-to-the-solution"></a>Adicionar um controle de usuário do WPF à solução

Primeiro, adicione um controle de usuário de Windows Presentation Foundation (WPF) à solução de página inicial.

1. Crie uma página inicial usando nós criamos em [criar uma página inicial personalizada](../extensibility/creating-a-custom-start-page.md).

2. Em **Gerenciador de soluções**, clique com o botão direito do mouse na solução, clique em **Adicionar**e em **novo projeto**.

3. No painel esquerdo da caixa de diálogo **novo projeto** , expanda o nó **Visual Basic** ou **Visual C#** e clique em **Windows**. No painel central, selecione **biblioteca de controle de usuário do WPF**.

4. Nomeie o controle `WebUserControl` e clique em **OK**.

## <a name="implement-the-user-control"></a>Implementar o controle de usuário

Para implementar um controle de usuário do WPF, crie a interface do usuário em XAML e, em seguida, escreva os eventos code-behind em C# ou em outra linguagem .NET.

### <a name="to-write-the-xaml-for-the-user-control"></a>Para gravar o XAML para o controle de usuário

1. Abra o arquivo XAML para o controle de usuário. No `<Grid>` elemento, adicione as seguintes definições de linha ao controle.

    ```vb
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="*" />
    </Grid.RowDefinitions>

    ```

2. No elemento principal `<Grid>` , adicione o novo elemento a seguir `<Grid>` , que contém uma caixa de texto para digitar endereços da Web e um botão para definir o novo endereço.

    ```xml
    <Grid Grid.Row="0">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="*" />
            <ColumnDefinition Width="Auto" />
        </Grid.ColumnDefinitions>
        <TextBox x:Name="UserSource" Grid.Column="0" />
        <Button Grid.Column="1" x:Name="SetButton" Content="Set Address" Click="SetButton_Click" />
    </Grid>
    ```

3. Adicione o quadro a seguir ao elemento de nível superior `<Grid>` logo após o `<Grid>` elemento que contém o botão e a caixa de texto.

    ```vb
    <Frame Grid.Row="1" x:Name="WebFrame" Source="http://www.bing.com" Navigated="WebFrame_Navigated" />
    ```

4. O exemplo a seguir mostra o XAML concluído para o controle de usuário.

    ```xml
    <UserControl x:Class="WebUserControl.UserControl1"
                 xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                 xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                 xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
                 xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
                 mc:Ignorable="d"
                 d:DesignHeight="300" d:DesignWidth="300">
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*" />
            </Grid.RowDefinitions>
            <Grid Grid.Row="0">
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="*" />
                    <ColumnDefinition Width="Auto" />
                </Grid.ColumnDefinitions>
                <TextBox x:Name="UserSource" Grid.Column="0" />
                <Button Grid.Column="1" x:Name="SetButton" Content="Set Address" Click="SetButton_Click" />
            </Grid>
            <Frame Grid.Row="1" x:Name="WebFrame" Source="http://www.bing.com" Navigated="WebFrame_Navigated" />
        </Grid>
    </UserControl>

    ```

### <a name="to-write-the-code-behind-events-for-the-user-control"></a>Para gravar os eventos code-behind para o controle de usuário

1. No designer XAML, clique duas vezes no botão **Set Address (Definir endereço** ) que você adicionou ao controle.

    O arquivo *UserControl1.cs* é aberto no editor de código.

2. Preencha o manipulador de eventos SetButton_Click da seguinte maneira.

    ```csharp
    private void SetButton_Click(object sender, RoutedEventArgs e)
    {
        try
        {
            this.WebFrame.Source = new Uri(this.UserSource.Text, UriKind.Absolute);
        }
        catch (Exception error)
        {
            MessageBox.Show(error.Message);
        }
    }
    ```

    Esse código define o endereço da Web que é digitado na caixa de texto como o destino do navegador da Web. Se o endereço não for válido, o código lançará um erro.

3. Você também deve manipular o evento WebFrame_Navigated:

    ```csharp
    private void WebFrame_Navigated(object sender, EventArgs e)
    { }
    ```

4. Compile a solução.

## <a name="add-the-user-control-to-the-start-page"></a>Adicionar o controle de usuário à página inicial

Para disponibilizar esse controle para o projeto de página inicial, no arquivo de projeto da página inicial, adicione uma referência à nova biblioteca de controle. Em seguida, você pode adicionar o controle à marcação XAML da página inicial.

1. No **Gerenciador de soluções**, no projeto de página inicial, clique com o botão direito do mouse em **referências** e clique em **Adicionar referência**.

2. Na guia **projetos** , selecione **webusercontrol** e clique em **OK**.

3. No menu **Compilar**, clique em **Compilar Solução**.

    A criação da solução torna o controle do usuário disponível para o IntelliSense para outros arquivos na solução.

    Para adicionar o controle à marcação XAML da página inicial, adicione uma referência de namespace ao assembly e, em seguida, coloque o controle na página.

### <a name="to-add-the-control-to-the-markup"></a>Para adicionar o controle à marcação

1. No **Gerenciador de soluções**, abra o arquivo Start Page *. XAML* .

2. No painel **XAML** , adicione a seguinte declaração de namespace ao elemento de nível superior <xref:System.Windows.Controls.Grid> .

   ```xml
   xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"
   ```

3. No painel **XAML** , role até a \<Grid> seção.

    A seção contém um <xref:System.Windows.Controls.TabControl> elemento em um <xref:System.Windows.Controls.Grid> elemento.

4. Adicione um \<TabControl> elemento que \<TabItem> contém uma referência a seu controle de usuário.

    ```xml

    <TabItem Header="Web" Height="Auto">
        <vsc:UserControl1 />
    </TabItem>

    ```

    Agora você pode testar o controle.

## <a name="test-a-manually-created-custom-start-page"></a>Testar uma página inicial personalizada criada manualmente

1. Copie o arquivo XAML e todos os arquivos de texto de suporte ou arquivos de marcação para a pasta *%USERPROFILE%\My Documentos\visual Studio 2015 \\ \ StartPages* .

2. Se a página inicial fizer referência a qualquer controle ou tipo em assemblies que não são instalados pelo Visual Studio, copie os assemblies e cole-os na _pasta de instalação do Visual Studio_** \\ \Common7\IDE\PrivateAssemblies**.

3. Em um prompt de comando do Visual Studio, digite **devenv/Rootsuffix exp** para abrir uma instância experimental do Visual Studio.

4. Na instância experimental, vá para a **Tools**  >  página de inicialização do ambiente**Opções**de ferramentas  >  **Environment**  >  **Startup** e selecione o arquivo XAML na lista suspensa **Personalizar página inicial** .

5. No menu **Exibir** , clique em **página inicial**.

    Sua página inicial personalizada deve ser exibida. Se você quiser alterar todos os arquivos, deverá fechar a instância experimental, fazer as alterações, copiar e colar os arquivos alterados e, em seguida, abrir novamente a instância experimental para exibir as alterações.

## <a name="see-also"></a>Confira também

- [Controles de contêiner do WPF](https://msdn.microsoft.com/library/a0177167-d7db-4205-9607-8ae316952566)
- [Walkthrough: Adicionar XAML personalizado à página inicial](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)
