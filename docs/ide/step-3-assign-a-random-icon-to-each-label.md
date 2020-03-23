---
title: 'Etapa 3: Atribuir um ícone aleatório a cada rótulo'
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: 0ba5ed7a-9aaa-41f4-95d2-e3c2d567bc79
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 366f6d7a07d2f30b5b8110fb7dae7a2311fcce23
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2020
ms.locfileid: "77579402"
---
# <a name="step-3-assign-a-random-icon-to-each-label"></a>Etapa 3: Atribuir um ícone aleatório a cada rótulo

Se os ícones aparecerem nas mesmas células a cada jogo, ele não será muito desafiador. Para evitar isso, atribua os ícones aleatoriamente aos controles de rótulo no seu formulário usando um método `AssignIconsToSquares()`.

## <a name="to-assign-a-random-icon-to-each-label"></a>Para atribuir um ícone aleatório a cada rótulo

1. Antes de adicionar o código a seguir, considere como o método funciona. Há uma nova palavra-chave: `foreach` em `For Each` C# e no Visual Basic. (Uma das linhas é comentada intencionalmente, que é explicada no fim deste procedimento.)

     [!code-csharp[VbExpressTutorial4Step2_3_4#2](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_1.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#2](../ide/codesnippet/VisualBasic/step-3-assign-a-random-icon-to-each-label_1.vb)]

      > [!IMPORTANT]
      > Use o controle de linguagem de programação no canto superior direito desta página para exibir o trecho de código C# ou o trecho de código Visual Basic.<br><br>![Controle de linguagem de programação para Docs.Microsoft.com](../ide/media/docs-programming-language-control.png)

2. Adicione o método `AssignIconsToSquares()`, conforme mostrado na etapa anterior. Você pode colocá-lo logo abaixo do código adicionado na [Etapa 2: Adicionar um objeto aleatório e uma lista de ícones](../ide/step-2-add-a-random-object-and-a-list-of-icons.md).

     Como mencionado anteriormente, há algo `AssignIconsToSquares()` novo `foreach` em seu método: um loop em C# e `For Each` no Visual Basic. Você pode usar um loop `For Each` no momento em que desejar realizar a mesma ação várias vezes. Nesse caso, execute as mesmas instruções para cada rótulo no seu <xref:System.Windows.Forms.TableLayoutPanel>, conforme explicado pelo código a seguir. A primeira linha cria uma variável denominada `control` que armazena cada controle, um por vez, enquanto as instruções no loop são executadas nesse controle.

     [!code-csharp[VbExpressTutorial4Step2_3_4#14](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_2.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#14](../ide/codesnippet/VisualBasic/step-3-assign-a-random-icon-to-each-label_2.vb)]

    > [!NOTE]
    > Os nomes "iconLabel" e "control" são usados porque são descritivos. É possível substituir esses nomes por quaisquer nomes, e o código funcionará exatamente da mesma forma, desde que você altere o nome em cada instrução dentro do loop.

     O método `AssignIconsToSquares()` é iterado por meio de cada controle de rótulo no TableLayoutPanel e executa as mesmas instruções para cada um deles. Essas instruções extraem um ícone aleatório da lista que você adicionou na [Etapa 2: Adicionar um objeto aleatório e uma lista de ícones](../ide/step-2-add-a-random-object-and-a-list-of-icons.md). (Por esse motivo, você incluiu dois de cada ícone na lista, de modo que haverá um par de ícones atribuídos aos controles de rótulo aleatórios).

     Observe mais detalhadamente o código que é executado no loop `foreach` ou `For Each`. Esse código é reproduzido aqui.

     [!code-csharp[VbExpressTutorial4Step2_3_4#16](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_3.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#16](../ide/codesnippet/VisualBasic/step-3-assign-a-random-icon-to-each-label_3.vb)]

     A primeira linha converte a variável **control** em um rótulo denominado **iconLabel**. A linha que vem a seguir está uma instrução `if` que verifica se a conversão funcionou. Se a conversão realmente funcionar, as instruções na instrução `if` serão executadas. (Como você pode lembrar dos tutoriais anteriores, a `if` declaração é usada para avaliar qualquer condição especificada.) A primeira linha `if` na declaração cria uma variável chamada **randomNumber** que contém um número aleatório que corresponde a um dos itens da lista de ícones. Para fazer isso, ela usa o método <xref:System.Random.Next> do objeto <xref:System.Random> que você criou anteriormente. O método `Next` retorna o número aleatório. Essa linha também usa a propriedade <xref:System.Collections.Generic.List%601.Count> da lista **icons** para determinar o intervalo do qual escolher o número aleatório. A próxima linha atribui um dos itens da lista de ícones à propriedade <xref:System.Windows.Forms.Label.Text> do rótulo. A linha comentada é explicada mais adiante neste tópico. Por fim, a última linha na instrução `if` remove da lista o ícone que foi adicionado ao formulário.

     Lembre-se de que se você não tiver certeza da função de alguma parte do código, será possível posicionar o ponteiro do mouse sobre um elemento do código e analisar a dica de ferramenta resultante. Você também pode percorrer cada linha do código enquanto o programa estiver em execução usando o depurador do Visual Studio. Veja [Como faço para executar em etapas com o depurador do Visual Studio?](https://msdn.microsoft.com/vstudio/ee672313.aspx) ou [Navegação pelo código com o depurador](../debugger/navigating-through-code-with-the-debugger.md) para obter mais informações.

3. Para preencher o tabuleiro do jogo com ícones, você precisa chamar o método `AssignIconsToSquares()` assim que programa for iniciado. Se você estiver usando C#, adicione uma declaração logo abaixo da chamada ao `InitializeComponent()` método no_construtor_ **Form1,** de modo que seu formulário chama seu novo método para configurar-se antes de ser mostrado. Os construtores são chamados quando você cria um novo objeto, como uma classe ou um struct. Veja [Construtores (Guia de programação do C#)](/dotnet/csharp/programming-guide/classes-and-structs/constructors) ou [Uso de construtores e destruidores](/previous-versions/visualstudio/visual-studio-2008/2z08e49e\(v\=vs.90\)) no Visual Basic para obter mais informações.

     [!code-csharp[VbExpressTutorial4Step2_3_4#13](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_4.cs)]

     Para o Visual Basic, adicione a chamada de método `AssignIconsToSquares()` ao método `Form1_Load` para que o código se pareça com o mostrado a seguir.

    ```vb
    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load
        AssignIconsToSquares()
    End Sub
    ```

4. Salve seu programa e o execute. Ele deve mostrar um formulário com ícones aleatórios atribuídos a cada rótulo.

5. Feche seu programa e, em seguida, execute-o novamente. Observe que diferentes ícones são atribuídos a cada rótulo, conforme mostrado na imagem a seguir.

     ![Jogo da memória com ícones aleatórios](../ide/media/express_tut4step3.png)<br/>
*Jogo da memória com ícones aleatórios*

     Os ícones estão visíveis agora porque você não os ocultou. Para ocultá-los do jogador, você pode definir a propriedade **ForeColor** de cada rótulo para a mesma cor de sua propriedade **BackColor**.

    > [!TIP]
    > Outra maneira de ocultar controles, como rótulos, é definir a propriedade **Visible** como **False**.

6. Para ocultar os ícones, interrompa o programa e remova as marcas de comentário da linha de código comentada dentro do loop `For Each`.

     [!code-csharp[VbExpressTutorial4Step2_3_4#15](../ide/codesnippet/CSharp/step-3-assign-a-random-icon-to-each-label_5.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#15](../ide/codesnippet/VisualBasic/step-3-assign-a-random-icon-to-each-label_5.vb)]

7. Na barra de menus, escolha o botão **Salvar Tudo** para salvar seu programa e, em seguida, execute-o. Os ícones parecem ter desaparecido; é exibido apenas um plano de fundo azul. No entanto, os ícones são atribuídos aleatoriamente e continuam lá. Como os ícones são da mesma cor do plano de fundo, eles ficam ocultos para o jogador. Até porque, ele não seria um jogo muito desafiador se o jogador pudesse ver todos os ícones imediatamente!

## <a name="to-continue-or-review"></a>Para continuar ou revisar

- Para ir para a próxima etapa do tutorial, consulte **[Passo 4: Adicione um manipulador de eventos clique em cada rótulo](../ide/step-4-add-a-click-event-handler-to-each-label.md)**.

- Para retornar à etapa anterior do tutorial, veja [Etapa 2: Adicionar um objeto aleatório e uma lista de ícones](../ide/step-2-add-a-random-object-and-a-list-of-icons.md).
