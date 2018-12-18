---
title: Depurar um aplicativo multithread
description: Depurar usando a janela Threads e a barra de ferramentas do local de depuração no Visual Studio
ms.custom: ''
ms.date: 11/21/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- multithreaded debugging, tutorial
- tutorials, multithreaded debugging
ms.assetid: adfbe002-3d7b-42a9-b42a-5ac0903dfc25
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: cd66d7f9d8f214e8e7166a77162553b694e20cc5
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389397"
---
# <a name="walkthrough-debug-a-multithreaded-app-using-the-threads-window"></a>Passo a passo: Depurar um aplicativo de vários threads usando a janela Threads

Vários elementos de interface do usuário Visual Studio ajudam a depurar aplicativos multithread. Este artigo apresenta os recursos de depuração multithread na janela do editor de código **local de depuração** barra de ferramentas, e **Threads** janela. Para obter informações sobre outras ferramentas para depurar aplicativos multi-threaded, consulte [começar a depurar aplicativos multithread](../debugger/get-started-debugging-multithreaded-apps.md). 
  
Concluir este tutorial leva apenas alguns minutos e familiariza você com as Noções básicas de depuração de aplicativos multithread.

## <a name="create-a-multithreaded-app-project"></a>Criar um projeto de aplicativo multithread  

Crie o seguinte projeto de aplicativo de vários threads para usar neste tutorial: 
  
1. No Visual Studio, selecione **Arquivo** > **Novo** > **Projeto**.  
   
1. Na caixa de diálogo **Novo Projeto**:
   - Para um C# aplicativo, selecione **Visual C#**    >  **aplicativo de Console (.NET Framework)**.  
   - Para um aplicativo em C++, selecione **Visual C++** > **aplicativo de Console do Windows**.
   
1. Nomeie o aplicativo MyThreadWalkthroughApp e, em seguida, selecione **Okey**.  
   
   O novo projeto aparece na **Gerenciador de soluções**, e um arquivo de origem chamado *Program.cs* ou *mythreadwalkthroughapp. cpp* é aberto na janela de código de origem.  
   
1. Substitua o código no arquivo de origem com o C# ou o código de exemplo do C++ de [começar a depurar aplicativos multithread](../debugger/get-started-debugging-multithreaded-apps.md).  
   
1. Selecione **arquivo** > **Salvar tudo**.  
  
## <a name="start-debugging"></a>Iniciar a depuração 

1. Localize as seguintes linhas no código-fonte:  
   
   ```csharp  
   Thread.Sleep(3000); 
   Console.WriteLine();
   ```  
   
   ```C++ 
   Thread::Sleep(3000); 
   Console.WriteLine(); 
   ```
   
1. Defina um ponto de interrupção a `Console.WriteLine();` linha clicando na medianiz esquerda, ou selecionar a linha e pressionando **F9**.  
   
   O ponto de interrupção aparece como um círculo vermelho na medianiz esquerda ao lado da linha de código.  
   
1. Selecione **Debug** > **iniciar depuração**, ou pressione **F5**.  
   
   O aplicativo é iniciado no modo de depuração e pausa no ponto de interrupção.  
   
1. No modo de interrupção, abra o **Threads** janela selecionando **Debug** > **Windows** > **Threads**. Você deve ser em uma sessão de depuração para abrir ou consulte os **Threads** e outras janelas de depuração. 
   
## <a name="examine-thread-markers"></a>Examine os marcadores de thread

1. No código-fonte, localize o `Console.WriteLine();` linha. 
   
   1. Com o botão direito no **Threads** janela e selecione **Mostrar Threads em origem** ![Mostrar Threads em origem](../debugger/media/dbg-multithreaded-show-threads.png "ThreadMarker") no menu.
   
   A medianiz ao lado do código-fonte da linha agora exibe uma *marcador de thread* ícone ![marcador de Thread](../debugger/media/dbg-thread-marker.png "marcador de Thread"). O marcador de thread indica que um thread está parado nesse local. Se não houver mais de um thread parado no local, o ![vários threads](../debugger/media/dbg-multithreaded-show-threads.png "vários threads") ícone é exibido.
   
1. Passe o ponteiro sobre o marcador de thread. Um DataTip aparece, mostrando o número de ID de thread e nome para o thread parado ou threads. Os nomes de thread podem ser `<No Name>`.  

   >[!TIP]
   >Para ajudar a identificar threads sem nome, você pode renomeá-los de **Threads** janela. O thread com o botão direito e selecione **Renomear**.
  
1. Clique com botão direito o marcador de thread no código-fonte para ver as opções disponíveis no menu de atalho. 

