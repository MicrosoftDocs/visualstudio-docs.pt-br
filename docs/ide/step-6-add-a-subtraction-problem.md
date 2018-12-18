---
title: 'Etapa 6: Adicionar um problema de subtração'
ms.custom: ''
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-acquisition
ms.topic: conceptual
ms.assetid: 59204ef9-24bd-4f81-b85f-e3168e518a3e
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6960f7ca6db9584af8d43b9cee0d0c6bc810bc7f
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34747887"
---
# <a name="step-6-add-a-subtraction-problem"></a>Etapa 6: Adicionar um problema de subtração
Na sexta parte deste tutorial, você adicionará um problema de subtração e aprenderá a executar as seguintes tarefas:

-   Armazenar os valores de subtração.

-   Gere números aleatórios para o problema (e certifique-se de que a resposta esteja entre 0 e 100).

-   Atualize o método que verifica as respostas de modo que verifique também o novo problema se subtração.

-   Atualize o manipulador de eventos de escala do temporizador <xref:System.Windows.Forms.Timer.Tick> de modo que ele preencha a resposta correta quando o tempo de execução se esgotar.

## <a name="to-add-a-subtraction-problem"></a>Para adicionar um problema de subtração

1.  Adicione duas variáveis inteiras para o problema de subtração ao formulário, entre as variáveis inteiras para o problema de adição e o timer. O código deve se parecer com o seguinte.

     [!code-vb[VbExpressTutorial3Step5_6#12](../ide/codesnippet/VisualBasic/step-6-add-a-subtraction-problem_1.vb)]
     [!code-csharp[VbExpressTutorial3Step5_6#12](../ide/codesnippet/CSharp/step-6-add-a-subtraction-problem_1.cs)]

     Os nomes das novas variáveis de inteiro — **minuendo** e **subtraendo** — não são termos de programação. São os nomes tradicionais em aritmética para o número sendo subtraído (o subtraendo) e o número de que o subtraendo está sendo subtraído (o minuendo). A diferença é o minuendo menos o subtraendo. É possível usar outros nomes, pois seu programa não exige nomes específicos para variáveis, controles, componentes ou métodos. Você deve seguir as regras como não iniciar nomes com os dígitos, mas geralmente é possível usar nomes como x1, x2, x3 e x4. No entanto, os nomes genéricos dificultam a leitura do código e tornam os problemas quase impossíveis de rastrear. Para manter nomes de variável exclusivas e úteis, você usará os nomes tradicionais para multiplicação (multiplicando x multiplicador = produto) e a divisão (dividendo ÷ divisor = quociente) posteriormente neste tutorial.

     Em seguida, você modificará o método de `StartTheQuiz()` para fornecer valores aleatórios para o problema de subtração.

2.  Adicione o seguinte código após o comentário "Preencha o problema de subtração".

     [!code-vb[VbExpressTutorial3Step5_6#13](../ide/codesnippet/VisualBasic/step-6-add-a-subtraction-problem_2.vb)]
     [!code-csharp[VbExpressTutorial3Step5_6#13](../ide/codesnippet/CSharp/step-6-add-a-subtraction-problem_2.cs)]

     Para evitar respostas negativas para o problema de subtração, esse código usa o método de <xref:System.Random.Next> da classe <xref:System.Random> de forma um pouco diferente de do problema de adição. Quando você fornece dois valores do método de `Next()`, ele escolhe um número aleatório maior ou igual ao primeiro valor e menor que o segundo. O código a seguir escolhe um número aleatório de 1 a 100 e o armazena na variável de minuendo.

     [!code-vb[VbExpressTutorial3Step5_6#21](../ide/codesnippet/VisualBasic/step-6-add-a-subtraction-problem_3.vb)]
     [!code-csharp[VbExpressTutorial3Step5_6#21](../ide/codesnippet/CSharp/step-6-add-a-subtraction-problem_3.cs)]

     Você pode chamar o método de `Next()` da classe Random, que você nomeou como "randomizer" anteriormente neste tutorial, de várias maneiras. Os métodos que você pode chamar em mais de uma maneira são conhecidos como sobrecarregados, e você pode usar o IntelliSense para explorá-los. Procure novamente na dica de ferramenta da janela do IntelliSense pelo método de `Next()`.

     ![Dica de ferramenta de janela do IntelliSense](../ide/media/express_overloads.png)
Dica de ferramenta de janela do**IntelliSense**

     A dica de ferramenta exibe **(+ 2 sobrecarga(s))**, o que significa que você pode chamar o método `Next()` de outras duas maneiras. As sobrecargas contêm números ou tipos diferentes de argumentos, para que funcionem ligeiramente diferentes um do outro. Por exemplo, um método pode levar um único argumento inteiro e uma de suas sobrecargas pode levar um inteiro e uma cadeia de caracteres. Você escolhe a sobrecarga correta com base no que você deseja fazer. Quando você adiciona código ao método de `StartTheQuiz()`, mais informações aparecem na janela do IntelliSense para você inserir `randomizer.Next(`. Para percorrer as sobrecargas, escolha as teclas de **seta para cima** e **seta para baixo** como mostrado na ilustração a seguir:

     ![Sobrecarga para o método Next&#40;&#41; no IntelliSense](../ide/media/express_nextoverload.png) Sobrecarga para o método **Next()** no **IntelliSense**

     Nesse caso, você deseja escolher a última sobrecarga, porque você pode especificar valores mínimo e máximo.

3.  Modifique o método de `CheckTheAnswer()` para verificar a resposta correta da subtração.

     [!code-vb[VbExpressTutorial3Step5_6#14](../ide/codesnippet/VisualBasic/step-6-add-a-subtraction-problem_4.vb)]
     [!code-csharp[VbExpressTutorial3Step5_6#14](../ide/codesnippet/CSharp/step-6-add-a-subtraction-problem_4.cs)]

     No Visual C#, `&&` é o operador `logical and`. No Visual Basic, o operador equivalente é `AndAlso`. Esses operadores indicam "Se a soma da addend1 e addend2 for igual ao valor da soma NumericUpDown e o minuendo menos o subtraendo for igual ao valor da diferença NumericUpDown". O `CheckTheAnswer()` método retorna `true` somente se as respostas para os problemas de adição e subtração estiverem corretas.

4.  Substitua a parte mais recente do manipulador de eventos de escala do timer pelo código a seguir, de modo que preencha a resposta correta quando o tempo de execução se esgotar.

     [!code-vb[VbExpressTutorial3Step5_6#22](../ide/codesnippet/VisualBasic/step-6-add-a-subtraction-problem_5.vb)]
     [!code-csharp[VbExpressTutorial3Step5_6#22](../ide/codesnippet/CSharp/step-6-add-a-subtraction-problem_5.cs)]

5.  Salve e execute seu código.

     Seu programa inclui um problema de subtração, como mostra a ilustração a seguir:

     ![Teste de matemática com problema de subtração](../ide/media/express_addsubtract.png)
**Tste de matemática** com problema de subtração

## <a name="to-continue-or-review"></a>Para continuar ou revisar

-   Para ir para a próxima etapa do tutorial, veja [Etapa 7: Adicionar problemas de multiplicação e divisão](../ide/step-7-add-multiplication-and-division-problems.md).

-   Para retornar à etapa anterior do tutorial, veja [Etapa 5: Adicionar manipuladores de eventos Enter para os controles NumericUpDown](../ide/step-5-add-enter-event-handlers-for-the-numericupdown-controls.md).
