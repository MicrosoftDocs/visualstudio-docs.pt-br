---
title: Alternar para outro thread durante a depuração
ms.custom: seodec18
ms.date: 04/27/2017
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- threads, switching [debugging]
ms.assetid: 5cd76c52-76fa-4fcc-b37e-e9f0ecac0e9e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7b6d90b820a2fd27b96c8b260480265166775bb1
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56697696"
---
# <a name="how-to-switch-to-another-thread-while-debugging-in-visual-studio-c-visual-basic-c"></a>Como: alternar para outro Thread durante a depuração no Visual Studio (C#, Visual Basic, C++)
Quando você depura um aplicativo multi-threaded, você pode usar qualquer um dos vários métodos para alternar do thread que você tem trabalhado com a outro thread.

> [!NOTE]
> Se você quiser controlar a ordem na qual os threads são executados, você precisará [congelar e descongelar threads](../debugger/get-started-debugging-multithreaded-apps.md).

Quando você examina os threads no editor de código e janelas de depuração multithread diferentes, a seta amarela indica que o thread atual. Uma seta verde com uma parte final encaracolada indica que um thread não atual tem o contexto atual do depurador.

### <a name="to-switch-to-any-thread-that-appears"></a>Para alternar para qualquer thread que é exibido

-   No **Threads** ou **inspeção paralela** janela, clique duas vezes o thread.

### <a name="to-switch-to-a-thread-in-a-source-window"></a>Para alternar para um thread em uma janela de origem

-   Na medianiz esquerda, clique com botão direito um ícone de marcador de thread ![marcador de Thread](../debugger/media/dbg-thread-marker.png "ThreadMarker"), aponte para **alternar para**e, em seguida, clique no nome do thread em questão para o qual você deseja alternar . O menu de atalho mostra apenas os threads nesse local específico.

     Se nenhum marcadores de thread aparecem, clique com botão direito no **Threads** janela e verifique **Mostrar Threads em origem** está selecionado.

### <a name="to-switch-to-a-thread-in-the-debug-location-toolbar"></a>Para alternar para um thread na barra de ferramentas do Local de Depuração

1.  Sobre o **local de depuração** barra de ferramentas, clique no **Thread** lista.

2.  Na lista, clique no thread para o qual você deseja alternar.

## <a name="see-also"></a>Consulte também
- [Depurar aplicativos multi-threaded](../debugger/debug-multithreaded-applications-in-visual-studio.md)
