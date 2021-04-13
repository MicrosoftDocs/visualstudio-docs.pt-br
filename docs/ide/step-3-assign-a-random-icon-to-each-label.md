---
title: 'Etapa 3: Atribuir um ícone aleatório a cada rótulo'
description: Saiba como atribuir um ícone aleatório a cada rótulo para que os ícones não apareçam nas mesmas células de cada jogo.
ms.custom: SEO-VS-2020
ms.date: 03/21/2020
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: 0ba5ed7a-9aaa-41f4-95d2-e3c2d567bc79
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 282f9ecc7b4f1f083eebe21c93a5bcc5c8fcc8d0
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107296450"
---
# <a name="step-3-assign-a-random-icon-to-each-label"></a>Etapa 3: Atribuir um ícone aleatório a cada rótulo

Se os ícones aparecerem nas mesmas células a cada jogo, ele não será muito desafiador. Para evitar isso, atribua os ícones aleatoriamente aos controles de rótulo no seu formulário usando um método `AssignIconsToSquares()`.

## <a name="to-assign-a-random-icon-to-each-label"></a>Para atribuir um ícone aleatório a cada rótulo

1. Antes de adicionar o código a seguir, considere como o método funciona. Há uma nova palavra-chave: `foreach` em C# e `For Each` em Visual Basic. (Uma das linhas é comentada intencionalmente, que é explicada no fim deste procedimento.)

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb" id="Snippet2":::

      > [!IMPORTANT]
      > Use o controle linguagem de programação no canto superior direito desta página para exibir o trecho de código C# ou o trecho de código de Visual Basic.<br><br>![Controle de linguagem de programação para Docs.Microsoft.com](../ide/media/docs-programming-language-control.png)

2. Adicione o método `AssignIconsToSquares()`, conforme mostrado na etapa anterior. Você pode colocá-lo logo abaixo do código adicionado na [Etapa 2: Adicionar um objeto aleatório e uma lista de ícones](../ide/step-2-add-a-random-object-and-a-list-of-icons.md).

     Como mencionado anteriormente, há algo novo em seu `AssignIconsToSquares()` método: um `foreach` loop em C# e `For Each` em Visual Basic. Você pode usar um loop `For Each` no momento em que desejar realizar a mesma ação várias vezes. Nesse caso, execute as mesmas instruções para cada rótulo no seu <xref:System.Windows.Forms.TableLayoutPanel>, conforme explicado pelo código a seguir. A primeira linha cria uma variável denominada `control` que armazena cada controle, um por vez, enquanto as instruções no loop são executadas nesse controle.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs" id="Snippet14":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb" id="Snippet14":::

    > [!NOTE]
    > Os nomes "iconLabel" e "control" são usados porque são descritivos. É possível substituir esses nomes por quaisquer nomes, e o código funcionará exatamente da mesma forma, desde que você altere o nome em cada instrução dentro do loop.

     O método `AssignIconsToSquares()` é iterado por meio de cada controle de rótulo no TableLayoutPanel e executa as mesmas instruções para cada um deles. Essas instruções extraem um ícone aleatório da lista que você adicionou na [Etapa 2: Adicionar um objeto aleatório e uma lista de ícones](../ide/step-2-add-a-random-object-and-a-list-of-icons.md). Como lembrete, cada um desses ícones é uma letra na fonte Webdings, que é o motivo pelo qual eles são expressos como texto nesse método. Você incluiu dois de cada ícone na lista, para que haja um par de ícones atribuídos a controles de rótulo aleatórios.

     Observe mais detalhadamente o código que é executado no loop `foreach` ou `For Each`. Esse código é reproduzido aqui.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs" id="Snippet16":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb" id="Snippet16":::

     A primeira linha converte a variável **control** em um rótulo denominado **iconLabel**. A linha que vem a seguir está uma instrução `if` que verifica se a conversão funcionou. Se a conversão realmente funcionar, as instruções na instrução `if` serão executadas. (Como você pode se lembrar dos tutoriais anteriores, a `if` instrução é usada para avaliar qualquer condição que você especificar.) A primeira linha na `if` instrução cria uma variável chamada **randomNumber** que contém um número aleatório que corresponde a um dos itens na lista de ícones. Para fazer isso, ela usa o método <xref:System.Random.Next> do objeto <xref:System.Random> que você criou anteriormente. O método `Next` retorna o número aleatório. Essa linha também usa a propriedade <xref:System.Collections.Generic.List%601.Count> da lista **icons** para determinar o intervalo do qual escolher o número aleatório. A próxima linha atribui um dos itens da lista de ícones à propriedade <xref:System.Windows.Forms.Label.Text> do rótulo. A linha comentada é explicada mais adiante neste tópico. Por fim, a última linha na instrução `if` remove da lista o ícone que foi adicionado ao formulário.

     Lembre-se de que se você não tiver certeza da função de alguma parte do código, será possível posicionar o ponteiro do mouse sobre um elemento do código e analisar a dica de ferramenta resultante. Você também pode percorrer cada linha do código enquanto o programa estiver em execução usando o depurador do Visual Studio. Veja [Como faço para executar em etapas com o depurador do Visual Studio?](https://msdn.microsoft.com/vstudio/ee672313.aspx) ou [Navegação pelo código com o depurador](../debugger/navigating-through-code-with-the-debugger.md) para obter mais informações.

3. Para preencher o tabuleiro do jogo com ícones, você precisa chamar o método `AssignIconsToSquares()` assim que programa for iniciado. Se você estiver usando C#, adicione uma instrução logo abaixo da chamada para o `InitializeComponent()` método no construtor **Form1** , para que seu formulário chame o novo método para se configurar antes de ser mostrado. Os construtores são chamados quando você cria um novo objeto, como uma classe ou um struct. Veja [Construtores (Guia de programação do C#)](/dotnet/csharp/programming-guide/classes-and-structs/constructors) ou [Uso de construtores e destruidores](/previous-versions/visualstudio/visual-studio-2008/2z08e49e\(v\=vs.90\)) no Visual Basic para obter mais informações.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs" id="Snippet13":::

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

6. Para ocultar os ícones, interrompa o programa e remova as marcas de comentário da linha de código comentada dentro do loop `For Each`.

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs" id="Snippet15":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb" id="Snippet15":::

7. Na barra de menus, escolha o botão **Salvar Tudo** para salvar seu programa e, em seguida, execute-o. Os ícones parecem ter desaparecido; é exibido apenas um plano de fundo azul. No entanto, os ícones são atribuídos aleatoriamente e continuam lá. Como os ícones são da mesma cor do plano de fundo, eles ficam ocultos para o jogador. Até porque, ele não seria um jogo muito desafiador se o jogador pudesse ver todos os ícones imediatamente!

## <a name="to-continue-or-review"></a>Para continuar ou revisar

- Para ir para a próxima etapa do tutorial, consulte **[etapa 4: adicionar um manipulador de eventos de clique a cada rótulo](../ide/step-4-add-a-click-event-handler-to-each-label.md)**.

- Para retornar à etapa anterior do tutorial, veja [Etapa 2: Adicionar um objeto aleatório e uma lista de ícones](../ide/step-2-add-a-random-object-and-a-list-of-icons.md).
