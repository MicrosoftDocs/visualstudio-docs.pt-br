---
title: 'Etapa 6: Nomear os controles de botão'
ms.custom: ''
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-acquisition
ms.topic: conceptual
ms.assetid: 56b3baa3-651e-4ad4-8942-e334c5c57158
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b11bace93efc253ffcb0f8d2b97ecc57c7462bb8
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34748391"
---
# <a name="step-6-name-your-button-controls"></a>Etapa 6: Nomear os controles de botão
Há apenas uma <xref:System.Windows.Forms.PictureBox> em seu formulário. Quando você a adicionou, o IDE a nomeou automaticamente como **pictureBox1**. Há apenas uma <xref:System.Windows.Forms.CheckBox>, que é denominada **checkBox1**. Em breve, você escreverá alguns códigos, e tais códigos se referirão à CheckBox e à PictureBox. Como há apenas um de cada desses controles, você saberá o que significa ver **pictureBox1** ou **checkBox1** em seu código.

> [!NOTE]
>  No Visual Basic, a primeira letra padrão de qualquer nome de controle é uma maiúscula inicial e, portanto, os nomes são **PictureBox1**, **CheckBox1** e assim por diante.

 Há quatro botões no formulário e o IDE os nomeou **button1**, **button2**, **button3** e **button4**. Apenas olhando seus nomes atuais, você não consegue saber qual botão é o botão de **Fechar** e qual é o botão **Mostrar uma imagem**. É por isso que é útil atribuir nomes mais informativos aos controles de botão.

 ![link para vídeo](../data-tools/media/playvideo.gif)Para ver uma versão em vídeo deste tópico, confira [Tutorial 1: Criar um visualizador de imagens no Visual Basic – Vídeo 3](http://go.microsoft.com/fwlink/?LinkId=205213) ou [Tutorial 1: Criar um visualizador de imagens em C# – Vídeo 3](http://go.microsoft.com/fwlink/?LinkId=205202). Esses vídeos usam uma versão anterior do Visual Studio, portanto, existem pequenas diferenças em alguns comandos de menu e em outros elementos da interface do usuário. No entanto, os conceitos e procedimentos funcionam de maneiras semelhantes na versão atual do Visual Studio.

## <a name="to-name-your-button-controls"></a>Para nomear os controles de botão

1.  No formulário, clique no botão **Fechar**. (Se você ainda tiver todos os botões selecionados, pressione a tecla **Esc** para cancelar a seleção). Role pela janela **Propriedades**, até ver a propriedade **(Name)**. (A propriedade **(Name)** fica próxima à parte superior quando as propriedades são alfabéticas.) Altere o nome para **closeButton**, conforme mostrado na imagem a seguir.

     ![Janela Propriedades com nome closeButton](../ide/media/express_setnameproperty.png)
Janela **Propriedades** com nome **closeButton**

    > [!NOTE]
    >  Se você tentar alterar o nome do botão para **closeButton**, com um espaço entre as palavras close e Button, o IDE exibirá uma mensagem de erro: "O valor da propriedade não é válido." Espaços (e mais alguns caracteres) não são permitidos em nomes de controle.

2.  Renomeie os outros três botões para **backgroundButton**, **clearButton** e **showButton**. Você pode verificar os nomes escolhendo a lista suspensa seletora de controle na janela **Propriedades**. Os nomes dos novos botões aparecem.

3.  Clique duas vezes no botão **Mostrar uma imagem** no formulário. Como alternativa, escolha o botão **Mostrar uma imagem** no formulário e, em seguida, pressione a tecla **Enter**. Quando você fizer isso, o IDE abrirá uma guia adicional na janela principal chamada **Form1.cs** (**Form1.vb** se você estiver usando Visual Basic). Esta guia mostra o arquivo de código por trás do formulário, conforme mostrado na seguinte imagem.

     ![Guia Form1.cs com código do Visual C&#35;](../ide/media/express_showbuttoncode.png)
Guia **Form1.cs** com código do Visual C#

4.  Foco nesta parte do código. (Escolha a guia **VB** abaixo se você estiver usando o Visual Basic para exibir a versão de Visual Basic do código.)

     [!code-vb[VbExpressTutorial1Step6#1](../ide/codesnippet/VisualBasic/step-6-name-your-button-controls_1.vb)]
     [!code-csharp[VbExpressTutorial1Step6#1](../ide/codesnippet/CSharp/step-6-name-your-button-controls_1.cs)]

     Você está examinando um código chamado `showButton_Click()`. O IDE adicionou isto ao código do formulário quando você abriu o arquivo de código para o botão **showButton**. No tempo de design, quando você abre o arquivo de código para um controle em um formulário, o código é gerado para o controle se ainda não existir. Esse código, conhecido como *método*, é executado quando você executa seu programa e escolhe o controle – nesse caso, o botão **Mostrar uma imagem**.

    > [!NOTE]
    >  Neste tutorial, o código do Visual Basic que é gerado automaticamente foi simplificado por meio da remoção de tudo entre os parênteses, `()`. Sempre que isso ocorre, você pode remover o mesmo código. Seu programa irá trabalhar de qualquer maneira. Para o restante dos tutoriais, qualquer código automaticamente gerado será simplificado sempre que possível.

5.  Escolha a guia **Designer de Formulários do Windows** novamente (**Form1.cs [Design]** no Visual C#, **Form1.vb [Design]** no Visual Basic) e abra o arquivo de código do botão **Limpar a imagem** para criar um método para ele no código do formulário. Repita isso para os dois botões restantes. A cada vez, o IDE adiciona um novo método ao arquivo de código do formulário.

6.  Para adicionar mais um método, abra o arquivo de código para o controle **CheckBox** no **Designer de Formulários do Windows** para fazer o IDE adicionar um método `checkBox1_CheckedChanged()`. Esse método é chamado sempre que o usuário seleciona ou desmarca a caixa de seleção.

    > [!NOTE]
    >  Ao trabalhar em um programa, você geralmente se movimenta entre o editor de códigos e o **Designer de Formulários do Windows**. O IDE torna fácil a navegação no projeto. Use o **Gerenciador de Soluções** para abrir o **Designer de Formulários do Windows** clicando duas vezes em *Form1.cs* no Visual C# ou *Form1.vb* no Visual Basic ou na barra de menus, escolha **Exibir** > **Designer**.

     A seguir temos o novo código que você vê no editor de códigos.

     [!code-vb[VbExpressTutorial1Step6#2](../ide/codesnippet/VisualBasic/step-6-name-your-button-controls_2.vb)]
     [!code-csharp[VbExpressTutorial1Step6#2](../ide/codesnippet/CSharp/step-6-name-your-button-controls_2.cs)]

     Os cinco métodos que você adicionou são chamados *manipuladores de eventos* porque seu programa os chama sempre que um evento (como um usuário que escolhe um botão ou que seleciona uma caixa) acontece.

     Ao exibir o código para um controle no IDE em tempo de design, o Visual Studio adiciona um método manipulador de eventos para o controle se um não estiver presente. Por exemplo, quando você clica duas vezes em um botão, o IDE adiciona um manipulador de eventos para seu evento <xref:System.Windows.Forms.Control.Click> (que é chamado sempre que o usuário escolhe o botão). Quando você clica duas vezes em uma caixa de seleção, o IDE adiciona um manipulador de eventos para o evento <xref:System.Windows.Forms.CheckBox.CheckedChanged> (que é chamado sempre que o usuário seleciona ou desmarca a caixa).

     Após adicionar um manipulador de eventos para um controle, você pode retornar a ele a qualquer momento do **Designer de Formulários do Windows** clicando duas vezes no controle ou na barra de menus, selecionando **Exibir** > **Código**.

     Os nomes são importantes quando você cria programas e métodos (incluindo manipuladores de eventos) podem ter qualquer nome que você desejar. Quando você adiciona um manipulador de eventos com o IDE, cria um nome com base no nome do controle e do evento que está sendo tratado. Por exemplo, o evento Click de um botão chamado **showButton** é chamado de o método manipulador de eventos de `showButton_Click()`. Além disso, os parênteses de abertura e fechamento `()` são adicionados geralmente após o nome do método para indicar que os métodos estão sendo discutidos. Se você decidir que deseja alterar um nome de variável de código, clique com o botão direito do mouse na variável no código e então escolha **Refatorar** > **Renomear**. Todas as instâncias desta variável no código são renomeadas. Confira a [Refatoração Renomear](../ide/reference/rename.md) para obter mais informações.

## <a name="to-continue-or-review"></a>Para continuar ou revisar

-   Para ir para a próxima etapa do tutorial, veja [Etapa 7: Adicionar componentes de diálogo ao formulário](../ide/step-7-add-dialog-components-to-your-form.md).

-   Para retornar à etapa anterior do tutorial, veja [Etapa 5: Adicionar controles ao formulário](../ide/step-5-add-controls-to-your-form.md).
