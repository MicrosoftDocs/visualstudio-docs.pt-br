---
title: 'CA1502: evitar complexidade excessiva | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidExcessiveComplexity
- CA1502
helpviewer_keywords:
- CA1502
- AvoidExcessiveComplexity
ms.assetid: d735454b-2f8f-47ce-907d-f7a5a5391221
caps.latest.revision: 32
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5da2e2bf26bb1894987caa8b748181d952bd7c18
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547830"
---
# <a name="ca1502-avoid-excessive-complexity"></a>CA1502: Evitar complexidade excessiva
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AvoidExcessiveComplexity|
|CheckId|CA1502|
|Categoria|Microsoft. Maintainabilidade|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um método tem uma complexidade ciclomática excessiva.

## <a name="rule-description"></a>Descrição da Regra
 A *complexidade ciclomática* mede o número de caminhos linearmente independentes por meio do método, que é determinado pelo número e pela complexidade de ramificações condicionais. Uma complexidade ciclomática baixa geralmente indica um método que é fácil de entender, testar e manter. A complexidade do ciclomática é calculada a partir de um grafo de fluxo de controle do método e é fornecida da seguinte maneira:

 complexidade ciclomática = o número de bordas – o número de nós + 1

 onde um nó representa um ponto de ramificação lógica e uma borda representa uma linha entre nós.

 A regra relata uma violação quando a complexidade do ciclomática é maior que 25.

 Você pode aprender mais sobre as métricas de código em [medindo a complexidade e a manutenção do código gerenciado](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md),

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, refatore o método para reduzir sua complexidade de ciclomática.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se a complexidade não puder ser facilmente reduzida e o método for fácil de entender, testar e manter. Em particular, um método que contém uma `switch` instrução ( `Select` in [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ) grande é um candidato para exclusão. O risco de desestabilizar a base de código no final do ciclo de desenvolvimento ou introduzir uma alteração inesperada no comportamento de tempo de execução no código fornecido anteriormente pode superar os benefícios de manutenção da refatoração do código.

## <a name="how-cyclomatic-complexity-is-calculated"></a>Como a complexidade do ciclomática é calculada
 A complexidade do ciclomática é calculada adicionando 1 ao seguinte:

- Número de ramificações (como `if` , `while` e `do` )

- Número de `case` instruções em um`switch`

  Os exemplos a seguir mostram métodos que têm complexidades ciclomática variáveis.

## <a name="example"></a>Exemplo
 **Complexidade ciclomática de 1**

 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cpp/FxCop.Maintainability.AvoidExcessiveComplexity.cpp#1)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cs/FxCop.Maintainability.AvoidExcessiveComplexity.cs#1)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/vb/FxCop.Maintainability.AvoidExcessiveComplexity.vb#1)]

## <a name="example"></a>Exemplo
 **Complexidade ciclomática de 2**

 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#2](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cpp/FxCop.Maintainability.AvoidExcessiveComplexity.cpp#2)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#2](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cs/FxCop.Maintainability.AvoidExcessiveComplexity.cs#2)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#2](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/vb/FxCop.Maintainability.AvoidExcessiveComplexity.vb#2)]

## <a name="example"></a>Exemplo
 **Complexidade ciclomática de 3**

 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#3](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cpp/FxCop.Maintainability.AvoidExcessiveComplexity.cpp#3)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#3](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cs/FxCop.Maintainability.AvoidExcessiveComplexity.cs#3)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#3](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/vb/FxCop.Maintainability.AvoidExcessiveComplexity.vb#3)]

## <a name="example"></a>Exemplo
 **Ciclomática complexidade de 8**

 [!code-cpp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cpp/FxCop.Maintainability.AvoidExcessiveComplexity.cpp#4)]
 [!code-csharp[FxCop.Maintainability.AvoidExcessiveComplexity#4](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/cs/FxCop.Maintainability.AvoidExcessiveComplexity.cs#4)]
 [!code-vb[FxCop.Maintainability.AvoidExcessiveComplexity#4](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.AvoidExcessiveComplexity/vb/FxCop.Maintainability.AvoidExcessiveComplexity.vb#4)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1501: Evitar herança excessiva](../code-quality/ca1501-avoid-excessive-inheritance.md)

## <a name="see-also"></a>Consulte Também
 [Medindo complexidade e facilidade de manutenção do código gerenciado](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)
