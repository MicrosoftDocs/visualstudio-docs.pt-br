---
title: Para visualizar Threads no depurador | Microsoft Docs
ms.custom: ''
ms.date: 10/29/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.threads
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- threading [Visual Studio], debugging
- Thread.Name property
- debugger, Threads window
- SetThreadName function
- Threads window
- '@TIB'
- debugging [Visual Studio], threads
ms.assetid: 590ffd57-0556-43d8-8962-ee27e5b2b7d7
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 14b170e6f8259776941ce0fcc2a2866a9084cffb
ms.sourcegitcommit: 6a955a2d179cd0e137942389f940d9fcbbe125de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51607712"
---
# <a name="view-threads-in-the-visual-studio-debugger-by-using-the-threads-window"></a>Exibir threads no depurador do Visual Studio usando a janela Threads
No **Threads** janela, você pode examinar e trabalhar com threads no aplicativo que você está depurando. Para obter orientação passo a passo sobre como usar o **Threads** janela, consulte [passo a passo: depurar usando a janela Threads](../debugger/how-to-use-the-threads-window.md).

## <a name="use-the-threads-window"></a>Usar a janela Threads 
 O **Threads** janela contém uma tabela em que cada linha descreve um thread separado em seu aplicativo. Por padrão, a tabela lista todos os threads em seu aplicativo, mas você pode filtrar a lista para mostrar apenas os threads que lhe interessam. Cada coluna descreve um tipo diferente de informações. Você também pode ocultar algumas colunas. Se você exibir todas as colunas, as colunas a seguir são exibidos da esquerda para a direita:  
  
- **Sinalizador**: nesta coluna sem rótulo, você pode marcar um thread ao qual você deseja prestar atenção especial. Para obter informações sobre como sinalizar um thread, consulte [como: sinalizador não sinalizar threads](../debugger/how-to-flag-and-unflag-threads.md).  
  
- **O thread atual**: nesta coluna sem nome, uma seta amarela indica que o thread atual. Uma estrutura de tópicos de seta indica o contexto atual do depurador para um thread não atual.
  
- **ID**: exibe o número de identificação para cada thread.  
  
- **ID gerenciada**: exibe os números de identificação gerenciados para threads gerenciados.  
  
- **Categoria**: exibe a categoria de threads como threads de interface do usuário, manipuladores de chamada de procedimento remoto ou threads de trabalho. Uma categoria especial identifica o thread principal do aplicativo.  
  
- **Nome da**: identifica cada thread por nome, se ele tiver um, ou como \<No Name >.  
  
- **Local**: mostra onde o thread está em execução. Você pode expandir este local para mostrar a pilha de chamadas inteira para o thread.  
  
- **Prioridade**: uma coluna avançada (ocultada por padrão) que exibe a prioridade ou precedência que o sistema atribuiu a cada thread.  
  
- **Máscara de afinidade**: uma coluna avançada (ocultada por padrão) que mostra a máscara de afinidade do processador para cada thread. Em um sistema com vários processadores, a máscara de afinidade determina quais processadores em qual thread pode ser executado.  
  
