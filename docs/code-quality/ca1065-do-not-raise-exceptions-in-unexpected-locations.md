---
title: 'CA1065: não acione exceções em locais inesperados'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1065
- DoNotRaiseExceptionsInUnexpectedLocations
helpviewer_keywords:
- DoNotRaiseExceptionsInUnexpectedLocations
- CA1065
ms.assetid: 4e1bade4-4ca2-4219-abc3-c7b2d741e157
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4999770367ad7b170398333cf7c7cf2cb9d1c407
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45546688"
---
# <a name="ca1065-do-not-raise-exceptions-in-unexpected-locations"></a>CA1065: não acione exceções em locais inesperados

|||
|-|-|
|NomeDoTipo|DoNotRaiseExceptionsInUnexpectedLocations|
|CheckId|CA1065|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa

Um método que não deve acionar exceções aciona uma exceção.

## <a name="rule-description"></a>Descrição da regra

Métodos que não são esperados para lançar exceções podem ser categorizados da seguinte maneira:

- Métodos Get de propriedade

- Métodos de acessador de evento

- Métodos Equals

- Métodos GetHashCode

- Métodos ToString

- Construtores estáticos

- Finalizadores

- Métodos de descarte

- Operadores de igualdade

- Operadores de conversão implícita

As seções a seguir discutem esses tipos de método.

### <a name="property-get-methods"></a>Métodos Get de propriedade

Propriedades são campos basicamente inteligentes. Portanto, eles devem se comportar como um campo tanto quanto possível. Campos não geram exceções e, tampouco em Propriedades. Se você tiver uma propriedade que gera uma exceção, considere fazer a ele um método.

As seguintes exceções podem ser geradas de um método get de propriedade:

- <xref:System.InvalidOperationException?displayProperty=fullName> e todos os derivados (incluindo <xref:System.ObjectDisposedException?displayProperty=fullName>)

- <xref:System.NotSupportedException?displayProperty=fullName> e todos os derivados

- <xref:System.ArgumentException?displayProperty=fullName> (apenas no get indexada)

- <xref:System.Collections.Generic.KeyNotFoundException> (apenas no get indexada)

### <a name="event-accessor-methods"></a>Métodos de acessador de evento

Acessadores de evento devem ser operações simples que não lançam exceções. Um evento não deve lançar uma exceção ao tentar adicionar ou remover um manipulador de eventos.

As exceções a seguir podem ser lançadas de um acessador de evento:

- <xref:System.InvalidOperationException?displayProperty=fullName> e todos os derivados (incluindo <xref:System.ObjectDisposedException?displayProperty=fullName>)

- <xref:System.NotSupportedException?displayProperty=fullName> e todos os derivados

- <xref:System.ArgumentException> e derivados

### <a name="equals-methods"></a>Métodos Equals

O seguinte **é igual a** métodos não devem lançar exceções:

- <xref:System.Object.Equals%2A?displayProperty=fullName>

- <xref:System.IEquatable%601.Equals%2A>

Uma **é igual a** método deverá retornar `true` ou `false` em vez de gerar uma exceção. Por exemplo, se for igual a é passado a dois tipos incompatíveis ele deve apenas retornar `false` em vez de gerar um <xref:System.ArgumentException>.

### <a name="gethashcode-methods"></a>Métodos GetHashCode

O seguinte **GetHashCode** métodos normalmente não devem lançar exceções:

- <xref:System.Object.GetHashCode%2A>

- <xref:System.Collections.IEqualityComparer.GetHashCode%2A>

**GetHashCode** sempre deve retornar um valor. Caso contrário, você poderá perder itens na tabela de hash.

As versões do **GetHashCode** que aceitam um argumento pode lançar um <xref:System.ArgumentException>. No entanto, **Object.GetHashCode** nunca deve lançar uma exceção.

### <a name="tostring-methods"></a>Métodos ToString

O depurador usa <xref:System.Object.ToString%2A?displayProperty=fullName> para ajudar a exibir informações sobre objetos no formato de cadeia de caracteres. Portanto, **ToString** não deve alterar o estado de um objeto, e ele não deve lançar exceções.

### <a name="static-constructors"></a>Construtores estáticos

Lançar exceções a partir de um construtor estático faz com que o tipo a ser inutilizável no domínio do aplicativo atual. Você deve ter um bom motivo (por exemplo, um problema de segurança) para gerar uma exceção de um construtor estático.

### <a name="finalizers"></a>Finalizadores

Gerar uma exceção de um finalizador faz com que o CLR para falhar rapidamente, qual encerrará o processo. Portanto, gerar exceções em um finalizador deve sempre ser evitada.

### <a name="dispose-methods"></a>Métodos de descarte

Um <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> método não deve lançar uma exceção. Dispose muitas vezes é chamado como parte da lógica de limpeza em um `finally` cláusula. Portanto, explicitamente, lançar uma exceção de Dispose força o usuário adicione dentro de tratamento de exceções de `finally` cláusula.

O **Dispose (False)** caminho de código nunca deve lançar exceções, como descarte quase sempre é chamado de um finalizador.

### <a name="equality-operators--"></a>Operadores de igualdade (= =,! =)

Assim como os métodos Equals, operadores de igualdade devem retornar um `true` ou `false`e não deve lançar exceções.

### <a name="implicit-cast-operators"></a>Operadores de conversão implícita

Como o usuário é muitas vezes ciente de que um operador de conversão implícita foi chamado, uma exceção lançada pelo operador de conversão implícita é inesperada. Portanto, nenhuma exceção será lançada de operadores de conversão implícita.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para getters de propriedade a alterar a lógica para que ele não tem mais lançar uma exceção ou alterar a propriedade em um método.

Para todos os outros tipos de método listados anteriormente, altere a lógica para que ele não deve lançar uma exceção.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Se a violação foi causada por uma declaração de exceção em vez de uma exceção lançada, é seguro suprimir um aviso nessa regra.

## <a name="related-rules"></a>Regras relacionadas

- [CA2219: não acionar exceções em cláusulas de exceção](../code-quality/ca2219-do-not-raise-exceptions-in-exception-clauses.md)

## <a name="see-also"></a>Consulte também

- [Avisos de design](../code-quality/design-warnings.md)