---
title: 'CA1036: substituir métodos em tipos comparáveis | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1036
- OverrideMethodsOnComparableTypes
helpviewer_keywords:
- OverrideMethodsOnComparableTypes
- CA1036
ms.assetid: 2329f844-4cb8-426d-bee2-cd065d1346d0
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 52247c9175b22d3d96aa91557ee133f37c55e789
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546595"
---
# <a name="ca1036-override-methods-on-comparable-types"></a>CA1036: Substituir métodos em tipos comparáveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|OverrideMethodsOnComparableTypes|
|CheckId|CA1036|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo público ou protegido implementa a <xref:System.IComparable?displayProperty=fullName> interface e não substitui <xref:System.Object.Equals%2A?displayProperty=fullName> ou não sobrecarrega o operador específico do idioma para igualdade, desigualdade, menor que ou maior que. A regra não relatará uma violação se o tipo herdar apenas uma implementação da interface.

## <a name="rule-description"></a>Descrição da Regra
 Tipos que definem uma ordem de classificação personalizada implementam a <xref:System.IComparable> interface. O <xref:System.IComparable.CompareTo%2A> método retorna um valor inteiro que indica a ordem de classificação correta para duas instâncias do tipo. Essa regra identifica os tipos que definem uma ordem de classificação; Isso implica que o significado comum de igualdade, desigualdade, menor que e maior que não se aplica. Quando você fornece uma implementação do <xref:System.IComparable> , normalmente também deve substituir <xref:System.Object.Equals%2A> para que ele retorne valores consistentes com o <xref:System.IComparable.CompareTo%2A> . Se você substituir <xref:System.Object.Equals%2A> e estiver codificando em uma linguagem que dá suporte a sobrecargas de operador, também deverá fornecer operadores que são consistentes com o <xref:System.Object.Equals%2A> .

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, substitua <xref:System.Object.Equals%2A> . Se sua linguagem de programação der suporte à sobrecarga de operador, forneça os seguintes operadores:

- op_Equality

- op_Inequality

- op_LessThan

- op_GreaterThan

  No C#, os tokens que são usados para representar esses operadores são os seguintes: = =,! =, \<, and > .

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra quando a violação é causada por operadores ausentes e sua linguagem de programação não dá suporte à sobrecarga de operador, como é o caso com Visual Basic .NET. Também é seguro suprimir um aviso para essa regra quando ele é acionado em operadores de igualdade diferentes de op_Equality se você determinar que a implementação dos operadores não faz sentido no contexto do aplicativo. No entanto, você deve sempre ultrapassar op_Equality e o operador = = se substituir Object. Equals.

## <a name="example"></a>Exemplo
 O exemplo a seguir contém um tipo que implementa corretamente <xref:System.IComparable> . Os comentários de código identificam os métodos que atendem a várias regras relacionadas ao <xref:System.Object.Equals%2A> e à <xref:System.IComparable> interface.

 [!code-csharp[FxCop.Design.IComparable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IComparable/cs/FxCop.Design.IComparable.cs#1)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir testa o comportamento da <xref:System.IComparable> implementação que foi mostrada anteriormente.

 [!code-csharp[FxCop.Design.TestIComparable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestIComparable/cs/FxCop.Design.TestIComparable.cs#1)]

## <a name="see-also"></a>Consulte Também
 <xref:System.IComparable?displayProperty=fullName> <xref:System.Object.Equals%2A?displayProperty=fullName>
 [Operadores de igualdade](https://msdn.microsoft.com/library/bc496a91-fefb-4ce0-ab4c-61f09964119a)
