---
title: 'Etapa 3: Atribuir um ícone aleatório a cada rótulo | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0ba5ed7a-9aaa-41f4-95d2-e3c2d567bc79
caps.latest.revision: 33
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 8ce8047cbdf6d487a1b4ff00ae99c617a9548fca
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49298773"
---
# <a name="step-3-assign-a-random-icon-to-each-label"></a>Etapa 3: Atribuir um ícone aleatório a cada rótulo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se os ícones aparecerem nas mesmas células a cada jogo, ele não será muito desafiador. Para evitar isso, atribua os ícones aleatoriamente aos controles de rótulo no seu formulário usando um método `AssignIconsToSquares()`.  
  
### <a name="to-assign-a-random-icon-to-each-label"></a>Para atribuir um ícone aleatório a cada rótulo  
  
1.  Antes de adicionar o código a seguir, considere como o método funciona. Há uma nova palavra-chave: `foreach` no Visual C# e `For Each` no Visual Basic. (Uma das linhas é comentada intencionalmente, que é explicada no fim deste procedimento.)  
  
     [!code-csharp[VbExpressTutorial4Step2_3_4#2](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs#2)]
     [!code-vb[VbExpressTutorial4Step2_3_4#2](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb#2)]  
  
2.  Adicione o método `AssignIconsToSquares()`, conforme mostrado na etapa anterior. Você pode colocá-lo logo abaixo do código adicionado na [Etapa 2: adicionar um objeto aleatório e uma lista de ícones](../ide/step-2-add-a-random-object-and-a-list-of-icons.md).  
  
     Conforme mencionado anteriormente, há algo novo no seu método `AssignIconsToSquares()`: um loop `foreach` no Visual C# e `For Each` no Visual Basic. Você pode usar um loop `For Each` no momento em que desejar realizar a mesma ação várias vezes. Nesse caso, você deseja executar as mesmas instruções para cada rótulo no seu TableLayoutPanel, conforme explicado pelo código a seguir. A primeira linha cria uma variável denominada `control` que armazena cada controle, um por vez, enquanto as instruções no loop são executadas nesse controle.  
  
     [!code-csharp[VbExpressTutorial4Step2_3_4#14](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs#14)]
     [!code-vb[VbExpressTutorial4Step2_3_4#14](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb#14)]  
  
    > [!NOTE]
    >  Os nomes "iconLabel" e "control" são usados porque são descritivos. É possível substituir esses nomes por quaisquer nomes, e o código funcionará exatamente da mesma forma, desde que você altere o nome em cada instrução dentro do loop.  
  
     O método `AssignIconsToSquares()` é iterado por meio de cada controle de rótulo no TableLayoutPanel e executa as mesmas instruções para cada um deles. Essas instruções extraem um ícone aleatório da lista que você adicionou na [Etapa 2: adicionar um objeto aleatório e uma lista de ícones](../ide/step-2-add-a-random-object-and-a-list-of-icons.md). (Por esse motivo você incluiu dois de cada ícone na lista, de modo que haverá um par de ícones atribuídos aos controles de rótulo aleatórios.)  
  
     Observe mais detalhadamente o código que é executado no loop `foreach` ou `For Each`. Esse código é reproduzido aqui.  
  
     [!code-csharp[VbExpressTutorial4Step2_3_4#16](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs#16)]
     [!code-vb[VbExpressTutorial4Step2_3_4#16](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb#16)]  
  
     A primeira linha converte a variável `control` em um rótulo denominado `iconLabel`. A linha que vem a seguir está uma instrução `if` que verifica se a conversão funcionou. Se a conversão realmente funcionar, as instruções na instrução `if` serão executadas. (Como talvez você se lembre dos tutoriais anteriores, a instrução `if` é usada para avaliar qualquer condição especificada.) A primeira linha na instrução `if` cria uma variável denominada `randomNumber` que contém um número aleatório que corresponde a um dos itens na lista de ícones. Para fazer isso, ela usa o método `Next` do objeto `Random` que você criou anteriormente. O método `Next` retorna o número aleatório. Essa linha também usa a propriedade `Count` da lista `icons` para determinar o intervalo do qual escolher o número aleatório. A próxima linha atribui um dos itens da lista de ícones à propriedade `Text` do rótulo. A linha comentada é explicada mais adiante neste tópico. Por fim, a última linha na instrução `if` remove da lista o ícone que foi adicionado ao formulário.  
  
     Lembre-se de que se você não tiver certeza da função de alguma parte do código, será possível posicionar o ponteiro do mouse sobre um elemento do código e analisar a dica de ferramenta resultante. Você também pode percorrer cada linha do código enquanto o programa estiver em execução usando o depurador do Visual Studio. Consulte [Como executar em etapas com o depurador do Visual Studio?](http://msdn.microsoft.com/vstudio/ee672313.aspx) ou [Navegando no código com o depurador](../debugger/navigating-through-code-with-the-debugger.md) para obter mais informações.  
  
3.  Para preencher o tabuleiro do jogo com ícones, você precisa chamar o método `AssignIconsToSquares()` assim que programa for iniciado. Se estiver usando o Visual C#, adicione uma instrução logo abaixo da chamada ao método `InitializeComponent()` no `Form1`*construtor*, de modo que o formulário chame o novo método para configurar a si mesmo antes de ser mostrado. Os construtores são chamados quando você cria um novo objeto, como uma classe ou um struct. Consulte [Construtores (Guia de programação do C#)](http://msdn.microsoft.com/library/ace5hbzh.aspx) ou [Usando construtores e destruidores](http://msdn.microsoft.com/library/2z08e49e%28v=vs.90%29.aspx) no Visual Basic para obter mais informações.  
  
     [!code-csharp[VbExpressTutorial4Step2_3_4#13](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs#13)]  
  
     Para o Visual Basic, adicione a chamada de método `AssignIconsToSquares()` ao método `Form1_Load` para que o código se pareça com o mostrado a seguir.  
  
    ```vb  
    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load  
        AssignIconsToSquares()  
    End Sub  
    ```  
  
4.  Salve seu programa e o execute. Ele deve mostrar um formulário com ícones aleatórios atribuídos a cada rótulo.  
  
5.  Feche seu programa e, em seguida, execute-o novamente. Observe que diferentes ícones são atribuídos a cada rótulo, conforme mostrado na imagem a seguir.  
  
     ![Jogo de memória com ícones aleatórios](../ide/media/express-tut4step3.png "Express_Tut4Step3")  
Jogo da memória com ícones aleatórios  
  
     Os ícones estão visíveis agora porque você não os ocultou. Para ocultá-los do jogador, você pode definir a propriedade `Forecolor` de cada rótulo para a mesma cor de sua propriedade `BackColor`.  
  
    > [!TIP]
    >  Outra maneira de ocultar controles, como rótulos, é definir a respectiva propriedade **Visível** como `False`.  
  
6.  Para ocultar os ícones, interrompa o programa e remova as marcas de comentário da linha de código comentada dentro do loop `For Each`.  
  
     [!code-csharp[VbExpressTutorial4Step2_3_4#15](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs#15)]
     [!code-vb[VbExpressTutorial4Step2_3_4#15](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb#15)]  
  
7.  Na barra de menus, escolha o botão **Salvar Tudo** para salvar seu programa e, em seguida, execute-o. Os ícones parecem ter desaparecido; é exibido apenas um plano de fundo azul. No entanto, os ícones são atribuídos aleatoriamente e continuam lá. Como os ícones são da mesma cor do plano de fundo, eles ficam ocultos para o jogador. Até porque, ele não seria um jogo muito desafiador se o jogador pudesse ver todos os ícones imediatamente!  
  
### <a name="to-continue-or-review"></a>Para continuar ou revisar  
  
-   Para ir para a próxima etapa do tutorial, consulte [Etapa 4: adicionar um manipulador de eventos de clique a cada rótulo](../ide/step-4-add-a-click-event-handler-to-each-label.md).  
  
-   Para retornar à etapa anterior do tutorial, consulte [Etapa 2: adicionar um objeto aleatório e uma lista de ícones](../ide/step-2-add-a-random-object-and-a-list-of-icons.md).



