---
title: 'Como: usar a janela Threads | Microsoft Docs'
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
- vs.debug.threads
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- threading [Visual Studio], debugging
- Thread.Name property
- debugger, Threads window
- SetThreadName function
- Threads window
- '@TIB'
- debugging [Visual Studio], threads
ms.assetid: adfbe002-3d7b-42a9-b42a-5ac0903dfc25
caps.latest.revision: 48
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 925e5ec609c07fa1ca6d703943cf3437f0f9bf84
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51791690"
---
# <a name="how-to-use-the-threads-window"></a>Como usar a janela Threads
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No **Threads** janela, você pode examinar e trabalhar com threads no aplicativo que você está depurando.  
  
 O **Threads** janela contém uma tabela em que cada linha representa um thread em seu aplicativo. Por padrão, a tabela lista todos os threads em seu aplicativo, mas você pode filtrar a lista para mostrar apenas os threads do seu interesse. Cada coluna contém um tipo diferente de informação. Você também pode ocultar algumas colunas. Se você exibir todas as colunas, as seguintes informações são exibidas, da esquerda para a direita:  
  
-   A coluna do sinalizador, em que você pode marcar um thread para o qual você deseja prestar atenção especial. Para obter informações sobre como sinalizar um thread, consulte [como: sinalizador e remover sinalização de Threads](../debugger/how-to-flag-and-unflag-threads.md).  
  
-   A coluna thread ativo, em que uma seta amarela indica um thread ativo. Um contorno de uma seta indica o thread onde a execução interrompe no depurador.  
  
-   O **ID** coluna, que contém o número de identificação para cada thread.  
  
-   O **Managed ID** coluna, que contém os números de identificação gerenciados para threads gerenciados.  
  
-   O **categoria** coluna, que categoriza threads como threads de interface do usuário, manipuladores de chamada de procedimento remoto ou threads de trabalho. Uma categoria especial identifica o thread principal do aplicativo.  
  
-   O **nome** coluna, que identifica cada thread por nome, se ele tiver um, ou como \<No Name >.  
  
-   O **local** coluna, que mostra onde o thread está em execução. Você pode expandir este local para mostrar a pilha de chamadas inteira para o thread.  
  
-   O **prioridade** coluna, que contém a prioridade ou precedência que o sistema atribuiu a cada thread.  
  
-   O **máscara de afinidade** coluna, que é uma coluna avançada que é normalmente oculta. Esta coluna mostra a máscara de afinidade do processador para cada thread. Em um sistema com vários processadores, a máscara de afinidade determina quais processadores em qual thread pode ser executado.  
  
-   O **contagem suspensa** coluna, que contém a contagem suspensa. Esta contagem determina se um thread pode ser executado. Para obter uma explicação de contagem suspensa, consulte “Congelando e descongelando threads” posteriormente neste tópico.  
  
-   O **nome do processo** coluna, que contém o processo ao qual cada thread pertence. Esta coluna pode ser útil quando você estiver depurando vários processos, mas geralmente está oculta.  
  
### <a name="to-display-the-threads-window-in-break-mode-or-run-mode"></a>Para exibir a janela de threads no modo de interrupção ou no modo de execução  
  
-   Sobre o **Debug** , aponte para **Windows**e, em seguida, clique em **Threads**.  
  
### <a name="to-display-or-hide-a-column"></a>Para exibir ou ocultar uma coluna  
  
-   Na barra de ferramentas na parte superior do **Threads** janela, clique em **colunas**, em seguida, selecione ou desmarque o nome da coluna que você deseja exibir ou ocultar.  
  
### <a name="to-switch-the-active-thread"></a>Para alternar o thread ativo  
  
-   Execute uma das seguintes etapas:  
  
    -   Clique duas vezes em qualquer thread.  
  
    -   Um thread com o botão direito e clique em **alternar para Thread**.  
  
         A seta amarela é exibida ao lado do novo thread ativo. O contorno cinza de uma seta identifica o thread onde a execução interrompe no depurador.  
  
## <a name="grouping-and-sorting-threads"></a>Agrupando e classificando threads  
 Quando você agrupa threads, um título aparece na tabela para cada grupo. O título contém uma descrição do grupo, como “Thread de trabalho” ou “Threads sem sinalização” e um controle de árvore. Os threads de membro de cada grupo aparecem no cabeçalho do grupo. Se você quiser ocultar os threads de membro para um grupo, poderá usar o controle de árvore para recolher o grupo.  
  
 Como o agrupamento tem precedência sobre a classificação, você poderá agrupar threads por categoria, por exemplo, e, em seguida, classificá-los por ID dentro de cada categoria.  
  
#### <a name="to-sort-threads"></a>Para classificar threads  
  
1.  Na barra de ferramentas na parte superior do **Threads** janela, clique no botão na parte superior de qualquer coluna.  
  
     Os threads agora são classificados pelos valores nessa coluna.  
  
2.  Se você quiser inverter a ordem de classificação, clique no mesmo botão novamente.  
  
     Os threads que apareceram na parte superior da lista agora aparecem na parte inferior.  
  
#### <a name="to-group-threads"></a>Para agrupar threads  
  
-   No **Threads** barra de ferramentas da janela, clique no **Group by** lista e, em seguida, clique nos critérios que você deseja agrupar threads.  
  
