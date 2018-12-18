---
title: Criando um Windows Forms o controle de caixa de ferramentas | Microsoft Docs
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
- winforms
- toolbox
- windows forms
ms.assetid: 0be6ffc1-8afd-4d02-9a5d-e27dde05fde6
caps.latest.revision: 20
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 371fd4269cee5918bd0d0b623eb49e1f709a311d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51781706"
---
# <a name="creating-a-windows-forms-toolbox-control"></a>Criando um controle de caixa de ferramentas do Windows Forms
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O modelo de item de controle de caixa de ferramentas do Windows Forms que está incluído no Visual Studio Extensibility Tools (SDK do VS) permite que você crie um controle que é adicionado automaticamente para o **caixa de ferramentas** quando a extensão está instalada. Este tópico mostra como usar o modelo para criar um controle de um contador simples que você pode distribuir a outros usuários.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="creating-a-windows-forms-toolbox-control"></a>Criando um controle de caixa de ferramentas do Windows Forms  
 O modelo de controle de caixa de ferramentas do Windows Forms cria um controle de usuário indefinido e fornece toda a funcionalidade que é necessário para adicionar o controle para o **caixa de ferramentas**.  
  
#### <a name="create-an-extension-with-a-windows-forms-toolbox-control"></a>Criar uma extensão com um controle de caixa de ferramentas do Windows Forms  
  
1.  Crie um projeto do VSIX chamado `MyWinFormsControl`. Você pode encontrar o modelo de projeto VSIX na **novo projeto** diálogo sob **Visual c# / extensibilidade**.  
  
2.  Quando o projeto aberto, adicione uma **controle de caixa de ferramentas do Windows Forms** modelo de item chamado `Counter`. No **Gerenciador de soluções**, clique com botão direito no nó do projeto e selecione **Add / Novo Item**. No **Adicionar Novo Item** caixa de diálogo, vá para **Visual c# / extensibilidade** e selecione **controle de caixa de ferramentas do Windows Forms**  
  
