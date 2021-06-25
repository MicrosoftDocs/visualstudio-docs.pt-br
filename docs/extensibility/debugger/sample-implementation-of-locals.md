---
title: Implementação de exemplo de locais | Microsoft Docs
description: Saiba como Visual Studio obtém os locais de um método do avaliador de expressão neste artigo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: sample
helpviewer_keywords:
- debugging [Debugging SDK], local variables
- expression evaluation, local variables
ms.assetid: 66a2e00a-f558-4e87-96b8-5ecf5509e04c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ac52f1524c4be2e4a7afcbd21fb437977fb663e3
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902274"
---
# <a name="sample-implementation-of-locals"></a>Implementação de exemplo de locais
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão foi preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte Avaliadores de expressão CLR e Exemplo de [avaliador](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) [de expressão gerenciada.](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)

 Veja a seguir uma visão geral de Visual Studio obtém os locais de um método do avaliador de expressão (EE):

1. Visual Studio chama [GetDebugProperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) do mecanismo de depuração para obter um objeto [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) que representa todas as propriedades do quadro de pilha, incluindo os locais.

2. `IDebugStackFrame2::GetDebugProperty` chama [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) para obter um objeto que descreve o método no qual o ponto de interrupção aconteceu. O DE fornece um provedor de símbolos ([IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)), um endereço ([IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)) e um binder ([IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)).

3. `IDebugExpressionEvaluator::GetMethodProperty` chama [GetContainerField](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md) com o objeto fornecido para obter `IDebugAddress` um [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) que representa o método que contém o endereço especificado.

4. A `IDebugContainerField` interface é consultada para a interface [IDebugMethodField.](../../extensibility/debugger/reference/idebugmethodfield.md) É essa interface que fornece acesso aos locais do método.

5. `IDebugExpressionEvaluator::GetMethodProperty` instalita uma classe (chamada no exemplo) que executa a `CFieldProperty` interface para representar os locais do `IDebugProperty2` método. O `IDebugMethodField` objeto é colocado nesse objeto junto com os objetos , e `CFieldProperty` `IDebugSymbolProvider` `IDebugAddress` `IDebugBinder` .

6. Quando o `CFieldProperty` objeto é inicializado, [GetInfo](../../extensibility/debugger/reference/idebugfield-getinfo.md) é chamado no objeto para obter uma estrutura FIELD_INFO que contém todas as informações exibiveis `IDebugMethodField` sobre o próprio método. [](../../extensibility/debugger/reference/field-info.md)

7. `IDebugExpressionEvaluator::GetMethodProperty` retorna o `CFieldProperty` objeto como um objeto `IDebugProperty2` .

8. Visual Studio chama [EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) no objeto retornado com o filtro , que retorna um objeto `IDebugProperty2` `guidFilterLocalsPlusArgs` [IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) que contém os locais do método. Essa enumeração é preenchida por chamadas para [EnumLocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md) [e EnumArguments.](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)

9. Visual Studio [chama Next](../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md) para obter uma [estrutura DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md) para cada local. Essa estrutura contém um ponteiro para uma `IDebugProperty2` interface para um local.

10. Visual Studio chama [GetPropertyInfo para](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) cada local para obter o nome, o valor e o tipo do local. Essas informações são exibidas na **janela Locais.**

## <a name="in-this-section"></a>Nesta seção
 [Implementar GetMethodProperty](../../extensibility/debugger/implementing-getmethodproperty.md) Descreve uma implementação de [GetMethodProperty.](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md)

 [Enumerar locais](../../extensibility/debugger/enumerating-locals.md) Descreve como o DE (mecanismo de depuração) faz uma chamada para enumerar variáveis ou argumentos locais.

 [Obter propriedades locais](../../extensibility/debugger/getting-local-properties.md) Descreve como o DE faz uma chamada para obter o nome, o tipo e o valor de um ou mais locais.

 [Obter valores locais](../../extensibility/debugger/getting-local-values.md) Discute como obter o valor do local, o que requer os serviços de um objeto de a binder dado pelo contexto de avaliação.

 [Avaliar locais](../../extensibility/debugger/evaluating-locals.md) Explica como os locais são avaliados.

## <a name="related-sections"></a>Seções relacionadas
 [Contexto de avaliação](../../extensibility/debugger/evaluation-context.md) Fornece os argumentos que são passados quando o DE chama o avaliador de expressão (EE).

 [Exemplo de MyCEE](/previous-versions/) Demonstra uma abordagem de implementação para criar um avaliador de expressão para a linguagem MyC.

## <a name="see-also"></a>Confira também
- [Exibindo locais](../../extensibility/debugger/displaying-locals.md)