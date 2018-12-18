---
title: Nenhuma origem disponível | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.nosource
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- No Source Code Available for the Current Location dialog box
ms.assetid: ed0732bc-4b8c-490f-adb1-af06869a2a6b
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: aae4b2428470e3e33477cfdb36699c2c1da20c1f
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31479721"
---
# <a name="no-source-available"></a>Nenhuma origem disponível
O projeto não contém código-fonte para o código que você está tentando exibir. A causa comum é duas vezes em um módulo que não tem o código-fonte no **janela pilha de chamadas** ou **janela Threads**. Você pode continuar a depuração, mas não pode usar a janela de origem para definir pontos de interrupção e executar outras ações nesse local. Se você precisa definir um ponto de interrupção, use o **janela de desmontagem** em vez disso.  
  
 Nas Páginas de Propriedades de Solução, você pode alterar os diretórios em que o depurador procura arquivos de origens e informa o depurador para ignorar os arquivos de origem selecionados. Consulte [caixa de diálogo de páginas de propriedade do origem arquivos, propriedades comuns, solução de depuração](../debugger/debug-source-files-common-properties-solution-property-pages-dialog-box.md).  
  
 **Localize o código-fonte**  
 Clique neste link para abrir uma caixa de diálogo onde você pode procurar para localizar o código-fonte.  
  
 **Mostrar desmontagem**  
 Inicia o **janela de desmontagem**.  
  
 **Sempre Mostrar desmontagem para arquivos de origem ausentes**  
 Selecione esta opção para exibir o **janela de desmontagem** automaticamente quando nenhuma fonte está disponível. Essa configuração também pode ser alterada no **opções** caixa de diálogo, **depuração** categoria, **geral** página, selecionando ou desmarcando **Mostrar desmontagem se fonte não está disponível**.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo de páginas de propriedade do origem arquivos, propriedades comuns, solução de depuração](../debugger/debug-source-files-common-properties-solution-property-pages-dialog-box.md)   
 [Especifique o símbolo (. PDB) e arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)   
 [SOS.dll (Extensão de Depuração SOS)](/dotnet/framework/tools/sos-dll-sos-debugging-extension)