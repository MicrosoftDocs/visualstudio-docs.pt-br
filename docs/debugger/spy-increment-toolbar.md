---
title: A barra de ferramentas Spy + + | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Spy++ toolbar
ms.assetid: 949c18fb-bb25-42ed-9130-c4a47869f24d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a7a3213d614caa19fb6df77a72efd05e36484c77
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54982670"
---
# <a name="spy-toolbar"></a>Barra de ferramentas do Spy++
A barra de ferramentas é exibida na barra de menus do Spy + +. Para exibir ou ocultar a barra de ferramentas, nos **modo de exibição** menu, clique em **barra de ferramentas**.  
  
 Os seguintes controles estão disponíveis na barra de ferramentas.  
  
## <a name="uielement-list"></a>Lista UIElement  
  
|Botão|Efeito|  
|------------|------------|  
|![Spy&#43; &#43; botão do Windows](../debugger/media/icon_spy--_windows.gif "Icon_Spy + + Windows")|Exibe uma exibição de árvore das janelas e controles no sistema. Para obter mais informações, consulte [modo de exibição do Windows](../debugger/windows-view.md).|  
|![Spy&#43; &#43; processa o botão](../debugger/media/icon_spy--_processes.gif "Icon_Spy + + _Processes")|Exibe uma exibição de árvore dos processos no sistema. Para obter mais informações, consulte [exibição de processos](../debugger/processes-view.md).|  
|![Spy&#43; &#43; botão de Threads](../debugger/media/icon_spy--_threads.gif "Icon_Spy + + _Threads")|Exibe uma exibição de árvore dos threads no sistema. Para obter mais informações, consulte [exibição de Threads](../debugger/threads-view.md).|  
|![Spy&#43; &#43; botão de mensagens](../debugger/media/icon_spy--_messages.gif "Icon_Spy + + _Messages")|Cria uma janela para exibir mensagens de janela e abre o **opções de mensagem** caixa de diálogo para que você possa selecionar a janela cujas mensagens serão exibidas e também selecionar outras opções. Para obter mais informações, consulte [exibição de mensagens](../debugger/messages-view.md).|  
|![Spy&#43; &#43; botão Iniciar Log](../debugger/media/icon_spy--_startlog.gif "Icon_Spy + + _StartLog")|Inicia o log de mensagens e exibe o fluxo de mensagens. Esse controle está disponível apenas quando um **mensagens** janela é a janela ativa. Para obter mais informações, confira [Como: Iniciar e parar a exibição do log de mensagem](../debugger/how-to-start-and-stop-the-message-log-display.md).|  
|![Spy&#43; &#43; Log botão Parar](../debugger/media/icon_spy--_stoplog.gif "Icon_Spy + + _StopLog")|Paradas de mensagem de registro em log e a exibição do fluxo de mensagens. Esse controle está disponível apenas quando um **mensagens** janela é a janela ativa. Para obter mais informações, confira [Como: Iniciar e parar a exibição do log de mensagem](../debugger/how-to-start-and-stop-the-message-log-display.md).|  
|![Spy&#43; &#43; botão de opções de Log](../debugger/media/icon_spy--_logoptions.gif "Icon_Spy + + _LogOptions")|Exibe a [opções de mensagem](../debugger/message-options-dialog-box.md) caixa de diálogo. Use essa caixa de diálogo para selecionar o windows e tipos para a exibição de mensagem. Esse controle está disponível apenas quando um **mensagens** janela é a janela ativa.|  
|![Spy&#43; &#43; botão de Log limpar](../debugger/media/spy--_clearlog.gif "Spy + + _ClearLog")|Limpa o conteúdo do ativo **mensagens** janela. Esse controle está disponível apenas quando um **mensagens** janela é a janela ativa.|  
|![Spy&#43; &#43; botão da janela localizar](../debugger/media/icon_spy--_findwindow.gif "Icon_Spy + + _FindWindow")|Abre o [localizar janela](../debugger/find-window-dialog-box.md) caixa de diálogo que permite que você definir critérios de pesquisa de janela e exibir as propriedades ou mensagens. Para obter mais informações, confira [Como: Usar a ferramenta Localizador](../debugger/how-to-use-the-finder-tool.md).|  
|![Spy&#43; &#43; localizar o primeiro botão da janela](../debugger/media/icon_spy--_window.gif "Icon_Spy + + _Window")|Pesquisa o modo de exibição atual para uma janela correspondente, processo, thread ou mensagem.|  
|![Spy&#43; &#43; botão Localizar próxima janela](../debugger/media/icon_spy--_nextwindow.gif "Icon_Spy + + _NextWindow")|Pesquisa o modo de exibição atual para a próxima janela correspondente, processo, thread ou mensagem. Esse controle (e o comando de menu relacionados) está disponíveis somente quando há um resultado de pesquisa válido que não é exclusivo. Por exemplo, quando você usa um identificador de janela como critério de pesquisa na árvore de janela, ela produz resultados exclusivos porque há apenas uma janela na árvore de janela que tem esse identificador; Nesse caso, **Localizar próximo** não está disponível.|  
|![Spy&#43; &#43; localizar o botão de janela anterior](../debugger/media/icon_spy--_prevwindow.gif "Icon_Spy + + _PrevWindow")|Pesquisa o modo de exibição atual para a janela correspondente anterior, processo, thread ou mensagem. Esse controle (e o comando de menu relacionados) está disponíveis somente quando há um resultado de pesquisa válido que não é exclusivo. Por exemplo, quando você usa um identificador de janela como critério de pesquisa na árvore de janela, ela produz resultados exclusivos porque há apenas uma janela na árvore de janela que tem esse identificador; Nesse caso, **Localizar anterior** não está disponível.|  
|![Spy&#43; &#43; botão Gerenciador de propriedade](../debugger/media/icon_spy--_propexp.gif "Icon_Spy + + _PropExp")|Exibe as propriedades da janela que está selecionado na exibição do Windows.|  
|![Spy&#43; &#43; botão Atualizar](../debugger/media/icon_spy--_refresh.gif "Icon_Spy + + atualiza_r")|Atualiza as exibições do sistema.|  
  
## <a name="see-also"></a>Consulte também  
 [Usando o Spy++](../debugger/using-spy-increment.md)   
 [Exibições do Spy++](../debugger/spy-increment-views.md)   
 [Referência a Spy++](../debugger/spy-increment-reference.md)