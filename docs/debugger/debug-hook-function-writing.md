---
title: Gravação da função de gancho de depuração | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vc.hooks
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], CRT debug support
- debug hook functions
- hooks, debug
- hooks
- debugging [CRT], debug hook functions
ms.assetid: 5510635f-cf69-4907-b72d-ae27af1f19af
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 365196a01ba9e62ef0b26eb3a99278d4d77a4dd4
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31457336"
---
# <a name="debug-hook-function-writing"></a>Gravação da função de gancho de depuração
Esta seção descreve várias funções de gancho de depuração personalizadas que você pode escrever que permitem inserir seu código em alguns pontos predefinidos no processamento normal do depurador.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Funções de gancho do bloco de clientes](../debugger/client-block-hook-functions.md)  
 Fornece orientação e um protótipo para escrever funções que validam ou reportam o conteúdo dos dados armazenados nos blocos _CLIENT_BLOCK.  
  
 [Funções de gancho de alocação](../debugger/allocation-hook-functions.md)  
 Define uma função de gancho de alocação, explora seus usos diferentes, indica limitações e fornece um protótipo.  
  
 [Ganchos de alocação e alocações de memória de CRT](../debugger/allocation-hooks-and-c-run-time-memory-allocations.md)  
 Descreve a limitação de funções de gancho de alocação de ignorar explicitamente blocos de `_CRT_BLOCK` se eles fizerem chamadas para as funções da biblioteca em tempo de execução C que alocam a memória interna. Este tópico também lista as consequências se sua gancho de alocação não ignorar `_CRT_BLOCK` função de gancho de blocos (com exemplos) e como alterar a alocação padrão **CrtDefaultAllocHook**.  
  
 [Funções de gancho de relatório](../debugger/report-hook-functions.md)  
 Discute `_CrtSetReportHook`, que você pode usar para filtrar relatórios para enfatizar tipos específicos de alocações. Este tópico também fornece um protótipo.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Técnicas de depuração CRT](../debugger/crt-debugging-techniques.md)  
 Links para técnicas de depuração para a biblioteca em tempo de execução C, incluindo o uso da biblioteca de depuração do CRT, macros para relatório, diferenças entre `malloc` e `_malloc_dbg`, escrevendo funções de gancho de depuração, e o heap de depuração do CRT.