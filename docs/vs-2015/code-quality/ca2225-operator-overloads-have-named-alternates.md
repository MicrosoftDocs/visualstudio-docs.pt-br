---
title: 'CA2225: Sobrecargas de operador possuem alternativas nomeadas | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- OperatorOverloadsHaveNamedAlternates
- CA2225
helpviewer_keywords:
- OperatorOverloadsHaveNamedAlternates
- CA2225
ms.assetid: af8f7ab1-63ad-4861-afb9-b7a7a2be15e1
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: aa90a1e97b563ef549cb3f628fcf9130a364c50a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201612"
---
# <a name="ca2225-operator-overloads-have-named-alternates"></a>CA2225: Sobrecargas de operador têm alternativas nomeadas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|OperatorOverloadsHaveNamedAlternates|
|CheckId|CA2225|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Uma sobrecarga de operador foi detectada, e o método alternativo nomeado esperado não foi encontrado.

## <a name="rule-description"></a>Descrição da Regra
 Sobrecarga de operador permite o uso de símbolos para representar os cálculos para um tipo. Por exemplo, um tipo que sobrecarrega o símbolo de adição (+) para adição normalmente teria um membro alternativo nomeado 'Adicionar'. O membro alternativo nomeado fornece acesso para a mesma funcionalidade que o operador e é fornecido para os desenvolvedores que programem em linguagens que não dão suporte a operadores sobrecarregados.

 Esta regra examina os operadores listados na tabela a seguir.

|C#|Visual Basic|C++|Nome alternativo|
|---------|------------------|-----------|--------------------|
|+ (binário)|+|+ (binário)|Adicionar|
|+=|+=|+=|Adicionar|
|&|e|&|BitwiseAnd|
|&=|And=|&=|BitwiseAnd|
|&#124;|Ou|&#124;|BitwiseOr|
|&#124;=|Ou =|&#124;=|BitwiseOr|
|--|N/D|--|Decremento|
|/|/|/|Divisão|
|/=|/=|/=|Divisão|
|==|=|==|Igual a|
|^|Xor|^|Xor|
|^=|Xor=|^=|Xor|
|>|>|>|Comparar|
|>=|>=|>=|Comparar|
|++|N/D|++|Incremento|
|<>|!=|Igual a|
|<<|<<|<<|LeftShift|
|<<=|<<=|<<=|LeftShift|
|<|<|<|Comparar|
|<=|<=|\<=|Comparar|
|&&|N/D|&&|LogicalAnd|
|&#124;&#124;|N/D|&#124;&#124;|LogicalOr|
|!|N/D|!|LogicalNot|
|%|Mod|%|Mod ou restante|
|%=|N/D|%=|Mod|
|* (binário)|*|*|Multiplicar|
|*=|N/D|*=|Multiplicar|
|~|não|~|OnesComplement|
|>>|>>|>>|SHIFT direita|
=|N/D|>>=|SHIFT direita|
|-(binário)|-(binário)|-(binário)|Subtração|
|-=|N/D|-=|Subtração|
|true|IsTrue|N/D|IsTrue (propriedade)|
|-(unário)|N/D|-|Negar|
|+ (unário)|N/D|+|sinal de adição|
|false|IsFalse|False|IsTrue (propriedade)|

 N/d = = não pode ser sobrecarregado no idioma selecionado.

 A regra também verifica se há operadores de conversão explícita e implícita em um tipo (`SomeType`) através da verificação de métodos chamados `ToSomeType` e `FromSomeType`.

 No c#, quando um operador binário está sobrecarregado, o operador de atribuição correspondente, se houver, também estará implicitamente sobrecarregado.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implemente o método alternativo para o operador; Nomeie-o usando o nome alternativo recomendado.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra, se você estiver implementando uma biblioteca compartilhada. Aplicativos podem ignorar um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir define uma estrutura que viola essa regra. Para corrigir o exemplo, adicione um público `Add(int x, int y)` método à estrutura.

 [!code-csharp[FxCop.Usage.OperatorOverloadsHaveNamedAlternates#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperatorOverloadsHaveNamedAlternates/cs/FxCop.Usage.OperatorOverloadsHaveNamedAlternates.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1046: Não sobrecarregar operador equals em tipos de referência](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)

 [CA2226: Os operadores devem ter sobrecargas simétricas](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)

 [CA2224: Substituir equals ao sobrecarregar operador equals](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)

 [CA2218: Substituir GetHashCode em igualdades de substituição](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)

 [CA2231: o operador de sobrecarga é igual ao substituir ValueType.Equals](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)
