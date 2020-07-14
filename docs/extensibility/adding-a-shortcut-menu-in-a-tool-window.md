---
title: Adicionando um menu de atalho em uma janela de ferramentas | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- context menus, adding to tool windows
- menus, context menus
- shortcut menus, adding to tool windows
- tool windows, adding context menus
ms.assetid: 50234537-9e95-4b7e-9cb7-e5cf26d6e9d2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aa8d6f5c47289e66a51653e39d31890f09e8ceb2
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904193"
---
# <a name="add-a-shortcut-menu-in-a-tool-window"></a>Adicionar um menu de atalho em uma janela de ferramentas
Este tutorial coloca um menu de atalho em uma janela de ferramentas. Um menu de atalho é um menu que aparece quando um usuário clica com o botão direito do mouse em um botão, caixa de texto ou plano de fundo da janela. Os comandos em um menu de atalho se comportam da mesma forma que comandos em outros menus ou barras de ferramentas. Para dar suporte a um menu de atalho, especifique-o no arquivo *. vsct* e exiba-o em resposta ao clique com o botão direito do mouse.

Uma janela de ferramentas consiste em um controle de usuário do WPF em uma classe de janela de ferramenta personalizada herdada de <xref:Microsoft.VisualStudio.Shell.ToolWindowPane> .

Este tutorial mostra como criar um menu de atalho como um menu do Visual Studio, declarando itens de menu no arquivo *. vsct* e, em seguida, usando a estrutura de pacote gerenciado para implementá-los na classe que define a janela de ferramentas. Essa abordagem facilita o acesso aos comandos do Visual Studio, aos elementos da interface do usuário e ao modelo de objeto de automação.

Como alternativa, se o menu de atalho não acessar a funcionalidade do Visual Studio, você poderá usar a <xref:System.Windows.FrameworkElement.ContextMenu%2A> propriedade de um elemento XAML no controle de usuário. Para obter mais informações, consulte [ContextMenu](/dotnet/framework/wpf/controls/contextmenu).

## <a name="prerequisites"></a>Pré-requisitos
A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-the-tool-window-shortcut-menu-package"></a>Criar o pacote do menu de atalho da janela de ferramentas

1. Crie um projeto VSIX denominado `TWShortcutMenu` e adicione um modelo de janela de ferramentas chamado **ShortcutMenu** a ele. Para obter mais informações sobre como criar uma janela de ferramentas, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).

## <a name="specifying-the-shortcut-menu"></a>Especificando o menu de atalho
Um menu de atalho como aquele mostrado neste passo a passos permite que o usuário selecione em uma lista de cores que são usadas para preencher o plano de fundo da janela de ferramentas.

1. Em *ShortcutMenuPackage. vsct*, localize no elemento GuidSymbol chamado guidShortcutMenuPackageCmdSet e declare o menu de atalho, o grupo de menus de atalho e as opções de menu. O elemento GuidSymbol agora deve ser assim:

    ```xml
    <GuidSymbol name="guidShortcutMenuPackageCmdSet" value="{00000000-0000-0000-0000-0000}"> // your GUID here
        <IDSymbol name="ShortcutMenuCommandId" value="0x0100" />
        <IDSymbol name="ColorMenu" value="0x1000"/>
        <IDSymbol name="ColorGroup" value="0x1100"/>
        <IDSymbol name="cmdidRed" value="0x102"/>
        <IDSymbol name="cmdidYellow" value="0x103"/>
        <IDSymbol name="cmdidBlue" value="0x104"/>
    </GuidSymbol>
    ```

2. Logo antes do elemento Buttons, crie um elemento menus e, em seguida, defina o menu de atalho nele.

    ```vb
    <Menus>
      <Menu guid="guidShortcutMenuPackageCmdSet" id="ColorMenu" type="Context">
        <Strings>
          <ButtonText>Color change</ButtonText>
          <CommandName>ColorChange</CommandName>
        </Strings>
      </Menu>
    </Menus>
    ```

    Um menu de atalho não tem um pai porque ele não faz parte de um menu ou barra de ferramentas.

