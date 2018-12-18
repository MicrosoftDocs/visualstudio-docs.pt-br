---
title: Avaliador de expressão | Microsoft Docs
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
- expressions [Debugging SDK]
- debugging [Debugging SDK], expression evaluation
- expression evaluation
ms.assetid: f9381b2f-99aa-426c-aea0-d9c15f3c859b
caps.latest.revision: 20
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 48763a1e943a63f129c4fa72c0885d0a287b2b31
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51736017"
---
# <a name="expression-evaluator"></a>Avaliador de expressão
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Avaliadores de expressão (EE) examinam a sintaxe de uma linguagem para analisar e avaliar as variáveis e expressões em tempo de execução, permitindo que eles sejam exibidos pelo usuário quando o IDE está no modo de interrupção.  
  
## <a name="using-expression-evaluators"></a>Usando os avaliadores de expressão  
 As expressões são criadas usando o [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) método, da seguinte maneira:  
  
1. O mecanismo de depuração (DES) implementa o [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) interface.  
  
2. Obtém o pacote de depuração uma `IDebugExpressionContext2` do objeto de um [IDebugStackFrame2](../../extensibility/debugger/reference/idebugstackframe2.md) interface e, em seguida, chama o `IDebugStackFrame2::ParseText` método nele para obter um [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) objeto.  
  
3. As chamadas de pacote de depuração a [EvaluateSync](../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) método ou o [EvaluateAsync](../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) método para obter o valor da expressão. `IDebugExpression2::EvaluateAsync` é chamado da janela de comando/imediato. Todos os outros componentes de interface do usuário chamar `IDebugExpression2::EvaluateSync`.  
  
4. O resultado da avaliação da expressão é um [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) objeto, que contém o nome, tipo e valor do resultado da avaliação da expressão.  
  
   Durante a avaliação da expressão, o EE requer informações do componente de provedor de símbolo. O provedor de símbolo fornece as informações simbólicas usadas para identificar e entender a expressão analisada.  
  
   Quando a avaliação da expressão assíncrona for concluída, um evento assíncrono é enviado por DE por meio do Gerenciador de depuração de sessão (SDM) para notificar o IDE que a avaliação da expressão foi concluída. Quando a avaliação da expressão síncrono for concluída, o resultado da avaliação é retornado da chamada para o `IDebugExpression2::EvaluateSync` método.  
  
## <a name="implementation-notes"></a>Notas de implementação  
 O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] esperam de mecanismos de depuração conversar com o avaliador de expressão usando as interfaces do Common Language Runtime (CLR). Como resultado, um avaliador de expressão que funciona com o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] mecanismos de depuração devem dar suporte o CLR (uma lista completa de CLR de todas as interfaces de depuração pode ser encontrada em debugref.doc, que é parte do [!INCLUDE[winsdklong](../../includes/winsdklong-md.md)]).  
  
## <a name="see-also"></a>Consulte também  
 [Componentes do depurador](../../extensibility/debugger/debugger-components.md)

