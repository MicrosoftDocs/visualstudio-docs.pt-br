---
title: Ganchos de alocação e alocações de memória de tempo de execução C | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.hooks
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], hook functions
- memory allocation, troubleshooting allocation hooks
- allocation hooks
- hooks, allocation
ms.assetid: cc34ee96-3d91-41bd-a019-aa3759139e7e
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7e4c631b72ae9b12f77daf2ddd49919651c0b3e5
ms.sourcegitcommit: 80f9daba96ff76ad7e228eb8716df3abfd115bc3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37433093"
---
# <a name="allocation-hooks-and-c-run-time-memory-allocations"></a>Ganchos de alocação e alocações de memória de tempo de execução do C
Uma restrição muito importante em funções de gancho de alocação é que eles devem ignorar explicitamente `_CRT_BLOCK` blocos. Esses blocos são as alocações de memória feitas internamente por funções da biblioteca de tempo de execução C se eles fizerem chamadas às funções de biblioteca de tempo de execução C que alocam memória interna. Você pode ignorar `_CRT_BLOCK` função de gancho de blocos, incluindo o código no início de sua alocação de seguintes:  
  
```cpp
if ( nBlockUse == _CRT_BLOCK )  
    return( TRUE );  
```  
  
 Se seu gancho de alocação não ignorar `_CRT_BLOCK` bloqueia, em seguida, qualquer função de biblioteca de tempo de execução C chamada em seu gancho pode interceptar o programa em um loop infinito. Por exemplo, `printf` faz uma alocação interna. Se o seu código de gancho chamar `printf`, em seguida, a alocação resultante fará o gancho ser chamado novamente, que chamará **printf** novamente, e assim por diante, até que o estouro de pilha. Se você precisar reportar operações de alocação `_CRT_BLOCK`, uma maneira de evitar essa restrição é usar funções de API do Windows, em vez de funções de tempo de execução C, para formatação e saída. Como as APIs do Windows não usam o heap da biblioteca em tempo de execução C, eles não interceptar o seu gancho de alocação em um loop infinito.  
  
 Se você examinar os arquivos de origem da biblioteca de tempo de execução, você verá que a alocação padrão de função de gancho, **CrtDefaultAllocHook** (que retorna apenas **verdadeiro**), está localizado em um arquivo separado das suas próprias, DBGHOOK. C. Se você quiser que o seu gancho de alocação seja chamado mesmo para as alocações feitas pelo código de inicialização de tempo de execução que é executado antes do seu aplicativo **principal** função, você pode substituir essa função padrão com um de seus próprios, em vez de usando o [crtsetallochook](/cpp/c-runtime-library/reference/crtsetallochook).  
  
## <a name="see-also"></a>Consulte também  
 [Gravação da função de gancho de depuração](../debugger/debug-hook-function-writing.md)   