3.  Isso adiciona um controle de usuário, uma `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> para posicionar o controle na **caixa de ferramentas**e um **Microsoft.VisualStudio.ToolboxControl** entrada de ativo no manifesto do VSIX para implantação.  
  
### <a name="building-a-user-interface-for-the-control"></a>Criando uma Interface do usuário para o controle  
 O `Counter` controle requer dois controles filho: uma <xref:System.Windows.Forms.Label> para exibir a contagem atual e um <xref:System.Windows.Forms.Button> para redefinir a contagem como 0. Nenhum outro controle filho é necessário porque chamadores incrementará o contador de forma programática.  
  
##### <a name="to-build-the-user-interface"></a>Para criar a interface do usuário  
  
1.  Na **Gerenciador de soluções**, clique duas vezes em Counter.cs para abri-lo no designer.  
  
2.  Remova o "Clique aqui!" **Botão** que está incluído por padrão quando você adiciona o modelo de item de controle de caixa de ferramentas do Windows Forms.  
  
3.  Dos **caixa de ferramentas**, arraste um `Label` controle e, em seguida, um `Button` controle abaixo dele para a superfície de design.  
  
4.  Redimensionar o controle de usuário geral para 150, 50 pixels e redimensionar o botão de controle como 50, 20 pixels.  
  
5.  No **propriedades** janela, defina os seguintes valores para os controles na superfície de design.  
  
    |Controle|Propriedade|Valor|  
    |-------------|--------------|-----------|  
    |`Label1`|**Texto**|""|  
    |`Button1`|**Nome**|btnReset|  
    |`Button1`|**Texto**|Redefinir|  
  
### <a name="coding-the-user-control"></a>Codificar o controle de usuário  
 O `Counter` controle irá expor um método para incrementar o contador, um evento a ser acionado sempre que o contador é incrementado, uma `Reset` botão e três propriedades para armazenar a contagem atual, o texto de exibição e se deseja mostrar ou ocultar o `Reset`botão. O `ProvideToolboxControl` atributo determina onde em de **caixa de ferramentas** o `Counter` controle será exibido.  
  
##### <a name="to-code-the-user-control"></a>Codificar o controle de usuário  
  
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
  
     Os chamadores podem acessar essas propriedades para obter e definir o texto de exibição do contador para mostrar ou ocultar o `Reset` botão. Os chamadores podem obter o valor atual de somente leitura `Value` propriedade, mas eles não é possível definir o valor diretamente.  
  
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
  
7.  Retornar ao modo de design e clique duas vezes o `Reset` botão para gerar o `btnReset_Click` manipulador de eventos e, em seguida, preenchê-lo conforme mostrado no exemplo a seguir.  
  
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
  
### <a name="testing-the-control"></a>Testando o controle  
 Para testar uma **caixa de ferramentas** controlar, primeiro testá-lo no ambiente de desenvolvimento e, em seguida, testá-lo em um aplicativo compilado.  
  
##### <a name="to-test-the-control"></a>Para testar o controle  
  
1.  Pressione F5.  
  
     Isso compila o projeto e abre uma segunda instância Experimental do Visual Studio que tem o controle instalado.  
  
2.  Na instância Experimental do Visual Studio, crie uma **aplicativo do Windows Forms** projeto.  
  
3.  Na **Gerenciador de soluções**, clique duas vezes em Form1 para abri-lo no designer, se ele não ainda estiver aberto.  
  
4.  No **caixa de ferramentas**, o `Counter` controle deve ser exibido no **geral** seção.  
  
5.  Arraste um `Counter` controle ao seu formulário e, em seguida, selecioná-lo. O `Value`, `Message`, e `ShowReset` propriedades serão exibidas no **as propriedades** janela, junto com as propriedades que são herdadas de <xref:System.Windows.Forms.UserControl>.  
  
6.  Defina a propriedade `Message` como `Count:`.  
  
7.  Arraste uma <xref:System.Windows.Forms.Button> o controle para o formulário e, em seguida, defina as propriedades de nome e o texto do botão para `Test`.  
  
8.  Clique duas vezes no botão para abrir Form1 na exibição de código e criar um manipulador de clique.  
  
9. No manipulador de clique, chame `counter1.Increment()`.  
  
10. Na função de construtor, após a chamada para `InitializeComponent`, digite `counter1``.``Incremented +=` e, em seguida, pressione TAB duas vezes.  
  
     O Visual Studio gera um manipulador de nível de formulário para o `counter1.Incremented` eventos.  
  
11. Realçar a `Throw` instrução no manipulador de eventos, o tipo `mbox`, e, em seguida, pressione TAB duas vezes para gerar uma caixa de mensagem do trecho de código mbox.  
  
12. Na próxima linha, adicione o seguinte `if` / `else` bloco para definir a visibilidade de `Reset` botão.  
  
    ```csharp  
    if (counter1.Value < 5) counter1.ShowReset = false;  
    else counter1.ShowReset = true;  
    ```  
  
13. Pressione F5.  
  
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
 Quando você cria um **caixa de ferramentas** controle, o Visual Studio cria um arquivo chamado *ProjectName*. VSIX na pasta \bin\debug\ do seu projeto. Você pode implantar o controle ao carregar o arquivo. VSIX para uma rede ou para um site da Web. Quando um usuário abre o arquivo. VSIX, o controle seja instalado e adicionado ao Visual Studio **caixa de ferramentas** no computador do usuário. Como alternativa, você pode carregar o arquivo. VSIX para o [Galeria do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=123847) Web site para que os usuários podem encontrá-lo, navegando na **ferramentas / extensões e atualizações** caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 [Estendendo a caixa de ferramentas](../misc/extending-the-toolbox.md)   
 [Criar um controle de caixa de ferramentas do WPF](../extensibility/creating-a-wpf-toolbox-control.md)   
 [Estender outras partes do Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)   
 [Noções básicas sobre o desenvolvimento de controles dos Windows Forms](http://msdn.microsoft.com/library/6277bb81-90f7-4c5b-9f4b-b02bb42dd316)

