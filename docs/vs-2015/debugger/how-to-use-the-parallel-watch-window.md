---
title: 'Como: usar a janela de inspeção paralela | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.parallelwatch
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, parallel watch window
ms.assetid: 28004d9b-420c-48f7-b80e-ab1519802558
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 734a55cb06ee46afc6fc3518d6dffe349690d3d7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697487"
---
# <a name="how-to-use-the-parallel-watch-window"></a>Como usar a janela Inspeção Paralela
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Na janela Inspeção Paralela, você pode exibir simultaneamente os valores que uma expressão mantém em vários threads. Cada linha representa um thread que está sendo executado em um aplicativo, mas um thread pode ser representado em várias linhas. Mais especificamente, cada linha representa uma chamada de função cuja assinatura de função corresponde à função no registro de ativação atual. Você pode classificar, reorganizar, remover e agrupar os itens que estão nas colunas. Você pode sinalizar, remover sinalização, congelar (suspender) e descongelar (retomar) threads. As colunas a seguir são exibidas na janela **Inspeção Paralela**:  
  
- A coluna do sinalizador, na qual você pode marcar um thread ao qual deseja prestar atenção especial.  
  
- A coluna do quadro, na qual uma seta indica o quadro selecionado.  
  
- Uma coluna configurável que pode exibir o computador, o processo, o bloco, a tarefa e o thread.  
  
  > [!TIP]
  > Você deve abrir a janela de **tarefa paralela** para exibir as informações da tarefa na janela de **inspeção paralela** .  
  
- A **\<Add Watch>** coluna, na qual você pode inserir expressões a serem inspecionadas.  
  
  [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
### <a name="to-display-the-parallel-watch-window"></a>Para exibir a janela Inspeção Paralela  
  
1. Defina um ponto de interrupção no código.  
  
2. Na barra de menus, escolha **Depurar**, **Iniciar Depuração**. Aguarde até que o aplicativo atinja o ponto de interrupção.  
  
3. Na barra de menus, escolha **Depurar**, **Janelas**, **Inspeção Paralela** e selecione uma janela de inspeção. Você pode abrir até quatro janelas.  
  
### <a name="to-add-a-watch-expression"></a>Para adicionar uma expressão de inspeção  
  
- Selecione **\<Add Watch>** e especifique uma expressão de inspeção.  
  
### <a name="to-flag-or-unflag-a-thread"></a>Para sinalizar ou remover sinalização de um thread  
  
- Selecione a coluna sinalizador para a linha ou abra o menu de atalho para o thread e escolha **sinalizar** ou **desmarcar**.  
  
### <a name="to-display-only-flagged-threads"></a>Para exibir somente threads sinalizados  
  
- Escolha o botão Mostrar somente sinalizado no canto superior esquerdo da janela de **inspeção paralela** .  
  
### <a name="to-switch-frames"></a>Para alternar quadros  
  
- Clique duas vezes na coluna do quadro. (Teclado: selecione a linha e pressione Enter.)  
  
### <a name="to-sort-a-column"></a>Para classificar uma coluna  
  
- Selecione o título da coluna.  
  
### <a name="to-group-threads"></a>Para agrupar threads  
  
- Abra o menu de atalho da janela Inspeção Paralela, escolha **Agrupar por** e selecione o item de submenu apropriado.  
  
### <a name="to-freeze-or-thaw-threads"></a>Para congelar ou descongelar threads  
  
- Abra o menu de atalho da linha e escolha **Congelar** ou **Descongelar**.  
  
### <a name="to-export-the-data-in-the-parallel-watch-window"></a>Para exportar os dados na janela Inspeção Paralela  
  
- Escolha o botão **Abrir no Excel** e, depois, **Abrir no Excel** ou **Exportar para CSV**.  
  
### <a name="to-filter-by-a-boolean-expression"></a>Para filtrar por uma expressão booliana  
  
- Insira uma expressão booliana na caixa **Filtrar por Expressão Booliana**. O depurador avalia a expressão para cada contexto de thread. Apenas as linhas nas quais o valor é `true` é exibido.  
  
## <a name="see-also"></a>Consulte Também  
 [Depurar aplicativos multissegmentados](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [Como: usar a janela threads GPU](../debugger/how-to-use-the-gpu-threads-window.md)   
 [Walkthrough: Depurando um aplicativo C++ AMP](https://msdn.microsoft.com/library/40e92ecc-f6ba-411c-960c-b3047b854fb5)
