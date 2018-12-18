---
title: Avaliação de expressão (SDK de depuração do Visual Studio) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: 5044ced5-c18c-4534-b0bf-cc3e50cd57ac
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 52c897e40b825f85e07b4b4f14796655618280a8
ms.sourcegitcommit: 25a62c2db771f938e3baa658df8b1ae54a960e4f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39230728"
---
# <a name="expression-evaluation-visual-studio-debugging-sdk"></a>Avaliação de expressão (depuração de SDK do Visual Studio)
Durante o modo de interrupção, o IDE deve avaliar expressões simples envolvendo diversas variáveis de programa. Para fazer sua avaliação, o mecanismo de depuração (DES) deve analisar e avaliar uma expressão que é inserida em uma das janelas do IDE. 
  
 As expressões são criadas com o [IDebugExpressionContext2::ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) método e são representados por resultante [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) interface.  
  
 O **IDebugExpression2** interface é implementada pelas chamadas e DE seus **EvalAsync** método retorne um [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) interface IDE, para exibir o resultados da avaliação da expressão no IDE. [IDebugProperty2::GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) retorna uma estrutura que é usada para colocar o valor de uma expressão em uma **inspeção** janela ou o **locais** janela.  
  
 O pacote ou a sessão de depuração Gerenciador de depuração (SDM) chama [IDebugExpression2::EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) ou [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) para obter um [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) interface que representa o resultado da avaliação. `IDebugProperty2` tem métodos que retornam o nome, tipo e valor da expressão. Essas informações são exibidas em várias janelas do depurador.  
  
## <a name="using-expression-evaluation"></a>Usando a avaliação da expressão  
 Para usar a avaliação da expressão, você deve implementar o [IDebugExpressionContext2::ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) método e todos os métodos da [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) de interface, conforme mostrado na tabela a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|Avalia uma expressão de forma assíncrona.|  
|[Anular](../../extensibility/debugger/reference/idebugexpression2-abort.md)|Termina a avaliação da expressão assíncrona.|  
|[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|Avalia uma expressão de forma síncrona.|  
  
 Avaliação síncrona e assíncrona exigir a implementação de [IDebugProperty2::GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) método. Avaliação da expressão assíncrona requer a implementação de [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md).  
  
## <a name="see-also"></a>Consulte também  
 [Avaliação de controle e o estado de execução](../../extensibility/debugger/execution-control-and-state-evaluation.md)