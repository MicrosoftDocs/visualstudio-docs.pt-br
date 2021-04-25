---
title: Depurar um despejo de memória gerenciado com os analisadores de diagnóstico do .NET | Microsoft Docs
description: Saiba como usar os analisadores de diagnóstico do .NET do Visual Studio para analisar um despejo de memória gerenciado
ms.custom: SEO-VS-2021
ms.date: 04/21/2021
ms.topic: how-to
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- analyzers
- dump debugging
- debugging managed memory dump
- debugging [Visual Studio]
author: poppastring
ms.author: madownie
manager: andster
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: 083095ad534aa6b9131ba103178313cb1cdc4b7c
ms.sourcegitcommit: 925db7adb9cb554b081c7e727d09680d4863feed
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2021
ms.locfileid: "107952885"
---
# <a name="how-to-debug-a-managed-memory-dump-with-net-diagnostic-analyzers"></a>Como depurar um despejo de memória gerenciado com analisadores de diagnóstico do .NET



Neste tutorial, você irá:

> [!div class="checklist"]
> * Abrindo um despejo de memória
> * Selecionar e executar analisadores em relação ao despejo
> * Examinar os resultados dos analisadores
> * Navegando até o código problemático


No exemplo descrito neste artigo, a preocupação é que seu aplicativo não está respondendo a solicitações em tempo hábil. 


## <a name="opening-a-memory-dump-in-visual-studio"></a>Abrindo um despejo de memória no Visual Studio

1. Abra o despejo de memória no Visual Studio usando o comando **arquivo > abrir > menu arquivo** e selecione o despejo de memória.

1. Observe na página Resumo de despejo de memória uma nova **ação** chamada **executar análise de diagnóstico**.

   ![Análise de ação-diagnóstico](../debugger/media/diagnostic-analyzer-dump-summary-actions.png)

1. Selecione essa ação para iniciar o depurador e abrir a nova página de **análise de diagnóstico** com uma lista de opções do analisador disponíveis, organizadas pelo sintoma subjacente.


## <a name="select-and-execute-analyzers-against-the-dump"></a>Selecionar e executar analisadores em relação ao despejo

Para investigar esses sintomas, as melhores opções estão disponíveis em **capacidade de resposta do processo** , pois ela melhor corresponde ao problema neste exemplo.

   ![Selecionar analisadores de diagnóstico](../debugger/media/diagnostic-analyzer-diagnostics-analysis-window.png)

1. Clique no botão **analisar** para iniciar o processo investigativo 

1. O analisador apresentará resultados com base na combinação de informações de processo e dados CLR capturados no despejo de memória.
 
## <a name="review-the-results-of-the-analyzers"></a>Examinar os resultados dos analisadores

1. Nesse caso, o analisador encontrou dois erros. Selecione o resultado do analisador para ver o **Resumo da análise** e a **correção** sugerida.

   ![Resultados dos analisadores de diagnóstico](../debugger/media/diagnostic-analyzer-diagnostics-analysis-results.png)

1. O **Resumo de análise** declarou que o "pool de threads do CLR está apresentando privação". Essas informações sugerem que o CLR usou atualmente todos os threads do pool de threads disponíveis, o que significa que o serviço não pode responder a novas solicitações até que um thread seja liberado.

    > [!NOTE] 
    > A **correção** , nesse caso, é "não esperar de forma síncrona em monitores, eventos, tarefas ou em qualquer outro objeto que possa bloquear seu thread. Veja se você pode atualizar o método para ser assíncrono. ".

## <a name="navigating-to-the-problematic-code"></a>Navegando até o código problemático

Meu próximo trabalho é encontrar esse código problemático.

1. Ao clicar no link **Mostrar pilha de chamadas** , o Visual Studio mudará imediatamente para os threads que estão exibindo esse comportamento.

1. A janela **pilha de chamadas** mostrará métodos que podem distinguir rapidamente entre meu código (SyncOverAsyncExmple.*) do código do Framework (System.*).

   ![Link de analisadores de diagnóstico para pilha de chamadas](../debugger/media/diagnostic-analyzer-call-stack.png)

1. Cada quadro da pilha de chamadas corresponde a um método e, ao clicar duas vezes nos quadros de pilha, o Visual Studio navegará até o código que levou diretamente a esse cenário neste thread.

1. Neste exemplo, não há nenhum símbolo ou código, no entanto, na página **símbolos não carregados** , você pode selecionar a opção **[descompilar código-fonte](../debugger/decompilation.md)** .

   ![Descompilação](../debugger/media/diagnostic-analyzer-decompilation.png)

1. Na fonte descompilada abaixo, é evidente que uma tarefa assíncrona (ConsumeThreadPoolThread) está chamando uma função de bloqueio síncrona.

    > [!NOTE]  
    > O método "doitem ()" que contém um método WaitHandle. WaitOne, que está bloqueando o thread do pool de threads atual até receber um sinal.

   Para melhorar a capacidade de resposta dos aplicativos, é importante remover o bloqueio de código síncrono de todos os contextos assíncronos.

   ![Analisar código descompilado](../debugger/media/diagnostic-analyzer-decompiled-code.png)


## <a name="see-also"></a>Confira também

* [Usar arquivos de despejo no depurador](../debugger/using-dump-files.md)
* [Gerar código-fonte de assemblies do .NET durante a depuração](../debugger/decompilation.md)
* [Especificar o símbolo (. pdb) e os arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