#### <a name="to-sort-threads-within-groups"></a>Para classificar threads dentro de grupos  
  
1.  Na barra de ferramentas na parte superior a **Threads** janela, clique no **Group by** lista e, em seguida, clique nos critérios que você deseja agrupar threads.  
  
2.  No **Threads** janela, clique no botão na parte superior de qualquer coluna.  
  
     Os threads agora são classificados pelos valores nessa coluna.  
  
#### <a name="to-expand-or-collapse-all-groups"></a>Para expandir ou recolher todos os grupos  
  
-   Na barra de ferramentas na parte superior do **Threads** janela, clique em **expandir grupos** ou **recolher grupos**.  
  
## <a name="searching-for-specific-threads"></a>Pesquisando threads específicos  
 No [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)], você pode procurar threads que correspondem a uma cadeia de caracteres especificada. Quando você procura threads na **Threads** janela, a janela exibe todos os threads que correspondem à cadeia de pesquisa em qualquer coluna. Que as informações incluem o local de thread que aparece na parte superior da pilha de chamadas na **local** coluna. Por padrão, no entanto, a pilha de chamadas completa não é pesquisada.  
  
#### <a name="to-search-for-specific-threads"></a>Para pesquisar threads específicos  
  
-   Na barra de ferramentas na parte superior a **Threads** janela, vá para o **pesquisa** caixa e:  
  
    -   Digite uma cadeia de caracteres de pesquisa e pressione ENTER.  
  
         \- ou -  
  
    -   Clique na lista suspensa ao lado de **pesquisa** caixa e selecione uma cadeia de caracteres de pesquisa de uma pesquisa anterior.  
  
-   (Opcional) Para incluir a pilha de chamadas inteira na pesquisa, selecione **pilha de chamadas de pesquisa**.  
  
## <a name="freezing-and-thawing-threads"></a>Congelando e descongelando threads  
 Quando você congela um thread, o sistema não iniciará a execução do thread mesmo se os recursos estiverem disponíveis.  
  
 No código nativo, você pode suspender ou retomar threads chamando as funções do Windows `SuspendThread` e `ResumeThread` ou as funções MFC [CWinThread::SuspendThread](http://msdn.microsoft.com/library/57189c7e-fd71-42e5-bc4b-3de7cd373d28) e [cwinthread:: ResumeThread](http://msdn.microsoft.com/library/d6f97a2f-5c9f-4ee1-b978-d74938784db5). Se você chamar `SuspendThread` ou `ResumeThread`, você altera o *contagem suspensa*, que aparece no **Threads** janela. Porém, se você congelar ou descongelar um thread nativo, não alterará a contagem suspensa. No código nativo, um thread não pode ser executado a menos que seja descongelado e tenha uma contagem suspensa de zero.  
  
 No código gerenciado, congelar ou descongelar um thread altera a contagem suspensa. No código gerenciado, um thread congelado tem uma contagem suspensa de 1. No código nativo, um thread congelado tem uma contagem suspensa de 0 a menos que o thread tenha sido suspenso por uma chamada `SuspendThread`.  
  
> [!NOTE]
>  Quando você depura uma chamada de código nativo para o código gerenciado, o código gerenciado é executado no mesmo thread físico que o código nativo que o chamou. Suspender ou congelar o thread nativo também congela o código gerenciado.  
  
#### <a name="to-freeze-or-thaw-execution-of-a-thread"></a>Para congelar ou descongelar a execução de um thread  
  
-   Na barra de ferramentas na parte superior do **Threads** janela, clique em **congelar Threads** ou **descongelar Threads**.  
  
     Essa ação afeta somente os threads selecionados na **Threads** janela.  
  
## <a name="displaying-flagged-threads"></a>Exibindo threads sinalizados  
 Você pode sinalizar um thread que você deseja dar atenção especial marcando-o com um ícone na **Threads** janela. Para obter mais informações, consulte [como: sinalizador e remover sinalização de Threads](../debugger/how-to-flag-and-unflag-threads.md). Na janela Threads, você pode optar por exibir todos os threads ou apenas os threads sinalizados.  
  
#### <a name="to-display-only-flagged-threads"></a>Para exibir somente threads sinalizados  
  
-   Escolha o botão de sinalizador no canto superior esquerdo dos **Threads** janela.  
  
## <a name="displaying-thread-call-stacks-and-switching-between-frames"></a>Exibindo pilhas de chamadas de threads e alternando entre quadros  
 Em um programa de vários threads, cada thread tem sua própria pilha de chamadas. O **Threads** janela fornece uma maneira conveniente de exibir essas pilhas.  
  
#### <a name="to-view-the-call-stack-of-a-thread"></a>Para exibir a pilha de chamadas de um thread  
  
-   No **local** coluna, clique no triângulo invertido ao lado do local do thread.  
  
     O local é expandido para mostrar a pilha de chamadas para o thread.  
  
#### <a name="to-view-or-collapse-the-call-stacks-of-all-threads"></a>Para exibir ou recolher as chamadas de pilhas de todos os threads  
  
-   Na barra de ferramentas na parte superior do **Threads** janela, clique em **expandir pilhas** ou **recolher pilhas**.  
  
## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos multithread](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [Passo a passo: depurando um aplicativo multi-threaded](../debugger/walkthrough-debugging-a-multithreaded-application.md)



