---
title: Criando um controle de caixa de ferramentas de Windows Forms | Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- winforms
- toolbox
- windows forms
ms.assetid: 0be6ffc1-8afd-4d02-9a5d-e27dde05fde6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d7c4d14f2970f9d77e78fd90dd58efcdac100e4c
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903962"
---
# <a name="create-a-windows-forms-toolbox-control"></a>Criar um controle de caixa de ferramentas de Windows Forms

O modelo de item de controle de caixa de ferramentas Windows Forms que está incluído no Ferramentas de Extensibilidade do Visual Studio (SDK do VS), permite criar um controle **caixa de ferramentas** que é adicionado automaticamente quando a extensão é instalada. Este tutorial mostra como usar o modelo para criar um controle de contador simples que você pode distribuir para outros usuários.

## <a name="prerequisites"></a>Pré-requisitos

A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-the-toolbox-control"></a>Criar o controle de caixa de ferramentas

O modelo de controle de caixa de ferramentas Windows Forms cria um controle de usuário indefinido e fornece toda a funcionalidade necessária para adicionar o controle à **caixa de ferramentas**.

### <a name="create-an-extension-with-a-windows-forms-toolbox-control"></a>Criar uma extensão com um controle de caixa de ferramentas Windows Forms

1. Crie um projeto VSIX denominado `MyWinFormsControl` . Você pode encontrar o modelo de projeto VSIX na caixa de diálogo **novo projeto** , pesquisando por "VSIX".

2. Quando o projeto for aberto, adicione um modelo de item de **controle de caixa de ferramentas de Windows Forms** chamado `Counter` . Na **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar**  >  **novo item**. Na caixa de diálogo **Adicionar novo item** , vá para extensibilidade do **Visual C#**  >  **Extensibility** e selecione **Windows Forms controle caixa de ferramentas**