- **Contagem suspensa**: uma coluna avançada (ocultada por padrão) que exibe a contagem suspensa. Esta contagem determina se um thread pode ser executado. Para obter mais informações sobre contagens suspensas, consulte [congelar e descongelar threads](#freeze-and-thaw-threads).  
  
- **Nome do processo**: uma coluna avançada (ocultada por padrão) que exibe o processo ao qual cada thread pertence. Os dados nesta coluna podem ser útil quando você estiver depurando vários processos.  

- **ID do processo**: ID de uma coluna avançada (oculta por padrão) que exibe o processo ao qual pertence a cada thread. 

- **Qualificador de transporte**: uma coluna avançada (ocultada por padrão) que identifica exclusivamente o computador ao qual o depurador está conectado. 
  
### <a name="to-display-the-threads-window-in-break-mode-or-run-mode"></a>Para exibir a janela de threads no modo de interrupção ou no modo de execução  
  
-   Enquanto o Visual Studio está no modo de depuração, selecione o **Debug** , aponte para **Windows**e, em seguida, selecione **Threads**.  
  
### <a name="to-display-or-hide-a-column"></a>Para exibir ou ocultar uma coluna  
  
-   Na barra de ferramentas na parte superior do **Threads** janela, selecione **colunas**. Em seguida, marque ou desmarque o nome da coluna que você deseja exibir ou ocultar.  

## <a name="display-flagged-threads"></a>Exibir threads sinalizados  
 Você pode sinalizar um thread que você deseja dar atenção especial marcando-o com um ícone na **Threads** janela. Para obter mais informações, consulte [como: sinalizar e remover sinalização de threads](../debugger/how-to-flag-and-unflag-threads.md). No **Threads** janela, que você pode optar por exibir todos os threads ou apenas os threads sinalizados.  
  
### <a name="to-display-only-flagged-threads"></a>Para exibir somente threads sinalizados  
  
-   Escolher **Mostrar somente Threads sinalizados** na barra de ferramentas na parte superior das **Threads** janela. (Se ele estiver esmaecido, você precisará sinalizar alguns threads pela primeira vez.) 

## <a name="freeze-and-thaw-threads"></a>Congelar e descongelar threads  
 Quando você congela um thread, o sistema não inicia a execução do thread, mesmo se os recursos estiverem disponíveis.  
  
 No código nativo, você pode suspender ou retomar threads chamando as funções do Windows `SuspendThread` e `ResumeThread`. Ou então, chamar as funções MFC [CWinThread::SuspendThread](/cpp/mfc/reference/CWinThread-class#suspendthread) e [cwinthread:: ResumeThread](/cpp/mfc/reference/CWinThread-class#resumethread). Se você chamar `SuspendThread` ou `ResumeThread`, o *contagem suspensa* mostra o **Threads** janela será alterada. A contagem suspensa não serão alteradas se você congelar ou descongelar um thread nativo. Um thread não é possível executar em código nativo, a menos que seja descongelado e tenha uma contagem suspensa de zero.  
  
 No código gerenciado, a contagem suspensa muda quando você congela ou descongelar um thread. Se você congela um thread em código gerenciado, sua contagem suspensa é 1. Quando você congela um thread em código nativo, sua contagem suspensa é 0, a menos que você usou o `SuspendThread` chamar.  
  
> [!NOTE]
>  Quando você depura uma chamada de código nativo para o código gerenciado, o código gerenciado é executado no mesmo thread físico que o código nativo que o chamou. Suspender ou congelar o thread nativo também congela o código gerenciado.  
  
### <a name="to-freeze-or-thaw-execution-of-a-thread"></a>Para congelar ou descongelar a execução de um thread  
  
-   Na barra de ferramentas na parte superior do **Threads** janela, selecione **congelar Threads** ou **descongelar Threads**.  
  
     Essa ação afeta somente os threads selecionados na **Threads** janela. 

### <a name="switch-to-another-thread"></a>Mudar para outro thread 

Uma seta amarela indica o thread atual (e o local do ponteiro de execução). Uma seta verde com uma parte final encaracolada indica que um thread não atual tem o contexto atual do depurador.

#### <a name="to-switch-to-another-thread"></a>Para alternar para outro thread  
  
-   Siga as etapas a seguir:  
  
    -   Clique duas vezes em qualquer thread.  
  
    -   Um thread com o botão direito e selecione **alternar para Thread**.

## <a name="group-and-sort-threads"></a>Agrupar e classificar threads  
 Quando você agrupa threads, um título aparece na tabela para cada grupo. O título contém uma descrição do grupo, como **Thread de trabalho** ou **Threads sem sinalização**e um controle de árvore. Os threads de membro de cada grupo aparecem no cabeçalho do grupo. Se você quiser ocultar os threads de membro de um grupo, use o controle de árvore para recolher o grupo.  
  
 Como o agrupamento tem precedência sobre a classificação, você poderá agrupar threads por categoria, por exemplo, e, em seguida, classificá-los por ID dentro de cada categoria.  
  
### <a name="to-sort-threads"></a>Para classificar threads  
  
1.  Na barra de ferramentas na parte superior do **Threads** janela, selecione o botão na parte superior de qualquer coluna.  
  
     Os threads agora são classificados pelos valores nessa coluna.  
  
2.  Se você quiser inverter a ordem de classificação, selecione o mesmo botão novamente.  
  
     Os threads que apareceram na parte superior da lista agora aparecem na parte inferior.  
  
### <a name="to-group-threads"></a>Para agrupar threads  
  
-   No **Threads** ferramentas da janela, selecione a **Group by** lista e, em seguida, selecione os critérios que você deseja agrupar threads.  
  
### <a name="to-sort-threads-within-groups"></a>Para classificar threads dentro de grupos  
  
1.  Na barra de ferramentas na parte superior a **Threads** janela, selecione a **Group by** lista e, em seguida, selecione os critérios que você deseja agrupar threads.  
  
2.  No **Threads** janela, selecione o botão na parte superior de qualquer coluna.  
  
     Os threads agora são classificados pelos valores nessa coluna.  
  
### <a name="to-expand-or-collapse-all-groups"></a>Para expandir ou recolher todos os grupos  
  
-   Na barra de ferramentas na parte superior do **Threads** janela, selecione **expandir grupos** ou **recolher grupos**.  
  
## <a name="search-for-specific-threads"></a>Pesquisar threads específicos  
 Você pode procurar threads que correspondem a uma cadeia de caracteres especificada de **Threads** janela. Quando você procura threads, a janela exibe todos os threads que a cadeia de caracteres de pesquisa em qualquer coluna de correspondência. Essas informações incluem o local de thread que aparece na parte superior da pilha de chamadas na **local** coluna. Por padrão, a pilha de chamadas completa não é pesquisada.  
  
### <a name="to-search-for-specific-threads"></a>Para pesquisar threads específicos  
  
1. Na barra de ferramentas na parte superior a **Threads** janela, vá para o **pesquisa** caixa e:  

     - Insira uma cadeia de caracteres de pesquisa e, em seguida, pressione **Enter**.  
  
     \- ou -  
  
     - Selecione a lista suspensa ao lado de **pesquisa** caixa e selecione uma cadeia de caracteres de pesquisa de uma pesquisa anterior.  
  
2. (Opcional) Para incluir a pilha de chamadas inteira na pesquisa, selecione **pilha de chamadas de pesquisa**.   
  
## <a name="display-thread-call-stacks-and-switch-between-frames"></a>Exibir pilhas de chamadas do thread e alternar entre os quadros  
Em um programa de vários threads, cada thread tem sua própria pilha de chamadas. O **Threads** janela fornece uma maneira conveniente de exibir essas pilhas.

> [!TIP]
> Para obter uma representação visual da pilha de chamadas para cada thread, use o [pilhas paralelas](../debugger/get-started-debugging-multithreaded-apps.md) janela.
  
### <a name="to-view-the-call-stack-of-a-thread"></a>Para exibir a pilha de chamadas de um thread  
  
-   No **local** coluna, selecione o triângulo invertido ao lado do local do thread.  
  
     O local é expandido para mostrar a pilha de chamadas para o thread.  
  
### <a name="to-view-or-collapse-the-call-stacks-of-all-threads"></a>Para exibir ou recolher as chamadas de pilhas de todos os threads  
  
-   Na barra de ferramentas na parte superior do **Threads** janela, selecione **expandir pilhas** ou **recolher pilhas**.  
  
## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos multithread](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [Introdução ao depurar aplicativos multithread](../debugger/get-started-debugging-multithreaded-apps.md)