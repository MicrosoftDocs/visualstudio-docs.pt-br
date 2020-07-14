---
title: Adicionando uma janela de ferramentas | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tutorials
- tool windows
ms.assetid: 8e16c381-03c8-404e-92ef-3614cdf3150a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 169f386128ccdd79aef6b90a6703f50323b9b6f3
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904144"
---
# <a name="add-a-tool-window"></a>Adicionar uma janela de ferramentas

Neste tutorial, você aprenderá a criar uma janela de ferramentas e a integrá-la ao Visual Studio das seguintes maneiras:

- Adicione um controle à janela de ferramentas.

- Adicione uma barra de ferramentas a uma janela de ferramentas.

- Adicione um comando à barra de ferramentas.

- Implemente os comandos.

- Defina a posição padrão para a janela de ferramentas.

## <a name="prerequisites"></a>Pré-requisitos

O SDK do Visual Studio está incluído como um recurso opcional na instalação do Visual Studio. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-tool-window"></a>Criar uma janela de ferramentas

1. Crie um projeto chamado **FirstToolWin** usando o modelo VSIX e adicione um modelo de item de janela de ferramenta personalizada chamado **FirstToolWindow**.

    > [!NOTE]
    > Para obter mais informações sobre como criar uma extensão com uma janela de ferramentas, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).

## <a name="add-a-control-to-the-tool-window"></a>Adicionar um controle à janela de ferramentas

1. Remova o controle padrão. Abra *FirstToolWindowControl. XAML* e exclua o **clique em mim!** .

2. Na **caixa de ferramentas**, expanda a seção **todos os controles WPF** e arraste o controle **elemento de mídia** para o formulário **FirstToolWindowControl** . Selecione o controle e, na janela **Propriedades** , nomeie esse elemento **mediaElement1**.

## <a name="add-a-toolbar-to-the-tool-window"></a>Adicionar uma barra de ferramentas à janela de ferramentas
Ao adicionar uma barra de ferramentas da maneira a seguir, você garante que seus gradientes e cores sejam consistentes com o restante do IDE.

1. Em **Gerenciador de soluções**, abra *FirstToolWindowPackage. vsct*. O arquivo *. vsct* define os elementos da GUI (interface gráfica do usuário) em sua janela de ferramentas usando XML.

2. Na `<Symbols>` seção, localize o `<GuidSymbol>` nó cujo `name` atributo é `guidFirstToolWindowPackageCmdSet` . Adicione os dois elementos a seguir `<IDSymbol>` à lista de `<IDSymbol>` elementos neste nó para definir uma barra de ferramentas e um grupo de barras de ferramentas.

    ```xml
    <IDSymbol name="ToolbarID" value="0x1000" />
    <IDSymbol name="ToolbarGroupID" value="0x1001" />
    ```

3. Logo acima da `<Buttons>` seção, crie uma `<Menus>` seção semelhante a esta:

    ```xml
    <Menus>
        <Menu guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" priority="0x0000" type="ToolWindowToolbar">
            <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" />
            <Strings>
                <ButtonText>Tool Window Toolbar</ButtonText>
                <CommandName>Tool Window Toolbar</CommandName>
            </Strings>
        </Menu>
    </Menus>
    ```

    Há vários tipos diferentes de menu. Esse menu é uma barra de ferramentas em uma janela de ferramentas, definida por seu `type` atributo. As `guid` `id` configurações e compõem a ID totalmente qualificada da barra de ferramentas. Normalmente, o `<Parent>` de um menu é o grupo recipiente. No entanto, uma barra de ferramentas é definida como seu próprio pai. Portanto, o mesmo identificador é usado para os `<Menu>` `<Parent>` elementos e. O `priority` atributo é apenas ' 0 '.

4. As barras de ferramentas são semelhantes aos menus de várias maneiras. Por exemplo, assim como um menu pode ter grupos de comandos, as barras de ferramentas também podem ter grupos. (Em menus, os grupos de comandos são separados por linhas horizontais. Nas barras de ferramentas, os grupos não são separados por divisores visuais.)

    Adicione uma `<Groups>` seção que contém um `<Group>` elemento. Isso define o grupo cuja ID você declarou na `<Symbols>` seção. Adicione a `<Groups>` seção logo após a `<Menus>` seção.

    ```xml
    <Groups>
        <Group guid="guidFirstToolWindowPackageCmdSet" id="ToolbarGroupID" priority="0x0000">
            <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" />
        </Group>
    </Groups>
    ```

    Ao definir o GUID pai e a ID como o GUID e a ID da barra de ferramentas, você adiciona o grupo à barra de ferramentas.

