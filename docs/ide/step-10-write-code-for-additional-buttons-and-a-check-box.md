---
title: 'Etapa 10: Escrever código para botões adicionais e uma caixa de seleção'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- csharp
- vb
ms.assetid: 185cf370-ab39-4ac0-b6bc-601d5b95a4a2
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5db017ac20c84b8d06832a9b40f98c6519842361
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68918872"
---
# <a name="step-10-write-code-for-additional-buttons-and-a-check-box"></a>Etapa 10: Escrever código para botões adicionais e uma caixa de seleção
Agora você está pronto para concluir os outros quatro métodos. Você pode copiar e colar esse código, mas se deseja saber a maioria deste tutorial, digite o código e use o IntelliSense.

Este código adiciona funcionalidades aos botões que você adicionou anteriormente. Sem esse código, os botões não fazem nada. Os botões usam o código em seus eventos de <xref:System.Windows.Forms.Control.Click> (e na caixa de seleção usa o evento de <xref:System.Windows.Forms.CheckBox.CheckedChanged>) para fazer coisas diferentes quando você ativa os controles. Por exemplo, o evento `clearButton_Click`, que é ativado quando você escolhe o botão **Limpar a imagem**, apaga a imagem atual configurando sua propriedade **Image** como **null** (ou **nothing**). Cada evento no código inclui comentários que explicam o que o código faz.

![link para vídeo](../data-tools/media/playvideo.gif) Para obter uma versão em vídeo deste tópico, confira [Tutorial 1: Criar um visualizador de imagens no Visual Basic – Vídeo 5](http://go.microsoft.com/fwlink/?LinkId=205216) ou [Tutorial 1: Criar um visualizador de imagens em C# – Vídeo 5](http://go.microsoft.com/fwlink/?LinkId=205206). Esses vídeos usam uma versão anterior do Visual Studio, portanto, existem pequenas diferenças em alguns comandos de menu e em outros elementos da interface do usuário. No entanto, os conceitos e procedimentos funcionam de maneiras semelhantes na versão atual do Visual Studio.

> [!NOTE]
> Como uma melhor prática: Sempre comente o seu código. Os comentários são informações para uma pessoa ler e vale a pena tornar seu código mais legível. Todo em uma linha de comentário será ignorado pelo programa. No Visual C#, você comenta uma linha digitando duas barras no início (//) e no Visual Basic, você comenta uma linha iniciando-a com aspas simples (').

## <a name="to-write-code-for-additional-buttons-and-a-check-box"></a>Para escrever códigos para botões adicionais e uma caixa de seleção

- Adicione o seguinte código ao seu arquivo de código **Form1** (*Form1.cs* ou *Form1.vb*). Escolha a guia **VB** para exibir o código do Visual Basic.

     [!code-vb[VbExpressTutorial1Step9_10#2](../ide/codesnippet/VisualBasic/step-10-write-code-for-additional-buttons-and-a-check-box_1.vb)]
     [!code-csharp[VbExpressTutorial1Step9_10#2](../ide/codesnippet/CSharp/step-10-write-code-for-additional-buttons-and-a-check-box_1.cs)]

## <a name="to-continue-or-review"></a>Para continuar ou revisar

- Para ir para a próxima etapa do tutorial, confira [Etapa 11: Executar o programa e experimentar outros recursos](../ide/step-11-run-your-program-and-try-other-features.md).

- Para retornar à etapa anterior do tutorial, confira [Etapa 9: Examinar, comentar e testar o código](../ide/step-9-review-comment-and-test-your-code.md).
