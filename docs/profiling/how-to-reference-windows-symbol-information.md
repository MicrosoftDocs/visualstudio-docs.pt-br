---
title: 'Como: Fazer referência a informações de símbolo do Windows | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- performance tools, symbol servers
- servers, symbol servers
- profiling tools, symbol servers
- symbol servers
ms.assetid: b7c67318-6be2-4b1e-a161-077b1f4a7c30
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 99e19df05aea81c9fe2b73fd1020318f3482d1bb
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54964230"
---
# <a name="how-to-reference-windows-symbol-information"></a>Como: Referenciar informações de símbolo do Windows
As Ferramentas de Criação de Perfil do Visual Studio usam arquivos de símbolo (.*pdb*) para resolver nomes simbólicos como nomes de função em binários de programa. Siga estas etapas para baixar automaticamente e atualizar os arquivos .*pdb* corretos para a versão do Windows no computador local.  
  
> [!NOTE]
>  Essa configuração não afeta os relatórios existentes. Somente os relatórios criados após especificar o servidor de símbolo terão as informações de símbolo.  
  
 Para obter mais informações, confira [Especificar arquivos de símbolo (.*pdb*) e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).  
  
### <a name="to-use-the-microsoft-symbol-server"></a>Para usar o servidor de símbolos da Microsoft  
  
1.  Crie uma pasta para conter as informações de arquivo de símbolo, como C:\SymbolCache.  
  
2.  No menu **Ferramentas**, clique em **Opções**.  
  
     A caixa de diálogo **Opções** é exibida.  
  
3.  Expanda a árvore **Depuração** e, em seguida, clique em **Símbolos**.  
  
4.  Em **Locais do arquivo de símbolo (.pdb)**, selecione **Servidores de Símbolos da Microsoft**  
  
5.  Em **Armazenar em cache os símbolos do servidor de símbolos para este diretório**, digite o caminho da pasta que foi criada na etapa 1, por exemplo:  
  
     **C:\SymbolCache**  
  
     Você também pode clicar no botão de reticências (**...** ) e, em seguida, selecionar um diretório na caixa de diálogo **Procurar Pasta**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar sessões de desempenho](../profiling/configuring-performance-sessions.md)   
 [Como: Serializar informações de símbolo](../profiling/how-to-serialize-symbol-information.md)