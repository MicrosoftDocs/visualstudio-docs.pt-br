---
title: Exemplo de implementação de Locals | Microsoft Docs
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
- debugging [Debugging SDK], local variables
- expression evaluation, local variables
ms.assetid: 66a2e00a-f558-4e87-96b8-5ecf5509e04c
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 2ca64ed08060df3a03dbb178fc636ca243e1e48d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51756820"
---
# <a name="sample-implementation-of-locals"></a>Implementação de exemplo de locais
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Aqui está uma visão geral de como o Visual Studio obtém os locais para um método do avaliador de expressão (EE):  
  
1.  Visual Studio chama o mecanismo de depuração (DE) [GetDebugProperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) para obter uma [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) objeto que representa todas as propriedades do registro de ativação, incluindo os locais.  
  
2.  `IDebugStackFrame2::GetDebugProperty` chamadas [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) para obter um objeto que descreve o método dentro do qual o ponto de interrupção ocorreu. O DE fornece um provedor de símbolo ([IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)), um endereço ([IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)) e um associador ([IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)).  
  
3.  `IDebugExpressionEvaluator::GetMethodProperty` chamadas [GetContainerField](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md) com fornecido `IDebugAddress` objeto para obter uma [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) que representa o método que contém o endereço especificado.  
  
4.  O `IDebugContainerField` interface é consultado para o [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) interface. É essa interface que fornece acesso a locais do método.  
  
5.  `IDebugExpressionEvaluator::GetMethodProperty` cria uma instância de uma classe (chamados `CFieldProperty` no exemplo) que implementa o `IDebugProperty2` interface para representar locais do método. O `IDebugMethodField` objeto é colocado neste `CFieldProperty` do objeto juntamente com o `IDebugSymbolProvider`, `IDebugAddress` e `IDebugBinder` objetos.  
  
6.  Quando o `CFieldProperty` é inicializado, [GetInfo](../../extensibility/debugger/reference/idebugfield-getinfo.md) é chamado no `IDebugMethodField` objeto para obter um [FIELD_INFO](../../extensibility/debugger/reference/field-info.md) estrutura que contém todas as informações que pode ser exibidas sobre o próprio método .  
  
7.  `IDebugExpressionEvaluator::GetMethodProperty` Retorna o `CFieldProperty` objeto como um `IDebugProperty2` objeto.  
  
8.  Chamadas do Visual Studio [EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) em retornado `IDebugProperty2` objeto com o filtro `guidFilterLocalsPlusArgs`. Isso retorna um [IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) objeto que contém os locais do método. Essa enumeração é preenchida por chamadas para [EnumLocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md) e [EnumArguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md).  
  
9. Chamadas do Visual Studio [próxima](../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md) para obter uma [DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md) estrutura para cada local. Essa estrutura contém um ponteiro para um `IDebugProperty2` interface para um local.  
  
10. Chamadas do Visual Studio [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) para cada local obter o nome, valor e tipo de local. Essas são as informações que são exibidas na **Locals** janela.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Implementar GetMethodProperty](../../extensibility/debugger/implementing-getmethodproperty.md)  
 Descreve a implementação de [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md).  
  
 [Enumerar Locals](../../extensibility/debugger/enumerating-locals.md)  
 Descreve como o mecanismo de depuração (DES) faz uma chamada para enumerar as variáveis locais ou argumentos.  
  
 [Obter as propriedades do Local](../../extensibility/debugger/getting-local-properties.md)  
 Descreve como o DE faz uma chamada para obter o nome, tipo e valor de um ou mais locais.  
  
 [Obter valores de Local](../../extensibility/debugger/getting-local-values.md)  
 Discute como obter o valor do local, que exige que os serviços de um objeto de associador fornecido pelo contexto de avaliação.  
  
 [Avaliar Locals](../../extensibility/debugger/evaluating-locals.md)  
 Explica como as variáveis locais são avaliadas.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Contexto da avaliação](../../extensibility/debugger/evaluation-context.md)  
 Fornece os argumentos que são passados quando o DE chama o avaliador de expressão (EE).  
  
 [Exemplo de MyCEE](http://msdn.microsoft.com/en-us/624a018b-9179-402f-9d48-3aec87b48f4f)  
 Demonstra uma abordagem de implementação para a criação de um avaliador de expressão para o idioma MyC.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir Locals](../../extensibility/debugger/displaying-locals.md)

