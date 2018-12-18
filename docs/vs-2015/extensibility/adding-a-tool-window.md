---
title: Adição de uma janela de ferramentas | Microsoft Docs
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
- tutorials
- tool windows
ms.assetid: 8e16c381-03c8-404e-92ef-3614cdf3150a
caps.latest.revision: 53
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 887466c588bf76c10e3fbf0487eb0da590121ec5
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51784826"
---
# <a name="adding-a-tool-window"></a>Adicionando uma janela de ferramentas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Neste passo a passo, você aprenderá como criar uma janela de ferramenta e integrá-la no Visual Studio das seguintes maneiras:  
  
-   Adicione um controle para a janela da ferramenta.  
  
-   Adicione uma barra de ferramentas para uma janela de ferramentas.  
  
-   Adicione um comando à barra de ferramentas.  
  
-   Implemente os comandos.  
  
-   Defina a posição padrão da janela de ferramentas.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="creating-a-tool-window"></a>Criação de uma janela de ferramentas  
  
1.  Crie um projeto chamado **FirstToolWin** usando o modelo VSIX e adicionar um modelo de item da janela de ferramenta personalizada denominado **FirstToolWindow**.  
  
    > [!NOTE]
    >  Para obter mais informações sobre como criar uma extensão com uma janela de ferramentas, consulte [criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md).  
  
## <a name="add-a-control-to-the-tool-window"></a>Adicionar um controle para a janela da ferramenta  
  
1.  Remova o controle padrão. Abra FirstToolWindowControl.xaml e exclua o **Click Me!** .  
  
2.  No **caixa de ferramentas**, expanda o **todos os controles do WPF** seção e arraste o **elemento de mídia** o controle para o **FirstToolWindowControl** formulário. Selecione o controle e, na **propriedades** janela, nomeie esse elemento **mediaElement1**.  
  
## <a name="add-a-toolbar-to-the-tool-window"></a>Adicionar uma barra de ferramentas para a janela da ferramenta  
 Adicionando uma barra de ferramentas da seguinte maneira, você garante que seus gradientes e cores sejam consistentes com o restante do IDE.  
  
1.  Na **Gerenciador de soluções**, abra FirstToolWindowPackage.vsct. O arquivo. VSCT define os elementos de (GUI) de interface gráfica do usuário em sua janela de ferramentas por meio de XML.  
  
2.  No `<Symbols>` seção, localize o `<GuidSymbol>` nó cujo `name` atributo é `guidFirstToolWindowPackageCmdSet`. Adicione as duas seguintes `<IDSymbol>` elementos à lista de `<IDSymbol>` elementos neste nó para definir uma barra de ferramentas e um grupo de barra de ferramentas.  
  
    ```xml  
    <IDSymbol name="ToolbarID" value="0x1000" />  
    <IDSymbol name="ToolbarGroupID" value="0x1001" />  
    ```  
  
3.  Logo acima de `<Buttons>` seção, crie um `<Menus>` seção que se parece com isso:  
  
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
  
     Há vários tipos diferentes de menu. Esse menu é uma barra de ferramentas em uma janela de ferramenta, definida pela sua `type` atributo. O `guid` e `id` configurações compõem a ID totalmente qualificada da barra de ferramentas. Normalmente, o `<Parent>` de um menu é o grupo que contém. No entanto, uma barra de ferramentas é definida como seu próprio pai. Portanto, o mesmo identificador é usado para o `<Menu>` e `<Parent>` elementos. O `priority` atributo é simplesmente ' 0'.  
  