3. Isso adiciona um controle de usuário, um `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> para posicionar o controle na **caixa de ferramentas**e uma entrada de ativo **Microsoft. VisualStudio. ToolboxControl** no manifesto do VSIX para implantação.

### <a name="build-a-user-interface-for-the-control"></a>Criar uma interface do usuário para o controle

O `Counter` controle requer dois controles filho: a <xref:System.Windows.Forms.Label> para exibir a contagem atual e um <xref:System.Windows.Forms.Button> para redefinir a contagem como 0. Nenhum outro controle filho é necessário, pois os chamadores incrementarão o contador programaticamente.

#### <a name="to-build-the-user-interface"></a>Para criar a interface do usuário

1. Em **Gerenciador de soluções**, clique duas vezes em *Counter.cs* para abri-lo no designer.

2. Remova o **clique aqui!** botão que é incluído por padrão quando você adiciona o modelo de item de controle Windows Forms caixa de ferramentas.

3. Na **caixa de ferramentas**, arraste um `Label` controle e, em seguida, um `Button` controle abaixo dele para a superfície de design.

4. Redimensione o controle de usuário geral para 150, 50 pixels e redimensione o controle de botão para 50, 20 pixels.

5. Na janela **Propriedades** , defina os seguintes valores para os controles na superfície de design.

    |Control|Propriedade|Valor|
    |-------------|--------------|-----------|
    |`Label1`|**Texto**|""|
    |`Button1`|**Nome**|btnReset|
    |`Button1`|**Texto**|Redefinir|

### <a name="code-the-user-control"></a>Codificar o controle de usuário

O `Counter` controle irá expor um método para incrementar o contador, um evento a ser gerado sempre que o contador for incrementado, um botão de **redefinição** e três propriedades para armazenar a contagem atual, o texto de exibição e se deseja mostrar ou ocultar o botão de **redefinição** . O `ProvideToolboxControl` atributo determina onde o controle será exibido na **caixa de ferramentas** `Counter` .

#### <a name="to-code-the-user-control"></a>Para codificar o controle de usuário

1. Clique duas vezes no formulário para abrir seu manipulador de eventos de carregamento na janela de código.

2. Acima do método do manipulador de eventos, na classe Control, crie um inteiro para armazenar o valor do contador e uma cadeia de caracteres para armazenar o texto de exibição, conforme mostrado no exemplo a seguir.

    ```csharp
    int currentValue;
    string displayText;
    ```

3. Crie as seguintes declarações de propriedade pública.

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

    Os chamadores podem acessar essas propriedades para obter e definir o texto de exibição do contador e para mostrar ou ocultar o botão **Redefinir** . Os chamadores podem obter o valor atual da propriedade somente leitura `Value` , mas não podem definir o valor diretamente.

4. Coloque o código a seguir no `Load` evento para o controle.

    ```csharp
    private void Counter_Load(object sender, EventArgs e)
    {
        currentValue = 0;
        label1.Text = Message + Value;
    }

    ```

    Definir o texto do **rótulo** no <xref:System.Windows.Forms.UserControl.Load> evento permite que as propriedades de destino sejam carregadas antes de seus valores serem aplicados. Definir o texto do **rótulo** no Construtor resultaria em um **rótulo**vazio.

5. Crie o seguinte método público para incrementar o contador.

    ```csharp
    public void Increment()
    {
        currentValue++;
        label1.Text = displayText + Value;
        Incremented(this, EventArgs.Empty);
    }

    ```

6. Adicione uma declaração para o `Incremented` evento à classe Control.

    ```csharp
    public event EventHandler Incremented;
    ```

    Os chamadores podem adicionar manipuladores a esse evento para responder às alterações no valor do contador.

7. Retorne ao modo de exibição de design e clique duas vezes no botão **Redefinir** para gerar o `btnReset_Click` manipulador de eventos e, em seguida, preencha-o como mostrado no exemplo a seguir.

    ```csharp
    private void btnReset_Click(object sender, EventArgs e)
    {
        currentValue = 0;
        label1.Text = displayText + Value;
    }

    ```

8. Imediatamente acima da definição de classe, na `ProvideToolboxControl` declaração de atributo, altere o valor do primeiro parâmetro de `"MyWinFormsControl.Counter"` para `"General"` . Isso define o nome do grupo de itens que hospedará o controle na **caixa de ferramentas**.

    O exemplo a seguir mostra o `ProvideToolboxControl` atributo e a definição de classe ajustada.

    ```csharp
    [ProvideToolboxControl("General", false)]
    public partial class Counter : UserControl
    ```

### <a name="test-the-control"></a>Testar o controle

 Para testar um controle de **caixa de ferramentas** , primeiro teste-o no ambiente de desenvolvimento e, em seguida, teste-o em um aplicativo compilado.

#### <a name="to-test-the-control"></a>Para testar o controle

1. Pressione **F5** para **iniciar a depuração**.

    Esse comando cria o projeto e abre uma segunda instância experimental do Visual Studio que tem o controle instalado.

2. Na instância experimental do Visual Studio, crie um projeto de **aplicativo Windows Forms** .

3. Em **Gerenciador de soluções**, clique duas vezes em *Form1.cs* para abri-lo no designer se ele ainda não estiver aberto.

4. Na **caixa de ferramentas**, o `Counter` controle deve ser exibido na seção **geral** .

5. Arraste um `Counter` controle para o formulário e, em seguida, selecione-o. As `Value` `Message` Propriedades,, e `ShowReset` serão exibidas na janela **Propriedades** , junto com as propriedades herdadas de <xref:System.Windows.Forms.UserControl> .

6. Defina a propriedade `Message` como `Count:`.

7. Arraste um <xref:System.Windows.Forms.Button> controle para o formulário e defina as propriedades Name e Text do botão como `Test` .

8. Clique duas vezes no botão para abrir *Form1.cs* na exibição de código e criar um manipulador de cliques.

9. No manipulador de cliques, chame `counter1.Increment()` .

10. Na função do Construtor, após a chamada para `InitializeComponent` , digite `counter1``.``Incremented +=` e pressione **Tab** duas vezes.

    O Visual Studio gera um manipulador de nível de formulário para o `counter1.Incremented` evento.

11. Realce a `Throw` instrução no manipulador de eventos, digite `mbox` e pressione **Tab** duas vezes para gerar uma caixa de mensagem a partir do trecho de código mbox.

12. Na próxima linha, adicione o seguinte `if` / `else` bloco para definir a visibilidade do botão **Redefinir** .

    ```csharp
    if (counter1.Value < 5) counter1.ShowReset = false;
    else counter1.ShowReset = true;
    ```

13. Pressione **F5**.

    O formulário é aberto. O `Counter` controle exibe o texto a seguir.

    **Contagem: 0**

14. Clique em **Testar**.

    O contador é incrementado e o Visual Studio exibe uma caixa de mensagem.

15. Feche a caixa de mensagem.

    O botão **Redefinir** desaparece.

16. Clique em **testar** até que o contador atinja **5** fechando as caixas de mensagem a cada vez.

    O botão **Redefinir** reaparece.

17. Clique em **redefinir**.

    O contador é redefinido como **0**.

## <a name="next-steps"></a>Próximas etapas

Quando você cria um controle de **caixa de ferramentas** , o Visual Studio cria um arquivo chamado *ProjectName. vsix* na pasta \bin\debug\ do seu projeto. Você pode implantar o controle carregando o arquivo *. vsix* em uma rede ou em um site da Web. Quando um usuário abre o arquivo *. vsix* , o controle é instalado e adicionado à **caixa de ferramentas** do Visual Studio no computador do usuário. Como alternativa, você pode carregar o arquivo *. vsix* para [Visual Studio Marketplace](https://marketplace.visualstudio.com/) para que os usuários possam encontrá-lo navegando **Tools**na  >  caixa de diálogo**extensões e atualizações** de ferramentas.

## <a name="see-also"></a>Confira também

- [Estender outras partes do Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)
- [Criar um controle de caixa de ferramentas do WPF](../extensibility/creating-a-wpf-toolbox-control.md)
- [Estender outras partes do Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)
- [Noções básicas de desenvolvimento de controle de Windows Forms](/dotnet/framework/winforms/controls/windows-forms-control-development-basics)
