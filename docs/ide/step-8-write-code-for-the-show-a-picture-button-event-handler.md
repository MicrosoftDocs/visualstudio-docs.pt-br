---
title: Escrever o código do manipulador de eventos do botão Mostrar uma Imagem
description: Escreva o código para o manipulador de eventos do botão Mostrar uma imagem no tutorial criar um visualizador de imagem.
ms.date: 08/30/2019
ms.custom: SEO-VS-2020
ms.assetid: 07f4ec00-cda4-42f4-98bb-37edc7167de7
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 87d07ade092869221b9a0848ed64899a0a8a41a5
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106214038"
---
# <a name="step-8-write-code-for-the-show-a-picture-button-event-handler"></a>Etapa 8: Escrever código para o manipulador de eventos do botão Mostrar uma Imagem

Nesta etapa, você faz com que o botão **mostrar uma imagem** funcione da seguinte maneira:

- Quando um usuário escolhe esse botão, o aplicativo abre uma <xref:System.Windows.Forms.OpenFileDialog> caixa.

- Se um usuário abrir um arquivo de imagem, o aplicativo mostrará a imagem no <xref:System.Windows.Forms.PictureBox> .

O IDE tem uma ferramenta poderosa chamada IntelliSense que ajuda você a gravar código. À medida que você digita o código, o IDE abre uma caixa com as conclusões sugeridas para palavras parciais que você inserir.

O IntelliSense tenta determinar o que você deseja fazer em seguida e salta automaticamente para o último item que você escolher na lista. Você pode usar as setas para cima ou para abaixo para mover na lista, ou continuar digitando letras para refinar as opções. Ao ver a opção que deseja, escolha a tecla **Tab** para selecioná-la. Ou, você pode ignorar as sugestões, se não forem necessárias.

## <a name="to-write-code-for-the-show-a-picture-button-event-handler"></a>Para escrever código para o manipulador de eventos do botão Mostrar uma imagem

1. Acesse o **Designer de Formulários do Windows** e clique duas vezes no botão **Mostrar uma imagem**. O IDE vai imediatamente para o designer de código e move o cursor para que ele fique dentro do `showButton_Click()` método (como alternativa `ShowButton_Click()` ) que você adicionou anteriormente.

