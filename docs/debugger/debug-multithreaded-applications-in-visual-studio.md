---
title: Depurar aplicativos multi-threaded | Microsoft Docs
ms.custom: seodec18
ms.date: 11/06/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.gputthreads
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- threading [Visual Studio], debugging
- debugging [Visual Studio], high-performance computing
- debugging [Visual Studio], multithreaded
- multithreaded debugging
- high-performance debugging
ms.assetid: 9d175bc2-1d95-4c47-9bc3-9755af968a9c
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7ea1af90ae775ed24f5cceabeca04cdc901f545f
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53059672"
---
# <a name="debug-multithreaded-applications-in-visual-studio"></a>Depurar aplicativos multi-threaded no Visual Studio
Um thread é uma sequência de instruções para o qual o sistema operacional concede tempo do processador. Cada processo que está em execução no sistema operacional consiste em pelo menos um thread. Os processos que têm mais de um thread são chamados multithread.  
  
Computadores com vários processadores, processadores de vários núcleos ou processos de hyperthreading podem executar vários threads simultâneos. Processamento paralelo usando vários threads pode melhorar significativamente o desempenho do programa, mas ele pode também tornar a depuração mais difícil porque você está acompanhando o número de threads.  
  
O multithreading pode introduzir novos tipos de bugs potenciais. Por exemplo, dois ou mais threads precisam acessar o mesmo recurso, mas apenas um thread por vez pode acessar com segurança o recurso. Alguma forma de exclusão mútua é necessária para certificar-se de que apenas um thread está acessando o recurso a qualquer momento. Se a exclusão mútua for implementada incorretamente, pode criar uma *deadlock* condição em que nenhum thread executará. Os deadlocks geralmente são um problema difícil de depurar.

## <a name="tools-for-debugging-multithreaded-apps"></a>Ferramentas para depurar aplicativos multithread

Visual Studio fornece ferramentas diferentes para uso na depuração de aplicativos multithreaded.

- Para threads, as ferramentas principais para depurar threads são a **Threads** janela, marcadores de thread em janelas de origem, o **pilhas paralelas** janela, o **inspeção paralela** janela e o **local de depuração** barra de ferramentas. Para saber mais sobre o **Threads** janela e **local de depuração** barra de ferramentas, consulte [passo a passo: Depurar usando a janela Threads](../debugger/how-to-use-the-threads-window.md). Para saber como usar o **pilhas paralelas** e **inspeção paralela** windows, consulte [começar a depurar um aplicativo multi-threaded](../debugger/get-started-debugging-multithreaded-apps.md). Os dois tópicos mostram como usar marcadores de thread.
  
- Para o código que usa o [tarefa TPL (biblioteca paralela)](/dotnet/standard/parallel-programming/task-parallel-library-tpl) ou o [tempo de execução de simultaneidade](/cpp/parallel/concrt/concurrency-runtime/), são as ferramentas principais para depurar o **pilhas paralelas** janela, o **Inspeção paralela** janela e o **tarefas** janela, que também dá suporte a JavaScript. Para começar, consulte [passo a passo: Depurando um aplicativo paralelo](../debugger/walkthrough-debugging-a-parallel-application.md) e [passo a passo: Depurando um aplicativo C++ AMP](/cpp/parallel/amp/walkthrough-debugging-a-cpp-amp-application). 

- Para depurar threads na GPU, a principal ferramenta é o **Threads da GPU** janela. Veja [Como: Usar a janela Threads da GPU](../debugger/how-to-use-the-gpu-threads-window.md).  

- Para processos, as ferramentas principais são as **anexar ao processo** caixa de diálogo, o **processos** janela e o **local de depuração** barra de ferramentas.  
  
Visual Studio também fornece pontos de interrupção avançados e pontos de controle, que pode ser útil quando você depura aplicativos multissegmentados. Usar condições de ponto de interrupção e filtros para colocar pontos de interrupção em threads individuais. Pontos de controle permitem que você para rastrear a execução do seu programa sem quebrar, para estudar problemas, como deadlocks. Para obter mais informações, consulte [ações de ponto de interrupção e tracepoints](../debugger/using-breakpoints.md#BKMK_Print_to_the_Output_window_with_tracepoints).

Depurar um aplicativo com vários thread que tenha uma interface de usuário pode ser especialmente difícil. Você pode considerar a execução do aplicativo em um segundo computador e usar a depuração remota. Para obter mais informações, consulte [depuração remota](../debugger/remote-debugging.md).  
  
## <a name="articles-about-debugging-multithreaded-apps"></a>Artigos sobre como depurar aplicativos multithread

 [Introdução ao depurar um aplicativo multithreaded](../debugger/get-started-debugging-multithreaded-apps.md)   
 Um tour pelos recursos, enfatizando os recursos de depuração a **pilhas paralelas** janela e o **inspeção paralela** janela.

 [Ferramentas para depurar threads e processos](../debugger/debug-threads-and-processes.md)  
 Lista os recursos das ferramentas para depurar threads e processos.  
  
 [Depurar vários processos](../debugger/debug-multiple-processes.md)  
 Explica como depurar vários processos.

 [Passo a passo: Depurar usando a janela Threads](../debugger/how-to-use-the-threads-window.md).  
 Passo a passo que mostra como usar o **Threads** janela e o **local de depuração** barra de ferramentas. 

 [Passo a passo: Depurar um aplicativo paralelo](../debugger/walkthrough-debugging-a-parallel-application.md)  
 Passo a passo que mostra como usar o **pilhas paralelas** e **tarefas** windows.  
  
 [Como: Mudar para outro thread durante a depuração](../debugger/how-to-switch-to-another-thread-while-debugging.md)  
 Várias maneiras para alternar o contexto de depuração para outro thread.  
  
 [Como: Sinalizar e remover sinalização de threads](../debugger/how-to-flag-and-unflag-threads.md)  
 Marque ou sinalize threads aos quais você deseja dar atenção especial durante a depuração.    
  
 [Como: Depurar em um cluster de alto desempenho](../debugger/how-to-debug-on-a-high-performance-cluster.md)  
 Técnicas para depurar um aplicativo executado em um conjunto de alto desempenho.  

 [Dicas para threads de depuração no código nativo](../debugger/tips-for-debugging-threads-in-native-code.md)  
 Técnicas simples que podem ser úteis para depurar threads nativos. 

 [Como: Definir um nome de thread em código nativo](../debugger/how-to-set-a-thread-name-in-native-code.md)  
 Atribua ao thread um nome que aparecerá na janela **Threads**.  
  
 [Como: Definir o nome de um thread no código gerenciado](../debugger/how-to-set-a-thread-name-in-managed-code.md)  
 Atribua ao thread um nome que aparecerá na janela **Threads**. 
  
## <a name="see-also"></a>Consulte também  

[Usar pontos de interrupção](../debugger/using-breakpoints.md)  
[Threading](/dotnet/standard/threading/index)  
[Multithreading em componentes](https://msdn.microsoft.com/Library/2fc31e68-fb71-4544-b654-0ce720478779)  
[Suporte de multithreading para código mais antigo (Visual C++)](/cpp/parallel/multithreading-support-for-older-code-visual-cpp)  
 [Depurar threads e processos](../debugger/debug-threads-and-processes.md)   
 [Depuração remota](../debugger/remote-debugging.md)