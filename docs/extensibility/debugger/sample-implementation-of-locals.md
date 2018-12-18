---
title: Exemplo de implementação de Locals | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], local variables
- expression evaluation, local variables
ms.assetid: 66a2e00a-f558-4e87-96b8-5ecf5509e04c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3faf3e42442db03bbb40bbc3e726b909956d4187
ms.sourcegitcommit: 3dd15e019cba7d35dbabc1aa3bf55842a59f5278
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/19/2018
ms.locfileid: "46370855"
---
# <a name="sample-implementation-of-locals"></a>Exemplo de implementação de locals
> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 A seguir está uma visão geral de como o Visual Studio obtém os locais para um método do avaliador de expressão (EE):  
  
1.  Visual Studio chama o mecanismo de depuração (DE) [GetDebugProperty](../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) para obter uma [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) objeto que representa todas as propriedades do registro de ativação, incluindo os locais.  
  
2.  `IDebugStackFrame2::GetDebugProperty` chamadas [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) para obter um objeto que descreve o método dentro do qual o ponto de interrupção ocorreu. O DE fornece um provedor de símbolo ([IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)), um endereço ([IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)) e um associador ([IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)).  
  
3.  `IDebugExpressionEvaluator::GetMethodProperty` chamadas [GetContainerField](../../extensibility/debugger/reference/idebugsymbolprovider-getcontainerfield.md) com fornecido `IDebugAddress` objeto para obter uma [IDebugContainerField](../../extensibility/debugger/reference/idebugcontainerfield.md) que representa o método que contém o endereço especificado.  
  
4.  O `IDebugContainerField` interface é consultado para o [IDebugMethodField](../../extensibility/debugger/reference/idebugmethodfield.md) interface. É essa interface que fornece acesso a locais do método.  
  
5.  `IDebugExpressionEvaluator::GetMethodProperty` cria uma instância de uma classe (chamados `CFieldProperty` no exemplo) que executa o `IDebugProperty2` interface para representar locais do método. O `IDebugMethodField` objeto é colocado neste `CFieldProperty` do objeto juntamente com o `IDebugSymbolProvider`, `IDebugAddress`, e `IDebugBinder` objetos.  
  
6.  Quando o `CFieldProperty` é inicializado, [GetInfo](../../extensibility/debugger/reference/idebugfield-getinfo.md) é chamado no `IDebugMethodField` objeto do qual obter um [FIELD_INFO](../../extensibility/debugger/reference/field-info.md) estrutura que contém todas as informações que pode ser exibidas sobre o próprio método.  
  
7.  `IDebugExpressionEvaluator::GetMethodProperty` Retorna o `CFieldProperty` objeto como um `IDebugProperty2` objeto.  
  
8.  Chamadas do Visual Studio [EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) em retornado `IDebugProperty2` objeto com o filtro `guidFilterLocalsPlusArgs`, que retorna um [IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) objeto que contém os locais do método. Essa enumeração é preenchida por chamadas para [EnumLocals](../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md) e [EnumArguments](../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md).  
  
9. Chamadas do Visual Studio [próxima](../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md) para obter uma [DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md) estrutura para cada local. Essa estrutura contém um ponteiro para um `IDebugProperty2` interface para um local.  
  
10. Chamadas do Visual Studio [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) para cada local obter o nome, valor e tipo de local. Essas informações são exibidas na **Locals** janela.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Implementar GetMethodProperty](../../extensibility/debugger/implementing-getmethodproperty.md)  
 Descreve a implementação de [GetMethodProperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md).  
  
 [Enumerar locals](../../extensibility/debugger/enumerating-locals.md)  
 Descreve como o mecanismo de depuração (DES) faz uma chamada para enumerar as variáveis locais ou argumentos.  
  
 [Obter propriedades do locais](../../extensibility/debugger/getting-local-properties.md)  
 Descreve como o DE faz uma chamada para obter o nome, tipo e valor de um ou mais locais.  
  
 [Obter valores locais](../../extensibility/debugger/getting-local-values.md)  
 Discute a obtenção do valor de local, que exige que os serviços de um objeto de associador fornecido pelo contexto de avaliação.  
  
 [Avaliar locals](../../extensibility/debugger/evaluating-locals.md)  
 Explica como as variáveis locais são avaliadas.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Contexto de avaliação](../../extensibility/debugger/evaluation-context.md)  
 Fornece os argumentos que são passados quando o DE chama o avaliador de expressão (EE).  
  
 [Exemplo de MyCEE](https://msdn.microsoft.com/library/624a018b-9179-402f-9d48-3aec87b48f4f)  
 Demonstra uma abordagem de implementação para a criação de um avaliador de expressão para o idioma MyC.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir locals](../../extensibility/debugger/displaying-locals.md)