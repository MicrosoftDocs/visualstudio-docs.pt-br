---
title: 'Como: pesquisar por um Thread na exibição de Threads | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- threads, searching
ms.assetid: 5609a9b3-c279-4426-9e2e-dd87896a6d6f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 58e16d0edce411192f7b6e40bd0e5fedb32bfac5
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49880566"
---
# <a name="how-to-search-for-a-thread-in-threads-view"></a>Como procurar um thread na exibição de threads
Você pode procurar um segmento específico na exibição de Threads por meio de sua cadeia de caracteres de ID ou o módulo de thread como critérios de pesquisa. Você também pode especificar a direção inicial da pesquisa. Os campos na caixa de diálogo mostrará os atributos de thread selecionado na árvore de thread.  
  
### <a name="to-search-for-a-thread-in-threads-view"></a>Para pesquisar por um thread na exibição de Threads  
  
1. Organizar as janelas assim que Spy + + e um ativo [exibição de Threads](../debugger/threads-view.md) janela são visíveis.  
  
2. Dos **pesquisa** menu, escolha **localizar Thread**.  
  
    O [caixa de diálogo de pesquisa de Thread](../debugger/thread-search-dialog-box.md) é aberta.  
  
3. Como critérios de pesquisa, digite a ID do thread ou uma cadeia de caracteres do módulo.  
  
4. Limpe todos os campos para o qual você deseja especificar valores.  
  
   > [!TIP]
   >  Para localizar todos os threads pertencentes a um módulo, desmarque a **Thread** nome de caixa de texto e o tipo de módulo na **módulo** caixa. Em seguida, use **Localizar próximo** para continuar a pesquisa de threads.  
  
5. Escolher **para cima** ou **para baixo** para a direção inicial da pesquisa.  
  
6. Clique em **OK**.  
  
   Se um thread correspondente for encontrado, ele é realçado na janela de exibição de Threads.