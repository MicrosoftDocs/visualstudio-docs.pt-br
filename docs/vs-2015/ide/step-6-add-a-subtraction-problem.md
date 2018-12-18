---
title: 'Etapa 6: adicionar um problema de subtração | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 59204ef9-24bd-4f81-b85f-e3168e518a3e
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 793204bf4a08d09d7ce6e48e37254dd311ac6a08
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49229236"
---
# <a name="step-6-add-a-subtraction-problem"></a>Etapa 6: Adicionar um problema de subtração
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Na sexta parte deste tutorial, você adicionará um problema de subtração e aprenderá a executar as seguintes tarefas:  
  
-   Armazenar os valores de subtração.  
  
-   Gere números aleatórios para o problema (e certifique-se de que a resposta esteja entre 0 e 100).  
  
-   Atualize o método que verifica as respostas de modo que verifique também o novo problema se subtração.  
  
-   Atualize o manipulador de eventos de escala do temporizador de modo que ele preencha a resposta correta quando o tempo de execução se esgotar.  
  
### <a name="to-add-a-subtraction-problem"></a>Para adicionar um problema de subtração  
  
1.  Adicione duas variáveis inteiras para o problema de subtração ao formulário, entre as variáveis inteiras para o problema de adição e o timer. O código deve se parecer com o seguinte.  
  
     [!code-csharp[VbExpressTutorial3Step5_6#12](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step5_6/cs/form1.cs#12)]
     [!code-vb[VbExpressTutorial3Step5_6#12](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step5_6/vb/form1.vb#12)]  
  
     Os nomes das novas variáveis de inteiro — **minuendo** e **subtraendo** — não são termos de programação. São os nomes tradicionais em aritmética para o número sendo subtraído (o subtraendo) e o número de que o subtraendo está sendo subtraído (o minuendo). A diferença é o minuendo menos o subtraendo. É possível usar outros nomes, pois seu programa não exige nomes específicos para variáveis, controles, componentes ou métodos. Você deve seguir as regras como não iniciar nomes com os dígitos, mas geralmente é possível usar nomes como x1, x2, x3 e x4. No entanto, os nomes genéricos dificultam a leitura do código e tornam os problemas quase impossíveis de rastrear. Para manter nomes de variável exclusivas e úteis, você usará os nomes tradicionais para multiplicação (multiplicando x multiplicador = produto) e a divisão (dividendo ÷ divisor = quociente) posteriormente neste tutorial.  
  
     Em seguida, você modificará o método de `StartTheQuiz()` para fornecer valores aleatórios para o problema de subtração.  
  
2.  Adicione o seguinte código após o comentário "Preencha o problema de subtração".  
  
     [!code-csharp[VbExpressTutorial3Step5_6#13](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step5_6/cs/form1.cs#13)]
     [!code-vb[VbExpressTutorial3Step5_6#13](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step5_6/vb/form1.vb#13)]  
  
     Para evitar respostas negativas para o problema de subtração, esse código usa o método de `Next()` da classe `Random` de forma um pouco diferente de do problema de adição. Quando você fornece dois valores do método de `Next()`, ele escolhe um número aleatório maior ou igual ao primeiro valor e menor que o segundo. O código a seguir escolhe um número aleatório de 1 a 100 e o armazena na variável de minuendo.  
  
     [!code-csharp[VbExpressTutorial3Step5_6#21](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step5_6/cs/form1.cs#21)]
     [!code-vb[VbExpressTutorial3Step5_6#21](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step5_6/vb/form1.vb#21)]  
  
     Você pode chamar o método de `Next()` da classe de `Random`, que você nomeou como "randomizer" anteriormente neste tutorial, de várias maneiras. Os métodos que você pode chamar em mais de uma maneira são conhecidos como sobrecarregados, e você pode usar o IntelliSense para explorá-los. Procure novamente na dica de ferramenta da janela do IntelliSense pelo método de `Next()`.  
  
     ![Dica de ferramenta da janela do IntelliSense](../ide/media/express-overloads.png "Express_Overloads")  
Dica de ferramenta da janela do Intellisense  
  
     A dica de ferramenta exibe **(+ 2 sobrecarga(s))**, o que significa que você pode chamar o método `Next()` de outras duas maneiras. As sobrecargas contêm números ou tipos diferentes de argumentos, para que funcionem ligeiramente diferentes um do outro. Por exemplo, um método pode levar um único argumento inteiro, enquanto uma de suas sobrecargas pode levar um inteiro e uma cadeia de caracteres. Você escolhe a sobrecarga correta com base no que você deseja fazer. Quando você adiciona código ao método de `StartTheQuiz()`, mais informações aparecem na janela do Intellisense para você inserir `randomizer.Next(`. Pressione as teclas de seta para cima e seta para baixo para percorrer as sobrecargas, como mostra a ilustração a seguir.  
  
     ![Sobrecarga para o método Next&#40;&#41; no IntelliSense](../ide/media/express-nextoverload.png "Express_NextOverload")  
Sobrecarga para o método Next() no IntelliSense  
  
     Nesse caso, você deseja escolher a última sobrecarga, porque você pode especificar valores mínimo e máximo.  
  
3.  Modifique o método de `CheckTheAnswer()` para verificar a resposta correta da subtração.  
  
     [!code-csharp[VbExpressTutorial3Step5_6#14](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step5_6/cs/form1.cs#14)]
     [!code-vb[VbExpressTutorial3Step5_6#14](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step5_6/vb/form1.vb#14)]  
  
     No Visual C#, `&&` é o operador `logical and`. No Visual Basic, o operador equivalente é `AndAlso`. Esses operadores indicam "Se a soma da addend1 e addend2 for igual ao valor da soma NumericUpDown e o minuendo menos o subtraendo for igual ao valor da diferença NumericUpDown". O `CheckTheAnswer()` método retorna `true` somente se as respostas para os problemas de adição e subtração estiverem corretas.  
  
4.  Substitua a parte mais recente do manipulador de eventos de escala do timer pelo código a seguir, de modo que preencha a resposta correta quando o tempo de execução se esgotar.  
  
     [!code-csharp[VbExpressTutorial3Step5_6#22](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step5_6/cs/form1.cs#22)]
     [!code-vb[VbExpressTutorial3Step5_6#22](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step5_6/vb/form1.vb#22)]  
  
5.  Salve e execute seu código.  
  
     Seu programa inclui um problema de subtração, como mostra a ilustração a seguir.  
  
     ![Teste de matemática com problema de subtração](../ide/media/express-addsubtract.png "Express_AddSubtract")  
Teste de matemática com problema de subtração  
  
### <a name="to-continue-or-review"></a>Para continuar ou revisar  
  
-   Para ir para a próxima etapa do tutorial, consulte [Etapa 7: adicionar problemas de multiplicação e divisão](../ide/step-7-add-multiplication-and-division-problems.md).  
  
-   Para retornar à etapa anterior do tutorial, consulte [Etapa 5: adicionar manipuladores de eventos Enter para os controles NumericUpDown](../ide/step-5-add-enter-event-handlers-for-the-numericupdown-controls.md).