3. Crie um elemento groups com um elemento Group que contém os itens de menu de atalho e associe o grupo ao menu de atalho.

    ```xml
    <Groups>
        <Group guid="guidShortcutMenuPackageCmdSet" id="ColorGroup">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorMenu"/>
        </Group>
    </Groups>
    ```

4. No elemento Buttons, defina os comandos individuais que serão exibidos no menu de atalho. O elemento Buttons deve ser assim:

    ```xml
    <Buttons>
        <Button guid="guidShortcutMenuPackageCmdSet" id="ShortcutMenuCommandId" priority="0x0100" type="Button">
            <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>
            <Icon guid="guidImages" id="bmpPic1" />
            <Strings>
                <ButtonText>ShortcutMenu</ButtonText>
            </Strings>
        </Button>

        <Button guid="guidShortcutMenuPackageCmdSet" id="cmdidRed" priority="1" type="Button">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorGroup" />
            <Strings>
                <ButtonText>Red</ButtonText>
            </Strings>
        </Button>

        <Button guid="guidShortcutMenuPackageCmdSet" id="cmdidYellow" priority="3" type="Button">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorGroup" />
            <Strings>
                <ButtonText>Yellow</ButtonText>
            </Strings>
        </Button>

        <Button guid="guidShortcutMenuPackageCmdSet" id="cmdidBlue" priority="5" type="Button">
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorGroup" />
            <Strings>
                <ButtonText>Blue</ButtonText>
            </Strings>
        </Button>
    </Buttons>
    ```

5. No *ShortcutMenuCommand.cs*, adicione as definições para o GUID do conjunto de comandos, o menu de atalho e os itens de menu.

    ```csharp
    public const string guidShortcutMenuPackageCmdSet = "00000000-0000-0000-0000-00000000"; // your GUID will differ
    public const int ColorMenu = 0x1000;
    public const int cmdidRed = 0x102;
    public const int cmdidYellow = 0x103;
    public const int cmdidBlue = 0x104;
    ```

    Essas são as mesmas IDs de comando que são definidas na seção Symbols do arquivo *ShortcutMenuPackage. vsct* . O grupo de contexto não está incluído aqui porque é necessário apenas no arquivo *. vsct* .

## <a name="implementing-the-shortcut-menu"></a>Implementando o menu de atalho
 Esta seção implementa o menu de atalho e seus comandos.

1. No *ShortcutMenu.cs*, a janela de ferramentas pode obter o serviço de comando de menu, mas o controle que ele contém não pode. As etapas a seguir mostram como tornar o serviço de comando de menu disponível para o controle de usuário.

2. No *ShortcutMenu.cs*, adicione as seguintes diretivas using:

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using System.ComponentModel.Design;
    ```

3. Substitua o método Initialize () da janela da ferramenta para obter o serviço de comando de menu e adicione o controle, passando o serviço de comando de menu para o construtor:

    ```csharp
    protected override void Initialize()
    {
        var commandService = (OleMenuCommandService)GetService(typeof(IMenuCommandService));
        Content = new ShortcutMenuControl(commandService);
    }
    ```

4. No construtor da janela de ferramentas ShortcutMenu, remova a linha que adiciona o controle. O Construtor agora deve ser assim:

    ```csharp
    public ShortcutMenu() : base(null)
    {
        this.Caption = "ShortcutMenu";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;
    }
    ```

5. No *ShortcutMenuControl.XAML.cs*, adicione um campo particular para o serviço de comando de menu e altere o construtor de controle para obter o serviço de comando de menu. Em seguida, use o serviço de comando de menu para adicionar os comandos do menu de contexto. O Construtor ShortcutMenuControl agora deve se parecer com o código a seguir. O manipulador de comando será definido mais tarde.

    ```csharp
    public ShortcutMenuControl(OleMenuCommandService service)
    {
        this.InitializeComponent();
        commandService = service;

        if (null !=commandService)
        {
            // Create an alias for the command set guid.
            Guid guid = new Guid(ShortcutMenuCommand.guidShortcutMenuPackageCmdSet);

            // Create the command IDs.
            var red = new CommandID(guid, ShortcutMenuCommand.cmdidRed);
            var yellow = new CommandID(guid, ShortcutMenuCommand.cmdidYellow);
            var blue = new CommandID(guid, ShortcutMenuCommand.cmdidBlue);

            // Add a command for each command ID.
            commandService.AddCommand(new MenuCommand(ChangeColor, red));
            commandService.AddCommand(new MenuCommand(ChangeColor, yellow));
            commandService.AddCommand(new MenuCommand(ChangeColor, blue));
        }
    }
    ```

6. Em *ShortcutMenuControl. XAML*, adicione um <xref:System.Windows.UIElement.MouseRightButtonDown> evento ao elemento de nível superior <xref:System.Windows.Controls.UserControl> . O arquivo XAML agora deve ser assim:

    ```vb
    <UserControl x:Class="TWShortcutMenu.ShortcutMenuControl"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
            Background="{DynamicResource VsBrush.Window}"
            Foreground="{DynamicResource VsBrush.WindowText}"
            mc:Ignorable="d"
            d:DesignHeight="300" d:DesignWidth="300"
            Name="MyToolWindow"
            MouseRightButtonDown="MyToolWindow_MouseRightButtonDown">
        <Grid>
            <StackPanel Orientation="Vertical">
                <TextBlock Margin="10" HorizontalAlignment="Center">ShortcutMenu</TextBlock>
            </StackPanel>
        </Grid>
    </UserControl>
    ```

7. No *ShortcutMenuControl.XAML.cs*, adicione um stub para o manipulador de eventos.

    ```csharp
    private void MyToolWindow_MouseRightButtonDown(object sender, MouseButtonEventArgs e)
    {
    . . .
    }
    ```

8. Adicione as seguintes diretivas using ao mesmo arquivo:

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using System.ComponentModel.Design;
    using System;
    using System.Windows.Input;
    using System.Windows.Media;
    ```

