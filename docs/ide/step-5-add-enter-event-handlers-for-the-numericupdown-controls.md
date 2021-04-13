---
title: Adicionar manipuladores de eventos de inserção aos controles NumericUpDown
description: Adicione manipuladores de eventos de entrada para controles NumericUpDown no tutorial criar um teste de matemática cronometrado.
ms.date: 11/04/2016
ms.custom: SEO-VS-2020
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: 45a99a5d-c881-4298-b74d-adb481dec5ee
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ef6207ebfa30401896a7681b599128cfb9648e96
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107296320"
---
# <a name="step-5-add-enter-event-handlers-for-the-numericupdown-controls"></a>Etapa 5: Adicionar manipuladores de eventos de inserção aos controles NumericUpDown

Na quinta parte deste tutorial, você adicionará manipuladores de eventos <xref:System.Windows.Forms.Control.Enter> para facilitar a inserção de respostas aos problemas do teste. Esse código selecionará e desmarcará o valor atual em cada controle <xref:System.Windows.Forms.NumericUpDown> para que o comprador de teste o escolha e comece a inserir um valor diferente.

> [!NOTE]
> Esse tópico faz parte de uma série de tutoriais sobre conceitos de codificação básica. Para obter uma visão geral do tutorial, consulte [tutorial 2: criar um teste de matemática cronometrado](../ide/tutorial-2-create-a-timed-math-quiz.md).

## <a name="to-verify-the-default-behavior"></a>Para verificar o comportamento padrão

1. Executar seu programa e iniciar o teste.

     No controle **NumericUpDown** para o problema de adição, o cursor pisca ao lado de **0** (zero).

2. Digite **3** e observe que o controle mostra **30**.

3. Digite **5** e observe que é exibido **350**, mas que esse valor é alterado para **100** após um segundo.

     Antes de corrigir esse problema, pense no que está acontecendo. Reflita sobre o motivo de **0** não ter desaparecido quando você inseriu **3** e como **350** foi alterado para **100**, mas não imediatamente.

     Esse comportamento pode parecer ímpar, mas faz sentido dada a lógica de código. Quando você escolhe o botão **Iniciar**, sua propriedade **Enabled** é definida como **False** e o botão aparece esmaecido e não disponível. Seu programa altera a seleção atual (foco) para o controle que tem o menor valor TabIndex a seguir, que é o controle NumericUpDown para o problema de adição. Quando você usa a tecla **Tab** para ir para um controle NumericUpDown, o cursor fica posicionado automaticamente no início do controle, por isso os números que você insere aparecem do lado esquerdo e não do lado direito. Quando você especifica um número maior que o valor da propriedade de **MaximumValue**, que é definida como 100, o número digitado é substituído pelo valor dessa propriedade.

## <a name="to-add-an-enter-event-handler-for-a-numericupdown-control"></a>Para adicionar um manipulador de eventos para inserir um controle NumericUpDown

1. Escolha o primeiro controle **NumericUpDown** (chamado "soma") no formulário e, em seguida, na caixa de diálogo **Propriedades**, escolha o ícone de **Eventos** na barra de ferramentas.

   ![Botão de eventos na barra de ferramentas de propriedades](media/control-properties-events.png)

   A guia **Eventos** na caixa de diálogo **Propriedades** exibe todos os eventos para os quais você pode responder (manipular) para o item que você escolher no formulário. Como você escolheu o controle NumericUpDown, todos os eventos listados serão pertinentes a ele.

2. Escolha o evento **Enter**, digite `answer_Enter` e pressione a tecla **Enter**.

   ![Nome do método do manipulador de eventos Enter](media/enter-event.png)

   Você adicionou um manipulador de eventos Enter para o controle NumericUpDown de soma e você nomeou esse manipulador **answer_Enter**.

3. No método para o manipulador de eventos **answer_Enter**, adicione o código a seguir:

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial3step5_6/vb/form1.vb" id="Snippet11":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial3step5_6/cs/form1.cs" id="Snippet11":::

     [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

     Este código pode parecer complexo, mas você pode entender se observar o passo a passo. Primeiro, olhe na parte superior de método: `object sender` no C# ou `sender As System.Object` no Visual Basic. Este parâmetro refere-se ao objeto cujo evento é acionando, que é conhecido como o remetente. Nesse caso, o objeto remetente é o controle NumericUpDown. Assim, na primeira linha do método, você especifica que o remetente não é apenas nenhum objeto genérico mas especificamente um controle NumericUpDown. (Cada controle NumericUpDown é um objeto, mas nem todo objeto é um controle NumericUpDown.) O controle NumericUpDown é nomeado **answerBox** neste método, porque ele será usado para todos os controles NumericUpDown no formulário, não apenas o controle Sum NumericUpDown. Como você declara a variável answerBox nesse método, seu escopo se aplica somente a este método. Ou seja, a variável pode ser usada somente dentro desse método.

     A próxima linha verifica se o answerBox foi convertido com êxito (conversão) de um objeto em um controle NumericUpDown. Se a conversão for malsucedida, a variável terá um valor de `null` (C#) ou de `Nothing` (Visual Basic). A terceira linha obtém o comprimento da resposta que aparece no controle NumericUpDown, e a quarta linha seleciona o valor atual no controle com base nesse comprimento. Agora, quando o comprador de teste escolher o controle, o Visual Studio aciona este evento, fazendo com que a resposta atual seja selecionada. Assim que o tomador de teste começa a inserir uma resposta diferente, a resposta anterior é apagada e substituída pela nova resposta.

4. No **Designer de Formulários do Windows**, escolha o controle **NumericUpDown** da diferença.

5. Na página **Eventos** da caixa de diálogo **Propriedades**, role para baixo até o evento **Enter**, escolha a seta suspensa no final da linha e, em seguida, escolha o manipulador de eventos `answer_Enter` que você acabou de adicionar.

6. Repita a etapa anterior para o produto e os controles NumericUpDown quocientes.

7. Salve seu programa e execute-o.

     Quando você escolhe um controle **NumericUpDown**, o valor existente é automaticamente selecionado e apagado quando você começa a inserir um valor diferente.

## <a name="to-continue-or-review"></a>Para continuar ou revisar

- Para ir para a próxima etapa do tutorial, consulte **[etapa 6: adicionar um problema de subtração](../ide/step-6-add-a-subtraction-problem.md)**.

- Para retornar à etapa anterior do tutorial, veja [Etapa 4: Adicionar o método CheckTheAnswer()](../ide/step-4-add-the-checktheanswer-parens-method.md).
