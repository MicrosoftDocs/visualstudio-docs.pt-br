---
title: Criando um Windows Forms o controle de caixa de ferramentas | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- winforms
- toolbox
- windows forms
ms.assetid: 0be6ffc1-8afd-4d02-9a5d-e27dde05fde6
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a44dfd224324ba641e70e0cfe6ded87f88fe6765
ms.sourcegitcommit: 8cdc6e2ad2341f34bd6b02859a7c975daa0c9320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53307695"
---
# <a name="create-a-windows-forms-toolbox-control"></a>Criar um controle de caixa de ferramentas do Windows Forms
O modelo de item de controle de caixa de ferramentas do Windows Forms que está incluído no Visual Studio Extensibility Tools (SDK do VS) permite que você crie um controle que é adicionado automaticamente para o **caixa de ferramentas** quando a extensão está instalada. Este tópico mostra como usar o modelo para criar um controle de um contador simples que você pode distribuir a outros usuários.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="create-a-windows-forms-toolbox-control"></a>Criar um controle de caixa de ferramentas do Windows Forms  
 O modelo de controle de caixa de ferramentas do Windows Forms cria um controle de usuário indefinido e fornece toda a funcionalidade que é necessário para adicionar o controle para o **caixa de ferramentas**.  
  
### <a name="create-an-extension-with-a-windows-forms-toolbox-control"></a>Criar uma extensão com um controle de caixa de ferramentas do Windows Forms  
  
1.  Crie um projeto do VSIX chamado `MyWinFormsControl`. Você pode encontrar o modelo de projeto VSIX na **novo projeto** diálogo sob **Visual c#** > **extensibilidade**.  
  
2.  Quando o projeto aberto, adicione uma **controle de caixa de ferramentas do Windows Forms** modelo de item chamado `Counter`. No **Gerenciador de soluções**, clique com botão direito no nó do projeto e selecione **Add** > **Novo Item**. No **Adicionar Novo Item** caixa de diálogo, vá para **Visual c#** > **extensibilidade** e selecione **controle de caixa de ferramentas do Windows Forms**  
  
