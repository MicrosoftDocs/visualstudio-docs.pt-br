---
title: Depurar um aplicativo multithread
description: Depurar usando a janela threads e a barra de ferramentas Debug Location no Visual Studio
ms.date: 02/14/2020
ms.topic: how-to
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 33375a8970638765d02a94e6e3e9cd8afc1a0fe7
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348646"
---
# <a name="walkthrough-debug-a-multithreaded-app-using-the-threads-window-c-visual-basic-c"></a>Walkthrough: Depurar um aplicativo multithread usando a janela threads (C#, Visual Basic, C++)

Vários elementos da interface do usuário do Visual Studio ajudam você a depurar aplicativos multithread. Este artigo apresenta recursos de depuração multithread na janela do editor de código, na barra de ferramentas **local de depuração** e na janela **threads** . Para obter informações sobre outras ferramentas para depurar aplicativos multithread, consulte [introdução à depuração de aplicativos multissegmentados](../debugger/get-started-debugging-multithreaded-apps.md).

A conclusão deste tutorial leva apenas alguns minutos e o familiariza com os conceitos básicos da depuração de aplicativos multissegmentados.

## <a name="create-a-multithreaded-app-project"></a>Criar um projeto de aplicativo multithread

Crie o seguinte projeto de aplicativo multithread para usar neste tutorial:

1. Abra o Visual Studio e crie um projeto.

   ::: moniker range=">=vs-2019"

   Se a janela iniciar não estiver aberta, escolha **arquivo** > **Iniciar janela**.

   Na janela iniciar, escolha **criar um novo projeto**.

   Na janela **Criar um novo projeto**, insira ou digite *console* na caixa de pesquisa. Em seguida, escolha **C#** ou **C++** na lista idioma e, em seguida, escolha **Windows** na lista plataforma. 

   Depois de aplicar os filtros de idioma e plataforma, escolha o **aplicativo de console (.NET Core)** ou, para C++, modelo de **aplicativo de console** e escolha **Avançar**.

   > [!NOTE]
   > Se você não vir o modelo correto, vá para **ferramentas**  >  **obter ferramentas e recursos...**, que abre a instalador do Visual Studio. Escolha o desenvolvimento de **área de trabalho .net** ou **desenvolvimento de desktop com** carga de trabalho C++ e, em seguida, escolha **Modificar**.

   Na janela **configurar seu novo projeto** , digite ou insira *MyThreadWalkthroughApp* na caixa **nome do projeto** . Em seguida, escolha **criar**.

   ::: moniker-end
   ::: moniker range="vs-2017"
   Na barra de menus superior, escolha **arquivo**  >  **novo**  >  **projeto**. No painel esquerdo da caixa de diálogo **novo projeto** , escolha o seguinte:

   - Para um aplicativo C#, em **Visual C#**, escolha **Windows Desktop**e, no painel central, escolha **aplicativo de console (.NET Framework)**.
   - Para um aplicativo C++, em **Visual C++**, escolha **Windows Desktop**, e, em seguida, escolha **aplicativo de console do Windows**.

   Se você não vir o **aplicativo de console (.NET Core)** ou, para C++, o modelo de projeto de **aplicativo de console** , vá para **ferramentas**  >  **obter ferramentas e recursos...**, que abre a instalador do Visual Studio. Escolha o desenvolvimento de **área de trabalho .net** ou **desenvolvimento de desktop com** carga de trabalho C++ e, em seguida, escolha **Modificar**.

   Em seguida, digite um nome como *MyThreadWalkthroughApp* e clique em **OK**.

   Selecione **OK**.
   ::: moniker-end

   Um novo projeto de console é exibido. Depois que o projeto tiver sido criado, um arquivo de origem será exibido. Dependendo do idioma escolhido, o arquivo de origem pode ser chamado *Program.cs*, *MyThreadWalkthroughApp. cpp*ou *Module1. vb*.

1. Substitua o código no arquivo de origem pelo código de exemplo C# ou C++ de [introdução depurar aplicativos multissegmentados](../debugger/get-started-debugging-multithreaded-apps.md).

1. Selecione **arquivo**  >  **salvar tudo**.

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

1. Defina um ponto de interrupção na `Console.WriteLine();` linha clicando na medianiz esquerda ou selecionando a linha e pressionando **F9**.

   O ponto de interrupção aparece como um círculo vermelho na medianiz esquerda ao lado da linha de código.

1. Selecione **depurar**  >  **Iniciar Depuração**ou pressione **F5**.

   O aplicativo é iniciado no modo de depuração e pausa no ponto de interrupção.

1. No modo de interrupção, abra a janela **threads** selecionando **depurar**  >  **Windows**  >  **threads**do Windows. Você deve estar em uma sessão de depuração para abrir ou Ver os **threads** e outras janelas de depuração.

## <a name="examine-thread-markers"></a>Examinar marcadores de thread

