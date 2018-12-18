---
title: 'Como: código-fonte do .NET Framework de depuração | Microsoft Docs'
ms.custom: ''
ms.date: 11/19/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- debugging, .NET Framework source
ms.assetid: fc12e472-ac6a-4e77-8e22-a769e13a03b8
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 234d9979ea1a16b917111e2a8937ad71dd55224f
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389274"
---
# <a name="how-to-debug-net-framework-source"></a>Como depurar o código-fonte do .NET Framework

Para depurar o código-fonte do .NET Framework, faça o seguinte:

- Habilite a depuração de código-fonte do .NET Framework.  
  
- Ter acesso aos símbolos de depuração para o código. 
  
  Você pode optar por baixar imediatamente os símbolos de depuração ou definir opções para baixar mais tarde. Se você não baixar símbolos imediatamente, ele baixará na próxima vez que você iniciar a depuração de seu aplicativo. Durante a depuração, você também pode usar o **módulos** ou **pilha de chamadas** windows para baixar e carregar símbolos.  
  
### <a name="to-enable-stepping-into-net-framework-source"></a>Para habilitar a depuração de código-fonte do .NET Framework 
  
1. Sob **ferramentas** (ou **Debug**) > **opções** > **depuração** > **geral**, selecione **origem do .NET Framework Habilitar depuração**.  
   
   - Se Apenas Meu Código tiver sido habilitado, uma caixa de diálogo de aviso mostrará que Apenas Meu Código está desabilitado agora. Selecione **OK**.  
   
   - Se você não tinha um cache de símbolo local definida, uma caixa de diálogo de aviso informa que um cache de símbolo padrão foi definido. Selecione **OK**.  
   
1. Selecione **Okey** para fechar o **opções** caixa de diálogo.
  
### <a name="to-set-or-change-symbol-source-locations-and-loading-behavior"></a>Para definir ou alterar o comportamento de carregamento e locais de origem de símbolo

1. Selecione o **símbolos** categoria sob **ferramentas** (ou **depurar**) > **opções** > **dedepuração**.  
  
1. No **símbolos** página, em **locais de arquivo (. PDB) de símbolo**, selecione **servidores de símbolo Microsoft** acesso os símbolos de servidores públicos de símbolo Microsoft. Selecione os botões de barra de ferramentas para adicionar outros locais de símbolos e alterar a ordem de carregamento. 
   
1. Para alterar seu cache de símbolos locais, editar ou navegue até um local diferente em **armazenar em Cache os símbolos neste diretório**.  
   
1. Para baixar símbolos imediatamente, selecione **carregar todos os símbolos**. Esse botão está disponível apenas durante a depuração.  
   
   Se você não baixar símbolos agora, eles serão baixados na próxima vez que você iniciar a depuração.  
   
1. Selecione **Okey** para fechar o **opções** caixa de diálogo.  
  
### <a name="to-load-symbols-from-the-modules-or-call-stack-windows"></a>Para carregar símbolos da pilha de chamadas ou módulos do windows  
  
1. Durante a depuração, abra a janela, selecionando **Debug** > **Windows** > **módulos** ou **pilha de chamadas** . 
   
1. Clique com botão direito um módulo para o qual os símbolos não foram carregados. No **módulos** , janela de status de carregamento de símbolos está a **símbolos Status** coluna. No **pilha de chamadas** , janela de status está a **Status do quadro** coluna e o quadro está esmaecida. 
   
   - Selecione **carregar símbolos** no menu para localizar e carregar arquivos de símbolo de uma pasta em seu computador. 
   
   - Selecione **informações de carregamento de símbolo** para mostrar os locais do depurador pesquisados para símbolos.  
   
   - Selecione **configurações de símbolo** para abrir o **símbolos** página. No **símbolos** página, em **locais de arquivo (. PDB) de símbolo**, selecione **servidores de símbolo Microsoft** acesso os símbolos de servidores públicos de símbolo Microsoft. Selecione os botões de barra de ferramentas para adicionar outros locais de símbolos e alterar a ordem de carregamento. Selecione **Okey** para fechar a caixa de diálogo. 
  
### <a name="see-also"></a>Consulte também  
 [Depurando código gerenciado](../debugger/debugging-managed-code.md)   
 [Especificar arquivos de símbolo (.pdb) e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)