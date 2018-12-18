---
title: Funções de gancho de bloco de clientes | Microsoft Docs
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
- client blocks, validating and reporting data
- debugging [C++], hook functions
- _CrtSetDumpClient function
- client blocks, hook functions
- hooks, client block
ms.assetid: f21c197e-565d-4e3f-9b27-4c018c9b87fc
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e9de7c0533d3ea55e7b78ca645735a60f84e66df
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49938013"
---
# <a name="client-block-hook-functions"></a>Funções de gancho do bloco de clientes
Se você quiser validar ou reportar o conteúdo dos dados armazenados em blocos `_CLIENT_BLOCK`, poderá escrever uma função especificamente para essa finalidade. A função que você escreve deverá ter um protótipo semelhante ao seguinte, conforme definido em CRTDBG.H:  

```cpp
void YourClientDump(void *, size_t)  
```  

 Em outras palavras, sua função de gancho deve aceitar uma **void** ponteiro para o início do bloco de alocação, junto com um **size_t** digite um valor que indica o tamanho da alocação e retornar `void`. Além disso, o conteúdo depende de você.  

 Depois de instalar a função de gancho usando [crtsetdumpclient](/cpp/c-runtime-library/reference/crtsetdumpclient), ele será chamado sempre que um `_CLIENT_BLOCK` bloco for despejado. Você pode usar [crtreportblocktype](/cpp/c-runtime-library/reference/crtreportblocktype) para obter informações sobre o tipo ou subtipo de blocos despejados.  

 O ponteiro para a função que você passa para `_CrtSetDumpClient` é do tipo **crt_dump_client**, conforme definido em CRTDBG. H:  

```cpp
typedef void (__cdecl *_CRT_DUMP_CLIENT)  
   (void *, size_t);  
```  

## <a name="see-also"></a>Consulte também  
 [Gravação da função de gancho de depuração](../debugger/debug-hook-function-writing.md)   
 [Exemplo de crt_dbg2](https://msdn.microsoft.com/library/21e1346a-6a17-4f57-b275-c76813089167)   
 [_CrtReportBlockType](/cpp/c-runtime-library/reference/crtreportblocktype)