4.  Barras de ferramentas são semelhantes a menus de várias maneiras. Por exemplo, assim como um menu pode ter grupos de comandos, barras de ferramentas também podem ter grupos. (Em menus, os grupos de comando são separados por linhas horizontais. Na barra de ferramentas, os grupos não são separados por visual divisores.)  
  
     Adicionar um `<Groups>` seção que contém um `<Group>` elemento. Isso define o grupo cujo ID declarados no `<Symbols>` seção. Adicione a `<Groups>` seção logo após o `<Menus>` seção.  
  
    ```xml  
    <Groups>  
       <Group guid="guidFirstToolWindowPackageCmdSet" id="ToolbarGroupID" priority="0x0000">  
           <Parent guid="guidFirstToolWindowPackageCmdSet" id="ToolbarID" />  
       </Group>  
    </Groups>  
    ```  
  
     Ao definir o pai GUID e ID como GUID e ID da barra de ferramentas, você pode adicionar o grupo à barra de ferramentas.  
  
## <a name="add-a-command-to-the-toolbar"></a>Adicionar um comando à barra de ferramentas  
 Adicione um comando à barra de ferramentas, que é exibida como um botão.  
  
1.  No `<Symbols>` seção, declare os seguintes elementos IDSymbol logo após a barra de ferramentas e barra de ferramentas de declarações de grupo.  
  
    ```xml  
    <IDSymbol name="cmdidWindowsMedia" value="0x0100" />  
    <IDSymbol name="cmdidWindowsMediaOpen" value="0x132" />  
    ```  
  
2.  Adicionar um elemento de botão dentro de `<Buttons>` seção. Esse elemento será exibido na barra de ferramentas na janela da ferramenta, com um ícone de pesquisa (Lupa).  
  
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
  
3.  Abra FirstToolWindowCommand.cs e adicione as seguintes linhas na classe logo após os campos existentes.  
  
    ```csharp  
    public const string guidFirstToolWindowPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file  
    public const uint cmdidWindowsMedia =        0x100;   
    public const int cmdidWindowsMediaOpen = 0x132;  
    public const int ToolbarID = 0x1000;  
    ```  
  
     Isso torna os comandos disponíveis no código.  
  
## <a name="add-a-mediaplayer-property-to-firsttoolwindowcontrol"></a>Adicionar uma propriedade de Media Player para FirstToolWindowControl  
 De manipuladores de eventos para os controles de barra de ferramentas, seu código deve ser capaz de acessar o controle Media Player, que é um filho da classe FirstToolWindowControl.  
  
 Na **Gerenciador de soluções**, clique com botão direito FirstToolWindowControl.xaml, clique em **Exibir código**e adicione o seguinte código à classe FirstToolWindowControl.  
  
```csharp  
public System.Windows.Controls.MediaElement MediaPlayer  
{  
    get { return mediaElement1; }  
}  
```  
  
## <a name="instantiate-the-tool-window-and-toolbar"></a>Instanciar a janela de ferramentas e a barra de ferramentas  
 Adicionar uma barra de ferramentas e um comando de menu que invoca a **abrir arquivo** caixa de diálogo e reproduz o arquivo de mídia selecionado.  
  
1.  Abra FirstToolWindow.cs e adicione o seguinte `using` instruções.  
  
    ```csharp  
    using System.ComponentModel.Design;  
    using System.Windows.Forms;  
    using Microsoft.VisualStudio.Shell.Interop;   
    ```  
  
2.  Dentro da classe FirstToolWindow, adicione uma referência pública para o controle FirstToolWindowControl.  
  
    ```csharp  
    public FirstToolWindowControl control;  
    ```  
  
3.  No final do construtor, defina essa variável de controle ao controle recém-criado.  
  
    ```csharp  
    control = new FirstToolWindowControl();   
    base.Content = control;  
    ```  
  
4.  Criar uma instância de barra de ferramentas dentro do construtor.  
  
    ```csharp  
    this.ToolBar = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),   
        FirstToolWindowCommand.ToolbarID);  
    this.ToolBarLocation = (int)VSTWT_LOCATION.VSTWT_TOP;  
    ```  
  
5.  Neste momento, o construtor FirstToolWindow deve ser assim:  
  
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
  
6.  Adicione o comando de menu na barra de ferramentas. Na classe FirstToolWindowCommand.cs, adicione a seguinte instrução using  
  
    ```csharp  
    using System.Windows.Forms;  
    ```  
  
