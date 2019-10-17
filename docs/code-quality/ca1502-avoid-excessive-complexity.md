---
title: 'CA1502: evitar complexidade excessiva'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AvoidExcessiveComplexity
- CA1502
helpviewer_keywords:
- CA1502
- AvoidExcessiveComplexity
ms.assetid: d735454b-2f8f-47ce-907d-f7a5a5391221
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 8eaaaa8b810e79b2bd1a4da0ab1d9887c8a46380
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72440120"
---
# <a name="ca1502-avoid-excessive-complexity"></a>CA1502: evitar complexidade excessiva

|||
|-|-|
|NomeDoTipo|AvoidExcessiveComplexity|
|CheckId|CA1502|
|Categoria|Microsoft. Maintainabilidade|
|Alteração significativa|Sem interrupção|

## <a name="cause"></a>Causa

Um método tem uma complexidade ciclomática excessiva.

## <a name="rule-description"></a>Descrição da regra

A *complexidade ciclomática* mede o número de caminhos linearmente independentes por meio do método, que é determinado pelo número e pela complexidade de ramificações condicionais. Uma complexidade ciclomática baixa geralmente indica um método que é fácil de entender, testar e manter. A complexidade do ciclomática é calculada a partir de um grafo de fluxo de controle do método e é fornecida da seguinte maneira:

complexidade ciclomática = o número de bordas – o número de nós + 1

Um *nó* representa um ponto de ramificação lógica e uma *borda* representa uma linha entre nós.

A regra relata uma violação quando a complexidade do ciclomática é maior que 25.

Você pode aprender mais sobre as métricas de código em [medir a complexidade do código gerenciado](../code-quality/code-metrics-values.md).

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, refatore o método para reduzir sua complexidade de ciclomática.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

É seguro suprimir um aviso dessa regra se a complexidade não puder ser facilmente reduzida e o método for fácil de entender, testar e manter. Em particular, um método que contém uma instrução grande `switch` (`Select` em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) é um candidato para exclusão. O risco de desestabilizar a base de código no final do ciclo de desenvolvimento ou introduzir uma alteração inesperada no comportamento de tempo de execução no código fornecido anteriormente pode superar os benefícios de manutenção da refatoração do código.

## <a name="how-cyclomatic-complexity-is-calculated"></a>Como a complexidade do ciclomática é calculada

A complexidade do ciclomática é calculada adicionando 1 ao seguinte:

- Número de ramificações (como `if`, `while` e `do`)

- Número de instruções `case` em um `switch`

## <a name="example"></a>Exemplo

Os exemplos a seguir mostram métodos que têm complexidades ciclomática variáveis.

**Complexidade ciclomática de 1**

[!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#1](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_1.cpp)]
[!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#1](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_1.vb)]
[!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#1](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_1.cs)]

## <a name="example"></a>Exemplo

**Complexidade ciclomática de 2**

[!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#2](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_2.cpp)]
[!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#2](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_2.vb)]
[!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#2](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_2.cs)]

## <a name="example"></a>Exemplo

**Complexidade ciclomática de 3**

[!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#3](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_3.cpp)]
[!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#3](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_3.vb)]
[!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#3](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_3.cs)]

## <a name="example"></a>Exemplo

**Ciclomática complexidade de 8**

[!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_4.cpp)]
[!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#4](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_4.vb)]
[!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_4.cs)]

## <a name="related-rules"></a>Regras relacionadas

[CA1501: evitar herança excessiva](../code-quality/ca1501-avoid-excessive-inheritance.md)

## <a name="see-also"></a>Consulte também

- [Medindo complexidade e facilidade de manutenção do código gerenciado](../code-quality/code-metrics-values.md)