1. No código-fonte, localize a `Console.WriteLine();` linha.

   1. Clique com o botão direito do mouse na janela **threads** e selecione **Mostrar threads em origem** ![Mostrar threads em origem](../debugger/media/dbg-multithreaded-show-threads.png "ThreadMarker") no menu.

   A medianiz ao lado da linha de código-fonte agora exibe um ![marcador](../debugger/media/dbg-thread-marker.png "Marcador de thread")de thread com ícone de *marcador de thread* . O marcador de thread indica que um thread está parado nesse local. Se houver mais de um thread parado no local, o ícone ![vários threads](../debugger/media/dbg-multithreaded-show-threads.png "vários threads") será exibido.

1. Passe o ponteiro sobre o marcador de thread. Um DataTip é exibido, mostrando o nome e o número de ID do thread para o thread ou threads interrompidos. Os nomes de thread podem ser `<No Name>` .

   >[!TIP]
   >Para ajudar a identificar os threads sem nome, você pode renomeá-los na janela **threads** . Clique com o botão direito do mouse no thread e selecione **renomear**.

1. Clique com o botão direito do mouse no marcador de thread no código-fonte para ver as opções disponíveis no menu de atalho.

## <a name="flag-and-unflag-threads"></a>Sinalizar e remover sinalizador de threads

Você pode sinalizar threads para acompanhar os threads para os quais você deseja prestar atenção especial.

Sinalizar e remover o sinalizador de threads do editor de código-fonte ou da janela **threads** . Escolha se deseja exibir somente threads sinalizados ou todos os threads, das barras de ferramentas **local de depuração** ou janela **threads** . As seleções feitas de qualquer local afetam todos os locais.

### <a name="flag-and-unflag-threads-in-source-code"></a>Sinalizar e remover o sinalizador de threads no código-fonte

1. Abra a barra de ferramentas **local de depuração** selecionando **Exibir**  >  **barras de ferramentas**  >  **local de depuração**. Você também pode clicar com o botão direito do mouse na área da barra de ferramentas e selecionar **local de depuração**.

1. A barra de ferramentas do **local de depuração** tem três campos: **processo**, **thread**e registro de **ativação**. Solte a lista de **threads** e observe quantos threads existem. Na lista de **threads** , o thread atualmente em execução é marcado por um **>** símbolo.

1. Na janela código-fonte, passe o mouse sobre um ícone de marcador de thread na medianiz e selecione o ícone de sinalizador (ou um dos ícones de sinalizador vazios) no DataTip. O ícone de sinalizador fica vermelho.

   Você também pode clicar com o botão direito do mouse em um ícone de marcador de thread, apontar para **sinalizador**e, em seguida, selecionar um thread para sinalizar no menu de atalho.