## <a name="add-a-command-to-the-toolbar"></a>Adicionar um comando à barra de ferramentas

Adicione um comando à barra de ferramentas, que é exibido como um botão.

1. Na `<Symbols>` seção, declare os elementos IDSymbol a seguir logo após a barra de ferramentas e as declarações de grupo da barra de ferramentas.

    ```xml
    <IDSymbol name="cmdidWindowsMedia" value="0x0100" />
    <IDSymbol name="cmdidWindowsMediaOpen" value="0x132" />
    ```

2. Adicione um elemento Button dentro da `<Buttons>` seção. Esse elemento aparecerá na barra de ferramentas na janela de ferramentas, com um ícone de **pesquisa** (lupa).

    ```xml
    <Button guid="guidFirstToolWindowPackageCmdSet" id="cmdidWindowsMediaOpen" priority="0x0101" type="Button">
        <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarGroupID"/>
        <Icon guid="guidImages" id="bmpPicSearch" />
        <Strings>
            <CommandName>cmdidWindowsMediaOpen</CommandName>
            <ButtonText>Load File</ButtonText>
        </Strings>
    </Button>
    ```

3. Abra *FirstToolWindowCommand.cs* e adicione as linhas a seguir na classe logo após os campos existentes.

    ```csharp
    public const string guidFirstToolWindowPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file
    public const uint cmdidWindowsMedia = 0x100;
    public const int cmdidWindowsMediaOpen = 0x132;
    public const int ToolbarID = 0x1000;
    ```

    Isso torna os comandos disponíveis no código.

## <a name="add-a-mediaplayer-property-to-firsttoolwindowcontrol"></a>Adicionar uma Propriedade MediaPlayer a FirstToolWindowControl
Dos manipuladores de eventos para os controles da barra de ferramentas, seu código deve ser capaz de acessar o controle do Media Player, que é um filho da classe FirstToolWindowControl.

Em **Gerenciador de soluções**, clique com o botão direito do mouse em *FirstToolWindowControl. XAML*, clique em **Exibir código**e adicione o código a seguir à classe FirstToolWindowControl.

```csharp
public System.Windows.Controls.MediaElement MediaPlayer
{
    get { return mediaElement1; }
}
```

## <a name="instantiate-the-tool-window-and-toolbar"></a>Criar uma instância da janela de ferramentas e da barra de ferramentas
Adicione uma barra de ferramentas e um comando de menu que invoque a caixa de diálogo **Abrir arquivo** e reproduza o arquivo de mídia selecionado.

1. Abra *FirstToolWindow.cs* e adicione as seguintes `using` diretivas:

    ```csharp
    using System.ComponentModel.Design;
    using System.Windows.Forms;
    using Microsoft.VisualStudio.Shell.Interop;
    ```

2. Dentro da classe FirstToolWindow, adicione uma referência pública ao controle FirstToolWindowControl.

    ```csharp
    public FirstToolWindowControl control;
    ```

3. No final do Construtor, defina essa variável de controle para o controle recém-criado.

    ```csharp
    control = new FirstToolWindowControl();
    base.Content = control;
    ```

4. Crie uma instância da barra de ferramentas dentro do construtor.

    ```csharp
    this.ToolBar = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),
        FirstToolWindowCommand.ToolbarID);
    this.ToolBarLocation = (int)VSTWT_LOCATION.VSTWT_TOP;
    ```

5. Neste ponto, o Construtor FirstToolWindow deve ser assim:

    ```csharp
    public FirstToolWindow() : base(null)
    {
        this.Caption = "FirstToolWindow";
        this.BitmapResourceID = 301;
        this.BitmapIndex = 1;
        control = new FirstToolWindowControl();
        base.Content = control;
        this.ToolBar = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),
            FirstToolWindowCommand.ToolbarID);
            this.ToolBarLocation = (int)VSTWT_LOCATION.VSTWT_TOP;
    }
    ```

6. Adicione o comando de menu à barra de ferramentas. Na classe FirstToolWindowCommand.cs, adicione o seguinte usando a diretiva:

    ```csharp
    using System.Windows.Forms;
    ```

7. Na classe FirstToolWindowCommand, adicione o código a seguir ao final do método ShowToolWindow (). O comando ButtonHandler será implementado na próxima seção.

    ```csharp
    // Create the handles for the toolbar command.
    var mcs = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
    var toolbarbtnCmdID = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),
        FirstToolWindowCommand.cmdidWindowsMediaOpen);
    var menuItem = new MenuCommand(new EventHandler(
        ButtonHandler), toolbarbtnCmdID);
    mcs.AddCommand(menuItem);
    ```