## <a name="flag-and-unflag-threads"></a>Sinalizar e remover sinalizador de threads 

Você pode sinalizar os threads para manter o controle de threads que você deseja prestar atenção especial ao. 

Sinalizar e remover sinalização de threads do editor de código fonte ou do **Threads** janela. Escolha se deseja exibir somente sinalizados threads ou todos os threads, do **local de depuração** ou **Threads** barras de ferramentas da janela. As seleções feitas em qualquer local afetam todos os locais. 

### <a name="flag-and-unflag-threads-in-source-code"></a>Sinalizar e remover sinalização de threads no código-fonte 

1. Abra o **local de depuração** barra de ferramentas selecionando **exibição** > **barras de ferramentas** > **local de depuração**. Você pode também com o botão direito na área de barra de ferramentas e selecione **local de depuração**. 
   
1. O **local de depuração** barra de ferramentas tem três campos: **processo**, **Thread**, e **quadro de pilha**. Lista suspensa a **Thread** listar e observe quantos threads lá. No **Thread** lista, o thread em execução no momento é marcado por um **>** símbolo. 
   
1. Na janela de código fonte, passe o mouse sobre um ícone de marcador de thread na medianiz e selecione o ícone de sinalizador (ou um dos ícones de sinalizador vazia) no DataTip. O ícone de sinalizador fica vermelho. 
   
   Você pode também com o botão direito um ícone de marcador de thread, aponte para **sinalizador**e, em seguida, selecione um thread para sinalizar no menu de atalho.  
   
