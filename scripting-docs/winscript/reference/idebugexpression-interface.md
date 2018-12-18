---
title: Interface IDebugExpression | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugExpression interface
ms.assetid: 36c00ffb-7160-4c30-a2c9-c9d70c8213cd
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 39e139e09362fc392d1110e26837c52fd4c642c4
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24727786"
---
# <a name="idebugexpression-interface"></a>Interface IDebugExpression
Representa uma expressão avaliada de forma assíncrona. Mecanismos de script geralmente implementam essa interface. Um depurador IDE normalmente usa essa interface para ativar uma janela de execução imediata ou janela de observação.  
  
> [!NOTE]
>  O `IDebugExpression` interface está disponível somente de um quadro de pilha.  
  
 Além dos métodos herdados de `IUnknown`, o `IDebugExpression` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugExpression::Start](../../winscript/reference/idebugexpression-start.md)|Começa a avaliação da expressão.|  
|[IDebugExpression::Abort](../../winscript/reference/idebugexpression-abort.md)|Anula a expressão.|  
|[IDebugExpression::QueryIsComplete](../../winscript/reference/idebugexpression-queryiscomplete.md)|Determina se a operação for concluída.|  
|[IDebugExpression::GetResultAsString](../../winscript/reference/idebugexpression-getresultasstring.md)|Retorna o resultado da avaliação da expressão como uma cadeia de caracteres e o valor de retorno da operação.|  
|[IDebugExpression::GetResultAsDebugProperty](../../winscript/reference/idebugexpression-getresultasdebugproperty.md)|Retorna o resultado da avaliação da expressão como uma propriedade de depuração e o valor de retorno da operação.|