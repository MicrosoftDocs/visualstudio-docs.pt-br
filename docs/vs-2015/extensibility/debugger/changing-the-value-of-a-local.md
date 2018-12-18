---
title: Alterando o valor de um Local | Microsoft Docs
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
- expression evaluation, changing values programmatically
ms.assetid: 8407d3df-d38a-4328-82d1-98084bef43ec
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 166b4d22ec24f3137044ab19255abb15b109fbe0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51807212"
---
# <a name="changing-the-value-of-a-local"></a>Alterando o valor de um local
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

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
  
   Esse procedimento também é usado para alterar o valor de uma variável na **Watch** janela exceto que é o `IDebugProperty2` objeto associado com o valor do local que é usado em vez do `IDebugProperty2` objeto associado ao local em si.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Exemplo de implementação da alteração de valores](../../extensibility/debugger/sample-implementation-of-changing-values.md)  
 Usa o exemplo de MyCEE para percorrer o processo de alteração de valores.  
  
## <a name="see-also"></a>Consulte também  
 [Escrever um avaliador de expressão de CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)   
 [Exibir Locals](../../extensibility/debugger/displaying-locals.md)

