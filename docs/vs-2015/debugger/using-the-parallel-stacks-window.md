---
title: Usar o paralelo janela pilhas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.parallelstacks
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, parallel tasks window
ms.assetid: f50efb78-5206-4803-bb42-426ef8133f2f
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 602fdd683ecb1b3244289c305e4fc850d337b03e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51792028"
---
# <a name="using-the-parallel-stacks-window"></a>Usando a janela Pilhas Paralelas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O **pilhas paralelas** janela é útil quando você estiver depurando aplicativos multithread. Sua **exibição de Threads** mostra informações da pilha de chamada para todos os threads em seu aplicativo. Permite navegar entre os threads e os quadros da pilha nesses threads. No código gerenciado, o **modo de exibição de tarefas** mostra pilhas de <xref:System.Threading.Tasks.Task?displayProperty=fullName> objetos. No código nativo, o **modo de exibição de tarefas** mostra pilhas de [grupos de tarefas](http://msdn.microsoft.com/library/42f05ac3-2098-494a-ba84-737fcdcad077), [algoritmos em paralelo](http://msdn.microsoft.com/library/045dca7b-4d73-4558-a44c-383b88a28473), [agentes assíncronos](http://msdn.microsoft.com/library/6cf6ccc6-87f1-4e14-af15-ea8ba58fef1a)e [tarefas leves](http://msdn.microsoft.com/library/9aba278c-e0c9-4ede-b7c6-fedf7a365d90).  
  
## <a name="threads-view"></a>Modo de Exibição de Threads  
 A ilustração a seguir mostra um thread que foi de Main para A para B e, em seguida, para algum código externo. Dois outros threads começaram de algum código externo e foram para A, mas um dos threads continuou para B e, em seguida, para algum código externo, e o outro thread continuou para C e, em seguida, para algum AnonymousMethod.  
  
 ![Exibição na janela pilhas paralelas de threads](../debugger/media/parallel-stacksthread.png "Parallel_StacksThread")  
  
 Na ilustração, o caminho de chamada do thread atual é realçado em azul, e o quadro de pilhas ativo é identificado pela seta amarela. Você pode alterar o quadro de pilhas atual selecionando um método diferente na **pilhas paralelas** janela. Isso também pode resultar em alternar o thread atual, dependendo se o método selecionado já faz parte do thread atual ou de outro thread. A tabela a seguir descreve os principais recursos do **pilhas paralelas** janela, conforme mostrado na ilustração.  
  
|Letra de texto explicativo|Nome de elementos|Descrição|  
|--------------------|------------------|-----------------|  
|Um|Segmento ou nó da pilha de chamadas|Contém uma série de contextos de método para um ou mais threads. Se o nó não tiver linhas de seta conectadas a ele, ele representará o caminho inteiro de chamada para os threads.|  
|B|Realce azul|Indica o caminho da chamada do thread atual.|  
|C|Linhas de seta|Conecte os nós para compor o caminho inteiro de chamada para os threads.|  
|D|Dica de ferramenta no cabeçalho do nó|Mostra a ID e o nome definido pelo usuário de cada thread cujo caminho de chamada compartilha esse nó.|  
|E|Contexto do método|Representa uma ou mais quadros de pilha no mesmo método.|  
|F|Dica de ferramenta no contexto do método|No modo de exibição de Threads, mostra todos os threads em uma tabela semelhante para o **Threads** janela. No modo de exibição de tarefas, mostra todas as tarefas em uma tabela semelhante para o **tarefas paralelas** janela.|  
  
 Além disso, a janela pilhas paralelas mostra um **panorama** ícone no painel principal quando o gráfico é muito grande para caber na janela. Você pode clicar no ícone para ver o gráfico inteiro na janela.  
  
## <a name="method-context-icons"></a>Ícones do Contexto do método  
 A tabela a seguir descreve os ícones que fornecem informações sobre os quadros de pilhas ativas e atuais:  
  
