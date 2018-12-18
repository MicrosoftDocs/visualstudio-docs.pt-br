---
title: 'Etapa 7: Adicionar problemas de multiplicação e divisão'
ms.custom: ''
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-acquisition
ms.topic: conceptual
ms.assetid: e638959e-f6a4-4eb4-b2e9-f63b7855cf8f
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0186ba637bdb1bc85a7ff60f23c9799972b6a931
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34747900"
---
# <a name="step-7-add-multiplication-and-division-problems"></a>Etapa 7: Adicionar problemas de multiplicação e divisão
Na sétima parte deste tutorial, você adicionará problemas de multiplicação e de divisão, mas primeiro pense em como fazer essa alteração. Considere a etapa inicial, que envolve armazenar valores.

## <a name="to-add-multiplication-and-division-problems"></a>Para adicionar problemas de multiplicação e de divisão

1.  Adicione mais quatro variáveis inteiras ao formulário.

     [!code-vb[VbExpressTutorial3Step7#15](../ide/codesnippet/VisualBasic/step-7-add-multiplication-and-division-problems_1.vb)]
     [!code-csharp[VbExpressTutorial3Step7#15](../ide/codesnippet/CSharp/step-7-add-multiplication-and-division-problems_1.cs)]

2.  Como você fez antes, modifique o método de `StartTheQuiz()` para preencher números aleatórios para os problemas de multiplicação e de divisão.

     [!code-vb[VbExpressTutorial3Step7#16](../ide/codesnippet/VisualBasic/step-7-add-multiplication-and-division-problems_2.vb)]
     [!code-csharp[VbExpressTutorial3Step7#16](../ide/codesnippet/CSharp/step-7-add-multiplication-and-division-problems_2.cs)]

3.  Modifique o método de `CheckTheAnswer()` de modo que ele também verifique os problemas de multiplicação e de divisão.

     [!code-vb[VbExpressTutorial3Step7#17](../ide/codesnippet/VisualBasic/step-7-add-multiplication-and-division-problems_3.vb)]
     [!code-csharp[VbExpressTutorial3Step7#17](../ide/codesnippet/CSharp/step-7-add-multiplication-and-division-problems_3.cs)]

     Não é possível inserir facilmente o sinal de multiplicação (×) e o sinal de divisão (÷) usando o teclado, então o Visual C# e o Visual Basic aceitam um asterisco (*) para multiplicação e uma barra (/) para divisão.

4.  Altere a parte a mais recente do manipulador de eventos de escala <xref:System.Windows.Forms.Timer.Tick> do timer de modo que preencha a resposta correta quando o tempo de execução se esgotar.

     [!code-vb[VbExpressTutorial3Step7#23](../ide/codesnippet/VisualBasic/step-7-add-multiplication-and-division-problems_4.vb)]
     [!code-csharp[VbExpressTutorial3Step7#23](../ide/codesnippet/CSharp/step-7-add-multiplication-and-division-problems_4.cs)]

5.  Salve e execute seu programa.

     Os participantes de teste devem responder quatro problemas para concluir o teste, conforme mostrado na ilustração.

     ![Teste de matemática com quatro problemas](../ide/media/express_finishedquiz.png)
**Teste de matemática** com quatro problemas

## <a name="to-continue-or-review"></a>Para continuar ou revisar

-   Para ir para a próxima etapa do tutorial, veja [Etapa 8: Personalizar o teste](../ide/step-8-customize-the-quiz.md).

-   Para retornar à etapa anterior do tutorial, veja [Etapa 6: Adicionar um problema de subtração](../ide/step-6-add-a-subtraction-problem.md).
