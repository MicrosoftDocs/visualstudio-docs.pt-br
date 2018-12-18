---
title: Funções de gancho de bloco de clientes | Microsoft Docs
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
- client blocks, validating and reporting data
- debugging [C++], hook functions
- _CrtSetDumpClient function
- client blocks, hook functions
- hooks, client block
ms.assetid: f21c197e-565d-4e3f-9b27-4c018c9b87fc
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2b16dc9eaff974e98e411d4f49d8aed6f9f656e8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51773932"
---
# <a name="client-block-hook-functions"></a>Funções de gancho do bloco de clientes
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se você quiser validar ou reportar o conteúdo dos dados armazenados em blocos `_CLIENT_BLOCK`, poderá escrever uma função especificamente para essa finalidade. A função que você escreve deverá ter um protótipo semelhante ao seguinte, conforme definido em CRTDBG.H:  
  
```  
void YourClientDump(void *, size_t)  
  
```  
  
 Em outras palavras, sua função de gancho deve aceitar uma **void** ponteiro para o início do bloco de alocação, junto com um **size_t** digite um valor que indica o tamanho da alocação e retornar `void`. Além disso, o conteúdo depende de você.  
  
 Depois de instalar a função de gancho usando [crtsetdumpclient](http://msdn.microsoft.com/library/f3dd06d0-c331-4a12-b68d-25378d112033), ele será chamado sempre que um `_CLIENT_BLOCK` bloco for despejado. Você pode usar [crtreportblocktype](http://msdn.microsoft.com/library/0f4b9da7-bebb-4956-9541-b2581640ec6b) para obter informações sobre o tipo ou subtipo de blocos despejados.  
  
 O ponteiro para a função que você passa para `_CrtSetDumpClient` é do tipo **crt_dump_client**, conforme definido em CRTDBG. H:  
  
```  
typedef void (__cdecl *_CRT_DUMP_CLIENT)  
   (void *, size_t);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Gravação da função de gancho de depuração](../debugger/debug-hook-function-writing.md)   
 [Exemplo de crt_dbg2](http://msdn.microsoft.com/en-us/21e1346a-6a17-4f57-b275-c76813089167)   
 [_CrtReportBlockType](http://msdn.microsoft.com/library/0f4b9da7-bebb-4956-9541-b2581640ec6b)



