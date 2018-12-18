---
title: Avaliação de expressão (SDK de depuração do Visual Studio) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: 5044ced5-c18c-4534-b0bf-cc3e50cd57ac
caps.latest.revision: 8
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: eb5bfe5f5c77e7ba1881f803830e1cb3d357561b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51781576"
---
# <a name="expression-evaluation-visual-studio-debugging-sdk"></a>Avaliação de expressão (SDK de depuração do Visual Studio)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Durante o modo de interrupção, o IDE deve ser capaz de avaliar expressões simples envolvendo diversas variáveis do programa. Para fazer isso, o mecanismo de depuração (DES) deve ser capaz de analisar e avaliar uma expressão que é inserida em uma das janelas do IDE.  
  
 As expressões são criadas usando o [IDebugExpressionContext2::ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) método e são representados por resultante [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) interface.  
  
 O **IDebugExpression2** interface é implementada pelas chamadas e DE seus **EvalAsync** método retorne um [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) interface IDE, para exibir o resultados da avaliação da expressão no IDE. [IDebugProperty2::GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) retorna uma estrutura que pode ser usada para colocar o valor de uma expressão em uma janela de observação ou na janela locais.  
  
 O pacote ou a sessão de depuração Gerenciador de depuração (SDM) chama [IDebugExpression2::EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) ou [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) para obter um [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) interface que representa o resultado da avaliação. `IDebugProperty2` tem métodos que retornam o nome, tipo e valor da expressão. Essas informações são exibidas em várias janelas do depurador.  
  
## <a name="using-expression-evaluation"></a>Usando a avaliação da expressão  
 Para usar a avaliação da expressão, você deve implementar o [IDebugExpressionContext2::ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) método e todos os métodos da [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) de interface, conforme mostrado na tabela a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)|Avalia uma expressão de forma assíncrona.|  
|[Anular](../../extensibility/debugger/reference/idebugexpression2-abort.md)|Termina a avaliação da expressão assíncrona.|  
|[EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)|Avalia uma expressão de forma síncrona.|  
  
 Avaliação síncrona e assíncrona exigir a implementação do [IDebugProperty2::GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) método. Avaliação da expressão assíncrona requer a implementação de [IDebugExpressionEvaluationCompleteEvent2](../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md).  
  
## <a name="see-also"></a>Consulte também  
 [Controle de execução e avaliação de estado](../../extensibility/debugger/execution-control-and-state-evaluation.md)

