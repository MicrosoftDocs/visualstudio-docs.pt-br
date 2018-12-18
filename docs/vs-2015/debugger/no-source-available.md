---
title: Nenhuma origem disponível | Microsoft Docs
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
- vs.debug.nosource
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- No Source Code Available for the Current Location dialog box
ms.assetid: ed0732bc-4b8c-490f-adb1-af06869a2a6b
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cc8331c710141a2cc2837d97101e9dff2b49785b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51798372"
---
# <a name="no-source-available"></a>Nenhuma origem disponível
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O projeto não contém código-fonte para o código que você está tentando exibir. A causa comum é clicar duas vezes em um módulo que não tem código-fonte na **janela de pilha de chamadas** ou **janela Threads**. Você pode continuar a depuração, mas não pode usar a janela de origem para definir pontos de interrupção e executar outras ações nesse local. Se você precisar definir um ponto de interrupção, use o **janela de desmontagem** em vez disso.  
  
 Nas Páginas de Propriedades de Solução, você pode alterar os diretórios em que o depurador procura arquivos de origens e informa o depurador para ignorar os arquivos de origem selecionados. Ver [caixa de diálogo de páginas de propriedade do código-fonte arquivos, propriedades comuns, solução de depuração](../debugger/debug-source-files-common-properties-solution-property-pages-dialog-box.md).  
  
 **Navegue para localizar o código-fonte**  
 Clique neste link para abrir uma caixa de diálogo onde você pode procurar para localizar o código-fonte.  
  
 **Mostrar desmontagem**  
 Inicia o **janela de desmontagem**.  
  
 **Sempre Mostrar desmontagem para arquivos de origem ausentes**  
 Selecione esta opção para exibir o **janela de desmontagem** automaticamente quando nenhuma origem estiver disponível. Essa configuração também pode ser alterada na **opções** caixa de diálogo **depuração** categoria, **geral** página, marcando ou desmarcando **Mostrar desmontagem se código-fonte não está disponível**.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo de páginas de propriedade do código-fonte arquivos, propriedades comuns, solução de depuração](../debugger/debug-source-files-common-properties-solution-property-pages-dialog-box.md)   
 [Especifique o símbolo (. PDB) e arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)   
 [SOS.dll (Extensão de Depuração SOS)](http://msdn.microsoft.com/library/9ac1b522-77ab-4cdc-852a-20fcdc9ae498)



