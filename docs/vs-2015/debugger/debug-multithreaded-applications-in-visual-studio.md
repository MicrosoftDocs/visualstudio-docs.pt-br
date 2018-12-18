---
title: Depurar aplicativos multi-threaded no Visual Studio | Microsoft Docs
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
- vs.debug.gputthreads
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- threading [Visual Studio], debugging
- debugging [Visual Studio], high-performance computing
- debugging [Visual Studio], multithreaded
- multithreaded debugging
- high-performance debugging
ms.assetid: 9d175bc2-1d95-4c47-9bc3-9755af968a9c
caps.latest.revision: 28
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f5b9ff27a8a864d648b5e9c545cee72ee64a4901
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51758435"
---
# <a name="debug-multithreaded-applications-in-visual-studio"></a>Depurar aplicativos multithread no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um thread é uma sequência de instruções para que o sistema operacional aloque tempo no processador. Cada processo que está em execução no sistema operacional consiste em pelo menos um thread. Os processos que têm mais de um thread são chamados multithread.  
  
 Os computadores com vários processadores, processadores de vários núcleos ou processos de hyperthreading podem executar vários threads ao mesmo tempo. O processamento paralelo de vários threads pode aumentar melhorar o desempenho do programa, mas também pode tornar a depuração mais difícil porque apresenta a necessidade de manter controle de vários threads.  
  
 Além disso, o multithreading apresenta alguns novos tipos de bugs potenciais. Geralmente, dois ou mais threads precisam acessar o mesmo recurso, mas apenas um thread pode acessar com segurança o recurso de cada vez. Alguma forma de exclusão mútua é necessário para certificar-se de que apenas um thread está acessando o recurso de cada vez. Se a exclusão mútua for executada incorretamente, pode criar uma *deadlock* condição em que nenhum thread possa executar. Deadlocks podem ser um problema particularmente difícil de depurar.  
  
 O Visual Studio fornece um **Threads** janela, uma janela de Threads da GPU, uma janela de inspeção paralela e outros recursos que tornam a depuração de vários segmentos. A melhor maneira de aprender sobre os recursos de threads é seguindo as orientações. Ver [instruções passo a passo: depurando um aplicativo multi-threaded](../debugger/walkthrough-debugging-a-multithreaded-application.md) e [passo a passo: depurando um aplicativo C++ AMP](http://msdn.microsoft.com/library/40e92ecc-f6ba-411c-960c-b3047b854fb5).  
  
 O Visual Studio também fornece os pontos de interrupção avançados e pontos de controle, que podem ser muito úteis quando você depura aplicativos multissegmentados. Você pode usar filtros de ponto de interrupção para incluir pontos de interrupção em threads individuais. Consulte [usando pontos de interrupção](../debugger/using-breakpoints.md)  
  
 Depurar um aplicativo com vários thread que tenha uma interface de usuário pode ser especialmente difícil. Nesse caso, você poderá considerar a execução do aplicativo em um segundo computador e o uso da depuração remota. Para obter informações, consulte [depuração remota](../debugger/remote-debugging.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Depurar threads e processos](../debugger/debug-threads-and-processes.md)  
 Explica as Noções básicas de depuração de threads e processos.  
  
 [Depurar vários processos](../debugger/debug-multiple-processes.md)  
 Explica como depurar vários processos.  
  
 [Como usar a janela Threads](../debugger/how-to-use-the-threads-window.md)  
 Procedimentos úteis para depurar threads com o **Threads** janela.  
  
 [Como mudar para outro thread durante a depuração](../debugger/how-to-switch-to-another-thread-while-debugging.md)  
 Três maneiras para alternar o contexto de depuração para outro segmento.  
  
 [Como sinalizar e remover sinalizador de threads](../debugger/how-to-flag-and-unflag-threads.md)  
 Marque ou sinalize threads aos quais você deseja dar atenção especial durante a depuração.  
  
 [Como definir um nome de thread em código nativo](../debugger/how-to-set-a-thread-name-in-native-code.md)  
 Atribua ao thread um nome que você vê na **Threads** janela.  
  
 [Como definir um nome de thread em código gerenciado](../debugger/how-to-set-a-thread-name-in-managed-code.md)  
 Atribua ao thread um nome que você vê na **Threads** janela.  
  
 [Passo a passo: Depurando um aplicativo multi-threaded](../debugger/walkthrough-debugging-a-multithreaded-application.md).  
 Um tour guiado dos recursos de depuração com ênfase nos recursos para [!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)].  
  
 [Como depurar em um cluster de alto desempenho](../debugger/how-to-debug-on-a-high-performance-cluster.md)  
 Técnicas para depurar um aplicativo executado em um conjunto de alto desempenho.  
  
 [Dicas para threads de depuração no código nativo](../debugger/tips-for-debugging-threads-in-native-code.md)  
 Técnicas simples que podem ser úteis para depurar threads nativos.  
  
 [Usando a janela Tarefas](../debugger/using-the-tasks-window.md)  
 Mostra uma lista de todos os objetos gerenciados ou nativos da tarefa que incluem seu status e outras informações úteis.  
  
 [Usando a janela Pilhas Paralelas](../debugger/using-the-parallel-stacks-window.md)  
 Mostra pilhas de chamadas de vários threads (ou de tarefas) em uma única exibição e também agrega os segmentos de pilha que são comuns entre segmentos (ou tarefas).  
  
 [Passo a passo: depurando um aplicativo paralelo](../debugger/walkthrough-debugging-a-parallel-application.md)  
 A explicação passo a passo mostra como usar a janela Pilhas Paralelas e a janela Tarefas Paralelas.  
  
 [Como usar a janela Inspeção Paralela](../debugger/how-to-use-the-parallel-watch-window.md)  
 Inspecione valores e expressões em vários threads.  
  
 [Como usar a janela Threads da GPU](../debugger/how-to-use-the-gpu-threads-window.md)  
 Examinar e trabalhar com threads que estão em execução no GPU durante a depuração.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Usando pontos de interrupção](../debugger/using-breakpoints.md)  
 -   Use filtros de ponto de interrupção quando você deseja colocar um ponto de interrupção em um segmento individual.  
  
- Os pontos de controle permitem que você rastreie a execução do programa sem interrupções. Isso pode ser útil para estudar problemas, como deadlocks.  
  
  [Threading](http://msdn.microsoft.com/library/7b46a7d9-c6f1-46d1-a947-ae97471bba87)  
  Conceitos de segmentação na programação de [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)], incluindo o código de exemplo.  
  
  [Multithreading em componentes](http://msdn.microsoft.com/library/2fc31e68-fb71-4544-b654-0ce720478779)  
  Como usar multithreading em componentes de [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].  
  
  [Suporte de multithreading para código anterior (Visual C++)](http://msdn.microsoft.com/library/24425b1f-5031-4c6b-aac7-017115a40e7c)  
  Conceitos de segmentação e código de exemplo para programadores de C++ que usam o MFC.  
  
## <a name="see-also"></a>Consulte também  
 [Depurar Threads e processos](../debugger/debug-threads-and-processes.md)   
 [Depuração remota](../debugger/remote-debugging.md)