1. Na barra de ferramentas **local de depuração** , selecione o ícone **Mostrar somente threads sinalizados** ![Mostrar threads sinalizados](../debugger/media/dbg-threads-show-flagged.png "Mostrar threads sinalizados"), à direita do campo **thread** . O ícone fica esmaecido, a menos que um ou mais threads sejam sinalizados.

   Somente o thread sinalizado agora aparece no menu suspenso **thread** na barra de ferramentas. Para mostrar todos os threads novamente, selecione o ícone **Mostrar somente threads sinalizados** novamente.

   >[!TIP]
   >Depois de sinalizar alguns threads, você pode posicionar o cursor no editor de códigos, clicar com o botão direito do mouse e selecionar **executar threads sinalizados para o cursor**. Verifique se você escolheu o código que todos os threads sinalizados atingirão. **Executar threads sinalizados para o cursor** pausará threads na linha de código selecionada, facilitando o controle da ordem de execução [congelando e descongelando threads](#bkmk_freeze).

1. Para alternar o status sinalizado ou não sinalizado do thread em execução no momento, marque o botão de barra de ferramentas de alternância de sinalizador único **thread atual marcado** para a esquerda do botão **Mostrar somente threads sinalizados** . A sinalização do thread atual é útil para localizar o thread atual quando apenas threads sinalizados são mostrados.

1. Para remover o sinalizador de um thread, passe o mouse sobre o marcador de thread no código-fonte e selecione o ícone de sinalizador vermelho para limpá-lo ou clique com o botão direito do mouse no marcador de thread e selecione **desmarcar**.

### <a name="flag-and-unflag-threads-in-the-threads-window"></a>Sinalizar e remover o sinalizador de threads na janela threads

Na janela **threads** , os threads sinalizados têm ícones de sinalizador vermelhos ao lado deles, enquanto os threads não sinalizados, se mostrados, têm ícones vazios.

![Janela Threads](../debugger/media/dbg-threads-window.png "Janela Threads")

Selecione um ícone de sinalizador para alterar o estado do thread para sinalizado ou não sinalizado, dependendo de seu estado atual.

Você também pode clicar com o botão direito do mouse em uma linha e selecionar **sinalizar**, **desmarcar**ou **desmarcar todos os threads** no menu de atalho.

A barra de ferramentas da janela **threads** também tem um botão **Mostrar somente threads sinalizados** , que é o righthand um dos dois ícones de sinalizador. Ele funciona da mesma forma que o botão na barra de ferramentas **local de depuração** e o botão controla a exibição em ambos os locais.

### <a name="other-threads-window-features"></a>Outros recursos da janela threads

Na janela **threads** , selecione o cabeçalho de qualquer coluna para classificar os threads por essa coluna. Selecione novamente para inverter a ordem de classificação. Se todos os threads estiverem sendo mostrados, a seleção da coluna ícone de sinalizador classificará os threads por status sinalizado ou não sinalizado.

A segunda coluna da janela **threads** (sem cabeçalho) é a coluna **thread atual** . Uma seta amarela nesta coluna marca o ponto de execução atual.

A coluna **local** mostra onde cada thread aparece no código-fonte. Selecione a seta de expansão ao lado da entrada **local** ou passe o mouse sobre a entrada para mostrar uma pilha de chamadas parcial para esse thread.

>[!TIP]
>Para uma exibição gráfica das pilhas de chamadas para threads, use a janela [pilhas paralelas](../debugger/using-the-parallel-stacks-window.md) . Para abrir a janela, durante a depuração, selecione **depurar** >  **Windows**  >  **pilhas paralelas**do Windows.

Além de **sinalizar**, **desmarcar**e remover **sinalizador de todos os threads**, o menu de contexto de clique com o botão direito do mouse para itens da janela de **thread** tem:

- O botão **Mostrar threads no código-fonte** .
- **Exibição hexadecimal**, que altera a **ID do thread**s na janela **threads** do formato decimal para hexadecimal.
- [Alterne para thread](#switch-to-another-thread), que imediatamente alterna a execução para esse thread.
- **Renomear**, que permite alterar o nome do thread.
- [Congelar e descongelar](#bkmk_freeze) comandos.

## <a name="freeze-and-thaw-thread-execution"></a><a name="bkmk_freeze"></a>Congelar e descongelar a execução do thread

Você pode congelar e descongelar, ou suspender e retomar, threads para controlar a ordem na qual os threads executam o trabalho. Congelar e descongelar Threads pode ajudá-lo a resolver problemas de simultaneidade, como deadlocks e condições de corrida.

> [!TIP]
> Para seguir um único thread sem congelar outros threads, que também é um cenário de depuração comum, consulte Introdução à [depuração de aplicativos multissegmentados](../debugger/get-started-debugging-multithreaded-apps.md#bkmk_follow_a_thread).

**Para congelar e descongelar Threads:**

1. Na janela **threads** , clique com o botão direito do mouse em qualquer thread e selecione **congelar**. Um ícone de **pausa** na coluna **thread atual** indica que o thread está congelado.

1. Selecione **colunas** na barra de ferramentas da janela **threads** e selecione **contagem suspensa** para exibir a coluna **contagem suspensa** . O valor da contagem suspensa para o thread congelado é **1**.

1. Clique com o botão direito do mouse no thread congelado e selecione **descongelar**.

   O ícone de **pausa** desaparece e o valor da **contagem suspensa** é alterado para **0**.

## <a name="switch-to-another-thread"></a>Alternar para outro thread

Você pode ver que **o aplicativo está na** janela de modo de interrupção quando você tenta alternar para outro thread. Essa janela informa que o thread não tem nenhum código que o depurador atual possa exibir. Por exemplo, você pode estar Depurando código gerenciado, mas o thread é código nativo. A janela oferece sugestões para resolver o problema.

**Para alternar para outro thread:**

1. Na janela **threads** , anote a ID do thread atual, que é o thread com uma seta amarela na coluna **thread atual** . Você desejará voltar para este thread para continuar seu aplicativo.

1. Clique com o botão direito do mouse em um thread diferente e selecione **alternar para thread** no menu de contexto.

1. Observe que o local da seta amarela foi alterado na janela **threads** . O marcador de thread atual original também permanece como um contorno.

   Examine a dica de ferramenta no marcador de thread no editor de código-fonte e a lista no menu suspenso **thread** na barra de ferramentas **local de depuração** . Observe que o thread atual também foi alterado lá.

1. Na barra de ferramentas **local de depuração** , selecione um thread diferente na lista **thread** . Observe que o thread atual também é alterado nos outros dois locais.

1. No editor de código-fonte, clique com o botão direito do mouse em um marcador de thread, aponte para **alternar para thread**e selecione outro thread na lista. Observe que o thread atual é alterado em todos os três locais.

Com o marcador de thread no código-fonte, você pode alternar somente para threads que são interrompidos nesse local. Ao usar a janela **Threads** e a barra de ferramentas **Localização de Depuração**, você pode alternar para qualquer thread.

Agora você aprendeu os conceitos básicos da depuração de aplicativos multissegmentados. Você pode observar, sinalizar e desmarcar e congelar e descongelar Threads usando a janela **threads** , a lista de **threads** na barra de ferramentas **local de depuração** ou marcadores de thread no editor de código-fonte.

## <a name="see-also"></a>Veja também
- [Depurar aplicativos multissegmentados](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [Como mudar para outro thread durante a depuração](../debugger/how-to-switch-to-another-thread-while-debugging.md)
