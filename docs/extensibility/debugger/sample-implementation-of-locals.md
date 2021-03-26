---
title: Exemplo de implementação de locais | Microsoft Docs
description: Saiba como o Visual Studio obtém os locais para um método do avaliador de expressão neste artigo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], local variables
- expression evaluation, local variables
ms.assetid: 66a2e00a-f558-4e87-96b8-5ecf5509e04c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4bf07dc6f47391af14c878021c742c2cb461bc85
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070408"
---
# <a name="sample-implementation-of-locals"></a>Exemplo de implementação de locais
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Veja a seguir uma visão geral de como o Visual Studio obtém os locais de um método do avaliador de expressão (EE):

1. O Visual Studio chama o mecanismo de depuração [Getdebugproperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) para obter um objeto [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) que representa todas as propriedades do quadro de pilha, incluindo os locais.

2. `IDebugStackFrame2::GetDebugProperty` chama [Getmethodproperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) para obter um objeto que descreve o método no qual o ponto de interrupção ocorreu. O DE fornece um provedor de símbolos ([IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)), um endereço ([IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)) e um associador ([IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)).

3. `IDebugExpressionEvaluator::GetMethodProperty` chama [Getcontainerfield](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md) com o `IDebugAddress` objeto fornecido para obter um [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) que representa o método que contém o endereço especificado.

4. A `IDebugContainerField` interface é consultada para a interface [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) . Essa interface fornece acesso aos locais do método.

5. `IDebugExpressionEvaluator::GetMethodProperty` Cria uma instância de uma classe (chamada `CFieldProperty` no exemplo) que executa a `IDebugProperty2` interface para representar os locais do método. O `IDebugMethodField` objeto é colocado nesse `CFieldProperty` objeto junto com os `IDebugSymbolProvider` objetos, `IDebugAddress` e `IDebugBinder` .

6. Quando o `CFieldProperty` objeto é inicializado, [GetInfo](../../extensibility/debugger/reference/idebugfield-getinfo.md) é chamado no `IDebugMethodField` objeto para obter uma estrutura de [FIELD_INFO](../../extensibility/debugger/reference/field-info.md) que contém todas as informações de exibição sobre o próprio método.

7. `IDebugExpressionEvaluator::GetMethodProperty` Retorna o `CFieldProperty` objeto como um `IDebugProperty2` objeto.

8. O Visual Studio chama [EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) no `IDebugProperty2` objeto retornado com o filtro `guidFilterLocalsPlusArgs` , que retorna um objeto [IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) que contém os locais do método. Essa enumeração é preenchida por chamadas para [EnumLocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md) e [EnumArguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md).

9. O Visual Studio chama [Next](../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md) para obter uma estrutura de [DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md) para cada local. Essa estrutura contém um ponteiro para uma `IDebugProperty2` interface para um local.

10. O Visual Studio chama [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) para cada local para obter o nome, o valor e o tipo do local. Essas informações são exibidas na janela **locais** .

## <a name="in-this-section"></a>Nesta seção
 [Implementar Getmethodproperty](../../extensibility/debugger/implementing-getmethodproperty.md) Descreve uma implementação de [Getmethodproperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md).

 [Enumerar locais](../../extensibility/debugger/enumerating-locals.md) Descreve como o mecanismo de depuração (DE) faz uma chamada para enumerar variáveis locais ou argumentos.

 [Obter propriedades locais](../../extensibility/debugger/getting-local-properties.md) Descreve como o DE faz uma chamada para obter o nome, o tipo e o valor de um ou mais locais.

 [Obter valores locais](../../extensibility/debugger/getting-local-values.md) Discute como obter o valor do local, que exige os serviços de um objeto de associador fornecido pelo contexto de avaliação.

 [Avaliar locais](../../extensibility/debugger/evaluating-locals.md) Explica como os locais são avaliados.

## <a name="related-sections"></a>Seções relacionadas
 [Contexto de avaliação](../../extensibility/debugger/evaluation-context.md) Fornece os argumentos que são passados quando o DE chama o avaliador de expressão (EE).

 [Exemplo de MyCEE](/previous-versions/) Demonstra uma abordagem de implementação para criar um avaliador de expressão para o idioma MyC.

## <a name="see-also"></a>Confira também
- [Exibindo locais](../../extensibility/debugger/displaying-locals.md)