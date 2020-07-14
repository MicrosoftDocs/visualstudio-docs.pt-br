---
title: Definir uma inspeção em variáveis em threads paralelos | Microsoft Docs
ms.date: 04/25/2017
ms.topic: how-to
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9fb0d5ac60ea5ab89b02a624488b5df4f8a7164b
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348620"
---
# <a name="set-a-watch-on-variables-in-parallel-threads-in-visual-studio-c-visual-basic-c"></a>Definir uma inspeção em variáveis em threads paralelos no Visual Studio (C#, Visual Basic, C++)
Na janela Inspeção Paralela, você pode exibir simultaneamente os valores que uma expressão mantém em vários threads. Cada linha representa um thread que está sendo executado em um aplicativo, mas um thread pode ser representado em várias linhas. Mais especificamente, cada linha representa uma chamada de função cuja assinatura de função corresponde à função no registro de ativação atual. Você pode classificar, reorganizar, remover e agrupar os itens que estão nas colunas. Você pode sinalizar, remover sinalização, congelar (suspender) e descongelar (retomar) threads. As colunas a seguir são exibidas na janela **Inspeção Paralela**:

- A coluna do sinalizador, na qual você pode marcar um thread ao qual deseja prestar atenção especial.

- A coluna de thread atual, na qual uma seta amarela indica o thread atual (uma seta verde com uma parte inferior indica que um thread não atual tem o contexto do depurador atual).

- Uma coluna configurável que pode exibir o computador, o processo, o bloco, a tarefa e o thread.

  > [!TIP]
  > Para exibir as informações da tarefa na janela de **inspeção paralela** , você deve primeiro abrir a janela de **tarefa** .

- As colunas *Adicionar inspeção* em branco, nas quais você pode inserir expressões para observar.

  [!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-display-the-parallel-watch-window"></a>Para exibir a janela Inspeção Paralela

1. Defina um ponto de interrupção no código.

2. Na barra de menus, escolha **Depurar**, **Iniciar Depuração**. Aguarde até que o aplicativo atinja o ponto de interrupção.

3. Na barra de menus, escolha **Depurar**, **Janelas**, **Inspeção Paralela** e selecione uma janela de inspeção. Você pode abrir até quatro janelas.

### <a name="to-add-a-watch-expression"></a>Para adicionar uma expressão de inspeção

- Selecione uma das colunas *Adicionar inspeção* em branco e, em seguida, insira uma expressão de inspeção.

### <a name="to-flag-or-unflag-a-thread"></a>Para sinalizar ou remover sinalização de um thread

- Selecione a coluna sinalizador para a linha (primeira coluna) ou abra o menu de atalho para o thread e escolha **sinalizar** ou **desmarcar**.

### <a name="to-display-only-flagged-threads"></a>Para exibir somente threads sinalizados

- Escolha o botão **Mostrar somente sinalizado** no canto superior esquerdo da janela de **inspeção paralela** .

### <a name="to-switch-to-another-thread"></a>Para alternar para outro thread

- Clique duas vezes na coluna thread atual (segunda coluna). (Teclado: selecione a linha e pressione Enter.)

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

## <a name="see-also"></a>Veja também
- [Depurar aplicativos multithread](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [Como: usar a janela threads GPU](../debugger/how-to-use-the-gpu-threads-window.md)
- [Walkthrough: Depurando um aplicativo C++ AMP](/cpp/parallel/amp/walkthrough-debugging-a-cpp-amp-application)