---
title: Depurar aplicativos multithread | Microsoft Docs
description: Depurar aplicativos multithread no Visual Studio. Reveja as ferramentas e outros artigos sobre como depurar aplicativos multithread.
ms.custom: SEO-VS-2020
ms.date: 11/06/2018
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5551ffd39bfe3485d0b6e31def0b3cfff9c7e3b1
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389755"
---
# <a name="debug-multithreaded-applications-in-visual-studio"></a>Depurar aplicativos multi-threaded no Visual Studio
Um thread é uma sequência de instruções para as quais o sistema operacional concede o tempo do processador. Cada processo que está em execução no sistema operacional consiste em pelo menos um thread. Os processos que têm mais de um thread são chamados multithread.

Computadores com vários processadores, processadores de vários núcleos ou processos de hyperthreading podem executar vários threads simultaneamente. O processamento paralelo usando muitos threads pode melhorar muito o desempenho do programa, mas também pode tornar a depuração mais difícil, pois você está acompanhando vários threads.

O multithreading pode introduzir novos tipos de bugs potenciais. Por exemplo, dois ou mais threads podem precisar acessar o mesmo recurso, mas apenas um thread por vez pode acessar com segurança o recurso. Alguma forma de exclusão mútua é necessária para garantir que apenas um thread acesse o recurso a qualquer momento. Se a exclusão mútua for implementada incorretamente, ela poderá criar uma condição de *deadlock* em que nenhum thread será executado. Os deadlocks geralmente são um problema difícil de depurar.

## <a name="tools-for-debugging-multithreaded-apps"></a>Ferramentas para depurar aplicativos multithread

O Visual Studio fornece ferramentas diferentes para uso na depuração de aplicativos multissegmentados.

- Para threads, as principais ferramentas para depuração de threads são a janela **threads** , marcadores de thread nas janelas de origem, a janela **pilhas paralelas** , a janela de **inspeção paralela** e a barra de ferramentas **local de depuração** . Para saber mais sobre o **Threads** janela e **local de depuração** barra de ferramentas, consulte [passo a passo: Depuração com a janela Threads](../debugger/how-to-use-the-threads-window.md). Para saber como usar as **pilhas paralelas** e as janelas de **inspeção paralelas** , consulte [introdução à depuração de um aplicativo multi-threaded](../debugger/get-started-debugging-multithreaded-apps.md). Os dois tópicos mostram como usar marcadores de thread.

- Para o código que usa a [TPL (biblioteca paralela de tarefas)](/dotnet/standard/parallel-programming/task-parallel-library-tpl) ou a [tempo de execução de simultaneidade](/cpp/parallel/concrt/concurrency-runtime/), as principais ferramentas para depuração são a janela **pilhas paralelas** , a janela de **inspeção paralela** e a janela **tarefas** , que também oferece suporte a JavaScript. Para começar, consulte [passo a passos: Depurando um aplicativo paralelo](../debugger/walkthrough-debugging-a-parallel-application.md) e [explicando: Depurando um aplicativo C++ amp](/cpp/parallel/amp/walkthrough-debugging-a-cpp-amp-application).

- Para depurar threads na GPU, a principal ferramenta é a janela **threads de GPU** . Consulte [como: usar a janela threads GPU](../debugger/how-to-use-the-gpu-threads-window.md).

- Para processos, as principais ferramentas são a caixa de diálogo **anexar ao processo** , a janela **processos** e a barra de ferramentas **local de depuração** .

O Visual Studio também fornece pontos de interrupção e tracepoints poderosos, que podem ser úteis quando você depura aplicativos multithread. Use condições e filtros de ponto de interrupção para posicionar pontos de interrupção em threads individuais. Os Tracepoints permitem rastrear a execução do seu programa sem interrupção, para estudar problemas como deadlocks. Para obter mais informações, consulte [ações de ponto de interrupção e tracepoints](../debugger/using-breakpoints.md#BKMK_Print_to_the_Output_window_with_tracepoints).

Depurar um aplicativo com vários thread que tenha uma interface de usuário pode ser especialmente difícil. Você pode considerar executar o aplicativo em um segundo computador e usar a depuração remota. Para obter mais informações, consulte [depuração remota](../debugger/remote-debugging.md).

## <a name="articles-about-debugging-multithreaded-apps"></a>Artigos sobre a depuração de aplicativos multithread

 [Introdução à depuração de um aplicativo multithread](../debugger/get-started-debugging-multithreaded-apps.md)

Um tour pelos recursos de depuração de threads, enfatizando recursos na janela **pilhas paralelas** e na janela de **inspeção paralela** .

 [Ferramentas para depurar threads e processos](../debugger/debug-threads-and-processes.md)

Lista os recursos das ferramentas para depurar threads e processos.

 [Depurar vários processos](../debugger/debug-multiple-processes.md)

Explica como depurar vários processos.

 [Walkthrough: Debug usando a janela threads](../debugger/how-to-use-the-threads-window.md).

Walkthrough que mostra como usar a janela **threads** e a barra de ferramentas **Location de depuração** .

 [Passo a passo: depurar um aplicativo paralelo](../debugger/walkthrough-debugging-a-parallel-application.md)

Walkthrough que mostra como usar as janelas de **pilhas paralelas** e **tarefas** .

 [Como mudar para outro thread durante a depuração](../debugger/how-to-switch-to-another-thread-while-debugging.md)

Várias maneiras de alternar o contexto de depuração para outro thread.

 [Como sinalizar e remover sinalizador de threads](../debugger/how-to-flag-and-unflag-threads.md)

Marque ou sinalize threads aos quais você deseja dar atenção especial durante a depuração.

 [Como depurar em um cluster de alto desempenho](../debugger/how-to-debug-on-a-high-performance-cluster.md)

Técnicas para depurar um aplicativo executado em um conjunto de alto desempenho.

 [Dicas para depurar threads no código nativo](../debugger/tips-for-debugging-threads-in-native-code.md)

Técnicas simples que podem ser úteis para depurar threads nativos.

 [Como definir um nome de thread em código nativo](../debugger/how-to-set-a-thread-name-in-native-code.md)

Atribua ao thread um nome que aparecerá na janela **Threads**.

 [Como: definir um nome de thread em código gerenciado](../debugger/how-to-set-a-thread-name-in-managed-code.md)

Atribua ao thread um nome que aparecerá na janela **Threads**.

## <a name="see-also"></a>Confira também

- [Usar pontos de interrupção](../debugger/using-breakpoints.md)
- [Threading](/dotnet/standard/threading/index)
- [Multithreading em componentes](/previous-versions/3es4b6yy(v=vs.140))
- [Suporte multithread para código mais antigo](/cpp/parallel/multithreading-support-for-older-code-visual-cpp)
- [Depurar threads e processos](../debugger/debug-threads-and-processes.md)
- [Depuração remota](../debugger/remote-debugging.md)