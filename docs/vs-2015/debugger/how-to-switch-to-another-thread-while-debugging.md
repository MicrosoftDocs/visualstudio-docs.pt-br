---
title: 'Como: alternar para outro Thread durante a depuração | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- threads, switching [debugging]
ms.assetid: 5cd76c52-76fa-4fcc-b37e-e9f0ecac0e9e
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ad13c81afc82ac69055ae117c862a1cf73b51478
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51737707"
---
# <a name="how-to-switch-to-another-thread-while-debugging"></a>Como alternar para outro thread durante a depuração
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você depura um aplicativo de vários threads, pode usar qualquer dos vários métodos para alternar o contexto do thread com o qual você vem trabalhando para outro thread.  
  
### <a name="to-switch-to-any-thread-that-appears-in-the-threads-window"></a>Para alternar para determinado thread exibido na janela de threads  
  
-   Clique duas vezes no thread.  
  
### <a name="to-switch-to-a-thread-in-a-source-window"></a>Para alternar para um thread em uma janela de origem  
  
-   Na medianiz esquerda, clique com botão direito um indicador de thread, aponte para **alternar para**e, em seguida, clique no nome do thread em questão para o qual você deseja alternar. O menu de atalho mostra apenas os threads nesse local específico.  
  
     Se nenhum indicador for exibido, clique com botão direito no **Threads** janela e verifique **Mostrar Threads em origem** está selecionado.  
  
### <a name="to-switch-to-a-thread-in-the-debug-location-toolbar"></a>Para alternar para um thread na barra de ferramentas do Local de Depuração  
  
1.  Sobre o **local de depuração** barra de ferramentas, clique no **Thread** caixa.  
  
2.  Na lista, clique no thread para o qual você deseja alternar.  
  
## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos multi-threaded](../debugger/debug-multithreaded-applications-in-visual-studio.md)



