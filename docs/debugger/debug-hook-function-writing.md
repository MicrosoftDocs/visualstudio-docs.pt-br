---
title: Depurar a gravação da função do gancho | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 038c976380ff1e1f0a1a7c4c150fc462f6b1d1db
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350713"
---
# <a name="debug-hook-function-writing"></a>Gravação da função de gancho de depuração
Esta seção descreve várias funções de gancho de depuração personalizadas que você pode escrever que permitem inserir seu código em alguns pontos predefinidos no processamento normal do depurador.

## <a name="in-this-section"></a>Nesta seção
 [Funções de gancho de bloco de cliente](../debugger/client-block-hook-functions.md) Fornece orientação e um protótipo para escrever funções que validam ou relatam o conteúdo dos dados armazenados em blocos de _CLIENT_BLOCK.

 [Funções de gancho de alocação](../debugger/allocation-hook-functions.md) Define uma função de gancho de alocação, explora seus usos diferentes, indica restrições e fornece um protótipo.

 [Ganchos de alocação e alocações de memória de CRT](../debugger/allocation-hooks-and-c-run-time-memory-allocations.md) Descreve a restrição nas funções de gancho de alocação de ignorar explicitamente `_CRT_BLOCK` os blocos se eles fizerem chamadas para as funções de biblioteca de tempo de execução C que alocam memória interna. Este tópico também listará as consequências se o gancho de alocação não ignorar os blocos de `_CRT_BLOCK` (com exemplos) e como alterar a função padrão de gancho de alocação, **CrtDefaultAllocHook**.

 [Funções do gancho de relatório](../debugger/report-hook-functions.md) Discute `_CrtSetReportHook` , que você pode usar para filtrar relatórios para se concentrar em tipos específicos de alocações. Este tópico também fornece um protótipo.

## <a name="related-sections"></a>Seções relacionadas

- [Técnicas de depuração do CRT](../debugger/crt-debugging-techniques.md) – links para técnicas de depuração para a biblioteca de tempo de execução do C, incluindo o uso da biblioteca de depuração do CRT, macros para relatórios, diferenças entre o `malloc` e `_malloc_dbg` o, gravando funções de gancho de depuração e o heap de depuração do CRT.