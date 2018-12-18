---
title: Definir uma inspeção nas variáveis em Threads paralelos | Microsoft Docs
ms.custom: ''
ms.date: 04/25/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.parallelwatch
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, parallel watch window
ms.assetid: 28004d9b-420c-48f7-b80e-ab1519802558
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e9381479fdfa3d64f3504e947f49411b99d53e2d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49857946"
---
# <a name="set-a-watch-on-variables-in-parallel-threads-in-visual-studio"></a>Definir uma inspeção nas variáveis em Threads paralelos no Visual Studio
Na janela Inspeção Paralela, você pode exibir simultaneamente os valores que uma expressão mantém em vários threads. Cada linha representa um thread que está sendo executado em um aplicativo, mas um thread pode ser representado em várias linhas. Mais especificamente, cada linha representa uma chamada de função cuja assinatura de função corresponde à função no registro de ativação atual. Você pode classificar, reorganizar, remover e agrupar os itens que estão nas colunas. Você pode sinalizar, remover sinalização, congelar (suspender) e descongelar (retomar) threads. As colunas a seguir são exibidas na **inspeção paralela** janela:  
  
- A coluna do sinalizador, na qual você pode marcar um thread ao qual deseja prestar atenção especial.  
  
- A coluna atual do thread, no qual uma seta amarela indica que o thread atual (uma seta verde com uma parte final encaracolada indica que um thread não atual tem o contexto do depurador atual).  
  
- Uma coluna configurável que pode exibir o computador, o processo, o bloco, a tarefa e o thread.  
  
  > [!TIP]
  >  Para informações sobre a exibição de tarefa na **inspeção paralela** , você deverá primeiro abrir o **tarefa** janela.  
  
- O espaço em branco *Adicionar inspeção* colunas, na qual você pode inserir expressões para assistir.  
  
  [!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]  
  
### <a name="to-display-the-parallel-watch-window"></a>Para exibir a janela Inspeção Paralela  
  
1.  Defina um ponto de interrupção no código.  
  
2.  Na barra de menus, escolha **Depurar**, **Iniciar Depuração**. Aguarde até que o aplicativo atinja o ponto de interrupção.  
  
3.  Na barra de menus, escolha **Debug**, **Windows**, **inspeção paralela**e, em seguida, escolha uma janela de observação. Você pode abrir até quatro janelas.  
  
### <a name="to-add-a-watch-expression"></a>Para adicionar uma expressão de inspeção  
  
-   Selecione uma do espaço em branco *Adicionar inspeção* colunas e, em seguida, insira uma expressão de inspeção.  
  
### <a name="to-flag-or-unflag-a-thread"></a>Para sinalizar ou remover sinalização de um thread  
  
-   Selecione a coluna do sinalizador da linha (primeira coluna), ou abra o menu de atalho para o thread e escolha **sinalizador** ou **Remover sinalização**.  
  
### <a name="to-display-only-flagged-threads"></a>Para exibir somente threads sinalizados  
  
-   Escolha o **Mostrar somente sinalizados** botão no canto superior esquerdo do **inspeção paralela** janela.  
  
### <a name="to-switch-to-another-thread"></a>Para alternar para outro thread  
  
-   Clique duas vezes a coluna de thread atual (segunda coluna). (Teclado: selecione a linha e pressione Enter.)  
  
### <a name="to-sort-a-column"></a>Para classificar uma coluna  
  
-   Selecione o título da coluna.  
  
### <a name="to-group-threads"></a>Para agrupar threads  
  
-   Abra o menu de atalho para a janela Inspeção paralela, escolha **Group By**e, em seguida, escolha o item de submenu apropriado.  
  
### <a name="to-freeze-or-thaw-threads"></a>Para congelar ou descongelar threads  
  
-   Abra o menu de atalho para a linha e escolha **congelar** ou **descongelar**.  
  
### <a name="to-export-the-data-in-the-parallel-watch-window"></a>Para exportar os dados na janela Inspeção Paralela  
  
-   Escolha o **abrir no Excel** botão e, em seguida, escolha **abrir no Excel** ou **exportar para CSV**.  
  
### <a name="to-filter-by-a-boolean-expression"></a>Para filtrar por uma expressão booliana  
  
-   Insira uma expressão booleana entre o **filtrar por expressão booliana** caixa. O depurador avalia a expressão para cada contexto de thread. Apenas as linhas nas quais o valor é `true` é exibido.  
  
## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos multithread](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [Como: usar a janela de Threads GPU](../debugger/how-to-use-the-gpu-threads-window.md)   
 [Passo a passo: depurando um aplicativo C++ AMP](/cpp/parallel/amp/walkthrough-debugging-a-cpp-amp-application)