7.  Na classe FirstToolWindowCommand, adicione o seguinte código ao final do método ShowToolWindow(). O comando ButtonHandler será implementado na próxima seção.  
  
    ```csharp  
    // Create the handles for the toolbar command.   
    var mcs = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
    var toolbarbtnCmdID = new CommandID(new Guid(FirstToolWindowCommand.guidFirstToolWindowPackageCmdSet),  
        FirstToolWindowCommand.cmdidWindowsMediaOpen);  
    var menuItem = new MenuCommand(new EventHandler(  
        ButtonHandler), toolbarbtnCmdID);  
    mcs.AddCommand(menuItem);  
    ```  
  
#### <a name="to-implement-a-menu-command-in-the-tool-window"></a>Para implementar um comando de menu na janela da ferramenta  
  
1.  Na classe FirstToolWindowCommand, adicione um método ButtonHandler que chama o **abrir arquivo** caixa de diálogo. Quando um arquivo tiver sido selecionado, ele executa o arquivo de mídia.  
  
2.  Na classe FirstToolWindowCommand, adicione uma referência privada para a janela de FirstToolWindow que é criada no método FindToolWindow().  
  
    ```csharp  
    private FirstToolWindow window;  
    ```  
  
3.  Alterar o método ShowToolWindow() para definir a janela definida acima (de modo que o manipulador de comandos ButtonHandler pode acessar o controle de janela. Aqui está o método ShowToolWindow() completo.  
  
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
  
4.  Adicione o método ButtonHandler. Ele cria uma OpenFileDialog para o usuário especifique o arquivo de mídia para executar, e reproduz o arquivo selecionado.  
  
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
  
## <a name="set-the-default-position-for-the-tool-window"></a>Definir a posição padrão da janela de ferramentas  
 Em seguida, especifique um local padrão no IDE para a janela da ferramenta. Informações de configuração para a janela da ferramenta estão no arquivo FirstToolWindowPackage.cs.  
  
1.  No FirstToolWindowPackage.cs, localize o <xref:Microsoft.VisualStudio.Shell.ProvideToolWindowAttribute> atributo a `FirstToolWindowPackage` classe, que passa o tipo de FirstToolWindow para o construtor. Para especificar uma posição padrão, você deve adicionar mais parâmetros para o construtor no exemplo a seguir.  
  
    ```csharp  
    [ProvideToolWindow(typeof(FirstToolWindow),  
        Style = Microsoft.VisualStudio.Shell.VsDockStyle.Tabbed,  
        Window = "3ae79031-e1bc-11d0-8f78-00a0c9110057")]  
    ```  
  
     É o primeiro parâmetro nomeado `Style` e seu valor é `Tabbed`, que significa que a janela será uma guia em uma janela existente. A posição de encaixe é especificada pelo `Window` parâmetro, n neste caso, o GUID do **Gerenciador de soluções**.  
  
    > [!NOTE]
    >  Para obter mais informações sobre os tipos de janelas no IDE, consulte <xref:EnvDTE.vsWindowType>.  
  
## <a name="testing-the-tool-window"></a>Testando a janela da ferramenta  
  
1.  Pressione F5 para abrir uma nova instância do Visual Studio experimental de compilação.  
  
2.  Sobre o **modo de exibição** , aponte para **Other Windows** e, em seguida, clique em **primeira janela da ferramenta**.  
  
     A janela de ferramentas do player de mídia deve abrir na mesma posição que **Gerenciador de soluções**. Se ele ainda aparece na mesma posição como antes, redefinir o layout de janela (**janela / Redefinir Layout da janela**).  
  
3.  Clique no botão (ele tem o ícone de pesquisa) na janela da ferramenta. Selecione um arquivo com suporte som ou vídeo, por exemplo, C:\windows\media\chimes.wav, em seguida, pressione **aberto**.  
  
     Você deve ouvir o som do alarme.  
  
## <a name="see-also"></a>Consulte também  
 [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)

