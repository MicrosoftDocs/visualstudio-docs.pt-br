---
title: Page Up ou down na memória | Microsoft Docs
description: Consulte Como paginar para cima ou para baixo na memória para exibir o conteúdo da memória em uma janela de memória ou a janela de desmontagem ao depurar no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugger, paging up or down in memory
- memory, paging up or down
- Disassembly window, viewing memory space
- Memory window, paging up or down in memory
ms.assetid: 50b30a68-66f6-43f8-a48b-59ce12c95471
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fef6ebceaca742b9bda417cad4dd218f25b114b6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99885229"
---
# <a name="how-to-page-up-or-down-in-memory"></a>Como subir ou descer a página na memória

Quando exibe conteúdos de memória na janela de **Memória** ou na janela de **Desmontagem**, você pode usar a barra de rolagem vertical para mover para cima ou para baixo no espaço de memória.

### <a name="to-page-up-or-down-in-memory"></a>Para mover para cima ou para baixo na memória

1. Para rolar a página para baixo (mover para um endereço de memória superior), clique na barra de rolagem vertical, abaixo da caixa de rolagem.

2. Para rolar a página para cima (mover para um endereço de memória inferior), clique na barra de rolagem vertical, acima do elevador.

   Você também notará que a barra de rolagem vertical opera de maneira não padrão. O espaço para endereço de um computador moderno é muito grande e é fácil perder-se ao segurar o elevador da barra de rolagem e arrastá-lo a um local aleatório. Por esse motivo, o elevador é "carregado" e sempre permanece no centro da barra de rolagem. Em aplicativos de código nativo, você pode rolar a página para cima ou para baixo, mas não pode rolar livremente.

   Em aplicativos gerenciados, a desmontagem é limitada a uma função e você pode rolar normalmente.

   Você observará que os endereços superiores aparecem na parte inferior da janela. Para exibir um endereço superior, você deve rolar para baixo, não para cima.

#### <a name="to-move-up-or-down-one-instruction"></a>Para mover para cima ou para baixo em uma instrução

- Clique na seta na parte superior ou inferior da barra de rolagem vertical.

## <a name="see-also"></a>Confira também
- [Janelas de memória](../debugger/memory-windows.md)
- [Como usar a Janela de Desmontagem](../debugger/how-to-use-the-disassembly-window.md)
- [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)