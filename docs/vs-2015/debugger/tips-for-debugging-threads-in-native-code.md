---
title: Dicas para Threads em código nativo de depuração | Microsoft Docs
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
- threading [Visual Studio], debugging
- debugging [Visual Studio], threads
ms.assetid: 0374c8c6-57a3-4cfe-8047-2effef5ff5dc
caps.latest.revision: 25
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1852e2d0b3e773e5be0f3f60ad191056a4af0889
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51774998"
---
# <a name="tips-for-debugging-threads-in-native-code"></a>Dicas para threads de depuração no código nativo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Veja algumas dicas que você pode usar durante a depuração de threads em código nativo:  
  
-   Você pode exibir o conteúdo do bloco de informações de Thread, digitando `@TIB` no **inspeção** janela ou **QuickWatch** caixa de diálogo.  
  
-   Você pode exibir o último código de erro para o thread atual digitando `@Err` no **inspeção** janela ou **QuickWatch** caixa de diálogo.  
  
-   As funções das bibliotecas em tempo de execução do C (CRT) podem ser úteis para depurar um aplicativo multithreaded. Para obter mais informações, consulte [_malloc_dbg](http://msdn.microsoft.com/library/c97eca51-140b-4461-8bd2-28965b49ecdb).  
  
## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos multithread](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [Depurando código nativo](../debugger/debugging-native-code.md)