1. Digite um `i` na linha vazia entre as duas chaves `{ }`. (Em Visual Basic, digite na linha vazia entre `Private Sub...` e `End Sub` .) Uma janela do **IntelliSense** é aberta, conforme mostrado na imagem a seguir.

    ![IntelliSense com o código do Visual C&#35;](../ide/media/express_ifintellisense.png)

    > [!NOTE]
    > Seu código pode não exibir manipuladores de eventos em letras "camelCase".

1. A janela do **IntelliSense** deve realçar a palavra `if` . (Caso contrário, insira uma letra minúscula `f` e ela vai.) Observe como uma caixa de *dica de ferramenta* ao lado da janela do **IntelliSense** aparece com a descrição, **trecho de código para instrução If**. (No Visual Basic, a dica de ferramenta também afirma que se trata de um trecho de código, mas com um texto ligeiramente diferente.) Você deseja usar esse trecho, portanto, escolha a tecla **Tab** para inserir `if` em seu código. Em seguida, pressione a tecla **Tab** novamente para usar o snippet `if`. (Se você pressionou outro item e sua janela do **IntelliSense** desapareceu, apague `i` e o digite novamente, e a janela do **IntelliSense** será reaberta).

    ![Código do Visual C&#35;](../ide/media/express_highlighttrue.png)

### <a name="use-intellisense-to-enter-more-code"></a>Use o IntelliSense para inserir mais código

Em seguida, use o IntelliSense para inserir mais código para abrir uma caixa de diálogo **Abrir Arquivo**. Se o usuário escolheu o botão **OK**, a PictureBox carrega o arquivo selecionado pelo usuário. As etapas a seguir mostram como inserir o código e, embora existam muitas etapas, são apenas alguns pressionamentos de teclas:

 1. Comece com o texto selecionado **true** no snippet. Digite `op` para substituí-lo. (No Visual Basic, você começa com um limite inicial, portanto, digite `Op`.)

 1. A janela do **IntelliSense** é aberta e exibe **openFileDialog1**. Escolha a tecla **Tab** para selecioná-lo. (No Visual Basic, ela começa com um limite inicial, portanto, você vê **OpenFileDialog1**. Certifique-se de que **OpenFileDialog1** está selecionado.)

     Para saber mais sobre `OpenFileDialog`, consulte [OpenFileDialog](<xref:System.Windows.Forms.OpenFileDialog>).

 1. Digite um ponto ( `.` ) (muitos programadores chamam esse ponto.) Como você digitou um ponto logo após **OpenFileDialog1**, uma janela do **IntelliSense** é aberta, preenchida com todas as propriedades e métodos do componente **OpenFileDialog** . Estas são as mesmas propriedades exibidas na janela **Propriedades** quando você a escolhe no **Designer de Formulários do Windows**. Você também pode escolher os métodos que demandam que o componente faça coisas (como abrir uma caixa de diálogo).

    > [!NOTE]
    > A janela do **IntelliSense** pode mostrar propriedades e métodos. Para determinar o que está sendo mostrado, veja o ícone à esquerda de cada item na janela do **IntelliSense**. Você vê uma imagem de um bloco ao lado de cada método e uma imagem de uma chave inglesa (ou de um superanne) ao lado de cada propriedade. Há também um ícone de raio ao lado de cada evento. <br><br>Estes são os ícones que aparecem:<br><br>![Ícone de método](../ide/media/express_iconmethod.png)<br>![Ícone de propriedade](../ide/media/express_iconproperty.png)<br>![Ícone de evento](../ide/media/express_iconevent.png)

 1. Comece digitando `ShowDialog` (as letras maiúsculas não são importantes para o IntelliSense). O método `ShowDialog()` exibirá a caixa de diálogo **Abrir Arquivo**. Depois que a janela tiver realçado **ShowDialog**, pressione a tecla **Tab**. Você também pode realçar "ShowDialog" e escolher a tecla **F1** para obter ajuda com isso.

    Para saber mais sobre o método `ShowDialog()`, consulte [ShowDialog Method (Método ShowDialog)](<xref:System.Windows.Forms.Form.ShowDialog%2A>).

 1. Ao usar um método em um controle ou em um componente (conhecido como *chamando um método*), é necessário adicionar parênteses. Assim, insira parênteses de abertura e fechamento imediatamente após o “g” em `ShowDialog`: `()` Agora isso terá a aparência "openFileDialog1.ShowDialog()".

    > [!NOTE]
    > Os métodos são uma parte importante de qualquer aplicativo, e este tutorial mostrou várias maneiras de usar métodos. É possível chamar o método de um componente para pedir que ele faça algo, da mesma forma como você chamou o método `ShowDialog()` do componente **OpenFileDialog**. Você pode criar seus próprios métodos para fazer com que seu aplicativo faça coisas, como aquela que você está criando agora, chamado de `showButton_Click()` método, que abre uma caixa de diálogo e uma imagem quando um usuário escolhe um botão.

 1. Para C#, adicione um espaço e, em seguida, adicione dois sinais de igual ( `==` ). Para o Visual Basic, adicione um espaço e, em seguida, use um único sinal de igual (`=`). (C# e Visual Basic usam operadores de igualdade diferentes.)

 1. Adicionar outro espaço. Assim que fizer isso, outra janela do **IntelliSense** será aberta. Comece digitando `DialogResult` e pressione a tecla **Tab** para adicioná-lo.

    > [!NOTE]
    > Quando você escreve um código para chamar um método, ele às vezes retorna um valor. Nesse caso, o método <xref:System.Windows.Forms.CommonDialog.ShowDialog> do componente **OpenFileDialog** retorna um valor <xref:System.Windows.Forms.DialogResult>. DialogResult é um valor especial que indica o que acontecem em uma caixa de diálogo. Um componente **OpenFileDialog** pode resultar em o usuário escolher **OK** ou **Cancelar**. Portanto, seu método `ShowDialog()` retorna `DialogResult.OK` ou `DialogResult.Cancel`.

 1. Digite um ponto para abrir a janela do **IntelliSense** de valor DialogResult. Insira a letra `O` e pressione a tecla **Tab** para inserir **OK**.

    Para saber mais sobre DialogResult, veja [DialogResult](<xref:System.Windows.Forms.DialogResult>).

    > [!NOTE]
    > A primeira linha de código deve ser preenchida. Para o C#, ele deve ser semelhante ao seguinte.
    >
    >  `if (openFileDialog1.ShowDialog() == DialogResult.OK)`
    >
    >  Para o Visual Basic, deve ser o seguinte.
    >
    >  `If OpenFileDialog1.ShowDialog() = DialogResult.OK Then`

 1. Agora adicione mais uma linha de código. Você pode digitar (ou copiar e colar), mas considere usar o IntelliSense para adicioná-lo. Quanto mais familiarizado você estiver com o IntelliSense, mais rapidamente você poderá escrever seu próprio código. O `showButton_Click()` método final deve ser semelhante ao código a seguir.

    [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial1step8/cs/form1.cs" id="Snippet1":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial1step8/vb/form1.vb" id="Snippet1":::

## <a name="next-steps"></a>Próximas etapas

* Para ir para a próxima etapa do tutorial, consulte **[etapa 9: revisar, comentar e testar seu código](../ide/step-9-review-comment-and-test-your-code.md)**.

* Para retornar à etapa anterior do tutorial, veja [Etapa 7: Adicionar componentes de caixa de diálogo ao seu formulário](../ide/step-7-add-dialog-components-to-your-form.md).

## <a name="see-also"></a>Confira também

* [Tutorial 2: criar um teste de matemática cronometrado](tutorial-2-create-a-timed-math-quiz.md)
* [Tutorial 3: criar um jogo de correspondência](tutorial-3-create-a-matching-game.md)
