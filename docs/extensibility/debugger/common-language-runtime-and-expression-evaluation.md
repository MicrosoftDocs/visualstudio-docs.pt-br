---
title: Tempo de execução de linguagem comum e avaliação de expressão | Microsoft Docs
description: Saiba como o Common Language Runtime interage com o mecanismo de depuração e como integrar uma linguagem de programação proprietária no IDE do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, and common language runtime
ms.assetid: b36c1eb5-1aaf-48a6-b287-ee7a273d2b1c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 35ddc218d0e9499253269a12687fa89122cfe007
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055005"
---
# <a name="common-language-runtime-and-expression-evaluation"></a>Tempo de execução de linguagem comum e avaliação de expressão
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Compiladores, como Visual Basic e C# (pronuncia-se C-Sharp), que visam o CLR (Common Language Runtime), produzem o MSIL (Microsoft Intermediate Language), que é posteriormente compilado no código nativo. O CLR fornece um mecanismo DE depuração (DE) para depurar o código resultante. Se você planeja integrar sua linguagem de programação proprietária no IDE do Visual Studio, você pode optar por Compilar para MSIL e, portanto, não precisará escrever seus próprios. No entanto, você precisará escrever um avaliador de expressão (EE) que seja capaz de avaliar expressões dentro do contexto de sua linguagem de programação.

## <a name="discussion"></a>Discussão
 As expressões de idioma do computador geralmente são analisadas para produzir um conjunto de objetos de dados e um conjunto de operadores usados para manipulá-los. Por exemplo, a expressão "A + B" pode ser analisada para aplicar o operador de adição (+) aos objetos de dados "A" e "B", possivelmente resultando em outro objeto de dados. O conjunto total de objetos de dados, operadores e suas associações geralmente é representado em um programa como uma árvore, com os operadores nos nós da árvore e os objetos de dados nas ramificações. Uma expressão que foi dividida em formulário de árvore geralmente é chamada de árvore analisada.

 Depois que uma expressão é analisada, um provedor de símbolo (SP) é chamado para avaliar cada objeto de dados. Por exemplo, se "A" for definido em mais de um método, a pergunta "qual?" deve ser respondido para que o valor de A possa ser determinado. A resposta retornada pelo SP é algo como "o terceiro item no quinto quadro de pilha" ou "o que é 50 bytes além do início da memória estática alocada para esse método".

 Além de produzir o MSIL para o próprio programa, os compiladores CLR também podem produzir informações de depuração muito descritivas que são gravadas em um arquivo de banco de dados do programa (*. pdb*). Desde que um compilador de linguagem proprietária produza informações de depuração no mesmo formato que os compiladores do CLR, o SP do CLR é capaz de identificar os objetos de dados nomeados do idioma. Depois que um objeto de dados nomeado tiver sido identificado, o EE usará um objeto de associador para associar (ou associar) o objeto de dados à área de memória que contém o valor desse objeto. O DE pode obter ou definir um novo valor para o objeto de dados.

 Um compilador proprietário pode fornecer informações de depuração CLR chamando a `ISymbolWriter` interface (que é definida no .NET Framework no namespace `System.Diagnostics.SymbolStore` ). Ao compilar para MSIL e gravar informações de depuração por meio dessas interfaces, um compilador proprietário pode usar o CLR DE e o SP. Isso simplifica muito a integração de uma linguagem proprietária ao IDE do Visual Studio.

 Quando o CLR DE chama o EE proprietário para avaliar uma expressão, o DE fornece o EE com interfaces para um SP e um objeto de fichário. Assim, escrever um mecanismo de depuração baseado em CLR significa que é necessário apenas implementar as interfaces do avaliador de expressão apropriadas; o CLR cuida da ligação e do tratamento de símbolos para você.

## <a name="see-also"></a>Confira também
- [Escrever um avaliador de expressão CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
