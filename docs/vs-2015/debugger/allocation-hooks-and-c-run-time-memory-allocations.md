---
title: Ganchos de alocação e alocações de memória de tempo de execução C | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.hooks
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- debugging [C++], hook functions
- memory allocation, troubleshooting allocation hooks
- allocation hooks
- hooks, allocation
ms.assetid: cc34ee96-3d91-41bd-a019-aa3759139e7e
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9e123e74597ced9ef08860c5369f75ddda2f6e25
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51780679"
---
# <a name="allocation-hooks-and-c-run-time-memory-allocations"></a>Ganchos de alocação e alocações de memória de tempo de execução do C
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Uma restrição muito importante em funções de gancho de alocação é que devem ignorar explicitamente blocos `_CRT_BLOCK` (as alocações de memória feitas internamente por funções da biblioteca em tempo de execução C) se fizerem chamadas às funções da biblioteca em tempo de execução C que alocam a memória interna. Os blocos `_CRT_BLOCK` podem ser ignorados incluindo o código como, por exemplo, o seguinte no início da função de gancho de alocação:  
  
```  
if ( nBlockUse == _CRT_BLOCK )  
    return( TRUE );  
```  
  
 Se seu gancho de alocação não ignorar blocos `_CRT_BLOCK`, qualquer função de biblioteca em tempo de execução C chamada em seu gancho pode interceptar o programa em um loop infinito. Por exemplo, `printf` faz uma alocação interna. Se o seu código de gancho chamar `printf`, em seguida, a alocação resultante fará o gancho ser chamado novamente, que chamará **printf** novamente, e assim por diante até que o estouro de pilha. Se você precisar reportar operações de alocação `_CRT_BLOCK`, uma maneira de evitar essa restrição é usar funções de API do Windows, em vez de funções de tempo de execução C, para formatação e saída. Como as APIs do Windows não usam o heap da biblioteca em tempo de execução C, elas não interceptarão seu gancho de alocação em um loop infinito.  
  
 Se você examinar os arquivos de origem da biblioteca de tempo de execução, você verá que a alocação padrão de função de gancho, **CrtDefaultAllocHook** (que retorna apenas **verdadeiro**), está localizado em um arquivo separado das suas próprias, DBGHOOK. C. Se você quiser que o seu gancho de alocação seja chamado mesmo para as alocações feitas pelo código de inicialização de tempo de execução que é executado antes do seu aplicativo **principal** função, você pode substituir essa função padrão com um de seus próprios, em vez de usando o [crtsetallochook](http://msdn.microsoft.com/library/405df37b-2fd1-42c8-83bc-90887f17f29d).  
  
## <a name="see-also"></a>Consulte também  
 [Gravação da função de gancho de depuração](../debugger/debug-hook-function-writing.md)   
 [Exemplo de crt_dbg2](http://msdn.microsoft.com/en-us/21e1346a-6a17-4f57-b275-c76813089167)



