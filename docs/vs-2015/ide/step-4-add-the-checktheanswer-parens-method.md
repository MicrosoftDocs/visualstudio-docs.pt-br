---
title: 'Etapa 4: adicionar o método CheckTheAnswer() | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c66f3831-b4a0-40bc-a109-8f46f4db35ed
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: cf3f58e9d597af067db9e5d3037a78572a1528ef
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49181099"
---
# <a name="step-4-add-the-checktheanswer-method"></a>Etapa 4: Adicionar o método CheckTheAnswer()
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Na primeira parte deste tutorial, você irá escrever um método, `CheckTheAnswer()`, que determina se as respostas para os problemas de matemática estão corretas. Esse tópico faz parte de uma série de tutoriais sobre conceitos de codificação básica. Para obter uma visão geral do tutorial, consulte [Tutorial 2: criar um teste de matemática temporizado](../ide/tutorial-2-create-a-timed-math-quiz.md).  
  
> [!NOTE]
>  Se você estiver seguindo o Visual Basic, você usará a palavra-chave de `Function` em vez da palavra-chave comum de `Sub` porque esse método retorna um valor. É realmente simples: um sub não retorna um valor, mas uma função sim.  
  
### <a name="to-verify-whether-the-answers-are-correct"></a>Para verificar se as respostas estão corretas  
  
1.  Adicione o método `CheckTheAnswer()`.  
  
     Quando esse método é chamado, ele adiciona os valores de addend1 e addend2 e compara o resultado com o valor no controle `NumericUpDown` de soma. Se os valores forem iguais, o método retornará um valor de `true`. Caso contrário, o método retorna um valor de `false`. Seu código deve se parecer com o seguinte.  
  
     [!code-csharp[VbExpressTutorial3Step4#8](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step4/cs/form1.cs#8)]
     [!code-vb[VbExpressTutorial3Step4#8](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step4/vb/form1.vb#8)]  
  
     Em seguida, você irá verificar a resposta atualizando o código no método para o manipulador de eventos de escala do timer para chamar o novo método de `CheckTheAnswer()`.  
  
2.  Adicione o seguinte código à instrução `if else`.  
  
     [!code-csharp[VbExpressTutorial3Step4#10](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step4/cs/form1.cs#10)]
     [!code-vb[VbExpressTutorial3Step4#10](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step4/vb/form1.vb#10)]  
  
     Se a resposta estiver correta, `CheckTheAnswer()` retornará `true`. O manipulador de eventos para o temporizador, mostra uma mensagem congratulatória e disponibiliza novamente o botão **Iniciar**. Caso contrário, o teste continua.  
  
3.  Salve seu programa, execute-o, inicie um teste e forneça uma resposta correta ao problema de adição.  
  
    > [!NOTE]
    >  Ao inserir sua resposta, você deve ou selecione o valor padrão antes de começar a inserir sua resposta ou excluir o zero manualmente. Você corrigirá esse comportamento mais tarde neste tutorial.  
  
     Quando você fornece uma resposta correta, uma caixa de mensagem abre, o botão **Iniciar** fica disponível e o temporizador para.  
  
### <a name="to-continue-or-review"></a>Para continuar ou revisar  
  
-   Para ir para a próxima etapa do tutorial, consulte [Etapa 5: adicionar manipuladores de eventos Enter para os controles NumericUpDown](../ide/step-5-add-enter-event-handlers-for-the-numericupdown-controls.md).  
  
-   Para retornar à etapa anterior do tutorial, consulte [Etapa 3: adicionar um temporizador de contagem regressiva](../ide/step-3-add-a-countdown-timer.md).



