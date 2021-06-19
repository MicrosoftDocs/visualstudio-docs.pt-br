---
title: Alternar para outro thread durante a depuração
description: Revise diferentes métodos para alternar para outro thread durante a depuração de um aplicativo multithread em Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 04/27/2017
ms.topic: how-to
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a0a68047c5c9e772fc978c56f2cd70dc9454ca57
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112384688"
---
# <a name="how-to-switch-to-another-thread-while-debugging-in-visual-studio-c-visual-basic-c"></a>Como alternar para outro thread durante a depuração no Visual Studio (C#, Visual Basic, C++)
Ao depurar um aplicativo multithread, você pode usar qualquer um dos vários métodos para alternar do thread com o qual você está trabalhando para outro thread.

> [!NOTE]
> Se você quiser controlar a ordem em que os threads são executados, precisará congelar [e descongelar threads](../debugger/get-started-debugging-multithreaded-apps.md).

Quando você examina threads no editor de códigos e as diferentes janelas de depuração multithread, a seta amarela indica o thread atual. Uma seta verde com uma cauda curly indica que um thread não atual tem o contexto atual do depurador.

### <a name="to-switch-to-any-thread-that-appears"></a>Para alternar para qualquer thread exibido

- Na janela **Threads** ou **Parallel Watch,** clique duas vezes no thread.

### <a name="to-switch-to-a-thread-in-a-source-window"></a>Para alternar para um thread em uma janela de origem

- Na medianiz esquerda, clique com o botão direito do mouse em um ícone de marcador de thread Marcador de Thread ![,](../debugger/media/dbg-thread-marker.png "ThreadMarker")aponte para Alternar para e clique no nome desse thread para o qual você deseja alternar. O menu de atalho mostra apenas os threads nesse local específico.

     Se nenhum marcador de thread aparecer, clique com o botão direito do mouse na **janela Threads** e verifique se **Mostrar Threads na Origem** está selecionado.

### <a name="to-switch-to-a-thread-in-the-debug-location-toolbar"></a>Para alternar para um thread na barra de ferramentas do Local de Depuração

1. Na barra **de ferramentas Localização** de Depuração, clique na **lista Thread.**

2. Na lista, clique no thread para o qual você deseja alternar.

## <a name="see-also"></a>Confira também
- [Depurar aplicativos multithread](../debugger/debug-multithreaded-applications-in-visual-studio.md)
