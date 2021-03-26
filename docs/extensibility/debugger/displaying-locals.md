---
title: Exibindo locais | Microsoft Docs
description: Saiba mais sobre a lista de variáveis e argumentos locais, coletivamente chamados de locais do método, que são exibidos quando a execução pausa.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, displaying locals
ms.assetid: 62264cec-845b-4233-aed7-0b038fa79250
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 564b42a15e1420027b79cb5f00c70f61649ad4f9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097260"
---
# <a name="display-locals"></a>Exibir locais
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 A execução sempre ocorre no contexto de um método, também conhecido como o método recipiente ou o método atual. Quando a execução é pausada, o Visual Studio chama o mecanismo de depuração (DE) para obter uma lista de variáveis e argumentos locais, coletivamente chamados de locais do método. O Visual Studio exibe esses locais e seus valores na janela **locais** .

 Para exibir locais, o DE chama o método [Getmethodproperty](../../extensibility/debugger/reference/idebugexpressionevaluator-getmethodproperty.md) que pertence ao EE e fornece a ele um contexto de avaliação, ou seja, um provedor de símbolos (SP), o endereço de execução atual e um objeto de fichário. Para obter mais informações, consulte [contexto de avaliação](../../extensibility/debugger/evaluation-context.md). Se a chamada for realizada com sucesso, o `IDebugExpressionEvaluator::GetMethodProperty` método retornará um objeto [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) , que representa o método que contém o endereço de execução atual.

 O DE chama [EnumChildren](../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) para obter um objeto [IEnumDebugPropertyInfo2](../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) , que é filtrado para retornar somente locais e enumerados para produzir uma lista de estruturas de [DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md) . Cada estrutura contém o nome, o tipo e o valor de um local. O tipo e o valor são armazenados como cadeias de caracteres formatadas, adequadas para exibição. O nome, o tipo e o valor normalmente são exibidos juntos em uma linha da janela **locais** .

> [!NOTE]
> As janelas **QuickWatch** e **Watch** também exibem variáveis com o mesmo formato de nome, valor e tipo. No entanto, esses valores são obtidos chamando [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) em vez de `IDebugProperty2::EnumChildren` .

## <a name="in-this-section"></a>Nesta seção
 [Exemplo de implementação de locais](../../extensibility/debugger/sample-implementation-of-locals.md) Usa exemplos para percorrer o processo de implementação de locais.

## <a name="related-sections"></a>Seções relacionadas
 [Contexto de avaliação](../../extensibility/debugger/evaluation-context.md) Explica que quando o mecanismo de depuração (DE) chama o avaliador de expressão (EE), ele passa três argumentos.

## <a name="see-also"></a>Confira também
 [Escrever um avaliador de expressão CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