### <a name="to-implement-a-menu-command-in-the-tool-window"></a>Para implementar um comando de menu na janela de ferramentas

1. Na classe FirstToolWindowCommand, adicione um método ButtonHandler que invoque a caixa de diálogo **Abrir arquivo** . Quando um arquivo tiver sido selecionado, ele reproduzirá o arquivo de mídia.

2. Na classe FirstToolWindowCommand, adicione uma referência privada à janela FirstToolWindow que é criada no método FindToolWindow ().

    ```csharp
    private FirstToolWindow window;
    ```

3. Altere o método ShowToolWindow () para definir a janela que você definiu acima (para que o manipulador de comandos ButtonHandler possa acessar o controle de janela. Aqui está o método ShowToolWindow () completo.

    ```csharp
    private void ShowToolWindow(object sender, EventArgs e)
    {
        window = (FirstToolWindow) this.package.FindToolWindow(typeof(FirstToolWindow), 0, true);
        if ((null == window) || (null == window.Frame))
        {
            throw new NotSupportedException("Cannot create tool window");
        }

        IVsWindowFrame windowFrame = (IVsWindowFrame)window.Frame;
        Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(windowFrame.Show());

        var mcs = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        var toolbarbtnCmdID = new CommandID(new Guid(FirstToolWindowCommandguidFirstToolWindowPackageCmdSet),
            FirstToolWindowCommand.cmdidWindowsMediaOpen);
        var menuItem = new MenuCommand(new EventHandler(
            ButtonHandler), toolbarbtnCmdID);
        mcs.AddCommand(menuItem);
    }
    ```

4. Adicione o método ButtonHandler. Ele cria um OpenFileDialog para que o usuário especifique o arquivo de mídia a ser reproduzido e, em seguida, reproduz o arquivo selecionado.

    ```csharp
    private void ButtonHandler(object sender, EventArgs arguments)
    {
        OpenFileDialog openFileDialog = new OpenFileDialog();
        DialogResult result = openFileDialog.ShowDialog();
        if (result == DialogResult.OK)
        {
            window.control.MediaPlayer.Source = new System.Uri(openFileDialog.FileName);
        }
    }
    ```

## <a name="set-the-default-position-for-the-tool-window"></a>Definir a posição padrão para a janela de ferramentas

Em seguida, especifique um local padrão no IDE para a janela de ferramentas. As informações de configuração para a janela de ferramentas estão no arquivo *FirstToolWindowPackage.cs* .

1. No *FirstToolWindowPackage.cs*, localize o <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> atributo na `FirstToolWindowPackage` classe, que passa o tipo FirstToolWindow para o construtor. Para especificar uma posição padrão, você deve adicionar mais parâmetros ao Construtor após o exemplo.

    ```csharp
    [ProvideToolWindow(typeof(FirstToolWindow),
        Style = Microsoft.VisualStudio.Shell.VsDockStyle.Tabbed,
        Window = "3ae79031-e1bc-11d0-8f78-00a0c9110057")]
    ```

    O primeiro parâmetro nomeado é `Style` e seu valor é `Tabbed` , o que significa que a janela será uma guia em uma janela existente. A posição de encaixe é especificada pelo `Window` parâmetro, n esse caso, o GUID do **Gerenciador de soluções**.

    > [!NOTE]
    > Para obter mais informações sobre os tipos de janelas no IDE, consulte <xref:EnvDTE.vsWindowType> .

## <a name="test-the-tool-window"></a>Testar a janela de ferramentas

1. Pressione **F5** para abrir uma nova instância da compilação experimental do Visual Studio.

2. No menu **Exibir** , aponte para **outras janelas** e clique em **primeira janela de ferramenta**.

    A janela de ferramentas do player de mídia deve ser aberta na mesma posição que **Gerenciador de soluções**. Se ele ainda aparecer na mesma posição que antes, redefina o layout da janela (**janela/redefinir layout da janela**).

3. Clique no botão (ele tem o ícone de **pesquisa** ) na janela de ferramentas. Selecione um arquivo de som ou vídeo com suporte, por exemplo, *C:\Windows\Media\chimes.wav*, em seguida, pressione **abrir**.

    Você deve ouvir o som alarme.

## <a name="see-also"></a>Confira também
- [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)
