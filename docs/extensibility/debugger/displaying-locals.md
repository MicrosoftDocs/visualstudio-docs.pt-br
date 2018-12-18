---
title: Exibir Locals | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, displaying locals
ms.assetid: 62264cec-845b-4233-aed7-0b038fa79250
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1e1a91de0d2a0f4f4e114ccfc77c6a3ce97084d1
ms.sourcegitcommit: 36835f1b3ec004829d6aedf01938494465587436
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2018
ms.locfileid: "39203375"
---
# <a name="display-locals"></a>Locais de exibição
> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Execução sempre ocorre dentro do contexto de um método, também conhecido como método de inclusão ou o método atual. Quando a execução pausa, o Visual Studio chama o mecanismo de depuração (DE) para obter uma lista de variáveis locais e os argumentos, coletivamente chamados de locais do método. Esses locais e seus valores no Visual Studio exibe a **Locals** janela.  
  
 Para exibir locais, o DE chama o [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) método pertencente ao EE e concede a ele um contexto de avaliação, que é, um provedor de símbolo (SP), o endereço de execução atual e um objeto de associador. Para obter mais informações, consulte [contexto de avaliação](../../extensibility/debugger/evaluation-context.md). Se a chamada for bem-sucedida, o `IDebugExpressionEvaluator::GetMethodProperty` método retorna um [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) objeto que representa o método que contém o endereço de execução atual.  
  
 As chamadas DE [EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) para obter uma [IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) object, que é filtrada para retornar somente locais e enumerado para produzir uma lista de [DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md)estruturas. Cada estrutura contém o nome, tipo e valor de um local. O tipo e valor são armazenados como cadeias de caracteres formatadas, adequadas para exibição. O nome, tipo e valor normalmente são exibidos juntos em uma linha do **Locals** janela.  
  
> [!NOTE]
>  O **QuickWatch** e **inspeção** janelas também exibem as variáveis com o mesmo formato de nome, valor e tipo. No entanto, esses valores são obtidos chamando [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) em vez de `IDebugProperty2::EnumChildren`.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Exemplo de implementação de locals](../../extensibility/debugger/sample-implementation-of-locals.md)  
 Usa exemplos para percorrer o processo de implementação de locals.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Contexto de avaliação](../../extensibility/debugger/evaluation-context.md)  
 Explica que, quando o mecanismo de depuração (DES) chama o avaliador de expressão (EE), ele passa três argumentos.  
  
## <a name="see-also"></a>Consulte também  
 [Escrever um avaliador de expressão de CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)