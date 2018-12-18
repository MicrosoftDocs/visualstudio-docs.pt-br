---
title: 'Como: usar a janela de Threads GPU | Microsoft Docs'
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
- vs.debug.gputhreads
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, GPU threads window
ms.assetid: c647c502-a9f0-48e0-a430-976744a5fa51
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8afd9cd09cf5977f58ee3a48b891f5291869b49c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51799165"
---
# <a name="how-to-use-the-gpu-threads-window"></a>Como usar a janela Threads de GPU
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Na janela Threads da GPU, você pode examinar e trabalhar com threads que estão sendo executadas no GPU no aplicativo que você está depurando. Para obter mais informações sobre aplicativos que são executados na GPU, consulte [visão geral do C++ AMP](http://msdn.microsoft.com/library/9e593b06-6e3c-43e9-8bae-6d89efdd39fc).  
  
 A janela de Threads da GPU contém uma tabela na qual cada linha representa um conjunto de threads de GPU que têm os mesmos valores em todas as colunas. Você pode classificar, reorganizar, remover e agrupar os itens que estão nas colunas. Você pode sinalizar, remover sinalização, congelar (suspender) e descongelar (retomar) threads da janela de Threads da GPU. As colunas a seguir são exibidas na janela Threads da GPU:  
  
- A coluna do sinalizador, na qual você pode marcar um thread ao qual deseja prestar atenção especial.  
  
- A coluna thread ativo, em que uma seta amarela indica um thread ativo. Uma seta indica um thread onde a execução interrompe no depurador.  
  
- O **contagem de threads** coluna, que exibe o número de threads no mesmo local.  
  
- O **linha** coluna, que exibe a linha de código em que cada grupo de threads está localizado.  
  
- O **endereço** coluna, que exibe o endereço da instrução onde cada grupo de threads está localizado. Por padrão, essa coluna está ocultada.  
  
- O **local** coluna, que é o local no código-fonte.  
  
- O **Status** coluna, que mostra se o thread está ativo, bloqueado, não iniciado ou concluído.  
  
- O **bloco** coluna, que mostra o índice do bloco para os segmentos na linha.  
  
  O cabeçalho da tabela mostra que o quadro e o thread estão sendo exibidos.  
  
  [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
### <a name="to-display-the-gpu-threads-window"></a>Para exibir a janela Threads da GPU  
  
1.  No **Gerenciador de Soluções**, abra o menu de atalho para o projeto e escolha **Propriedades**.  
  
2.  No **páginas de propriedades** janela para o projeto sob **propriedades de configuração**, escolha **depuração**.  
  
3.  No **depurador a iniciar** lista, selecione **depurador Local do Windows**. No **tipo de depurador** lista, selecione **somente GPU**. Você deve escolher este depurador para parar em pontos de interrupção no código executado no GPU.  
  
4.  Escolha o botão **OK**.  
  
5.  Defina um ponto de interrupção no código do GPU.  
  
6.  Na barra de menus, escolha **Depurar**, **Iniciar Depuração**. Aguarde até que o aplicativo atinja o ponto de interrupção.  
  
7.  Barra de menus, escolha **Debug**, **Windows**, **Threads da GPU**.  
  
### <a name="to-change-to-a-different-active-thread"></a>Para alterar para um thread ativo diferente  
  
-   Clique duas vezes na coluna. (Teclado: selecione a linha e escolha Enter.)  
  
### <a name="to-display-a-particular-tile-and-thread"></a>Para exibir um determinado bloco e o thread  
  
1.  Escolha o **expandir o comutador de Thread** botão na janela Threads da GPU.  
  
2.  Insira os valores do quadro e de thread nas caixas de texto.  
  
3.  Escolha o botão que tem a seta.  
  
### <a name="to-display-or-hide-a-column"></a>Para exibir ou ocultar uma coluna  
  
-   Abra o menu de atalho para a janela Threads da GPU, escolha **colunas**e, em seguida, escolha a coluna que você deseja exibir ou ocultar.  
  
### <a name="to-sort-by-a-column"></a>Para classificar por coluna  
  
-   Selecione o título da coluna.  
  
### <a name="to-group-threads"></a>Para agrupar threads  
  
-   Abra o menu de atalho para a janela Threads da GPU, escolha **Group By**e, em seguida, escolha um dos nomes de coluna exibidos. Escolher **nenhum** para desagrupar os threads.  
  
### <a name="to-freeze-or-thaw-a-row-of-threads"></a>Para congelar ou descongelar uma linha de threads  
  
-   Abra o menu de atalho para a linha e escolha **congelar** ou **descongelar**.  
  
### <a name="to-flag-or-unflag-a-row-of-threads"></a>Para sinalizar ou remover sinalização de uma linha de threads  
  
-   Selecione a coluna do sinalizador do thread, ou abra o menu de atalho para o thread e escolha **sinalizador** ou **Remover sinalização**.  
  
### <a name="to-display-only-flagged-threads"></a>Para exibir somente threads sinalizados  
  
-   Escolha o botão de sinalizador na janela Threads da GPU.  
  
## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos multithread](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [Como: usar a janela Inspeção paralela](../debugger/how-to-use-the-parallel-watch-window.md)   
 [Passo a passo: depurando um aplicativo C++ AMP](http://msdn.microsoft.com/library/40e92ecc-f6ba-411c-960c-b3047b854fb5)



