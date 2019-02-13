---
title: 'Etapa 3: Adicionar um temporizador de contagem regressiva | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 62670a2b-efdc-45c6-9646-9b17eeb33dcb
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 4440370453db96fa207c283e9c4a03b28d7ef6b7
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54775962"
---
# <a name="step-3-add-a-countdown-timer"></a>Etapa 3: Adicionar um temporizador de contagem regressiva
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Na terceira parte deste tutorial, você adicionará um timer de contagem regressiva para controlar o número de segundos restantes até o término do teste.  
  
> [!NOTE]
>  Esse tópico faz parte de uma série de tutoriais sobre conceitos de codificação básica. Para obter uma visão geral do tutorial, consulte [Tutorial 2: criar um teste de matemática temporizado](../ide/tutorial-2-create-a-timed-math-quiz.md).  
  
### <a name="to-add-a-countdown-timer"></a>Para adicionar um timer de contagem regressiva  
  
1.  Adicione uma variável de inteiro chamada **timeLeft**, exatamente como você fez no procedimento anterior. Seu código deve se parecer com o seguinte.  
  
     [!code-csharp[VbExpressTutorial3Step3#5](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs#5)]
     [!code-vb[VbExpressTutorial3Step3#5](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb#5)]  
  
     Agora você precisa de um método que realmente conte os segundos, assim como um timer, que gera um evento após a quantidade de tempo que você especificar.  
  
2.  Na janela de design, mova um controle de `Timer` da categoria **Componentes** da caixa de ferramentas para seu formulário.  
  
     O controle aparece na área cinza na parte inferior da janela de design.  
  
3.  No formulário, escolha o ícone **timer1** que você acabou de adicionar e defina sua propriedade **Interval** para **1000**.  
  
     Como o valor do intervalo é milissegundos, um valor de 1000 fará com que o evento de escala seja acionado a cada segundo.  
  
4.  No formulário, clique duas vezes no controle de timer, ou selecione-o e pressione a tecla Enter.  
  
     O editor de códigos aparece e exibe o método para a marcação que o manipulador de eventos que você adicionou.  
  
5.  Adicione as seguintes instruções ao novo método do manipulador de eventos.  
  
     [!code-csharp[VbExpressTutorial3Step3#6](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs#6)]
     [!code-vb[VbExpressTutorial3Step3#6](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb#6)]  
  
     Com base no que você adicionou, o temporizador verificará a cada segundo se o tempo limite foi ou não atingido determinando se a variável de inteiro **timeLeft** é ou não maior que 0. Se for, o tempo ainda permanece. Primeiro, o temporizador subtrai 1 de timeLeft e atualiza a propriedade **Text** do controle `timeLabel` para exibir quantos segundos restam à pessoa realizando o teste.  
  
     Se não houver nenhum tempo restante, o temporizador parará e alterará o texto do controle `timeLabel` de modo que ele exiba **Tempo esgotado!** Uma caixa de mensagem informa que o teste acabou, e a resposta é revelada, nesse caso, adicionando addend1 e addend2. A propriedade **Enabled** do controle `startButton` está definida como `true` de modo que a pessoa realizando o teste pode começar outro teste.  
  
     Você adicionou uma instrução de `if else`, que é como você informa os programas a tomar decisões. Uma instrução de `if else` se parece com o seguinte.  
  
    > [!NOTE]
    >  O exemplo a seguir é somente para ilustração - não o adicione a seu projeto.  
  
    ```vb  
    If (something that your program will check) Then  
        ' One or more statements that will run  
        ' if what the program checked is true.   
    Else  
        ' One or more statements that will run  
        ' if what the program checked is false.  
    End If  
    ```  
  
    ```csharp  
    if (something that your program will check)  
    {  
        // One or more statements that will run  
        // if what the program checked is true.   
    }  
    else  
    {  
        // One or more statements that will run  
        // if what the program checked is false.  
    }  
    ```  
  
     Examine atenciosamente a instrução que você adicionou no bloco de `else` para mostrar a resposta ao problema de adição.  
  
     [!code-csharp[VbExpressTutorial3Step3#24](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs#24)]
     [!code-vb[VbExpressTutorial3Step3#24](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb#24)]  
  
     A instrução `addend1 + addend2` adiciona os valores em duas variáveis juntas. A primeira parte (`sum.Value`) usa a propriedade **Value** do controle `NumericUpDown` da soma para exibir a resposta correta. Você usa a mesma propriedade posteriormente para verificar as respostas para o teste.  
  
     As pessoas realizando testes podem inserir números mais facilmente usando um controle `NumericUpDown`, que é o motivo pelo qual você usa um controle desse tipo para as respostas dos problemas matemáticos. Todas as respostas possíveis são números inteiros de 0 a 100. Deixando os valores padrão das propriedades de **Minimum**, **Maximum** e **DecimalPlaces**, você garante que as pessoas realizando testes não possam inserir decimais, números negativos ou números muito altos. (Se você quiser permitir que as pessoas realizando testes digitem 3,141 mas não 3,1415, você pode definir a propriedade **DecimalPlaces** para 3.)  
  
6.  Adicione três linhas ao final do método de `StartTheQuiz()`, para que o código se pareça com o seguinte.  
  
     [!code-csharp[VbExpressTutorial3Step3#7](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs#7)]
     [!code-vb[VbExpressTutorial3Step3#7](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb#7)]  
  
     Agora, quando seu teste for iniciado, a variável **timeLeft** será definida para 30 e a propriedade **Text** do controle `timeLabel` será definida para 30 segundos. Em seguida, o método `Start()` do controle `Timer` inicia a contagem regressiva. (O teste não verifica a resposta ainda, isso acontece em seguida.)  
  
7.  Salve seu programa, execute-o e então escolha o botão **Iniciar** no formulário.  
  
     O temporizador inicia a contagem regressiva. Quando o tempo se esgota, o teste termina e a resposta aparece. A ilustração a seguir mostra o teste em andamento.  
  
     ![Teste de matemática em andamento](../ide/media/express-addcountdown.png "Express_AddCountdown")  
Teste de matemática em andamento  
  
### <a name="to-continue-or-review"></a>Para continuar ou revisar  
  
-   Para ir para a próxima etapa do tutorial, veja [Etapa 4: adicionar o método CheckTheAnswer()](../ide/step-4-add-the-checktheanswer-parens-method.md).  
  
-   Para retornar à etapa anterior do tutorial, veja [Etapa 2: criar um problema de adição aleatório](../ide/step-2-create-a-random-addition-problem.md).
