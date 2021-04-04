---
title: 'Etapa 3: Adicionar um temporizador de contagem regressiva'
description: Saiba como adicionar um temporizador de contagem regressiva para acompanhar o número de segundos que permanecem para que o Secretário seja concluído.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: 62670a2b-efdc-45c6-9646-9b17eeb33dcb
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f64189cbde62ea70ae51fcdcbb8869377dd865f1
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106214298"
---
# <a name="step-3-add-a-countdown-timer"></a>Etapa 3: Adicionar um temporizador de contagem regressiva

Na terceira parte deste tutorial, você adicionará um timer de contagem regressiva para controlar o número de segundos restantes até o término do teste.

> [!NOTE]
> Esse tópico faz parte de uma série de tutoriais sobre conceitos de codificação básica. Para obter uma visão geral do tutorial, consulte [tutorial 2: criar um teste de matemática cronometrado](../ide/tutorial-2-create-a-timed-math-quiz.md).

## <a name="to-add-a-countdown-timer"></a>Para adicionar um timer de contagem regressiva

1. Adicione uma variável de inteiro chamada **timeLeft**, exatamente como você fez no procedimento anterior. Seu código deve se parecer com o seguinte.

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb" id="Snippet5":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs" id="Snippet5":::

     [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

     Agora você precisa de um método que realmente conte os segundos, assim como um timer, que gera um evento após a quantidade de tempo que você especificar.

2. Na janela de design, mova um controle de <xref:System.Windows.Forms.Timer> da categoria **Componentes** da **caixa de ferramentas** para seu formulário.

     O controle aparece na área cinza na parte inferior da janela de design.

3. No formulário, escolha o ícone **timer1** que você acabou de adicionar e defina sua propriedade **Interval** para **1000**.

     Como o valor do intervalo é milissegundos, um valor de 1000 fará com que o evento de escala <xref:System.Windows.Forms.Timer.Tick> seja acionado a cada segundo.

4. No formulário, clique duas vezes no controle de **timer**, ou selecione-o e pressione a tecla **Enter**.

     O editor de códigos aparece e exibe o método para a marcação que o manipulador de eventos que você adicionou.

5. Adicione as seguintes instruções ao novo método do manipulador de eventos.

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb" id="Snippet6":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs" id="Snippet6":::

     Com base no que você adicionou, o temporizador verificará a cada segundo se o tempo limite foi ou não atingido determinando se a variável de inteiro **timeLeft** é ou não maior que 0. Se for, o tempo ainda permanece. Primeiro o temporizador subtrai 1 do timeLeft e atualiza a propriedade **Text** do controle **timeLabel** para exibir o comprador de teste quantos segundos restam.

     Se nenhuma hora permanecer, o timer para e altera o texto do controle de **timeLabel** de modo que mostre **Time's up!** Uma caixa de mensagem informa que o teste acabou, e a resposta é revelada, nesse caso, adicionando addend1 e addend2. A propriedade **Habilitado** do controle **startButton** está definida como **true** de modo que o comprador de teste possa começar outro teste.

     Você adicionou uma instrução de `if else`, que é como você informa os programas a tomar decisões. Uma instrução de `if else` se parece com o seguinte.

    > [!NOTE]
    > O exemplo a seguir é apenas para demonstração – não o adicione ao seu projeto.

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

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb" id="Snippet24":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs" id="Snippet24":::

     A instrução `addend1 + addend2` adiciona os valores em duas variáveis juntas. A primeira parte (`sum.Value`) usa a propriedade **Valor** do controle da soma NumericUpDown para exibir a resposta correta. Você usa a mesma propriedade posteriormente para verificar as respostas para o teste.

     As pessoas realizando testes podem inserir números mais facilmente usando um controle <xref:System.Windows.Forms.NumericUpDown>, que é o motivo pelo qual você usa um controle desse tipo para as respostas dos problemas matemáticos. Todas as respostas possíveis são números inteiros de 0 a 100. Deixando os valores padrão das propriedades de **Minimum**, **Maximum** e **DecimalPlaces**, você garante que as pessoas realizando testes não possam inserir decimais, números negativos ou números muito altos. (Se você quiser permitir que as pessoas realizando testes digitem 3,141 mas não 3,1415, você pode definir a propriedade **DecimalPlaces** para 3.)

6. Adicione três linhas ao final do método de `StartTheQuiz()`, para que o código se pareça com o seguinte.

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step3/vb/form1.vb" id="Snippet7":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step3/cs/form1.cs" id="Snippet7":::

     Agora, quando seu teste for iniciado, a variável de **timeLeft** será definida para 30 e a propriedade **Text** do controle de **timeLabel** será definida para 30 segundos. O método <xref:System.Windows.Forms.Timer.Start> de controle do Temporizador inicia a contagem regressiva. (O teste não verifica a resposta ainda, isso acontece em seguida.)

7. Salve seu programa, execute-o e então escolha o botão **Iniciar** no formulário.

     O temporizador inicia a contagem regressiva. Quando o tempo se esgota, o teste termina e a resposta aparece. A ilustração a seguir mostra o teste em andamento.

     ![Teste de matemática em andamento](../ide/media/express_addcountdown.png)<br/>
*Teste de matemática em andamento*

## <a name="to-continue-or-review"></a>Para continuar ou revisar

- Para ir para a próxima etapa do tutorial, consulte **[etapa 4: Adicionar o método CheckTheAnswer ()](../ide/step-4-add-the-checktheanswer-parens-method.md)**.

- Para retornar à etapa anterior do tutorial, veja [Etapa 2: Criar um problema de adição aleatório](../ide/step-2-create-a-random-addition-problem.md).
