---
title: Escrever um avaliador de expressão de tempo de execução de linguagem comum | Microsoft Docs
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
- expression evaluators, tutorial
- expression evaluation, samples
- debugging [Debugging SDK], expression evaluators tutorial
ms.assetid: bd79d57f-8e0a-4e14-a417-0b1de28fa1b2
caps.latest.revision: 24
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: cfd368bb0302fec1fcf9fdd1f6e6e069377846ab
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51783006"
---
# <a name="writing-a-common-language-runtime-expression-evaluator"></a>Escrevendo um avaliador de expressão do Common Language Runtime
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 O avaliador de expressão (EE) é a parte de um mecanismo de depuração (DES) que lida com a sintaxe e semântica da linguagem de programação que gerou o código que está sendo depurado. As expressões devem ser avaliadas dentro do contexto de uma linguagem de programação. Por exemplo, em alguns idiomas, a expressão "A + B" significa "a soma de A e b." Em outras linguagens, a mesma expressão pode significar "A ou B." Portanto, um separado EE deve ser escrito para cada linguagem de programação que gera o código de objeto a ser depurado no IDE do Visual Studio.  
  
 Alguns aspectos do pacote de depuração do Visual Studio devem interpretar o código no contexto da linguagem de programação. Por exemplo, quando a execução é interrompida no ponto de interrupção, todas as expressões que o usuário digitou em uma **inspeção** janela deve ser avaliada e exibida. Além disso, o usuário pode alterar o valor de uma variável local digitando uma expressão em uma **Watch** janela ou o **imediato** janela.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Common Language Runtime e Avaliação de expressão](../../extensibility/debugger/common-language-runtime-and-expression-evaluation.md)  
 Explica que quando você precisa integrar a linguagem de programação proprietária ao IDE do Visual Studio, escrever um EE capaz de avaliar expressões dentro do contexto da linguagem proprietária permite que você compilar para um Microsoft intermediate language (MSIL) sem escrever um mecanismo de depuração.  
  
 [Arquitetura do Avaliador de expressão](../../extensibility/debugger/expression-evaluator-architecture.md)  
 Discute como implementar as interfaces EE necessárias e chamar o provedor de símbolo de tempo de execução de linguagem comum (SP) e interfaces de associador.  
  
 [Registrar um Avaliador de expressão](../../extensibility/debugger/registering-an-expression-evaluator.md)  
 Observa que o EE deve ser registrado como uma fábrica de classes com o common language runtime e os ambientes de tempo de execução do Visual Studio.  
  
 [Implementar um Avaliador de expressão](../../extensibility/debugger/implementing-an-expression-evaluator.md)  
 Descreve como o processo de avaliar uma expressão inclui o mecanismo de depuração (DE), o provedor de símbolo (SP), o objeto de associador e o avaliador de expressão (EE).  
  
 [Exibir Locals](../../extensibility/debugger/displaying-locals.md)  
 Descreve como fazer isso, quando a execução pausa, o pacote de depuração chama DE para obter uma lista de argumentos e variáveis locais.  
  
 [Avaliar uma expressão da janela Inspeção](../../extensibility/debugger/evaluating-a-watch-window-expression.md)  
 Documenta como o pacote de depuração do Visual Studio chama o DE para determinar o valor atual de cada expressão em sua lista de inspeção.  
  
 [Alterar o valor de um Local](../../extensibility/debugger/changing-the-value-of-a-local.md)  
 Explica como alterar o valor de um local, cada linha da janela locais tem um objeto associado que fornece o nome, o tipo e o valor atual de um local.  
  
 [Implementar visualizadores de tipo e visualizadores personalizados](../../extensibility/debugger/implementing-type-visualizers-and-custom-viewers.md)  
 Explica a interface que precisa ser implementada pelo componente que para dar suporte a visualizadores de tipo e visualizadores personalizados.  
  
## <a name="see-also"></a>Consulte também  
 [Extensibilidade do depurador do Visual Studio](../../extensibility/debugger/visual-studio-debugger-extensibility.md)

