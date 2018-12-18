---
title: 'Como: sinalizar e remover sinalização de Threads | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- treads, switching [debugging]
ms.assetid: 952d579d-6911-413e-b3e5-54e7e797e70c
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 09d26c87867e071b7dafce80d95e4bc46cb88bb8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49891369"
---
# <a name="how-to-flag-and-unflag-threads"></a>Como sinalizar não sinalizar threads
Você pode sinalizar um thread que você deseja dar atenção especial marcando-o com um ícone na **Threads**, **pilhas paralelas** (exibição de thread), **inspeção paralela**e  **Threads da GPU** windows. Esse ícone pode ajudá-lo e a outros a distinguir threads sinalizados de outros threads.  
  
Threads sinalizados também recebem tratamento especial na **Thread** lista o **local de depuração** barra de ferramentas e as outras janelas de depuração multithread. Você pode mostrar todos os threads ou apenas os threads sinalizados na **Thread** lista ou nas outras janelas.
  
### <a name="to-flag-or-unflag-a-thread"></a>Para sinalizar ou remover sinalização de um thread 
  
- No **Threads** ou **inspeção paralela** janela, localize o thread que você está interessado e clique no ícone de sinalizador para marcar ou desmarcar o sinalizador. 
- No **pilhas paralelas** janela, o botão direito do mouse em um thread ou o grupo de threads e selecione **sinalizador / <thread>**  ou **Remover sinalização / <thread>** .
  
### <a name="to-unflag-all-threads"></a>Para remover a sinalização de todos os threads  
  
-   No **Threads** janela, clique em qualquer thread e, em seguida, clique em **Remover sinalização de todos os Threads**.
-   No **inspeção paralela** janela, selecione todos os threads sinalizados e, em seguida, clique com botão direito e selecione **Remover sinalização**.  
  
### <a name="to-display-only-flagged-threads"></a>Para exibir somente threads sinalizados  
  
-   Escolha o **Mostrar somente Threads sinalizados** botão em uma das janelas de depuração multithread.  
  
### <a name="to-flag-just-my-code"></a>Para sinalizar apenas meu código  
  
1.  Na barra de ferramentas na parte superior do **Threads** janela, clique no ícone de sinalizador.  
  
2.  Na lista suspensa, clique em **sinalizar apenas meu código**.  
  
### <a name="to-flag-threads-that-are-associated-with-selected-modules"></a>Para sinalizar os threads que estão associados com os módulos selecionados  
  
1.  Na barra de ferramentas do **Threads** janela, clique no ícone de sinalizador.  
  
2.  Na lista suspensa, clique em **sinalizar seleção de módulo personalizado**.  
  
3.  No **selecionar módulos** caixa de diálogo, selecione os módulos desejados.  
  
4.  (Opcional) No **pesquisa** , digite uma cadeia de caracteres para pesquisar módulos específicos.  
  
5.  Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos multithread](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [Introdução ao depurar aplicativos multithread](../debugger/get-started-debugging-multithreaded-apps.md)  
 [Passo a passo: Depurar aplicativos multithread usando a janela Threads](../debugger/how-to-use-the-threads-window.md)