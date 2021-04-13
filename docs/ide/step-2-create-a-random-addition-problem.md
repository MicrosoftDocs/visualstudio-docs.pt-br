---
title: 'Etapa 2: Criar um problema de adição aleatório'
description: Saiba como tornar o teste desafiador adicionando problemas de matemática que se baseiam em números aleatórios.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: 6461c4cf-f2aa-4bf5-91ed-06820a4f893d
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 13508845e2d1592715530c2961af3d1c114aea84
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107296522"
---
# <a name="step-2-create-a-random-addition-problem"></a>Etapa 2: Criar um problema de adição aleatório

Na segunda parte deste tutorial, você deixa o teste desafiador adicionando problemas de matemática baseados em números aleatórios. Você também cria um método que nomeado como `StartTheQuiz()` e que preenche os problemas e inicia o timer de contagem regressiva. Posteriormente neste tutorial, você adicionará problemas de subtração, multiplicação, e de divisão.

> [!NOTE]
> Esse tópico faz parte de uma série de tutoriais sobre conceitos de codificação básica. Para obter uma visão geral do tutorial, consulte [tutorial 2: criar um teste de matemática cronometrado](../ide/tutorial-2-create-a-timed-math-quiz.md).

## <a name="to-create-a-random-addition-problem"></a>Para criar um problema aleatório de adição

1. No designer de formulário, escolha o formulário (**Form1**).

2. Na barra de menus, escolha **Exibir**  >  **código**.

     *Form1.cs* ou *Form1.vb* aparecerá, dependendo da linguagem de programação que você estiver usando, para que você possa exibir o código do formulário.

3. Crie um objeto de <xref:System.Random> adicionando uma instrução de `new` próximo à parte superior do código, como a seguir.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step2/cs/form1.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step2/vb/form1.vb" id="Snippet1":::

     [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

     Você adicionou um objeto Random ao seu formulário e nomeou o objeto **randomizer**.

     `Random` é conhecido como um objeto. Provavelmente, você ouviu essa palavra antes e aprenderá mais sobre o significado de programação no tutorial seguir. Por enquanto, apenas lembre-se de que você pode usar instruções `new` para criar botões, rótulos, painéis, OpenFileDialogs, ColorDialogs, SoundPlayers, Randoms e até mesmo formulários, e esses itens são chamados de objetos. Quando você executa o programa, o formulário é iniciado, e o código por trás dele cria um objeto random e o nomeia como **randomizer**.

     Logo você irá criar um método para verificar as respostas, de modo que seu teste use variáveis para armazenar os números aleatórios que gera para cada problema. Consulte [Variáveis](/dotnet/visual-basic/programming-guide/language-features/variables/index) ou [Tipos](/dotnet/csharp/programming-guide/types/index). Para usar variáveis corretamente, você deve declará-los, o que significa listar seus nomes e tipos de data.

4. Adicione duas variáveis de inteiro ao formulário e nomeie-as **addend1** e **addend2**.

    > [!NOTE]
    > Uma variável inteira é conhecida como um int em C# ou como Integer no Visual Basic. Esse tipo de variável armazena um número positivo ou negativo de -2147483648 a 2147483647 e pode armazenar apenas números inteiros, não decimais.

     Use uma sintaxe semelhante para adicionar uma variável inteira como fez para adicionar o objeto random, desde que o código a seguir seja mostrado.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step2/cs/form1.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step2/vb/form1.vb" id="Snippet2":::

5. Adicione um método chamado `StartTheQuiz()` que usa o método <xref:System.Random.Next> do objeto Random para mostrar os números aleatórios nos rótulos. Por fim, o `StartTheQuiz()` preencherá todos os problemas e iniciar o temporizador, adicione um comentário. A função deve se parecer com o seguinte.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step2/cs/form1.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step2/vb/form1.vb" id="Snippet3":::

     Quando você digita o ponto (.) após `randomizer` no código, uma janela do IntelliSense é aberta e mostra todos os métodos do objeto Random que você pode chamar. Por exemplo, o IntelliSense lista o método `Next()`, como segue.

     ![Próximo método](../ide/media/express_randomwhite.png)<br/>
*Próximo método*

     Quando você inseri um ponto depois de um objeto, o IntelliSense exibe uma lista de membros do objeto, como propriedades, métodos e eventos.

    > [!NOTE]
    > Quando você usa o método de `Next()` com o objeto de `Random`, como quando você chama `randomizer.Next(50)`, você obtém um número aleatório que é menor que 50 (de 0 a 49). Nesse exemplo, você chamou `randomizer.Next(51)`. Você usou 51 e não 50, portanto os dois números aleatórios serão adicionados a uma resposta entre 0 e 100. Se você passar 50 para o método de `Next()`, ele escolherá um número de 0 a 49, para que a resposta possível mais alta seja 98, não 100. Após as duas primeiras instruções no método serem executadas, cada uma das duas variáveis inteiras, **addend1** e **addend2**, conterá um número aleatório de 0 a 50. Esta captura de tela mostra o código C#, mas o IntelliSense funciona da mesma maneira para Visual Basic.

     Confira de perto estas instruções.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step2/cs/form1.cs" id="Snippet18":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step2/vb/form1.vb" id="Snippet18":::

     As instruções definem propriedades **Text** de **plusLeftLabel** e **plusRightLabel** de modo que elas exibam os dois números aleatórios. Você deve usar o método de `ToString()` inteiro para converter números para texto. (Na programação, a cadeia de caracteres significa o texto. Os controles de rótulo exibem apenas texto, não números.

6. Na janela de design, clique duas vezes no botão **Iniciar** ou selecione-o e pressione a tecla **Enter**.

     Quando um participante de teste escolhe esse botão, o teste deve iniciar, e você acabou de adicionar um manipulador de eventos de clique para implementar esse comportamento.

7. Adicione as duas instruções a seguir.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step2/cs/form1.cs" id="Snippet4":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step2/vb/form1.vb" id="Snippet4":::

     A primeira instrução chama o novo método de `StartTheQuiz()`. A segunda instrução define a propriedade de **Enabled** do controle **startButton** para **False** de modo que a pessoa realizando o teste não pode escolher o botão durante um teste.

8. Salve seu código, execute-o e então escolha o botão **Iniciar**.

     Um problema de adição aleatória é exibido, conforme mostrado na captura de tela a seguir.

     ![Problema aleatório de adição](../ide/media/express_additionproblem.png)<br/>
*Problema aleatório de adição*

     Na próxima etapa do tutorial, você adicionará o resultado.

## <a name="to-continue-or-review"></a>Para continuar ou revisar

- Para ir para a próxima etapa do tutorial, consulte **[etapa 3: adicionar um temporizador de contagem regressiva](../ide/step-3-add-a-countdown-timer.md)**.

- Para retornar à etapa anterior do tutorial, veja [Etapa 1: Criar um projeto e adicionar rótulos ao formulário](../ide/step-1-create-a-project-and-add-labels-to-your-form.md).
