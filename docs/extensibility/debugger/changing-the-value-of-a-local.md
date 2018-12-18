---
title: Alterando o valor de um Local | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, changing values programmatically
ms.assetid: 8407d3df-d38a-4328-82d1-98084bef43ec
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1ed8ea2aa16ec9bddd626c08f1e45d502d402b57
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49823184"
---
# <a name="change-the-value-of-a-local"></a>Altere o valor de um local
> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Quando um novo valor é digitado no campo de valor de **Locals** janela, o pacote de depuração passa a cadeia de caracteres, como digitado, o avaliador de expressão (EE). O EE avalia essa cadeia de caracteres, que pode conter um valor simples ou uma expressão e armazena o valor resultante no local associado.  
  
 Isso é uma visão geral do processo de alteração do valor de um local:  
  
1. Depois que o usuário inserir o novo valor, o Visual Studio chama [SetValueAsString](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md) sobre o [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) objeto associado ao local.  
  
2. `IDebugProperty2::SetValueAsString` executa as seguintes tarefas:  
  
   1.  Avalia a cadeia de caracteres para produzir um valor.  
  
   2.  Associa o associados [IDebugField](../../extensibility/debugger/reference/idebugfield.md) objeto para obter uma [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) objeto.  
  
   3.  Converte o valor em uma série de bytes.  
  
   4.  Chamadas [SetValue](../../extensibility/debugger/reference/idebugobject-setvalue.md) para colocar os bytes do valor na memória para que o programa que está sendo depurado possa acessá-los.  
  
3. O Visual Studio atualizará os **Locals** exibir (consulte [exibindo locais](../../extensibility/debugger/displaying-locals.md) para obter detalhes).  
  
   Esse procedimento também é usado para alterar o valor de uma variável na **Watch** janela, exceto que ele é o `IDebugProperty2` objeto associado com o valor do local que é usado em vez do `IDebugProperty2` objeto associado ao local em si.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Exemplo de implementação de valores de variáveis](../../extensibility/debugger/sample-implementation-of-changing-values.md)  
 Usa o exemplo de MyCEE para percorrer o processo de alteração de valores.  
  
## <a name="see-also"></a>Consulte também  
 [Escrever um avaliador de expressão de CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)   
 [Exibir locals](../../extensibility/debugger/displaying-locals.md)