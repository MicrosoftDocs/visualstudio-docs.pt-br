---
title: Exibição de processos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.externaltools.spyplus.processesview
helpviewer_keywords:
- Processes view
ms.assetid: e144e70e-eef2-45a7-a562-a177f177d9a1
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 003ea4962766d9c0b8adef698912024fecd1508e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49936700"
---
# <a name="processes-view"></a>Exibição de processos
A tela processos exibe uma árvore de todos os processos ativos no sistema. O nome do módulo e a ID de processo são mostrados. Se você quiser examinar um processo de determinado sistema, que normalmente corresponde a um programa em execução, use o modo de exibição de processos. Processos são identificados por nomes de módulo, ou eles são designados "processos do sistema".  
  
 Microsoft Windows dá suporte a vários processos. Cada processo pode ter um ou mais threads e cada thread pode ter um ou mais associadas janelas de nível superior. Cada janela de nível superior pode possuir uma série de janelas. Um + símbolo indica que um nível é recolhido. Modo de exibição recolhido consiste em uma linha por processo. Clique o símbolo para expandir o nível +.  
  
 Se você quiser examinar um processo de determinado sistema, que normalmente corresponde a um programa em execução, use o modo de exibição de processos. Processos são identificados por nomes de módulo, ou eles são designados "processos do sistema". Para localizar um processo, recolher a árvore e a lista de pesquisa.  
  
## <a name="procedures"></a>Procedimentos  
  
#### <a name="to-open-the-processes-view"></a>Para abrir a exibição de processos  
  
1. Dos **Spy** menu, escolha **processos**.  
  
   ![Spy&#43; &#43; exibição de processos](../debugger/media/spy--_processes.png "Spy + + _Processes")  
   Exibição de processos do Spy + +  
  
   A figura acima mostra a exibição de processos conosco de processo e thread expandidos.  
  
### <a name="in-this-section"></a>Nesta seção  
 [Procurando por um processo na exibição de processos](../debugger/how-to-search-for-a-process-in-processes-view.md)  
 Explica como localizar um processo específico na exibição de processos.  
  
 [Exibindo propriedades do processo](../debugger/how-to-display-process-properties.md)  
 Explica como mostrar mais informações sobre uma mensagem.  
  
### <a name="related-sections"></a>Seções relacionadas  
 [Exibições do Spy++](../debugger/spy-increment-views.md)  
 Explica as exibições de árvore do Spy + + do windows, as mensagens, processos e threads.  
  
 [Usando Spy++](../debugger/using-spy-increment.md)  
 Apresenta a ferramenta Spy + + e explica como ele pode ser usado.  
  
 [Caixa de diálogo Pesquisa de Processos](../debugger/process-search-dialog-box.md)  
 Usado para localizar o nó para um determinado processo na exibição de processos.  
  
 [Caixa de diálogo Propriedades do Processo](../debugger/process-properties-dialog-box.md)  
 Exibe as propriedades de um processo selecionado na exibição de processos.  
  
 [Referência a Spy++](../debugger/spy-increment-reference.md)  
 Inclui as seções que descrevem cada Spy + + menu e caixa de diálogo caixa.