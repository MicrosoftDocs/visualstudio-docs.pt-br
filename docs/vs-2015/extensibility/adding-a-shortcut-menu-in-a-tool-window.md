---
title: Adicionar um Menu de atalho em uma janela de ferramentas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- context menus, adding to tool windows
- menus, context menus
- shortcut menus, adding to tool windows
- tool windows, adding context menus
ms.assetid: 50234537-9e95-4b7e-9cb7-e5cf26d6e9d2
caps.latest.revision: 38
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 179a103475a47be95cbf45f88640b8a635a7ff34
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51796214"
---
# <a name="adding-a-shortcut-menu-in-a-tool-window"></a>Adicionando um menu de atalho a uma janela de ferramentas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo coloca um menu de atalho em uma janela de ferramentas. Um menu de atalho é um menu que aparece quando um usuário clica um botão, a caixa de texto ou o plano de fundo da janela. Comandos em um menu de atalho se comportam da mesma maneira como os comandos em outros menus ou barras de ferramentas. Para dar suporte a um menu de atalho, especifique-o no arquivo. VSCT e exibi-la na resposta para o botão direito do mouse.  
  
 Uma janela de ferramentas consiste em um controle de usuário do WPF em uma classe de janela de ferramenta personalizada que herda de <xref:Microsoft.VisualStudio.Shell.ToolWindowPane>.  
  
 Este passo a passo mostra como criar um menu de atalho como um menu do Visual Studio, declarando a itens de menu no arquivo. VSCT, e, em seguida, usando a estrutura de pacote gerenciado para implementá-los na classe que define a janela da ferramenta. Essa abordagem facilita o acesso a comandos do Visual Studio, elementos de interface do usuário e o modelo de objeto de automação.  
  
 Como alternativa, se seu menu de atalho não for acessar a funcionalidade do Visual Studio, você pode usar o <xref:System.Windows.FrameworkElement.ContextMenu%2A> propriedade de um elemento XAML no controle de usuário. Para obter mais informações, consulte [ContextMenu](http://msdn.microsoft.com/library/2f40b2bb-b702-4706-9fc4-10bcfd7cc35d).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="creating-the-tool-window-shortcut-menu-package"></a>Criando o pacote de Menu de atalho de janela de ferramenta  
  
1.  Crie um projeto do VSIX chamado `TWShortcutMenu` e adicione um modelo de janela de ferramenta denominado **MenuDeAtalho** a ele. Para obter mais informações sobre como criar uma janela de ferramentas, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).  
  
## <a name="specifying-the-shortcut-menu"></a>Especificando o Menu de atalho  
 Um menu de atalho, como mostrado neste passo a passo permite que o usuário selecionar em uma lista de cores que são usados para preencher a tela de fundo da janela de ferramentas.  
  
1.  No ShortcutMenuPackage.vsct, localize no elemento GuidSymbol chamado guidShortcutMenuPackageCmdSet e declare o menu de atalho, grupo de menus de atalho e opções de menu. O elemento GuidSymbol agora deve ser assim:  
  
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
  
2.  Logo antes do elemento de botões, crie um elemento de Menus e, em seguida, defina o menu de atalho nele.  
  
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
  
     Um menu de atalho não tem um pai porque ele não é parte de um menu ou barra de ferramentas.  
  
3.  Criar um elemento de grupos com um elemento de grupo que contém os itens de menu de atalho e associe o grupo de menu de atalho.  
  
    ```xml  
    <Groups>  
        <Group guid="guidShortcutMenuPackageCmdSet" id="ColorGroup">  
            <Parent guid="guidShortcutMenuPackageCmdSet" id="ColorMenu"/>  
        </Group>  
    </Groups>  
    ```  
  
4.  O elemento de botões, define os comandos individuais que serão exibido no menu de atalho. O elemento de botões deve ter esta aparência:  
  
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
  
5.  No ShortcutMenuPackageGuids.cs, adicione que as definições para o comando definir GUID, o menu de atalho e os itens de menu.  
  
    ```csharp  
    public const string guidShortcutMenuPackageCmdSet = "00000000-0000-0000-0000-00000000"; // your GUID will differ  
    public const int ColorMenu = 0x1000;  
    public const int cmdidRed = 0x102;  
    public const int cmdidYellow = 0x103;  
    public const int cmdidBlue = 0x104;  
    ```  
  
     Essas são as mesmas IDs de comando que são definidas na seção símbolos do arquivo ShortcutMenuPackage.vsct. O grupo de contexto não é incluído aqui porque ela é necessária apenas no arquivo. VSCT.  
  
## <a name="implementing-the-shortcut-menu"></a>Implementando o Menu de atalho  
 Esta seção implementa o menu de atalho e seus comandos.  
  
1.  Em ShortcutMenu.cs, a janela da ferramenta pode obter o serviço de comando de menu, mas não é o controle que ele contém. As etapas a seguir mostram como disponibilizar o serviço de comando de menu para o controle de usuário.  
  
2.  No ShortcutMenu.cs, adicione as seguintes instruções using:  
  
    ```csharp  
    using Microsoft.VisualStudio.Shell;  
    using System.ComponentModel.Design;  
    ```  
  
3.  Substitua método de Initialize () da janela de ferramentas para obter o serviço de comando de menu e adicionar o controle, passando o serviço de comando de menu para o construtor:  
  
    ```csharp  
    protected override void Initialize()  
    {  
        commandService = (OleMenuCommandService)GetService(typeof(IMenuCommandService));  
        Content = new ShortcutMenuControl(commandService);  
    }  
    ```  
  
