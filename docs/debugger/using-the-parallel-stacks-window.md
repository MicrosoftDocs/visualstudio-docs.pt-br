---
title: Para visualizar threads na janela pilhas paralelas | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.parallelstacks
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, parallel tasks window
ms.assetid: f50efb78-5206-4803-bb42-426ef8133f2f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0bf1ca8fabf70f2d4fbe5920803773af07db0a99
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389222"
---
# <a name="view-threads-and-tasks-in-the-parallel-stacks-window"></a>Exibir threads e tarefas na janela pilhas paralelas

O **pilhas paralelas** janela é útil para depurar aplicativos multithread. Ele tem vários modos de exibição:

- [Exibição de threads](#threads-view) informações da pilha de chamadas de mostra para todos os threads no aplicativo. Você pode navegar entre os threads e quadros de pilha nesses threads. 

- [Modo de exibição tarefas](#tasks-view) mostra informações de pilha de chamada centrado na tarefa. 
  - No código gerenciado, **tarefas** modo de exibição mostra pilhas de chamadas de <xref:System.Threading.Tasks.Task?displayProperty=fullName> objetos. 
  - No código nativo, **tarefas** modo de exibição mostra pilhas de chamadas de [grupos de tarefas](/cpp/parallel/concrt/task-parallelism-concurrency-runtime), [algoritmos em paralelo](/cpp/parallel/concrt/parallel-algorithms), [agentes assíncronos](/cpp/parallel/concrt/asynchronous-agents)e [tarefas leves](/cpp/parallel/concrt/task-scheduler-concurrency-runtime).  
  
- [Modo de exibição do método](#method-view) inverte a pilha de chamadas em um método selecionado. 

## <a name="use-the-parallel-stacks-window"></a>Usar a janela Pilhas Paralelas 

Para abrir o **pilhas paralelas** janela, você deve ser em uma sessão de depuração. Selecione **Debug** > **Windows** > **pilhas paralelas**. 

### <a name="toolbar-controls"></a>Controles da barra de ferramentas

O **pilhas paralelas** janela tem os seguintes controles de barra de ferramentas: 

![Barra de ferramentas da janela pilhas paralelas](../debugger/media/parallel_stackstoolbar.png "barra de ferramentas de pilhas paralelas")  
  
|Ícone|Controle|Descrição|  
|-|-|-|  
|![Caixa de combinação de threads/tarefas](media/parallel_toolbar1.png "caixa de combinação de Threads/tarefas")|**Threads**/**tarefas** caixa de combinação|Alterna a exibição entre pilhas de chamadas de threads e pilhas de chamadas de tarefas. Para obter mais informações, confira [Exibição de tarefas](#tasks-view) e [Exibição de threads](#threads-view).|  
|![Mostrar somente sinalizados ícone](media/parallel_toolbar2.png "ícone Mostrar somente sinalizados")|Mostrar somente sinalizados|Mostra pilhas de chamadas apenas para os threads que estão sinalizados em outras janelas do depurador, como o **Threads da GPU** janela e o **inspeção paralela** janela.|  
|![Ícone do modo de exibição do método de alternância](media/parallel_toolbar3.png "ícone Ativar/desativar exibição de método")|Alternar **Exibição do Método**|Alterna entre os modos de exibição de pilha de chamada e **modo de exibição do método**. Para obter mais informações, confira [Exibição do Método](#method-view).|  
|![Role para o ícone atual](media/parallel_toolbar4.png "Autorrolagem para ícone atual")|Autorrolagem para Quadro de Pilha Atual|Rola automaticamente o gráfico para que o quadro de pilhas atual está no modo de exibição. Esse recurso é útil quando você altera o quadro de pilhas atual de outras janelas ou quando você atinge um novo ponto de interrupção em gráficos maiores.|  
|![Ícone de Zoom de alternância](media/parallel_toolbar5.png "Zoom de alternância de ícone")|Ativar/Desativar Controle de Zoom|Mostra ou oculta o controle de zoom à esquerda da janela. <br /><br />Independentemente da visibilidade do controle de zoom, você também pode aplicar zoom pressionando **Ctrl** e ativar a roda do mouse ou pressionando por **Ctrl**+**Shift** + **+** ampliar e **Ctrl**+**Shift** + **-** para diminuir o zoom. |  
  
### <a name="stack-frame-icons"></a>Ícones de quadro de pilha
Os ícones a seguir fornecem informações sobre os quadros de pilhas ativas e atuais em todos os modos de exibição:

|Ícone|Descrição|  
|-|-|  
|![Seta amarela](media/icon_parallelyellowarrow.gif)|Indica o local atual (quadro de pilhas ativas) do thread atual.|
|![Ícone de threads](media/icon_parallelthreads.gif)|Indica o local atual (quadro de pilhas ativas) de um thread não atual.|
|![Seta verde](media/icon_parallelgreenarrow.gif)|Indica o quadro de pilhas atual (o contexto do depurador atual). O nome do método é sempre que ele aparece em negrito.|  

### <a name="context-menu-items"></a>Itens de menu de contexto  
Os seguintes itens de menu de atalho estão disponíveis quando o botão direito do mouse em um método de **Threads** modo de exibição ou **tarefas** modo de exibição. Os últimos seis itens são as mesmas que na [janela pilha de chamadas](how-to-use-the-call-stack-window.md).  

![Menu de atalho na janela pilhas paralelas](../debugger/media/parallel_contmenu.png "menu de atalho na janela pilhas paralelas")  

|Item de menu|Descrição|  
|-|-|  
|**Sinalizar**|Sinaliza o item selecionado.|  
|**Remover Sinalização**|Remove a sinalização do item selecionado.|  
|**Congelar**|Congela o item selecionado.|  
|**Descongelar**|Descongela o item selecionado.|  
|**Alternar para Quadro**|Mesmo que o menu correspondente de comando na **pilha de chamadas** janela. No entanto, o **pilhas paralelas** janela, um método pode estar em vários quadros. Você pode selecionar o quadro desejado no submenu para este item. Se um dos quadros de pilhas estiver no thread atual, esse quadro é selecionado por padrão no submenu.|  
|**Vá para a tarefa** ou **ir para Thread**|Alterna para o **tarefa** ou **Threads** modo de exibição e mantém a mesma pilha quadro realçado.|  
|**Ir para Código-fonte**|Vai para o local correspondente na janela de código de origem. |  
|**Ir para Desmontagem**|Vai para o local correspondente na **desmontagem** janela.|  
|**Mostrar Código Externo**|Mostra ou oculta o código externo.|  
|**Exibição Hexadecimal**|Alterna entre a exibição decimal e hexadecimal.|  
|**Mostrar Threads na Origem**|Sinaliza o local do thread na janela de código de origem. |  
|**Informações de Carregamento de Símbolos**|Abre o **informações de carregamento de símbolo** caixa de diálogo.|  
|**Configurações de Símbolo**|Abre o **configurações de símbolo** caixa de diálogo. |  
  
## <a name="threads-view"></a>exibição Threads  

Na **Threads** exibir, o quadro de pilhas e o caminho da chamada do thread atual são realçados em azul. O local atual do thread é mostrado pela seta amarela. 

Para alterar o quadro de pilhas atual, clique duas vezes em um método diferente. Isso também pode alternar o thread atual, dependendo se o método selecionado faz parte do thread atual ou de outro thread. 

Quando o **Threads** exibir o gráfico é muito grande para caber na janela, um **panorama** controle aparece na janela. Você pode mover o quadro no controle para navegar para diferentes partes do gráfico.  
  
A ilustração a seguir mostra um thread que vai do principal para um gerenciado para fazer a transição de código nativo. Seis threads estão no método atual. Um continua Sleep e outro continua para console. WriteLine e, em seguida, SyncTextWriter.WriteLine.  

 ![Exibição na janela pilhas paralelas de threads](../debugger/media/parallel_stack1.png "exibição na janela pilhas paralelas de Threads")  

A tabela a seguir descreve os principais recursos do **Threads** exibição:  
  
|Texto Explicativo|Nome do elemento|Descrição|  
|-|-|-|  
|1|Segmento ou nó da pilha de chamadas|Contém uma série de métodos para um ou mais threads. Se o quadro tiver sem linhas de seta conectadas a ele, o quadro mostra o caminho de chamada inteira para os threads.|  
|2|Realce azul|Indica o caminho da chamada do thread atual.|  
|3|Linhas de seta|Conecte os nós para compor o caminho inteiro de chamada para os threads.|  
|4|Cabeçalho do nó|Mostra o número de processos e threads para o nó.|  
|5|Método|Representa uma ou mais quadros de pilha no mesmo método.|  
|6|Dica de ferramenta no método|Aparece quando você focaliza um método. Na **Threads** modo de exibição, a dica de ferramenta mostra todos os threads, em uma tabela semelhante a **Threads** janela. |  

## <a name="tasks-view"></a>Exibição de tarefas  
Se seu aplicativo usa <xref:System.Threading.Tasks.Task?displayProperty=fullName> objetos (código gerenciado) ou `task_handle` objetos (código nativo) para expressar o paralelismo, você pode usar **tarefas** modo de exibição. A exibição de **Tarefas** mostra as pilhas de chamadas de tarefas reais em vez de threads. 

Na **tarefas** exibição:  
  
- Pilhas de chamadas de threads que não estão executando tarefas não são mostradas.  
- Pilhas de chamadas de threads que estão executando tarefas serão cortadas visualmente na parte superior e inferior, para mostrar os quadros mais relevantes para tarefas.  
- Quando várias tarefas estão em um thread, as pilhas de chamadas dessas tarefas são mostradas em nós separados.  

Para ver uma pilha de chamadas inteira, alterne de volta para **Threads** modo de exibição clicando duas vezes em um quadro de pilha e selecionando **ir para Thread**.  

A ilustração a seguir mostra a **Threads** modo de exibição na parte superior e correspondente **tarefas** exibição na parte inferior.  

![Modos de exibição de threads e tarefas](../debugger/media/parallel_threads-tasks.png "modos de exibição de Threads e tarefas")  

Passe o mouse sobre um método para mostrar uma dica de ferramenta com informações adicionais. Na **tarefas** modo de exibição, a dica de ferramenta mostra todas as tarefas em uma tabela semelhante do **tarefas** janela. 

A imagem a seguir mostra a dica de ferramenta para um método na **Threads** modo de exibição na parte superior e para o controle correspondente **tarefas** exibição na parte inferior.  

![Dicas de ferramenta de threads e tarefas](../debugger/media/parallel_threads-tasks-tooltips.png "dicas de ferramenta de Threads e tarefas")  

## <a name="method-view"></a>Modo de Exibição do Método  
De qualquer um **Threads** modo de exibição ou **tarefas** modo de exibição, você pode girar o gráfico no método atual, selecionando o **Alternar modo de exibição do método** ícone na barra de ferramentas. A **Exibição do Método** mostra rapidamente todos os métodos em todos os threads que chamam ou são chamados pelo método atual. A ilustração a seguir mostra as mesmas informações **Threads** exibir à esquerda e, na **modo de exibição do método** à direita.  

![Modo de exibição e modo de exibição de threads](../debugger/media/parallel_methodview.png "exibição e modo de exibição de Threads")  
  
Se você alternar para um novo quadro de pilha, você torna o método atual, e **modo de exibição do método** mostra todos os chamadores e chamados para o novo método. Isso pode fazer os threads serem exibidos ou desaparecerem da exibição, dependendo se esse método for exibido em suas pilhas de chamadas. Para retornar para o modo de exibição de pilha de chamadas, selecione a **modo de exibição do método** ícone da barra de ferramentas novamente.  
  
## <a name="see-also"></a>Consulte também  
 [Introdução ao depurar um aplicativo multithreaded](../debugger/get-started-debugging-multithreaded-apps.md)   
 [Passo a passo: depurar um aplicativo paralelo](../debugger/walkthrough-debugging-a-parallel-application.md)   
 [Noções básicas do depurador](../debugger/getting-started-with-the-debugger.md)   
 [Depurando código gerenciado](../debugger/debugging-managed-code.md)   
 [Programação paralela](/dotnet/standard/parallel-programming/index)   
 [Usar a janela Tarefas](../debugger/using-the-tasks-window.md)   
 [Classe de tarefa](../extensibility/debugger/task-class-internal-members.md)
