---
title: Como pesquisar um thread no modo de exibição de threads | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- threads, searching
ms.assetid: 5609a9b3-c279-4426-9e2e-dd87896a6d6f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e97d381fd0b1f6340035eec129e7304a8e73b03d
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85349257"
---
# <a name="how-to-search-for-a-thread-in-threads-view"></a>Como procurar um thread na exibição de threads
Você pode pesquisar um thread específico na exibição Threads usando sua ID de thread ou cadeia de caracteres de módulo como critérios de pesquisa. Você também pode especificar a direção inicial da pesquisa. Os campos na caixa de diálogo mostrarão os atributos do thread selecionado na árvore de thread.

### <a name="to-search-for-a-thread-in-threads-view"></a>Para procurar um thread na exibição threads

1. Organize suas janelas para que o Spy + + e uma janela de [exibição de threads](../debugger/threads-view.md) ativas fiquem visíveis.

2. No menu **Pesquisar** , escolha **Localizar thread**.

    A [caixa de diálogo pesquisa de threads](../debugger/thread-search-dialog-box.md) é aberta.

3. Digite a ID do thread ou uma cadeia de caracteres do módulo como critérios de pesquisa.

4. Desmarque os campos para os quais você não deseja especificar valores.

   > [!TIP]
   > Para localizar todos os threads pertencentes a um módulo, desmarque a caixa de texto **thread** e digite o nome do módulo na caixa **módulo** . Em seguida, use **Localizar próximo** para continuar a procurar por threads.

5. Escolha para **cima** ou para **baixo** na direção inicial da pesquisa.

6. Clique em **OK**.

   Se um thread correspondente for encontrado, ele será realçado na janela exibição de threads.