4.  No construtor de janela de ferramenta MenuDeAtalho, remova a linha que adiciona o controle. Agora, o construtor deve ser assim:  
  
    ```csharp  
    public ShortcutMenu() : base(null)  
    {  
        this.Caption = "ShortcutMenu";  
        this.BitmapResourceID = 301;  
        this.BitmapIndex = 1;  
    }  
    ```  
  
5.  No ShortcutMenuControl.xaml.cs, adicione um campo particular para o serviço de comando de menu e altere o construtor de controle para aproveitar o serviço de comando de menu. Em seguida, use o serviço de comando de menu para adicionar os comandos de menu de contexto. O construtor ShortcutMenuControl agora deve parecer com o código a seguir. O manipulador de comandos será definido posteriormente.  
  
    ```csharp  
    public ShortcutMenuControl(OleMenuCommandService service)  
    {  
        this.InitializeComponent();  
        commandService = service;  
  
        if (null !=commandService)  
        {  
            // Create an alias for the command set guid.  
            Guid guid = new Guid(ShortcutMenuPackageGuids.guidShortcutMenuPackageCmdSet);  
  
            // Create the command IDs.   
            var red = new CommandID(guid, ShortcutMenuPackageGuids.cmdidRed);  
            var yellow = new CommandID(guid, ShortcutMenuPackageGuids.cmdidYellow);  
            var blue = new CommandID(guid, ShortcutMenuPackageGuids.cmdidBlue);  
  
            // Add a command for each command ID.  
            commandService.AddCommand(new MenuCommand(ChangeColor, red));  
            commandService.AddCommand(new MenuCommand(ChangeColor, yellow));  
            commandService.AddCommand(new MenuCommand(ChangeColor, blue));  
        }  
    }  
    ```  
  
6.  No ShortcutMenuControl.xaml, adicione uma <xref:System.Windows.UIElement.MouseRightButtonDown> eventos para o nível superior <xref:System.Windows.Controls.UserControl> elemento. O arquivo XAML agora deve ser assim:  
  
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
  
7.  ShortcutMenuControl.xaml.cs, adiciona um stub para o manipulador de eventos.  
  
    ```csharp  
    private void MyToolWindow_MouseRightButtonDown(object sender, MouseButtonEventArgs e)  
    {  
    . . .  
    }  
    ```  
  
8.  Adicione o seguinte usando instruções para o mesmo arquivo:  
  
    ```csharp  
    using Microsoft.VisualStudio.Shell;  
    using System.ComponentModel.Design;  
    using System;  
    using System.Windows.Input;  
    using System.Windows.Media;  
    ```  
  
9. Implementar o `MyToolWindowMouseRightButtonDown` evento da seguinte maneira.  
  
    ```csharp  
    private void MyToolWindow_MouseRightButtonDown(object sender, MouseButtonEventArgs e)  
    {  
        if (null != commandService)  
        {  
            CommandID menuID = new CommandID(  
                new Guid(ShortcutMenuPackageGuids.guidShortcutMenuPackageCmdSet),  
                ShortcutMenuPackageGuids.ColorMenu);  
            Point p = this.PointToScreen(e.GetPosition(this));  
            commandService.ShowContextMenu(menuID, (int)p.X, (int)p.Y);  
        }  
    }  
    ```  
  
     Isso cria uma <xref:System.ComponentModel.Design.CommandID> objeto para o menu de atalho, identifica o local do clique do mouse e abre o menu de atalho no local usando o <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService.ShowContextMenu%2A> método.  
  
10. Implemente o manipulador de comandos.  
  
    ```csharp  
    private void ChangeColor(object sender, EventArgs e)  
    {  
        var mc = sender as MenuCommand;  
  
        switch (mc.CommandID.ID)  
        {  
            case ShortcutMenuPackageGuids.cmdidRed:  
                MyToolWindow.Background = Brushes.Red;  
                break;  
            case ShortcutMenuPackageGuids.cmdidYellow:  
                MyToolWindow.Background = Brushes.Yellow;  
                break;  
            case ShortcutMenuPackageGuids.cmdidBlue:  
                MyToolWindow.Background = Brushes.Blue;  
                break;  
        }  
    }  
    ```  
  
     Nesse caso, apenas um método trata os eventos para todos os itens de menu, identificando o <xref:System.ComponentModel.Design.CommandID> e definindo a cor do plano de fundo adequadamente. Se os itens de menu continha comandos relacionadas, você teria criado um manipulador de eventos separado para cada comando.  
  
## <a name="testing-the-tool-window-features"></a>Testar os recursos da janela de ferramenta  
  
1.  Compile o projeto e comece a depuração. A instância experimental é exibida.  
  
2.  Na instância experimental, clique em **exibição / Windows outras**e, em seguida, clique em **MenuDeAtalho**. Isso deve exibir a janela de ferramenta.  
  
3.  Clique com botão direito no corpo da janela de ferramenta. Deve ser exibido um menu de atalho que tem uma lista de cores.  
  
4.  Clique em uma cor no menu de atalho. A cor de plano de fundo da janela de ferramenta deverá ser alterada para a cor selecionada.  
  
## <a name="see-also"></a>Consulte também  
 [Comandos, Menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)   
 [Usar e fornecer serviços](../extensibility/using-and-providing-services.md)