9. Implemente o `MyToolWindowMouseRightButtonDown` evento da seguinte maneira.

    ```csharp
    private void MyToolWindow_MouseRightButtonDown(object sender, MouseButtonEventArgs e)
    {
        if (null != commandService)
        {
            CommandID menuID = new CommandID(
                new Guid(ShortcutMenuCommand.guidShortcutMenuPackageCmdSet),
                ShortcutMenuCommand.ColorMenu);
            Point p = this.PointToScreen(e.GetPosition(this));
            commandService.ShowContextMenu(menuID, (int)p.X, (int)p.Y);
        }
    }
    ```

    Isso cria um <xref:System.ComponentModel.Design.CommandID> objeto para o menu de atalho, identifica o local do clique do mouse e abre o menu de atalho nesse local usando o <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService.ShowContextMenu%2A> método.

10. Implemente o manipulador de comandos.

    ```csharp
    private void ChangeColor(object sender, EventArgs e)
    {
        var mc = sender as MenuCommand;

        switch (mc.CommandID.ID)
        {
            case ShortcutMenuCommand.cmdidRed:
                MyToolWindow.Background = Brushes.Red;
                break;
            case ShortcutMenuCommand.cmdidYellow:
                MyToolWindow.Background = Brushes.Yellow;
                break;
            case ShortcutMenuCommand.cmdidBlue:
                MyToolWindow.Background = Brushes.Blue;
                break;
        }
    }
    ```

    Nesse caso, apenas um método manipula eventos para todos os itens de menu identificando o <xref:System.ComponentModel.Design.CommandID> e definindo a cor do plano de fundo de acordo. Se os itens de menu contivessem comandos não relacionados, você teria criado um manipulador de eventos separado para cada comando.

## <a name="test-the-tool-window-features"></a>Testar os recursos da janela de ferramentas

1. Compile o projeto e comece a depuração. A instância experimental é exibida.

2. Na instância experimental, clique em **Exibir/outras janelas**e, em seguida, clique em **ShortcutMenu**. Fazer isso deve exibir a janela da ferramenta.

3. Clique com o botão direito do mouse no corpo da janela de ferramentas. Um menu de atalho que tem uma lista de cores deve ser exibido.

4. Clique em uma cor no menu de atalho. A cor do plano de fundo da janela de ferramentas deve ser alterada para a cor selecionada.

## <a name="see-also"></a>Confira também
- [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)
- [Usando e fornecendo serviços](../extensibility/using-and-providing-services.md)
