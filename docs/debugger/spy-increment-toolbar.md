---
title: A barra de ferramentas Spy + + | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Spy++ toolbar
ms.assetid: 949c18fb-bb25-42ed-9130-c4a47869f24d
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f90c9f249ea0091d7cd5b899ffcd9b7cdadc5a7c
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31477375"
---
# <a name="spy-toolbar"></a>Barra de ferramentas do Spy++
A barra de ferramentas aparece na barra de menu do Spy + +. Para exibir ou ocultar a barra de ferramentas, sobre o **exibição** menu, clique em **barra de ferramentas**.  
  
 Os seguintes controles estão disponíveis na barra de ferramentas.  
  
## <a name="uielement-list"></a>Lista UIElement  
  
|Botão|Efeito|  
|------------|------------|  
|![Spy&#43; &#43; botão Windows](../debugger/media/icon_spy--_windows.gif "Icon_Spy + + Windows")|Exibe uma exibição de árvore do windows e controles no sistema. Para obter mais informações, consulte [exibição Windows](../debugger/windows-view.md).|  
|![Spy&#43; &#43; processa botão](../debugger/media/icon_spy--_processes.gif "Icon_Spy + + _Processes")|Exibe uma exibição de árvore dos processos no sistema. Para obter mais informações, consulte [exibição processos](../debugger/processes-view.md).|  
|![Spy&#43; &#43; Threads botão](../debugger/media/icon_spy--_threads.gif "Icon_Spy + + _Threads")|Exibe uma exibição de árvore dos threads do sistema. Para obter mais informações, consulte [exibição de Threads](../debugger/threads-view.md).|  
|![Spy&#43; &#43; mensagens botão](../debugger/media/icon_spy--_messages.gif "Icon_Spy + + _Messages")|Cria uma janela para exibir mensagens de janela e abre o **opções de mensagem** caixa de diálogo para que você possa selecionar a janela cujas mensagens serão exibidas e também selecionar outras opções. Para obter mais informações, consulte [exibição de mensagens](../debugger/messages-view.md).|  
|![Spy&#43; &#43; botão Iniciar Log](../debugger/media/icon_spy--_startlog.gif "Icon_Spy + + _StartLog")|Inicia o log de mensagens e exibe o fluxo de mensagem. Este controle só está disponível quando um **mensagens** janela é a janela ativa. Para obter mais informações, consulte [como: Iniciar e interromper a exibição de Log de mensagem](../debugger/how-to-start-and-stop-the-message-log-display.md).|  
|![Spy&#43; &#43; parar Log botão](../debugger/media/icon_spy--_stoplog.gif "Icon_Spy + + _StopLog")|Paradas de mensagem de log e a exibição de fluxo de mensagens. Este controle só está disponível quando um **mensagens** janela é a janela ativa. Para obter mais informações, consulte [como: Iniciar e interromper a exibição de Log de mensagem](../debugger/how-to-start-and-stop-the-message-log-display.md).|  
|![Spy&#43; &#43; botão de opções de Log](../debugger/media/icon_spy--_logoptions.gif "Icon_Spy + + _LogOptions")|Exibe o [opções de mensagem](../debugger/message-options-dialog-box.md) caixa de diálogo. Use essa caixa de diálogo para selecionar o windows e tipos de exibição de mensagem. Este controle só está disponível quando um **mensagens** janela é a janela ativa.|  
|![Spy&#43; &#43; Limpar Log botão](../debugger/media/spy--_clearlog.gif "Spy + + _ClearLog")|Limpa o conteúdo do ativo **mensagens** janela. Este controle só está disponível quando um **mensagens** janela é a janela ativa.|  
|![Spy&#43; &#43; janela botão Localizar](../debugger/media/icon_spy--_findwindow.gif "Icon_Spy + + _FindWindow")|Abre o [encontrar janela](../debugger/find-window-dialog-box.md) caixa de diálogo que permite definir critérios de pesquisa de janela e exibir propriedades ou mensagens. Para obter mais informações, consulte [como: usar a ferramenta localizador](../debugger/how-to-use-the-finder-tool.md).|  
|![Spy&#43; &#43; primeiro botão da janela localizar](../debugger/media/icon_spy--_window.gif "Icon_Spy + + _Window")|Pesquisa o modo de exibição atual para uma janela, processo, thread ou mensagem.|  
|![Spy&#43; &#43; botão Localizar próxima janela](../debugger/media/icon_spy--_nextwindow.gif "Icon_Spy + + _NextWindow")|Pesquisa o modo de exibição atual para a próxima janela, processo, thread ou mensagem. Esse controle (e o comando de menu relacionados) estão disponíveis somente quando há um resultado de pesquisa válido que não é exclusivo. Por exemplo, quando você usa um identificador de janela como o critério de pesquisa na árvore de janela, ele produz resultados exclusivos porque há apenas uma janela na árvore de janela com esse identificador; Neste exemplo, **Localizar próximo** não está disponível.|  
|![Spy&#43; &#43; localizar botão anterior da janela](../debugger/media/icon_spy--_prevwindow.gif "Icon_Spy + + _PrevWindow")|Pesquisa o modo de exibição atual para a janela anterior, processo, thread ou mensagem. Esse controle (e o comando de menu relacionados) estão disponíveis somente quando há um resultado de pesquisa válido que não é exclusivo. Por exemplo, quando você usa um identificador de janela como o critério de pesquisa na árvore de janela, ele produz resultados exclusivos porque há apenas uma janela na árvore de janela com esse identificador; Neste exemplo, **Localizar anterior** não está disponível.|  
|![Spy&#43; &#43; propriedade Explorer botão](../debugger/media/icon_spy--_propexp.gif "Icon_Spy + + _PropExp")|Exibe as propriedades da janela que está selecionado na exibição do Windows.|  
|![Spy&#43; &#43; botão Atualizar](../debugger/media/icon_spy--_refresh.gif "Icon_Spy + + _Refresh")|Atualiza as exibições do sistema.|  
  
## <a name="see-also"></a>Consulte também  
 [Usando Spy + +](../debugger/using-spy-increment.md)   
 [Exibições do Spy + +](../debugger/spy-increment-views.md)   
 [Referência a Spy++](../debugger/spy-increment-reference.md)