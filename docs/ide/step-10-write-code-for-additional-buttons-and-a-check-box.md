---
title: Escrever código para botões adicionais e uma caixa de seleção
description: Saiba como escrever código para botões adicionais e uma caixa de seleção no tutorial criar um visualizador de imagem.
ms.date: 08/30/2019
ms.custom: SEO-VS-2020
ms.assetid: 185cf370-ab39-4ac0-b6bc-601d5b95a4a2
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 095c402b54e32dbd0839ff89def83d64d1522f4a
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107296554"
---
# <a name="step-10-write-code-for-additional-buttons-and-a-check-box"></a>Etapa 10: Escrever código para botões adicionais e uma caixa de seleção

Agora você está pronto para concluir os outros quatro métodos. Você pode copiar e colar esse código, mas se deseja saber a maioria deste tutorial, digite o código e use o IntelliSense.

Este código adiciona funcionalidades aos botões que você adicionou anteriormente. Sem esse código, os botões não fazem nada. Os botões usam o código em seus eventos de <xref:System.Windows.Forms.Control.Click> (e na caixa de seleção usa o evento de <xref:System.Windows.Forms.CheckBox.CheckedChanged>) para fazer coisas diferentes quando você ativa os controles. Por exemplo, o `clearButton_Click` evento ( `ClearButton_Click` ou), que é ativado quando você escolhe o **botão limpar imagem** , apaga a imagem atual definindo sua propriedade **Image** como **NULL** (ou, **Nothing**). Cada evento no código inclui comentários que explicam o que o código faz.

> [!TIP]
> Como prática recomendada: Comente sempre o seu código. Os comentários são informações para uma pessoa ler e vale a pena tornar seu código mais legível. Tudo em uma linha de comentário é ignorado pelo aplicativo. Em C#, você comenta uma linha digitando duas barras no início (//) e, em Visual Basic você comenta uma linha, começando com uma aspa simples (').

## <a name="how-to-write-code-for-additional-buttons-and-a-check-box"></a>Como escrever código para botões adicionais e uma caixa de seleção

Adicione o seguinte código ao seu arquivo de código **Form1** (*Form1.cs* ou *Form1.vb*).

  [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

  :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial1step9_10/cs/form1.cs" id="Snippet2":::

  :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial1step9_10/vb/form1.vb" id="Snippet2":::

> [!NOTE]
> Seu código pode não exibir as letras "camelCase".

## <a name="next-steps"></a>Próximas etapas

* Para ir para a próxima etapa do tutorial, consulte **[etapa 11: executar seu aplicativo e experimentar outros recursos](../ide/step-11-run-your-program-and-try-other-features.md)**.

* Para retornar à etapa anterior do tutorial, veja [Etapa 9: Revisar, comentar e testar o código](../ide/step-9-review-comment-and-test-your-code.md).

## <a name="see-also"></a>Confira também

* [Tutorial 2: criar um teste de matemática cronometrado](tutorial-2-create-a-timed-math-quiz.md)
* [Tutorial 3: criar um jogo de correspondência](tutorial-3-create-a-matching-game.md)
