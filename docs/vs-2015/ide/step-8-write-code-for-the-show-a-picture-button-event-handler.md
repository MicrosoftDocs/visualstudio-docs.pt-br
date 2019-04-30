---
title: 'Etapa 8: Escrever código para mostrar um manipulador de eventos do botão de imagem | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 07f4ec00-cda4-42f4-98bb-37edc7167de7
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 2f162f827fa1866b5ca241bd9aaae2aadffb56e6
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63428607"
---
# <a name="step-8-write-code-for-the-show-a-picture-button-event-handler"></a>Etapa 8: Escrever o código do manipulador de eventos do botão Mostrar uma Imagem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Nesta etapa, você fará o botão **Mostrar uma imagem** funcionar desta forma:  
  
- Quando um usuário escolher esse botão, o programa abrirá uma caixa de diálogo **Abrir Arquivo**.  
  
- Se um usuário abrir um arquivo de imagem, o programa mostrará essa imagem em PictureBox.  
  
  O IDE tem uma ferramenta poderosa chamada IntelliSense que ajuda você a gravar código. À medida que você insere o código, a IDE abre uma caixa com conclusões sugeridas para as palavras parciais que você insere. Tenta determinar o que você deseja fazer em seguida e pula automaticamente para o último item escolhido na lista. Você pode usar as setas para cima ou para abaixo para mover na lista, ou continuar digitando letras para refinar as opções. Ao ver a opção que deseja, escolha a tecla TAB para selecioná-la. Ou, você pode ignorar as sugestões, se não forem necessárias.  
  
  ![link para vídeo](../data-tools/media/playvideo.gif "PlayVideo")para uma versão em vídeo deste tópico, consulte [Tutorial 1: Criar um visualizador de imagens no Visual Basic – vídeo 4](http://go.microsoft.com/fwlink/?LinkId=205215) ou [Tutorial 1: Criar um visualizador de imagens em c# – vídeo 4](http://go.microsoft.com/fwlink/?LinkId=205203). Esses vídeos usam uma versão anterior do Visual Studio, portanto, existem pequenas diferenças em alguns comandos de menu e em outros elementos da interface do usuário. No entanto, os conceitos e procedimentos funcionam de maneiras semelhantes na versão atual do Visual Studio.  
  
### <a name="to-write-code-for-the-show-a-picture-button-event-handler"></a>Para escrever código para o manipulador de eventos do botão Mostrar uma imagem  
  
1. Acesse o Designer de Formulários do Windows e clique duas vezes no botão **Mostrar uma imagem**. O IDE aparece imediatamente para o designer de código e move o cursor para que esteja dentro do método `showButton_Click()` que você adicionou anteriormente.  
  
2. Digite um `i` na linha vazia entre as duas chaves { }. (No Visual Basic, digite na linha vazia entre Private Sub… e End Sub.) Uma janela do **IntelliSense** é aberta, conforme mostrado na imagem a seguir.  
  
     ![IntelliSense com código do Visual C&#35;](../ide/media/express-ifintellisense.png "Express_IfIntellisense")  
IntelliSense com código do Visual C#  
  
3. A janela do **IntelliSense** deve estar realçando a palavra **if**. (Se não estiver, digite um `f` em minúsculas, e ela realçará.) Observe como uma pequena caixa de *dica de ferramenta* ao lado da janela do **IntelliSense** é exibida com a descrição, **Snippet de código para instrução if**. (No Visual Basic, a dica de ferramenta também indica que este é um snippet, mas com palavras ligeiramente diferentes.) Use esse snippet de código e pressione a tecla TAB para inserir **if** em seu código. Em seguida, pressione a tecla TAB novamente para usar o snippet **if**. (Se você pressionou outra coisa e sua janela do **IntelliSense** desapareceu, apague **i** e o digite novamente, e a janela do **IntelliSense** será aberta novamente.)  
  
     ![Código do Visual C&#35;](../ide/media/express-highlighttrue.png "Express_HighlightTrue")  
Código Visual C#  
  
4. Em seguida, use o IntelliSense para inserir mais código para abrir uma caixa de diálogo **Abrir Arquivo**. Se o usuário escolheu o botão **OK**, a PictureBox carrega o arquivo selecionado pelo usuário. As etapas a seguir mostram como inserir o código e, embora sejam várias etapas, são apenas alguns pressionamentos de teclas:  
  
    1. Comece com o texto selecionado **true** no snippet. Digite `op` para substituí-lo. (No Visual Basic, você começa com um limite inicial, portanto, digite `Op`.)  
  
    2. A janela do **IntelliSense** é aberta e exibe **openFileDialog1**. Escolha a tecla TAB para selecioná-lo. (No Visual Basic, ela começa com um limite inicial, portanto, você vê **OpenFileDialog1**. Certifique-se de que **OpenFileDialog1** está selecionado.)  
  
         Para saber mais sobre `OpenFileDialog`, consulte [OpenFileDialog](http://msdn.microsoft.com/library/system.windows.forms.openfiledialog.aspx).  
  
    3. Digite um ponto (`.`) (muitos programadores chamam isso de ponto.) Como você digitou um ponto logo após **openFileDialog1**, uma janela do **IntelliSense** é aberta, preenchida com todas as propriedades e métodos do componente **OpenFileDialog**. Estas são as mesmas propriedades exibidas na janela **Propriedades** quando você a escolhe no Designer de Formulários do Windows. Você também pode escolher os métodos que demandam que o componente faça coisas (como abrir uma caixa de diálogo).  
  
        > [!NOTE]
        > A janela do **IntelliSense** pode mostrar propriedades e métodos. Para determinar o que está sendo mostrado, veja o ícone à esquerda de cada item na janela do **IntelliSense**. Você verá uma imagem de um bloco ao lado de cada método, e uma imagem de uma chave (ou de chave em inglês) ao lado de cada propriedade. Há também um ícone de raio ao lado de cada evento. Essas imagens são exibidas como se segue.  
  
         ![Ícone de método](../ide/media/express-iconmethod.png "Express_IconMethod")  
Ícone de método  
  
         ![Ícone de propriedade](../ide/media/express-iconproperty.png "Express_IconProperty")  
Ícone de propriedade  
  
         ![Ícone de evento](../ide/media/express-iconevent.png "Express_IconEvent")  
Ícone de evento  
  
    4. Comece digitando `ShowDialog` (as letras maiúsculas não são importantes para o IntelliSense). O método `ShowDialog()` exibirá a caixa de diálogo **Abrir Arquivo**. Depois que a janela tiver realçado **ShowDialog**, pressione a tecla TAB. Você também pode realçar “ShowDialog” e escolher a tecla F1 para obter ajuda para ele.  
  
         Para saber mais sobre o método `ShowDialog()`, consulte [ShowDialog Method (Método ShowDialog)](http://msdn.microsoft.com/library/c7ykbedk.aspx).  
  
    5. Ao usar um método em um controle ou em um componente (conhecido como *chamando um método*), é necessário adicionar parênteses. Assim, insira a abertura e fechamento parênteses imediatamente após o "g" em `ShowDialog`: `()` Agora, ele deve ser semelhante a "openFileDialog1.ShowDialog()".  
  
        > [!NOTE]
        > Os métodos são uma parte importante de qualquer programa, e este tutorial mostrou várias maneiras de usar métodos. É possível chamar o método de um componente para pedir que ele faça algo, da mesma forma como você chamou o método `ShowDialog()` do componente **OpenFileDialog**. Você pode criar seus próprios métodos para fazer seu programa executar ações, como aquela que você está compilando agora, chamado método `showButton_Click()`, que abre um caixa de diálogo e uma imagem quando um usuário escolhe um botão.  
  
    6. Para o Visual C#, adicione um espaço e, em seguida, adicione dois sinais de igual (`==`). Para o Visual Basic, adicione um espaço e, em seguida, use um único sinal de igual (`=`). (O Visual C# e Visual Basic usam operadores de igualdade diferentes.)  
  
    7. Adicionar outro espaço. Assim que fizer isso, outra janela do **IntelliSense** será aberta. Comece digitando `DialogResult` e pressione a tecla TAB para adicioná-lo.  
  
        > [!NOTE]
        > Quando você escreve um código para chamar um método, ele às vezes retorna um valor. Nesse caso, o método `ShowDialog()` do componente **OpenFileDialog** retorna um valor DialogResult. DialogResult é um valor especial que indica o que acontecem em uma caixa de diálogo. Um componente **OpenFileDialog** pode resultar em o usuário escolher **OK** ou **Cancelar**. Portanto, seu método `ShowDialog()` retorna DialogResult.OK ou DialogResult.Cancel.  
  
    8. Digite um ponto para abrir a janela do **IntelliSense** de valor DialogResult. Insira a letra `O` e pressione a tecla TAB para inserir **OK**.  
  
         Para saber mais sobre `DialogResult`, consulte [DialogResult](http://msdn.microsoft.com/library/system.windows.forms.dialogresult.aspx).  
  
        > [!NOTE]
        > A primeira linha de código deve ser preenchida. Para o Visual C#, deve ser o seguinte.  
        >   
        >  `if (openFileDialog1.ShowDialog() == DialogResult.OK)`  
        >   
        >  Para o Visual Basic, deve ser o seguinte.  
        >   
        >  `If OpenFileDialog1.ShowDialog() = DialogResult.OK Then`  
  
    9. Agora adicione mais uma linha de código. Você pode digitar (ou copiar e colar), mas considere usar o IntelliSense para adicioná-lo. Quanto mais familiarizado você estiver com o IntelliSense, mais rapidamente você poderá escrever seu próprio código. O método final de `showButton_Click()` parece com o seguinte. (Escolha a guia **VB** para exibir a versão do Visual Basic do código.)  
  
         [!code-csharp[VbExpressTutorial1Step8#1](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial1step8/cs/form1.cs#1)]
         [!code-vb[VbExpressTutorial1Step8#1](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial1step8/vb/form1.vb#1)]  
  
### <a name="to-continue-or-review"></a>Para continuar ou revisar  
  
- Para ir para a próxima etapa do tutorial, confira [Etapa 9: Revisar, comentar e testar seu código](../ide/step-9-review-comment-and-test-your-code.md).  
  
- Para retornar à etapa anterior do tutorial, confira [Etapa 7: Adicionar componentes de caixa de diálogo ao formulário](../ide/step-7-add-dialog-components-to-your-form.md).