|||  
|-|-|  
|Ícone|Descrição|  
|![Seta amarela de pilhas paralelas](../debugger/media/icon-parallelyellowarrow.gif "Icon_ParallelYellowArrow")|Indica que o contexto do método contém o quadro de pilhas ativas do thread atual.|  
|![Ícone de Threads de pilhas paralelas](../debugger/media/icon-parallelthreads.gif "Icon_ParallelThreads")|Indica que o contexto do método contém o quadro de pilhas ativas de um thread não atual.|  
|![Seta verde de pilhas paralelas](../debugger/media/icon-parallelgreenarrow.gif "Icon_ParallelGreenArrow")|Indica que o contexto do método contém o quadro de pilhas atual. O nome desse método está em negrito em todos os nós em que aparece.|  
  
## <a name="toolbar-controls"></a>Controles da barra de ferramentas  
 A ilustração e a tabela a seguir descrevem os controles disponíveis na barra de ferramentas das Pilhas Paralelas.  
  
 ![Barra de ferramentas da janela pilhas paralelas](../debugger/media/parallel-stackstoolbar.png "Parallel_StacksToolbar")  
  
|Letra de texto explicativo|Controle|Descrição|  
|--------------------|-------------|-----------------|  
|Um|Caixa de combinação de threads e tarefas|Alterna a exibição entre pilhas de chamadas de threads e pilhas de chamadas de tarefas. Para obter mais informações, consulte Modo de Exibição de Tarefas e Modo de Exibição de Threads.|  
|B|Mostrar somente sinalizados|Mostra pilhas de chamadas apenas para os threads sinalizados em outras janelas de depuração, como o **Threads da GPU** janela e o **inspeção paralela** janela.|  
|C|Ativar/Desativar Modo de Exibição do Método|Alterna entre o Modo de Exibição de Pilha e o Modo de Exibição do Método. Para obter mais informações, consulte o Modo de Exibição do Método.|  
|D|Autorrolagem para Quadro de Pilha Atual|Rola automaticamente o diagrama de forma que o quadro de pilhas atual esteja no modo de exibição. Este recurso é útil quando você está modificando o quadro de pilhas atual de outras janelas ou quando você está atingindo um novo ponto de interrupção em grandes diagramas.|  
|E|Ativar/Desativar Controle de Zoom|Mostra ou oculta o controle de zoom. Você também pode aplicar zoom pressionando CTRL e girando a roda do mouse, independentemente da visibilidade do controle de zoom, ou usando **CTRL + SHIFT + '+'** para ampliar e **CTRL + SHIFT +'-'** para diminuir o zoom. Pressionar **CTRL + F8** zoom será aplicado para caber na tela.|  
  
### <a name="context-menu-items"></a>Itens de menu de contexto  
 A ilustração e a tabela a seguir descrevem os itens de menu de atalho disponíveis quando você clica com o botão direito em um contexto do método no Modo de Exibição de Threads ou Modo de Exibição de Tarefas. Os últimos seis itens são emprestados diretamente da janela Pilha de Chamadas e não apresentam comportamento novo.  
  
 ![Menu de atalho na janela pilhas paralelas](../debugger/media/parallel-contmenu.png "Parallel_ContMenu")  
  
|Item de menu|Descrição|  
|---------------|-----------------|  
|Sinalizador|Sinaliza o item selecionado.|  
|Remover sinalização|Remove a sinalização do item selecionado.|  
|Congelar|Congela o item selecionado.|  
|Descongelar|Descongela o item selecionado.|  
|Ir para Tarefa (thread)|Executa a mesma função que a caixa de combinação na barra de ferramentas, mas mantém o mesmo quadro de pilhas realçado.|  
|Vá para o código-fonte|Navega até o local no código-fonte que corresponde ao quadro de pilhas que o usuário clicou com o botão direito.|  
|Alternar para Quadro|O mesmo que o comando do menu correspondente na janela Pilha de Chamadas. No entanto, com Pilhas Paralelas, vários itens podem corresponder a um contexto do método. Por isso, o item de menu tem submenus, cada um representando um quadro de pilhas específico. Se um dos quadros de pilhas estiver no thread atual, o menu que corresponda a esse quadro de pilhas estará selecionado.|  
|Ir para Desmontagem|Navega até o local na janela de desmontagem que corresponde ao quadro de pilhas que o usuário clicou com o botão direito.|  
|Mostrar Código Externo|Mostra ou oculta o código externo.|  
|Exibição Hexadecimal|Alterna entre a exibição decimal e hexadecimal.|  
|Informações de Carregamento de Símbolos|Exibe a caixa de diálogo correspondente.|  
|Configurações de Símbolo|Exibe a caixa de diálogo correspondente.|  
  
