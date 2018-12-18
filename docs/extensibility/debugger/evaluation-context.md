---
title: Contexto de avaliação | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, context
ms.assetid: 008a20c7-1b27-4013-bf96-d6a3f510da02
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 523ef45d52a81a475eca0e3560243e0eb8357bbd
ms.sourcegitcommit: 25a62c2db771f938e3baa658df8b1ae54a960e4f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39232449"
---
# <a name="evaluation-context"></a>Contexto de avaliação
> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Quando o mecanismo de depuração (DES) chama o avaliador de expressão (EE), três argumentos que são passados para [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) determinar o contexto para localizar e avaliar os símbolos, conforme mostrado na tabela a seguir.  
  
## <a name="arguments"></a>Arguments  
  
|Argumento|Descrição|  
|--------------|-----------------|  
|`pSymbolProvider`|Uma [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md) interface que especifica o manipulador de símbolo (SH) a ser usado para identificar o símbolo.|  
|`pAddress`|Uma [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md) interface que especifica o ponto atual de execução. Essa interface localiza o método que contém o código que está sendo executado.|  
|`pBinder`|Uma [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md) interface que localiza o valor e o tipo de um símbolo dado seu nome.|  
  
 `IDebugParsedExpression::EvaluateSync` Retorna um [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) interface que representa o valor resultante e seu tipo.  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces do avaliador de expressão de chave](../../extensibility/debugger/key-expression-evaluator-interfaces.md)   
 [Exibir locals](../../extensibility/debugger/displaying-locals.md)   
 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)   
 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)   
 [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)   
 [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)   
 [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)