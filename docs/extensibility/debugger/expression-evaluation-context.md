---
title: Contexto de avaliação de expressão | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, context
ms.assetid: a2fd3758-09bd-45ae-8ecc-2d276c0036ba
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 9a01d8fd9e1ac7a439898775bc8b4b0fc933650c
ms.sourcegitcommit: 25a62c2db771f938e3baa658df8b1ae54a960e4f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39232488"
---
# <a name="expression-evaluation-context"></a>Contexto de avaliação de expressão
Na [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depuração, um **contexto de avaliação de expressão**:  
  
-   Representa um contexto de avaliação da expressão. Geralmente, um contexto de avaliação corresponde ao escopo léxico na qual você deseja avaliar as variáveis, parâmetros, funções e métodos. Por exemplo, um contexto de avaliação de expressão associado com um quadro de pilha fornecerá o contexto para avaliar as variáveis locais, parâmetros de método e membros de classe (se aplicável).  
  
-   Existe quando um programa foi interrompido no ponto de interrupção. A expressão em si é uma estrutura de dados que representa uma expressão analisada que está pronta para vinculação e avaliar dentro do contexto especificado.  
  
     Mais detalhadamente, as expressões são criadas usando o [ParseText](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) método. Quando uma expressão é avaliada, ele gera uma cadeia de caracteres imprimível, que contém o nome e tipo de variável ou argumento e seu valor. Essa cadeia de caracteres é exibida na janela de observação ou na janela locais do IDE.  
  
     Considerando um `BSTR` e uma [IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md) interface, um mecanismo de depuração (DES) pode criar um [IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md) interface analisando uma expressão. Dado um `IDebugExpression2` interface, a Alemanha pode obter um valor por meio da avaliação da expressão síncrona ou assíncrona. Esse valor, junto com o nome e o tipo da variável ou argumento, é enviado para o IDE para exibição.  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de avaliação de expressão](../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)