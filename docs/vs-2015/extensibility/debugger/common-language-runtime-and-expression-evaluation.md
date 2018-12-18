---
title: Common Language Runtime e avaliação de expressão | Microsoft Docs
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
- expression evaluation, and common language runtime
ms.assetid: b36c1eb5-1aaf-48a6-b287-ee7a273d2b1c
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 85cf4d2029dc25dc993fcc32b89fdc60bd91171d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51779340"
---
# <a name="common-language-runtime-and-expression-evaluation"></a>Common Language Runtime e avaliação de expressão
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Compiladores, como Visual Basic e c# (pronuncia-se C-sharp), que direcionam o tempo de execução de linguagem comum (CLR), produzem MSIL Microsoft Intermediate Language (), que é posterior compilados para código nativo. O CLR fornece um mecanismo de depuração (DE) para depurar o código resultante. Se você pretende integrar a linguagem de programação proprietária ao IDE do Visual Studio, você pode optar por compilar para MSIL e, portanto, não precisa escrever seu próprio DE. No entanto, você terá que escrever um avaliador de expressão (EE) que é capaz de avaliar expressões dentro do contexto de sua linguagem de programação.  
  
## <a name="discussion"></a>Discussão  
 Expressões de idioma do computador geralmente são analisadas para produzir um conjunto de objetos de dados e um conjunto de operadores usados para manipulá-los. Por exemplo, a expressão "A + B" pode ser analisada para aplicar o operador de adição (+) para os dados de objetos "A" e "B", possivelmente resultando em outro objeto de dados. O conjunto total de objetos de dados, operadores e suas associações com mais frequência são representados em um programa como uma árvore, os operadores em nós da árvore e os objetos de dados nas ramificações. Uma expressão que tem sido dividida em forma de árvore é frequentemente chamada de uma árvore analisada.  
  
 Depois que uma expressão foi analisada, um provedor de símbolo (SP) é chamado para avaliar cada objeto de dados. Por exemplo, se "A" é definida em mais de um método e, em seguida, a pergunta "Qual A?" deve ser atendida antes que o valor de A pode ser determinado. A resposta retornada pelo SP é algo como "O terceiro item na estrutura de pilhas quinta" ou "O que é de 50 bytes além do início da memória estática A alocado para esse método."  
  
 Além de produzir MSIL para o próprio programa, os compiladores do CLR também podem produzir as informações de depuração muito descritivas que são gravadas em um arquivo de banco de dados do programa (. PDB). Desde que um compilador de linguagem proprietários produz informações de depuração no mesmo formato que os compiladores CLR, SP do CLR é capaz de identificar que da linguagem denominada objetos de dados. Depois que um objeto de dados chamado tiver sido identificado, o EE usa um objeto de fichário para associar o objeto de dados (ou associar uma) para a área de memória que contém o valor desse objeto. O DE, em seguida, pode obter ou definir um novo valor para o objeto de dados.  
  
 Um compilador proprietário pode fornecer informações de depuração por meio da chamada do CLR a `ISymbolWriter` interface (que é definido no .NET Framework no namespace `System.Diagnostics.SymbolStore`). Compilando para MSIL e gravar informações de depuração por meio dessas interfaces, um compilador proprietário pode usar os campos DE CLR e SP. Isso simplifica bastante a integração de uma linguagem proprietária ao IDE do Visual Studio.  
  
 Quando o CLR DE chama o EE proprietária para avaliar uma expressão, o DE fornece o EE com interfaces para um SP e um objeto de associador. Portanto, escrever um meio de mecanismo de depuração com base em CLR é necessário somente implementar as interfaces de avaliador de expressão apropriada; o CLR se encarrega de associação e o símbolo de tratamento para você.  
  
## <a name="see-also"></a>Consulte também  
 [Escrevendo um avaliador de expressão do CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)