3.  Isso adiciona um controle de usuário, uma `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> para posicionar o controle na **caixa de ferramentas**e um **Microsoft.VisualStudio.ToolboxControl** entrada de ativo no manifesto do VSIX para implantação.  
  
### <a name="build-a-user-interface-for-the-control"></a>Criar uma interface do usuário para o controle  
 O `Counter` controle requer dois controles filho: uma <xref:System.Windows.Forms.Label> para exibir a contagem atual e um <xref:System.Windows.Forms.Button> para redefinir a contagem como 0. Nenhum outro controle filho é necessário porque chamadores incrementará o contador de forma programática.  
  
#### <a name="to-build-the-user-interface"></a>Para criar a interface do usuário  
  
1.  Na **Gerenciador de soluções**, clique duas vezes em *Counter.cs* para abri-lo no designer.  
  
2.  Remover o **clique aqui!** botão que está incluído por padrão quando você adiciona o modelo de item de controle de caixa de ferramentas do Windows Forms.  
  
3.  Dos **caixa de ferramentas**, arraste um `Label` controle e, em seguida, um `Button` controle abaixo dele para a superfície de design.  
  
4.  Redimensionar o controle de usuário geral para 150, 50 pixels e redimensionar o botão de controle como 50, 20 pixels.  
  
5.  No **propriedades** janela, defina os seguintes valores para os controles na superfície de design.  
  
    |Controle|Propriedade|Valor|  
    |-------------|--------------|-----------|  
    |`Label1`|**Texto**|""|  
    |`Button1`|**Nome**|btnReset|  
    |`Button1`|**Texto**|Redefinir|  
  
### <a name="code-the-user-control"></a>Código de controle de usuário  
 O `Counter` controle irá expor um método para incrementar o contador, um evento a ser acionado sempre que o contador é incrementado, uma **redefinir** botão e três propriedades para armazenar a contagem atual, o texto de exibição e se deseja mostrar ou ocultar a **redefinir** botão. O `ProvideToolboxControl` atributo determina onde em de **caixa de ferramentas** o `Counter` controle será exibido.  
  
#### <a name="to-code-the-user-control"></a>Codificar o controle de usuário  
  
1.  Clique duas vezes no formulário para abrir seu manipulador de eventos de carga na janela de código.  
  
2.  Acima do método de manipulador de eventos na classe de controle, crie um número inteiro para armazenar o valor do contador e uma cadeia de caracteres para armazenar o texto de exibição, conforme mostrado no exemplo a seguir.  
  
    ```csharp  
    int currentValue;  
    string displayText;  
    ```  
  
3.  Crie as seguintes declarações de propriedade pública.  
  
    ```csharp  
    public int Value {  
        get { return currentValue; }   
    }  
  
    public string Message {  
        get { return displayText; }  
        set { displayText = value; }  
    }  
  
    public bool ShowReset {  
        get { return btnReset.Visible; }  
        set { btnReset.Visible = value; }  
    }  
  
    ```  
  
     Os chamadores podem acessar essas propriedades para obter e definir o texto de exibição do contador para mostrar ou ocultar a **redefinir** botão. Os chamadores podem obter o valor atual de somente leitura `Value` propriedade, mas eles não é possível definir o valor diretamente.  
  
4.  Coloque o seguinte código no `Load` evento para o controle.  
  
    ```csharp  
    private void Counter_Load(object sender, EventArgs e)  
    {  
        currentValue = 0;  
        label1.Text = Message + Value;  
    }  
  
    ```  
  
     Definindo o **etiqueta** texto no <xref:System.Windows.Forms.UserControl.Load> evento permite que as propriedades de destino carregar antes que seus valores sejam aplicados. Definindo o **etiqueta** texto no construtor pode resultar em um vazio **rótulo**.  
  
5.  Crie o seguinte método público para incrementar o contador.  
  
    ```csharp  
    public void Increment()  
    {  
        currentValue++;  
        label1.Text = displayText + Value;  
        Incremented(this, EventArgs.Empty);  
    }  
  
    ```  
  
6.  Adicionar uma declaração para o `Incremented` eventos à classe do controle.  
  
    ```csharp  
    public event EventHandler Incremented;  
    ```  
  
     Os chamadores podem adicionar manipuladores para este evento responda às alterações no valor do contador.  
  
7.  Retornar ao modo de design e clique duas vezes o **redefina** botão para gerar o `btnReset_Click` manipulador de eventos e, em seguida, preenchê-lo conforme mostrado no exemplo a seguir.  
  
    ```csharp  
    private void btnReset_Click(object sender, EventArgs e)  
    {  
        currentValue = 0;  
        label1.Text = displayText + Value;  
    }  
  
    ```  
  
8.  Imediatamente acima da definição de classe, na `ProvideToolboxControl` declaração de atributo, altere o valor do primeiro parâmetro da `"MyWinFormsControl.Counter"` para `"General"`. Isso define o nome do grupo de itens que hospedará o controle na **caixa de ferramentas**.  
  
     A exemplo a seguir mostra o `ProvideToolboxControl` atributo e a definição de classe ajustado.  
  
    ```csharp  
    [ProvideToolboxControl("General", false)]  
    public partial class Counter : UserControl  
    ```  
  
### <a name="test-the-control"></a>Testar o controle  
 Para testar uma **caixa de ferramentas** controlar, primeiro testá-lo no ambiente de desenvolvimento e, em seguida, testá-lo em um aplicativo compilado.  
  
#### <a name="to-test-the-control"></a>Para testar o controle  
  
1.  Pressione **F5**.  
  
     Isso compila o projeto e abre uma segunda instância Experimental do Visual Studio que tem o controle instalado.  
  
2.  Na instância Experimental do Visual Studio, crie uma **aplicativo do Windows Forms** projeto.  
  
3.  Na **Gerenciador de soluções**, clique duas vezes em *Form1.cs* para abri-lo no designer, se ele não ainda estiver aberto.  
  
4.  No **caixa de ferramentas**, o `Counter` controle deve ser exibido no **geral** seção.  
  
5.  Arraste um `Counter` controle ao seu formulário e, em seguida, selecioná-lo. O `Value`, `Message`, e `ShowReset` propriedades serão exibidas no **as propriedades** janela, junto com as propriedades que são herdadas de <xref:System.Windows.Forms.UserControl>.  
  
6.  Defina a propriedade `Message` como `Count:`.  
  
7.  Arraste uma <xref:System.Windows.Forms.Button> o controle para o formulário e, em seguida, defina as propriedades de nome e o texto do botão para `Test`.  
  
8.  Clique duas vezes no botão para abrir *Form1.cs* na exibição de código e criar um manipulador de clique.  
  
9. No manipulador de clique, chame `counter1.Increment()`.  
  
10. Na função de construtor, após a chamada para `InitializeComponent`, digite `counter1``.``Incremented +=` e, em seguida, pressione **guia** duas vezes.  
  
     O Visual Studio gera um manipulador de nível de formulário para o `counter1.Incremented` eventos.  
  
11. Realçar a `Throw` instrução no manipulador de eventos, o tipo `mbox`e, em seguida, pressione **guia** duas vezes para gerar uma caixa de mensagem do trecho de código mbox.  
  
12. Na próxima linha, adicione o seguinte `if` / `else` bloco para definir a visibilidade de **redefinir** botão.  
  
    ```csharp  
    if (counter1.Value < 5) counter1.ShowReset = false;  
    else counter1.ShowReset = true;  
    ```  
  
13. Pressione **F5**.  
  
     O formulário é aberto. O `Counter` controle exibe o texto a seguir.  
  
     **Contagem: 0**  
  
14. Clique em **teste**.  
  
     Os incrementos de contador e o Visual Studio exibe uma caixa de mensagem.  
  
15. Feche a caixa de mensagem.  
  
     O **redefinir** desaparece do botão.  
  
16. Clique em **teste** até que atinja o contador **5** fechar a mensagem de caixas de cada vez.  
  
     O **redefinir** botão é exibida novamente.  
  
17. Clique em **redefinir**.  
  
     O contador é redefinido como **0**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Quando você cria um **caixa de ferramentas** controle, o Visual Studio cria um arquivo chamado *ProjectName.vsix* na pasta \bin\debug\ do seu projeto. Você pode implantar o controle ao carregar o *VSIX* arquivo a uma rede ou para um site da Web. Quando um usuário abre o *. VSIX* arquivo, o controle está instalado e adicionado ao Visual Studio **caixa de ferramentas** no computador do usuário. Como alternativa, você pode carregar os *. VSIX* arquivo [Visual Studio Marketplace](http://go.microsoft.com/fwlink/?LinkID=123847) para que os usuários podem encontrá-lo, navegando no **ferramentas**  >   **Extensões e atualizações** caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 [Estender outras partes do Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)   
 [Criar um controle de caixa de ferramentas do WPF](../extensibility/creating-a-wpf-toolbox-control.md)   
 [Estender outras partes do Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)   
 [Noções básicas sobre o desenvolvimento de controles do Windows Forms](/dotnet/framework/winforms/controls/windows-forms-control-development-basics)