## <a name="tasks-view"></a>Modo de Exibição de Tarefas  
 Se seu aplicativo está usando <xref:System.Threading.Tasks.Task?displayProperty=fullName> objetos (código gerenciado) ou `task_handle` objetos (código nativo) para expressar o paralelismo, você pode usar a caixa de combinação na barra de ferramentas de janela pilhas paralelas para alternar para o *modo de exibição tarefas*. O Modo de Exibição de Tarefas mostra as chamadas de pilhas de tarefas reais em vez de threads. O Modo de Exibição de Tarefas é diferente do Modo de Exibição de Threads da seguinte maneira:  
  
- As pilhas de chamadas de threads que não estão executando tarefas não são mostradas.  
  
- As pilhas de chamadas de threads que estão executando tarefas serão cortadas visualmente na parte superior e inferior para mostrar os quadros mais relevantes que pertencem a tarefas.  
  
- Quando várias tarefas estiverem em um thread, as pilhas de chamadas dessas tarefas serão divididas em nós separados.  
  
  A ilustração a seguir mostra o Modo de Exibição de Tarefas de Pilhas Paralelas à direita e o Modo de Exibição de Threads correspondente à esquerda.  
  
  ![Modo de exibição na janela pilhas paralelas de tarefas](../debugger/media/parallel-tasksview.png "Parallel_TasksView")  
  
  Para ver a pilha de chamadas inteira, simplesmente alternar para exibição de Threads clicando duas vezes um quadro de pilha e, em seguida, clicando em **ir para Thread**.  
  
  Como descrito na tabela anterior, ao passar o cursor sobre um contexto do método, você poderá ver informações adicionais. A imagem a seguir mostra as informações na dica de ferramentas para o Modo de Exibição de Threads e o Modo de Exibição de Tarefas.  
  
  ![Dicas de ferramentas na janela pilhas paralelas](../debugger/media/parallel-stack-tooltips.png "Parallel_Stack_Tooltips")  
  
## <a name="method-view"></a>Modo de Exibição do Método  
 Do Modo de Exibição de Threads ou de Tarefas, você pode girar o gráfico no método atual clicando no ícone do Modo de Exibição do Método na barra de ferramentas. O Modo de Exibição do Método mostra rapidamente todos os métodos em todos os threads que chamam ou são chamados pelo método atual. A ilustração a seguir mostra um Modo de Exibição de Threads e também como as mesmas informações aparecem no Modo de Exibição do Método.  
  
 ![Exibição do método na janela pilhas paralelas](../debugger/media/parallel-methodview.png "Parallel_MethodView")  
  
 Ao alternar para um novo quadro de pilhas, você torna o método atual e faz a janela mostrar todos os chamadores e chamados para o novo método. Isso pode fazer os threads serem exibidos ou desaparecerem da exibição, dependendo se esse método for exibido em suas pilhas de chamadas. Para retornar ao Modo de Exibição de Pilha, clique no botão da barra de ferramentas do Modo de Exibição do Método novamente.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Depurando um aplicativo paralelo](../debugger/walkthrough-debugging-a-parallel-application.md)   
 [Noções básicas do depurador](../debugger/debugger-basics.md)   
 [Depurando código gerenciado](../debugger/debugging-managed-code.md)   
 [Programação paralela](http://msdn.microsoft.com/library/4d83c690-ad2d-489e-a2e0-b85b898a672d)   
 [Usando a janela tarefas](../debugger/using-the-tasks-window.md)   
 [Passo a passo: Depurando um aplicativo paralelo](../debugger/walkthrough-debugging-a-parallel-application.md)   
 [Classe de tarefa](../extensibility/debugger/task-class-internal-members.md)



