---
title: Exibir DLLs e executáveis
titleSuffix: Visual Studio Modules window
ms.custom: seodec18
ms.date: 11/04/2018
ms.topic: how-to
f1_keywords:
- vs.debug.modules
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugger, Modules window
- Modules window
- executable files, displaying while debugging
- debugging [Visual Studio], displaying modules
- DLLs, displaying while debugging
- modules, displaying
ms.assetid: d840fdca-b035-4452-b652-72580c831896
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4fa284a44f75503a2890a15981d2b4f9947be2fa
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348672"
---
# <a name="view-dlls-and-executables-in-the-modules-window-c-c-visual-basic-f"></a>Exibir DLLs e executáveis na janela módulos (C#, C++, Visual Basic, F #)

Durante a depuração do Visual Studio, a janela **módulos** lista e mostra informações sobre as DLLs e os executáveis (arquivos *. exe* ) que seu aplicativo usa.

> [!NOTE]
> A janela Modules não está disponível para depuração de script ou SQL.

## <a name="use-the-modules-window"></a>Usar a janela Módulos

Para abrir a janela módulos, enquanto estiver Depurando, selecione **depurar**  >  **Windows**  >  **módulos** do Windows (ou pressione **Ctrl + Alt + U**).

Por padrão, a janela **Módulos** classifica os módulos pela ordem de carregamento. Para classificar por qualquer coluna de janela, selecione o cabeçalho na parte superior da coluna.

## <a name="load-symbols"></a>Carregar símbolos

A coluna **status do símbolo** na janela **módulos** mostra quais módulos têm símbolos de depuração carregados. Se o status for **ignorado ao carregar símbolos**, **não for possível localizar ou abrir o arquivo PDB**ou **carregar desabilitado pela configuração incluir/excluir**, você poderá carregar os símbolos manualmente. Para obter mais informações sobre como carregar e usar símbolos, consulte [especificar símbolo (. pdb) e arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

**Para carregar os símbolos manualmente:**

1. Na janela **módulos** , clique com o botão direito do mouse no módulo para o qual os símbolos não foram carregados.

   - Selecione **informações de carregamento de símbolo** para obter detalhes sobre por que os símbolos não foram carregados.

   - Selecione **carregar símbolos** para carregar os símbolos manualmente.

1. Se os símbolos não forem carregados, selecione **configurações de símbolo** para abrir a caixa de diálogo **Opções** e especifique ou altere os locais de carregamento de símbolos.

   Você pode baixar símbolos dos servidores de símbolos públicos da Microsoft ou outros servidores ou carregar símbolos de uma pasta no seu computador. Para obter detalhes, consulte [especificar locais de símbolo e comportamento de carregamento](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#BKMK_Specify_symbol_locations_and_loading_behavior).

**Para alterar as configurações de comportamento de carregamento de símbolos:**

1. Na janela **Módulos**, clique com o botão direito do mouse direito em qualquer módulo.

1. Selecione **configurações de símbolo**.

1. Selecione **carregar todos os símbolos**ou selecione os módulos a serem incluídos ou excluídos.

1. Selecione **OK**. As alterações entrarão em vigor na próxima sessão de depuração.

**Para alterar o comportamento de carregamento de símbolos para um módulo específico:**

1. Na janela **Módulos**, clique com o botão direito do mouse no módulo.

1. No menu de clique com o botão direito do mouse, selecione ou desmarque **sempre carregar automaticamente**. As alterações entrarão em vigor na próxima sessão de depuração.

## <a name="see-also"></a>Veja também
- [Interrompendo a execução](/previous-versions/visualstudio/visual-studio-2010/7z9se2d8(v=vs.100))
- [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)
- [Especificar o símbolo (. pdb) e os arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)