---
title: 'Etapa 6: nomear os controles de botão | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 56b3baa3-651e-4ad4-8942-e334c5c57158
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: e02c240f8e4146ce1c87fd1d90c30eb7787cef5d
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49303778"
---
# <a name="step-6-name-your-button-controls"></a>Etapa 6: Nomear os controles de botão
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Há apenas uma PictureBox em seu formulário. Quando você a adicionou, o IDE a nomeou automaticamente como **pictureBox1**. Há apenas uma CheckBox, que é denominada **checkBox1**. Em breve, você escreverá alguns códigos, e tais códigos se referirão à CheckBox e à PictureBox. Como há apenas um de cada desses controles, você saberá o que significa ver **pictureBox1** ou **checkBox1** em seu código.  
  
> [!NOTE]
>  No Visual Basic, a primeira letra padrão de qualquer nome de controle é uma maiúscula inicial e, portanto, os nomes são **PictureBox1**, **CheckBox1** e assim por diante.  
  
 Há quatro botões no formulário e o IDE os nomeou **button1**, **button2**, **button3** e **button4**. Apenas olhando seus nomes atuais, você não consegue saber qual botão é o botão de **Fechar** e qual é o botão **Mostrar uma imagem**. É por isso que é útil atribuir nomes mais informativos aos controles de botão.  
  
 ![link para vídeo](../data-tools/media/playvideo.gif "PlayVideo")Para uma versão em vídeo deste tópico, consulte o [Tutorial 1: criar um Visualizador de Imagens no Visual Basic – Vídeo 3](http://go.microsoft.com/fwlink/?LinkId=205213) ou o [Tutorial 1: criar um Visualizador de Imagens em C# – Vídeo 3](http://go.microsoft.com/fwlink/?LinkId=205202). Esses vídeos usam uma versão anterior do Visual Studio, portanto, existem pequenas diferenças em alguns comandos de menu e em outros elementos da interface do usuário. No entanto, os conceitos e procedimentos funcionam de maneiras semelhantes na versão atual do Visual Studio.  
  
### <a name="to-name-your-button-controls"></a>Para nomear os controles de botão  
  
1.  No formulário, clique no botão **Fechar**. (Se você ainda tiver todos os botões selecionados, pressione a tecla ESC para cancelar a seleção.) Role pela janela **Propriedades**, até ver a propriedade **(Name)**. (A propriedade **(Name)** fica próxima à parte superior quando as propriedades são alfabéticas.) Altere o nome para **closeButton**, conforme mostrado na imagem a seguir.  
  
     ![Janela Propriedades com o nome closeButton](../ide/media/express-setnameproperty.png "Express_SetNameProperty")  
A janela Propriedades com nome de closeButton  
  
    > [!NOTE]
    >  Se você tentar alterar o nome do botão para **closeButton**, com um espaço entre as palavras close e Button, o IDE exibirá uma mensagem de erro: "O valor da propriedade não é válido." Espaços (e mais alguns caracteres) não são permitidos em nomes de controle.  
  
2.  Renomeie os outros três botões para **backgroundButton**, **clearButton** e **showButton**. Você pode verificar os nomes escolhendo a lista suspensa seletora de controle na janela **Propriedades**. Os nomes dos novos botões aparecem.  
  
3.  Clique duas vezes no botão **Mostrar uma imagem** no formulário. Como alternativa, escolha o botão **Mostrar uma imagem** no formulário e, em seguida, pressione a tecla ENTER. Quando você fizer isso, o IDE abrirá uma guia adicional na janela principal chamada **Form1.cs** (**Form1.vb** se você estiver usando Visual Basic). Esta guia mostra o arquivo de código por trás do formulário, conforme mostrado na seguinte imagem.  
  
     ![Guia Form1.cs com o código Visual C&#35;](../ide/media/express-showbuttoncode.png "Express_ShowButtonCode")  
Guia Form1.cs com código do Visual c#  
  
4.  Foco nesta parte do código. (Escolha a guia **VB** abaixo se você estiver usando o Visual Basic para exibir a versão de Visual Basic do código.)  
  
     [!code-csharp[VbExpressTutorial1Step6#1](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial1step6/cs/form1.cs#1)]
     [!code-vb[VbExpressTutorial1Step6#1](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial1step6/vb/form1.vb#1)]  
  
     Você está examinando um código chamado `showButton_Click()`. O IDE adicionou isto ao código do formulário quando você abriu o arquivo de código para o botão **showButton**. No tempo de design, quando você abre o arquivo de código para um controle em um formulário, o código é gerado para o controle se ainda não existir. Esse código, conhecido como *método*, é executado quando você executa seu programa e escolhe o controle – nesse caso, o botão **Mostrar uma imagem**.  
  
    > [!NOTE]
    >  Neste tutorial, o código do Visual Basic que é gerado automaticamente foi simplificado por meio da remoção de tudo entre os parênteses, (). Sempre que isso ocorre, você pode remover o mesmo código. Seu programa irá trabalhar de qualquer maneira. Para o restante dos tutoriais, qualquer código automaticamente gerado será simplificado sempre que possível.  
  
5.  Escolha o guia do Designer de Formulários do Windows novamente (**Form1.cs [Design]** no Visual c#, **Form1.vb [Design]** no Visual Basic) e abra o arquivo de código do botão **Limpar a imagem** para criar um método para ele no código do formulário. Repita isso para os dois botões restantes. A cada vez, o IDE adiciona um novo método ao arquivo de código do formulário.  
  
6.  Para adicionar mais um método, abra o arquivo de código para o controle CheckBox no Windows Forms Designer para fazer o IDE adicionar um método `checkBox1_CheckedChanged()`. Esse método é chamado sempre que o usuário seleciona ou desmarca a caixa de seleção.  
  
    > [!NOTE]
    >  Ao trabalhar em um programa, você geralmente move entre o editor de códigos e o designer do Windows Forms. O IDE torna fácil a navegação no projeto. Use o **Gerenciador de Soluções** para abrir o Designer de Formulários do Windows clicando duas vezes em **Form1.cs** no Visual C# ou **Form1.vb** no Visual Basic ou na barra de menus, escolha **Exibir**, **Designer**.  
  
     A seguir temos o novo código que você vê no editor de códigos.  
  
     [!code-csharp[VbExpressTutorial1Step6#2](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial1step6/cs/form1.cs#2)]
     [!code-vb[VbExpressTutorial1Step6#2](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial1step6/vb/form1.vb#2)]  
  
     Os cinco métodos que você adicionou são chamados *manipuladores de eventos* porque seu programa os chama sempre que um evento (como um usuário que escolhe um botão ou que seleciona uma caixa) acontece.  
  
     Ao exibir o código para um controle no IDE em tempo de design, o Visual Studio adiciona um método manipulador de eventos para o controle se um não estiver presente. Por exemplo, quando você clica duas vezes em um botão, o IDE adiciona um manipulador de eventos para seu evento Clicar (que é chamado sempre que o usuário escolhe o botão). Quando você clica duas vezes em uma caixa de seleção, o IDE adiciona um manipulador de eventos para o evento CheckedChanged (que é chamado sempre que o usuário seleciona ou desmarca a caixa).  
  
     Após adicionar um manipulador de eventos para um controle, você pode retornar a ele a qualquer momento do Designer de Formulários do Windows clicando duas vezes no controle ou na barra de menus, selecionando **Modo de Exibição**, **Código**.  
  
     Os nomes são importantes quando você cria programas e métodos (incluindo manipuladores de eventos) podem ter qualquer nome que você desejar. Quando você adiciona um manipulador de eventos com o IDE, cria um nome com base no nome do controle e do evento que está sendo tratado. Por exemplo, o evento Click de um botão chamado **showButton** é chamado de o método manipulador de eventos de `showButton_Click()`. Além disso, os parênteses de abertura e fechamento () são adicionados geralmente após o nome do método para indicar que os métodos estão sendo discutidos. Se você decidir que deseja alterar um nome de variável de código, clique com o botão direito do mouse na variável no código e então escolha **Refatorar**, **Renomear**. Todas as instâncias desta variável no código são renomeadas. Ver [refatoração de renomeação (c#)](../csharp-ide/rename-refactoring-csharp.md) ou [refatoração e renomear a caixa de diálogo](http://msdn.microsoft.com/library/001d2d81-9bb6-4e8e-ae3a-20c0daaa3959) para obter mais informações.  
  
### <a name="to-continue-or-review"></a>Para continuar ou revisar  
  
-   Para ir para a próxima etapa do tutorial, consulte [Etapa 7: adicionar componentes de diálogo ao formulário](../ide/step-7-add-dialog-components-to-your-form.md).  
  
-   Para retornar à etapa anterior do tutorial, consulte [Etapa 5: adicionar controles ao formulário](../ide/step-5-add-controls-to-your-form.md).



