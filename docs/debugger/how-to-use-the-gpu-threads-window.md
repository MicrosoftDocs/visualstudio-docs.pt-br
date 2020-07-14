---
title: Exibindo threads de GPU no depurador | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.gputthreads
- vs.debug.gputhreads
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, GPU threads window
ms.assetid: c647c502-a9f0-48e0-a430-976744a5fa51
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cbbb49a1017fb0bc65300f3c16050db4954e1103
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348711"
---
# <a name="how-to-use-the-gpu-threads-window-c"></a>Como: usar a janela threads GPU (C++)
Na janela Threads da GPU, você pode examinar e trabalhar com threads que estão sendo executadas no GPU no aplicativo que você está depurando. Para obter mais informações sobre aplicativos executados na GPU, consulte [C++ amp Visão geral](/cpp/parallel/amp/cpp-amp-overview).

 A janela de Threads da GPU contém uma tabela na qual cada linha representa um conjunto de threads de GPU que têm os mesmos valores em todas as colunas. Você pode classificar, reorganizar, remover e agrupar os itens que estão nas colunas. Você pode sinalizar, remover sinalização, congelar (suspender) e descongelar (retomar) threads da janela de Threads da GPU. As colunas a seguir são exibidas na janela Threads da GPU:

- A coluna do sinalizador, na qual você pode marcar um thread ao qual deseja prestar atenção especial.

- A coluna de thread atual, na qual uma seta amarela indica o thread atual.

- A coluna **Contagem de Threads**, que exibe o número de segmentos na mesma localização.

- A coluna de **Linha**, que exibe a linha de código em que cada grupo de segmentos está localizado.

- A coluna de **Endereço** que exibe o endereço da instrução em que cada grupo de threads está localizado. Por padrão, essa coluna está ocultada.

- A coluna **Localização**, que é a localização no código-fonte.

- A coluna **Status**, que mostra se o thread está ativo, bloqueado, não iniciado ou concluído.

- A coluna **Lado a lado**, que mostra o índice lado a lado para os segmentos na linha.

  O cabeçalho da tabela mostra que o quadro e o thread estão sendo exibidos.

  [!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-display-the-gpu-threads-window"></a>Para exibir a janela Threads da GPU

1. No **Gerenciador de soluções**, abra o menu de atalho do projeto e, em seguida, escolha **Propriedades**.

2. Na janela **Páginas de Propriedades** para o projeto, em **Propriedades de Configuração**, escolha **Depuração**.

3. Na lista **Depurador a iniciar**, selecione **Depurador Local do Windows**. Na lista **Tipo de Depurador**, selecione **Somente GPU**. Você deve escolher este depurador para parar em pontos de interrupção no código executado no GPU.

4. Clique no botão **OK**.

5. Defina um ponto de interrupção no código do GPU.

6. Na barra de menus, escolha **Depurar**, **Iniciar Depuração**. Aguarde até que o aplicativo atinja o ponto de interrupção.

7. Na barra de menus, escolha **Depurar**, **Janelas**, **Threads da GPU**.

### <a name="to-switch-to-a-different-thread"></a>Para alternar para um thread diferente

- Clique duas vezes na coluna. (Teclado: selecione a linha e escolha Enter.)

### <a name="to-display-a-particular-tile-and-thread"></a>Para exibir um determinado bloco e o thread

1. Escolha o botão **Expandir o Comutador de Thread** na janela Threads da GPU.

2. Insira os valores do quadro e de thread nas caixas de texto.

3. Escolha o botão que tem a seta.

### <a name="to-display-or-hide-a-column"></a>Para exibir ou ocultar uma coluna

- Abra o menu de atalho para a janela Threads da GPU, escolha **Colunas** e, em seguida, escolha a coluna que você quer exibir ou ocultar.

### <a name="to-sort-by-a-column"></a>Para classificar por coluna

- Selecione o título da coluna.

### <a name="to-group-threads"></a>Para agrupar threads

- Abra o menu de atalho da janela Threads da GPU, escolha **Agrupar por** e escolha um dos nomes de coluna exibidos. Escolha **Nenhum** para desagrupar os threads.

### <a name="to-freeze-or-thaw-a-row-of-threads"></a>Para congelar ou descongelar uma linha de threads

- Abra o menu de atalho da linha e escolha **Congelar** ou **Descongelar**.

### <a name="to-flag-or-unflag-a-row-of-threads"></a>Para sinalizar ou remover sinalização de uma linha de threads

- Selecione a coluna do sinalizador do thread ou abra o menu de atalho do thread e escolha **Sinalizar** ou **Remover Sinalização**.

### <a name="to-display-only-flagged-threads"></a>Para exibir somente threads sinalizados

- Escolha o botão de sinalizador na janela Threads da GPU.

## <a name="see-also"></a>Veja também
- [Depurar aplicativos multithread](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [Como: usar a janela de inspeção paralela](../debugger/how-to-use-the-parallel-watch-window.md)
- [Walkthrough: Depurando um aplicativo C++ AMP](/cpp/parallel/amp/walkthrough-debugging-a-cpp-amp-application)