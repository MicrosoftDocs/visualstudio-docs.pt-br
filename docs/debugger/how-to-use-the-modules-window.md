---
title: Exibir as DLLs e executáveis
titleSuffix: Visual Studio Modules window
ms.custom: seodec18
ms.date: 11/04/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2702eb38e895f5fa9021fae754ae1e4a9325cf18
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53066776"
---
# <a name="view-dlls-and-executables-in-the-modules-window-c-c-visual-basic-f"></a>Exibir as DLLs e executáveis na janela de módulos (C#, C++, Visual Basic, F#)
 
Durante a depuração do Visual Studio, o **módulos** janela lista e mostra informações sobre as DLLs e executáveis (*.exe* arquivos) seu aplicativo usa. 

> [!NOTE]
> A janela de módulos não está disponível para depuração de script ou SQL. 
  
## <a name="use-the-modules-window"></a>Usar a janela módulos

Para abrir a janela de módulos, enquanto você estiver depurando, selecione **Debug** > **Windows** > **módulos**. 
  
Por padrão, a janela **Módulos** classifica os módulos pela ordem de carregamento. Para classificar por qualquer coluna da janela, selecione o cabeçalho na parte superior da coluna.  
  
## <a name="load-symbols"></a>Carregar símbolos  

O **Status do símbolo** coluna o **módulos** janela mostra quais módulos têm símbolos de depuração carregados. Se o status for **carregamento de símbolos ignorado**, **não é possível localizar ou abrir o arquivo PDB**, ou **carregamento desabilitado pela configuração de inclusão/exclusão**, você pode carregar símbolos manualmente. Para obter mais informações sobre como carregar e usando símbolos, consulte [especificar arquivos de símbolo (. PDB) e código-fonte](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

**Para carregar símbolos manualmente:**  

1. No **módulos** janela, clique com botão direito do módulo para o qual os símbolos não carregados. 
   
   - Selecione **informações de carga de símbolo** para obter detalhes sobre por que os símbolos não foi carregado. 
   
   - Selecione **carregar símbolos** para carregar os símbolos manualmente.  
   
1. Se os símbolos não são carregados, selecione **configurações de símbolo** para abrir o **opções** caixa de diálogo e especificar ou alterar locais de carregamento de símbolo. 
   
   Você pode baixar os símbolos de servidores públicos de símbolos Microsoft ou de outros servidores ou carregar símbolos de uma pasta no seu computador. Para obter detalhes, consulte [especificar locais de símbolo e o comportamento de carregamento](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#BKMK_Specify_symbol_locations_and_loading_behavior).   

**Para alterar as configurações de comportamento de carregamento de símbolo:**  

1. Na janela **Módulos**, clique com o botão direito do mouse direito em qualquer módulo.  
   
1. Selecione **configurações de símbolo**.  
  
1. Selecione **carregar todos os símbolos**, ou selecione quais módulos para incluir ou excluir.  
  
1. Selecione **OK**. As alterações entram em vigor na próxima sessão de depuração.  
  
**Para alterar o comportamento de um módulo específico de carregamento de símbolo:**  

1.  Na janela **Módulos**, clique com o botão direito do mouse no módulo.  

1.  No menu de atalho, marque ou desmarque **sempre carregar automaticamente**. As alterações entram em vigor na próxima sessão de depuração.  
  
## <a name="see-also"></a>Consulte também  
 [Interrompendo a execução](/previous-versions/visualstudio/visual-studio-2010/7z9se2d8(v=vs.100))   
 [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)   
 [Especificar arquivos de símbolo (.pdb) e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)