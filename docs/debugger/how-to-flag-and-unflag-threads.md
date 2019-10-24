---
title: 'Como: sinalizar e remover o sinalizador de threads | Microsoft Docs'
ms.date: 11/04/2016
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 68a2ce8b6ec429b3f7f5cd782c3dac52602eff16
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72733231"
---
# <a name="how-to-flag-and-unflag-threads-c-visual-basic-c"></a>Como sinalizar e remover o sinalizador de threads (C#, C++Visual Basic,)

Você pode sinalizar um thread que deseja dar atenção especial marcando-o com um ícone nas janelas **threads**, **pilhas paralelas** (exibição de thread), **inspeção paralela**e **threads de GPU** . Esse ícone pode ajudá-lo e a outros a distinguir threads sinalizados de outros threads.

Threads sinalizados também recebem tratamento especial na lista de **threads** na barra de ferramentas do **local de depuração** e nas outras janelas de depuração multithread. Você pode mostrar todos os threads ou somente threads sinalizados na lista de **threads** ou nas outras janelas.

### <a name="to-flag-or-unflag-a-thread"></a>Para sinalizar ou remover sinalização de um thread

- Na janela **threads** ou de **inspeção paralela** , localize o thread em que você está interessado e clique no ícone de sinalizador para selecionar ou limpar o sinalizador.
- Na janela **pilhas paralelas** , clique com o botão direito do mouse em um thread ou grupo de threads e selecione **sinalizar/\<thread >** ou **desmarcar/\<thread >** .

### <a name="to-unflag-all-threads"></a>Para remover a sinalização de todos os threads

- Na janela **Threads**, clique com o botão direito do mouse em qualquer thread e clique em **Remover Sinalização de Todos os Threads**.
- Na janela de **inspeção paralela** , selecione todos os threads sinalizados, clique com o botão direito do mouse e selecione **remover sinalizador**.

### <a name="to-display-only-flagged-threads"></a>Para exibir somente threads sinalizados

- Escolha o botão **Mostrar threads sinalizados apenas** em uma das janelas de depuração multi-threaded.

### <a name="to-flag-just-my-code"></a>Para sinalizar apenas meu código

1. Na barra de ferramentas na parte superior da janela **Threads**, clique no ícone do sinalizador.

2. Na lista suspensa, clique em **Sinalizar Apenas Meu Código**.

### <a name="to-flag-threads-that-are-associated-with-selected-modules"></a>Para sinalizar os threads que estão associados com os módulos selecionados

1. Na barra de ferramentas da janela **Threads**, clique no ícone do sinalizador.

2. Na lista suspensa, clique em **Sinalizar Seleção de Módulo Personalizada**.

3. Na caixa de diálogo **Selecionar Módulos**, selecione os módulos desejados.

4. (Opcional) Na caixa **Pesquisar**, digite uma cadeia de caracteres para pesquisar módulos específicos.

5. Clique em **OK**.

## <a name="see-also"></a>Consulte também
- [Depurar aplicativos multi-threaded](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [Introdução à depuração de aplicativos multi-threaded](../debugger/get-started-debugging-multithreaded-apps.md)
- [Walkthrough: depurar aplicativos multithread usando a janela threads](../debugger/how-to-use-the-threads-window.md)