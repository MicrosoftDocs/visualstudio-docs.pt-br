---
title: 'CA1036: substituir métodos em tipos comparáveis'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1036
- OverrideMethodsOnComparableTypes
helpviewer_keywords:
- OverrideMethodsOnComparableTypes
- CA1036
ms.assetid: 2329f844-4cb8-426d-bee2-cd065d1346d0
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ed69ba759d63ba27114bc097ac1fd9ccbe424edd
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45547731"
---
# <a name="ca1036-override-methods-on-comparable-types"></a>CA1036: substituir métodos em tipos comparáveis

|||
|-|-|
|NomeDoTipo|OverrideMethodsOnComparableTypes|
|CheckId|CA1036|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um tipo público ou protegido implementa o <xref:System.IComparable?displayProperty=fullName> da interface e não substitui <xref:System.Object.Equals%2A?displayProperty=fullName> ou sobrecarrega o operador de idioma específico para igualdade, desigualdade, menor-que ou maior-que. A regra não relata uma violação se o tipo herdar apenas uma implementação da interface.

## <a name="rule-description"></a>Descrição da regra

Tipos que definem uma ordem de classificação personalizada é implementar o <xref:System.IComparable> interface. O <xref:System.IComparable.CompareTo%2A> método retorna um valor inteiro que indica a ordem de classificação correta para que duas instâncias do tipo. Essa regra identifica os tipos que definir uma ordem de classificação. Definir uma ordem de classificação implica que o significado comum de igualdade, desigualdade, menor-que e maior-que não se aplicam. Quando você fornece uma implementação de <xref:System.IComparable>, você geralmente deve também substituir <xref:System.Object.Equals%2A> para que ele retorna valores que são consistentes com <xref:System.IComparable.CompareTo%2A>. Se você substituir <xref:System.Object.Equals%2A> e está codificando em uma linguagem que dá suporte a sobrecargas de operador, você também deve fornecer os operadores que são consistentes com <xref:System.Object.Equals%2A>.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, substituir <xref:System.Object.Equals%2A>. Se sua linguagem de programação dá suporte à sobrecarga de operador, fornece os seguintes operadores:

- op_Equality

- op_Inequality

- op_LessThan

- op_GreaterThan

No c#, os tokens que são usados para representar esses operadores são:

```csharp
==
!=
<
>
```

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso de regra CA1036 quando a violação é causada por falta de operadores e sua linguagem de programação não oferece suporte a sobrecarga de operador, como é o caso com o Visual Basic. Também é seguro suprimir um aviso para essa regra quando ela é acionada em operadores de igualdade diferente de op_Equality se você determinar que os operadores a implementação não faz sentido no contexto do aplicativo. No entanto, você deve sempre sobre op_Equality e o operador = = se substitui Object. Equals.

## <a name="example"></a>Exemplo
 O exemplo a seguir contém um tipo que implementa corretamente <xref:System.IComparable>. Comentários de código identificam os métodos que atendem a várias regras que estão relacionadas ao <xref:System.Object.Equals%2A> e o <xref:System.IComparable> interface.

 [!code-csharp[FxCop.Design.IComparable#1](../code-quality/codesnippet/CSharp/ca1036-override-methods-on-comparable-types_1.cs)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir testa o comportamento do <xref:System.IComparable> implementação mostrado anteriormente.

 [!code-csharp[FxCop.Design.TestIComparable#1](../code-quality/codesnippet/CSharp/ca1036-override-methods-on-comparable-types_2.cs)]

## <a name="see-also"></a>Consulte também

- <xref:System.IComparable?displayProperty=fullName>
- <xref:System.Object.Equals%2A?displayProperty=fullName>
- [Operadores de igualdade](/dotnet/standard/design-guidelines/equality-operators)