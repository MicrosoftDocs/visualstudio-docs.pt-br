---
title: 'CA1502: evitar complexidade excessiva'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
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
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: bfa12a2a1ade8d32c5518660c46ce79bc997d776
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49819297"
---
# <a name="ca1502-avoid-excessive-complexity"></a>CA1502: evitar complexidade excessiva

|||
|-|-|
|NomeDoTipo|AvoidExcessiveComplexity|
|CheckId|CA1502|
|Categoria|Microsoft.Maintainability|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa

Um método tem uma complexidade ciclomática excessiva.

## <a name="rule-description"></a>Descrição da regra

*A complexidade ciclomática* mede o número de caminhos linearmente independentes por meio do método, que é determinado pelo número e pela complexidade das ramificações condicionais. Geralmente, uma complexidade ciclomática baixa indica um método que é fácil de entender, testar e manter. A complexidade ciclomática é calculada a partir de um gráfico de fluxo de controle do método e recebe da seguinte maneira:

a complexidade ciclomática = o número de bordas - o número de nós + 1

em que um nó representa um ponto de ramificação de lógica e uma borda representa uma linha entre os nós.

A regra relata uma violação, quando a complexidade ciclomática é a mais de 25.

Você pode aprender mais sobre as métricas de código em [medindo complexidade e facilidade de manutenção do código gerenciado](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md),

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, Refatore o método para reduzir sua complexidade ciclomática.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

É seguro suprimir um aviso nessa regra se facilmente não pode ser reduzida a complexidade e o método é fácil de entender, testar e manter. Em particular, um método que contém um grande `switch` (`Select` em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) instrução é um candidato para exclusão. O risco de desestabilizar a tarde no ciclo de desenvolvimento ou introduzir uma alteração inesperada no comportamento de tempo de execução no código fornecido anteriormente pode superar os benefícios de facilidade de manutenção de refatorar o código de base de código.

## <a name="how-cyclomatic-complexity-is-calculated"></a>Como a complexidade ciclomática é calculada

A complexidade ciclomática é calculada adicionando 1 ao seguinte:

- Número de ramificações (como `if`, `while`, e `do`)

- Número de `case` instruções em um `switch`

## <a name="example"></a>Exemplo

Os exemplos a seguir mostram os métodos que possuem as complexidades de ciclomática variados.

**Complexidade ciclomática igual a 1**

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

**Complexidade ciclomática de 8**

[!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../code-quality/codesnippet/CPP/ca1502-avoid-excessive-complexity_4.cpp)]
[!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#4](../code-quality/codesnippet/VisualBasic/ca1502-avoid-excessive-complexity_4.vb)]
[!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../code-quality/codesnippet/CSharp/ca1502-avoid-excessive-complexity_4.cs)]

## <a name="related-rules"></a>Regras relacionadas

[CA1501: evitar herança excessiva](../code-quality/ca1501-avoid-excessive-inheritance.md)

## <a name="see-also"></a>Consulte também

- [Medindo complexidade e facilidade de manutenção do código gerenciado](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)