---
title: Funções de gancho de alocação | Microsoft Docs
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
- memory allocation, logging allocation information
- insufficient memory
- debugging [C++], hook functions
- _CrtSetAllocHook function
- allocation hooks
- hooks, allocation
ms.assetid: 6bfbdb65-8cb1-4c21-8c45-7194a2b77c1e
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0d49bbff482683c4ac3e0f5f6a4060b176db0d94
ms.sourcegitcommit: 97204b85caadbcf14baeb6738710e287a196673e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "37433350"
---
# <a name="allocation-hook-functions"></a>Funções de gancho da alocação
Uma função de gancho de alocação, instalada usando [crtsetallochook](/cpp/c-runtime-library/reference/crtsetallochook), é chamado sempre que a memória é alocada, realocada ou liberada. Você pode usar esse tipo de gancho para muitas finalidades diferentes. Usá-lo para testar como um aplicativo trata situações de memória insuficiente, por exemplo, para examinar padrões de alocação ou registrar informações de alocação para análise posterior.  
  
> [!NOTE]
>  Lembre-se da restrição sobre como usar funções da biblioteca de tempo de execução C em uma função de gancho de alocação, descrita em [ganchos de alocação e alocações de memória de tempo de execução C](../debugger/allocation-hooks-and-c-run-time-memory-allocations.md).  
  
 Uma função de gancho de alocação deve ter um protótipo como o exemplo a seguir:  
  
```cpp
int YourAllocHook(int nAllocType, void *pvData,  
        size_t nSize, int nBlockUse, long lRequest,  
        const unsigned char * szFileName, int nLine )  
```  
  
 O ponteiro que você passa para [crtsetallochook](/cpp/c-runtime-library/reference/crtsetallochook) é do tipo **crt_alloc_hook**, conforme definido em CRTDBG. H:  
  
```cpp
typedef int (__cdecl * _CRT_ALLOC_HOOK)  
    (int, void *, size_t, int, long, const unsigned char *, int);  
```  
  
 Quando a biblioteca de tempo de execução chama seu gancho, o *nAllocType* argumento indica quais alocação operação está prestes a ser realizada (**hook_alloc**, **hook_realloc**, ou **Hook_free**). Em um livre ou em uma realocação, `pvData` tem um ponteiro para o artigo de usuário do bloco para ser liberado. No entanto para uma alocação, esse ponteiro é null, porque a alocação ainda não ocorreu. Os argumentos restantes contêm o tamanho da alocação em questão, seu tipo de bloco, o número sequencial da solicitação associada com ele e um ponteiro para o nome do arquivo. Se estiver disponível, os argumentos também incluem o número da linha na qual a alocação foi feita. Depois que a função de gancho executa as análises e outras tarefas que o autor desejar, ele deve retornar **verdadeira**, indicando que a operação de alocação pode continuar, ou **falso**, indicando que o operação deve falhar. Um gancho simple desse tipo pode verificar a quantidade de memória alocada até agora e retornar **falsos** se essa quantidade exceder um limite pequeno. O aplicativo apresentaria o tipo de erros de alocação que ocorreriam normalmente apenas quando a memória disponível estivesse muito baixa. Ganchos mais complexos podem controlar os padrões de alocação, analisar o uso de memória ou reportar quando as situações específicas surgem.  
  
## <a name="see-also"></a>Consulte também  
 [Ganchos de alocação e alocações de memória de tempo de execução C](../debugger/allocation-hooks-and-c-run-time-memory-allocations.md)   
 [Gravação da função de gancho de depuração](../debugger/debug-hook-function-writing.md)   
