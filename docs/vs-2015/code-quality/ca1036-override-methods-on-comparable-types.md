---
title: 'CA1036: Substituir métodos em tipos comparáveis | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- CA1036
- OverrideMethodsOnComparableTypes
helpviewer_keywords:
- OverrideMethodsOnComparableTypes
- CA1036
ms.assetid: 2329f844-4cb8-426d-bee2-cd065d1346d0
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 67fa52a674b9e3d77d7e3eed7493bf28c1b2514d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49948754"
---
# <a name="ca1036-override-methods-on-comparable-types"></a>CA1036: substituir métodos em tipos comparáveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|OverrideMethodsOnComparableTypes|
|CheckId|CA1036|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um tipo público ou protegido implementa o <xref:System.IComparable?displayProperty=fullName> da interface e não substitui <xref:System.Object.Equals%2A?displayProperty=fullName> ou não sobrecarrega o operador específico da linguagem para igualdade, desigualdade, menor ou maior que. A regra não relata uma violação se o tipo herdar apenas uma implementação da interface.

## <a name="rule-description"></a>Descrição da Regra
 Tipos que definem uma ordem de classificação personalizada é implementar o <xref:System.IComparable> interface. O <xref:System.IComparable.CompareTo%2A> método retorna um valor inteiro que indica a ordem de classificação correta para que duas instâncias do tipo. Essa regra identifica os tipos que definir uma ordem de classificação; Isso implica que o significado comum de igualdade, desigualdade, menor e maior que não se aplicam. Quando você fornece uma implementação de <xref:System.IComparable>, você geralmente deve também substituir <xref:System.Object.Equals%2A> para que ele retorna valores que são consistentes com <xref:System.IComparable.CompareTo%2A>. Se você substituir <xref:System.Object.Equals%2A> e está codificando em uma linguagem que dá suporte a sobrecargas de operador, você também deve fornecer os operadores que são consistentes com <xref:System.Object.Equals%2A>.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, substituir <xref:System.Object.Equals%2A>. Se sua linguagem de programação dá suporte à sobrecarga de operador, fornece os seguintes operadores:

- op_Equality

- op_Inequality

- op_LessThan

- op_GreaterThan

  No c#, os tokens que são usados para representar esses operadores são os seguintes: = =,! =, \<, e >.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, quando a violação é causada por falta de operadores e sua linguagem de programação não oferece suporte a sobrecarga de operador, como é o caso com o Visual Basic .NET. Também é seguro suprimir um aviso para essa regra quando ela é acionada em operadores de igualdade diferente de op_Equality se você determinar que os operadores a implementação não faz sentido no contexto do aplicativo. No entanto, você deve sempre sobre op_Equality e o operador = = se substitui Object. Equals.

## <a name="example"></a>Exemplo
 O exemplo a seguir contém um tipo que implementa corretamente <xref:System.IComparable>. Comentários de código identificam os métodos que atendem a várias regras que estão relacionadas ao <xref:System.Object.Equals%2A> e o <xref:System.IComparable> interface.

 [!code-csharp[FxCop.Design.IComparable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.IComparable/cs/FxCop.Design.IComparable.cs#1)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir testa o comportamento do <xref:System.IComparable> implementação mostrado anteriormente.

 [!code-csharp[FxCop.Design.TestIComparable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestIComparable/cs/FxCop.Design.TestIComparable.cs#1)]

## <a name="see-also"></a>Consulte também
 <xref:System.IComparable?displayProperty=fullName> <xref:System.Object.Equals%2A?displayProperty=fullName>
 [Operadores de igualdade](http://msdn.microsoft.com/library/bc496a91-fefb-4ce0-ab4c-61f09964119a)