1. Sobre o **local de depuração** barra de ferramentas, selecione a **Mostrar somente Threads sinalizados** ícone ![Mostrar Threads sinalizados](../debugger/media/dbg-threads-show-flagged.png "Mostrar Threads sinalizados"), para o à direita do **Thread** campo. O ícone está esmaecido, a menos que um ou mais threads sinalizados.  
   
   Somente o thread sinalizado agora aparece na **Thread** lista suspensa na barra de ferramentas. Para mostrar todos os threads novamente, selecione a **Mostrar somente Threads sinalizados** ícone novamente.
   
   >[!TIP]
   >Após você sinalizou alguns threads, você pode colocar o cursor no editor de códigos, clique com botão direito e selecione **executar Threads sinalizados Cursor**. Certifique-se de escolher entrará em código que todos os threads sinalizados. **Executar Threads sinalizados até o Cursor** segmentos na linha de código, tornando mais fácil controlar a ordem de execução pelo selecionada fará uma pausa [congelando e Descongelando threads](#bkmk_freeze).
   
1. Para alternar o status de sinalizado ou sem sinalização do thread em execução no momento, selecione o único sinalizador **estado atual threads sinalizados** botão de barra de ferramentas, à esquerda do **Mostrar somente Threads sinalizados** botão. Sinalizar o thread atual é útil para localizar o thread atual, quando apenas threads sinalizados estão sendo exibidos. 
   
1. Para remover a sinalização de um thread, passe o mouse sobre o marcador de thread no código-fonte e selecione o ícone de sinalizador vermelho desmarcá-la, ou o marcador de thread com o botão direito e selecione **Remover sinalização**.  

### <a name="flag-and-unflag-threads-in-the-threads-window"></a>Sinalizar e remover sinalização de threads na janela Threads 

No **Threads** janela, o thread sinalizado possui vermelho sinalizador ícones ao lado deles, enquanto os threads sem sinalização, se mostrado, têm ícones vazios.

![Janela Threads](../debugger/media/dbg-threads-window.png "janela Threads")  
  
Selecione um ícone de sinalizador para alterar o estado de thread sinalizado ou sem sinalização, dependendo do seu estado atual. 

Você pode também uma linha com o botão direito e selecione **sinalizador**, **Remover sinalização**, ou **Remover sinalização de todos os Threads** no menu de atalho. 

O **Threads** barra de ferramentas da janela também tem um **Mostrar somente Threads sinalizados** botão, que é à direita, um dos ícones de sinalizador de dois. Funciona da mesma maneira como o botão sobre o **local de depuração** barra de ferramentas e um dos botões controla a exibição em ambos os locais. 

### <a name="other-threads-window-features"></a>Outros recursos da janela de Threads

No **Threads** janela, selecione o cabeçalho de qualquer coluna para classificar os threads por essa coluna. Selecione novamente para inverter a ordem de classificação. Se todos os threads estão sendo exibidos, selecionando a coluna de ícone de sinalizador classifica os threads por status sinalizado ou sem sinalização. 

A segunda coluna dos **Threads** janela (com nenhum cabeçalho) é a **do Thread atual** coluna. Uma seta amarela nesta coluna marca o ponto de execução atual. 

O **local** coluna mostra onde cada thread aparece no código-fonte. Selecione a seta de expansão ao lado de **local** entrada ou passe o mouse sobre a entrada, para mostrar uma pilha de chamadas parcial para esse thread. 

>[!TIP]
>Para obter uma exibição gráfica das pilhas de chamada para threads, use o [pilhas paralelas](../debugger/using-the-parallel-stacks-window.md) janela. Para abrir a janela durante a depuração, selecione **Debug**> **Windows** > **pilhas paralelas**.  

Além **sinalizador**, **Remover sinalização**, e **Remover sinalização de todos os Threads**, o menu de contexto para **Thread** tem itens da janela:

- O **Mostrar Threads em origem** botão.
- **Exibição hexadecimal**, as alterações que o **ID do Thread**s no **Threads** janela de decimal para o formato hexadecimal. 
- [Alternar para Thread](#switch-to-another-thread), que mudará imediatamente a execução para esse thread. 
- **Renomear**, que permite que você altere o nome do thread. 
- [Congelar e descongelar](#bkmk_freeze) comandos.

## <a name="bkmk_freeze"></a> Congelar e descongelar a execução de thread 

Você pode congelar e descongelar, ou suspender e retomar os threads para controlar a ordem na qual os threads de executam o trabalho. Congelando e Descongelando threads podem ajudá-lo a resolver problemas de simultaneidade, como deadlocks e condições de corrida.

> [!TIP]
> Para seguir um único thread sem congelamento de outros threads, que também é um cenário comum de depuração, consulte [começar a depurar aplicativos multissegmentados](../debugger/get-started-debugging-multithreaded-apps.md#bkmk_follow_a_thread).
  
**Para congelar e descongelar threads:**  
  
1. No **Threads** janela, clique em qualquer thread e, em seguida, selecione **congelar**. Um **pausa** ícone na **Thread atual** coluna indica que o thread está congelado.  
   
1. Selecione **colunas** na **Threads** barra de ferramentas da janela e, em seguida, selecione **contagem suspensa** para exibir o **contagem suspensa** coluna. É o valor de contagem suspensa para o thread congelado **1**.  
   
1. Clique com botão direito no thread congelado e selecione **descongelar**.  
  
   O **pausa** ícone desaparece e o **contagem suspensa** valor muda para **0**. 
  
## <a name="switch-to-another-thread"></a>Mudar para outro thread 

Você poderá ver uma **o aplicativo está no modo de interrupção** janela quando você tentar mudar para outro thread. Esta janela indica que o thread não tem qualquer código que o depurador atual pode exibir. Por exemplo, você pode depurar o código gerenciado, mas o thread é o código nativo. A janela oferece sugestões para resolver o problema. 
  
**Para alternar para outro thread:**

1. No **Threads** janela, anote a ID do thread atual, que é o thread com uma seta amarela na **Thread atual** coluna. Você vai querer voltar para esse thread para continuar seu aplicativo. 
   
1. Um thread diferente com o botão direito e selecione **alternar para Thread** no menu de contexto.  
   
1. Observe que o local de seta amarela foi alterado na **Threads** janela. O marcador de thread atual original também permanece, como uma estrutura de tópicos. 
   
   Examine a dica de ferramenta sobre o marcador de thread no editor de código fonte e a lista na **Thread** lista suspensa a **local de depuração** barra de ferramentas. Observe que o thread atual também foi alterado lá. 
   
1. Sobre o **local de depuração** barra de ferramentas, selecione um thread diferente do **Thread** lista. Observe que o thread atual também será alterada em dois locais. 
   
1. No editor de código fonte, clique com botão direito um marcador de thread, aponte para **alternar para Thread**e selecione outro thread na lista. Observe que o thread atual é alterado em todos os três locais.  
   
Com o marcador de thread no código-fonte, você pode alternar somente para threads que pararam nesse local. Ao usar a janela **Threads** e a barra de ferramentas **Localização de Depuração**, você pode alternar para qualquer thread.   

Você aprendeu as Noções básicas de depuração de aplicativos multithread. Você pode observar, sinalizar e remover sinalização e congelar e descongelar threads usando a **Threads** janela, o **Thread** listar no **local de depuração** barra de ferramentas ou marcadores de thread no editor de código fonte.
  
## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos multi-threaded](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [Como mudar para outro thread durante a depuração](../debugger/how-to-switch-to-another-thread-while-debugging.md)
