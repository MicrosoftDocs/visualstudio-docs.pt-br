---
title: Estratégia de implementação do avaliador de expressão | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, implementation strategy
- debug engines, implementation strategies
ms.assetid: 1bccaeb3-8109-4128-ae79-16fd8fbbaaa2
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a0b60a82b9451dfa43f5cd231fd38dd32b1729ed
ms.sourcegitcommit: 25a62c2db771f938e3baa658df8b1ae54a960e4f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39233042"
---
# <a name="expression-evaluator-implementation-strategy"></a>Estratégia de implementação do avaliador de expressão
> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Uma abordagem para criar rapidamente um avaliador de expressão (EE) é primeiro implementar o código mínimo necessário para exibir as variáveis locais na **Locals** janela. É útil observar que cada linha na **Locals** janela exibe o nome, tipo e valor de uma variável local e que todos os três são representados por uma [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) objeto. O nome, tipo e valor de uma variável local é obtido de um `IDebugProperty2` objeto chamando seu [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) método. Para obter mais informações sobre como exibir as variáveis locais na **Locals** janela, consulte [exibindo locais](../../extensibility/debugger/displaying-locals.md).  
  
## <a name="discussion"></a>Discussão  
 Uma sequência de implementação possível começa com a implementação [IDebugExpressionEvaluator](../../extensibility/debugger/reference/idebugexpressionevaluator.md). O [analisar](../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) e o [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) métodos devem ser implementados para exibir os locais. Chamando `IDebugExpressionEvaluator::GetMethodProperty` retorna um `IDebugProperty2` objeto que representa um método: ou seja, um [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) objeto. Métodos em si não são exibidos na **Locals** janela.  
  
 O [EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) método deve ser implementado em seguida. O mecanismo de depuração (DES) chama esse método para obter uma lista de argumentos e variáveis locais, passando `IDebugProperty2::EnumChildren` uma `guidFilter` argumento de `guidFilterLocalsPlusArgs`. `IDebugProperty2::EnumChildren` chamadas [EnumArguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md) e [EnumLocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md), combinando os resultados em uma única enumeração. Ver [exibir locals](../../extensibility/debugger/displaying-locals.md) para obter mais detalhes.  
  
## <a name="see-also"></a>Consulte também  
 [Implementar um avaliador de expressão](../../extensibility/debugger/implementing-an-expression-evaluator.md)   
 [Locais de exibição](../../extensibility/debugger/displaying-locals.md)