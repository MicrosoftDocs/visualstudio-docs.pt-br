---
title: 'Etapa 11: Executar o programa e experimentar outros recursos'
ms.custom: ''
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-acquisition
ms.topic: conceptual
ms.assetid: 656614d0-4fe7-4a67-8edc-c10919377d09
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 87992bb8ab2557dbca4c8e7e3a94dd99e5de7682
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50671918"
---
# <a name="step-11-run-your-program-and-try-other-features"></a>Etapa 11: Executar o programa e experimentar outros recursos
O programa é concluído e pronto para ser executado. Você pode executar o programa e definir a cor do plano de fundo de <xref:System.Windows.Forms.PictureBox>. Para saber mais, tente melhorar o programa alterando a cor do formulário, personalizando os botões e a caixa de seleção, e modificando as propriedades do formulário.

 Para baixar uma versão concluída do exemplo, veja [Exemplo de tutorial completo do Visualizador de Imagens](https://code.msdn.microsoft.com/Complete-Picture-Viewer-7d91d3a8).

 ![link para vídeo](../data-tools/media/playvideo.gif)Para ver uma versão em vídeo deste tópico, confira [Tutorial 1: Criar um visualizador de imagens no Visual Basic – Vídeo 5](http://go.microsoft.com/fwlink/?LinkId=205216) ou [Tutorial 1: Criar um visualizador de imagens em C# – Vídeo 5](http://go.microsoft.com/fwlink/?LinkId=205206). Esses vídeos usam uma versão anterior do Visual Studio, portanto, existem pequenas diferenças em alguns comandos de menu e em outros elementos da interface do usuário. No entanto, os conceitos e procedimentos funcionam de maneiras semelhantes na versão atual do Visual Studio.

## <a name="to-run-your-program-and-set-the-background-color"></a>Para executar o programa e definir a cor do plano de fundo

1.  Selecione **F5** ou, na barra de menus, selecione **Depurar** > **Iniciar Depuração**.

2.  Antes de abrir uma imagem, clique no botão **Definir a cor da tela de fundo**. A caixa de diálogo **Cor** é aberta.

     ![Caixa de diálogo Cor](../ide/media/express_colordialog.png)
Caixa de diálogo **Cor**

3.  Escolha uma cor para definir a cor do plano de fundo de PictureBox. Examine cuidadosamente o método `backgroundButton_Click()` para compreender como ele funciona.

    > [!NOTE]
    >  Você pode carregar uma imagem da Internet colando sua URL na caixa de diálogo **Abrir Arquivo**. Tente localizar uma imagem com um plano de fundo transparente, para que sua cor do plano de fundo seja exibida.

4.  Escolha o botão **Limpar a imagem** para certificar-se de que ela desaparece. Em seguida, sai do programa escolhendo o botão **Fechar**.

## <a name="to-try-other-features"></a>Para testar outros recursos

-   Altere a cor do formulário e os botões usando a propriedade **BackColor**.

-   Personalize seus botões e sua caixa de seleção usando as propriedades **Font** e **ForeColor**.

-   Altere as propriedades **FormBorderStyle** e **ControlBox** do formulário.

-   Use as propriedades **AcceptButton** e **CancelButton** do formulário de modo que os botões sejam escolhidos automaticamente quando o usuário escolher as teclas **Enter** ou **Esc**. Faça o programa abrir a caixa de diálogo **Abrir Arquivo** quando o usuário escolher **Enter** e fechar a caixa quando o usuário escolher **Esc**.

## <a name="to-continue-or-review"></a>Para continuar ou revisar

-   Para aprender sobre programação no Visual Studio, veja [Conceitos de programação](https://msdn.microsoft.com/Library/65c12cca-af4f-4017-886e-2dbc00a189d6).

-   Para saber mais sobre o Visual Basic, veja [Desenvolver aplicativos com o Visual Basic](/dotnet/visual-basic/developing-apps/index).

-   Para saber mais sobre o Visual [Introdução à linguagem C# e ao .NET Framework](/dotnet/csharp/getting-started/introduction-to-the-csharp-language-and-the-net-framework).

-   Para ir para o próximo tutorial, veja [Tutorial 2: Criar um teste de matemática temporizado](../ide/tutorial-2-create-a-timed-math-quiz.md).

-   Para retornar à etapa anterior do tutorial, veja [Etapa 10: Escrever código para botões adicionais e uma caixa de seleção](../ide/step-10-write-code-for-additional-buttons-and-a-check-box.md).
