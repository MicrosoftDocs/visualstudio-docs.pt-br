---
title: 'CA1816: chamar GC.SuppressFinalize corretamente'
ms.date: 06/30/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1816
- DisposeMethodsShouldCallSuppressFinalize
helpviewer_keywords:
- DisposeMethodsShouldCallSuppressFinalize
- CA1816
ms.assetid: 47915fbb-103f-4333-b157-1da16bf49660
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 5c874aac5d84d45159ef7d169ab2749269fa0905
ms.sourcegitcommit: f37affbc1b885dfe246d4b2c295a6538b383a0ca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37174225"
---
# <a name="ca1816-call-gcsuppressfinalize-correctly"></a>CA1816: chamar GC.SuppressFinalize corretamente

|||
|-|-|
|NomeDoTipo|CallGCSuppressFinalizeCorrectly|
|CheckId|CA1816|
|Categoria|Microsoft. Uso|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa

As violações dessa regra podem ser causadas por:

- Um método que é uma implementação de <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> e não chama <xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>.

- Um método que não é uma implementação de <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> e chama <xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>.

- Um método que chama <xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType> e passa algo diferente de [this (c#)](/dotnet/csharp/language-reference/keywords/this) ou [Me (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass#me).

## <a name="rule-description"></a>Descrição da regra

O <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> método permite que os usuários liberar os recursos a qualquer momento antes do objeto ficarem disponíveis para a coleta de lixo. Se o <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> método é chamado, ele libera os recursos do objeto. Isso torna a finalização desnecessária. <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> deve chamar <xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType> para que o coletor de lixo não chamar o finalizador do objeto.

Para impedir que os tipos derivados com finalizadores tenham de reimplementar <xref:System.IDisposable> e para chamá-lo, sem lacre tipos sem os finalizadores devem chamar ainda <xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra:

- Se o método é uma implementação de <xref:System.IDisposable.Dispose%2A>, adicione uma chamada para <xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>.

- Se o método não é uma implementação de <xref:System.IDisposable.Dispose%2A>, ou remova a chamada para <xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType> ou movê-lo para o tipo <xref:System.IDisposable.Dispose%2A> implementação.

- Alterar todas as chamadas para <xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType> passar [this (c#)](/dotnet/csharp/language-reference/keywords/this) ou [Me (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass#me).

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Suprimir um aviso nessa regra somente se você estiver usando deliberadamente <xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType> para controlar o tempo de vida de outros objetos. Não suprimir um aviso nessa regra, se uma implementação de <xref:System.IDisposable.Dispose%2A> não chama <xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>. Nessa situação, falhar suprimir a finalização degrada o desempenho e não oferece nenhum benefício.

## <a name="example-that-violates-ca1816"></a>Exemplo que viola CA1816

Este código mostra um método que chama <xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType>, mas não passa [this (c#)](/dotnet/csharp/language-reference/keywords/this) ou [Me (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass#me). Como resultado, esse código viola a regra CA1816.

[!code-vb[FxCop.Usage.CallGCSuppressFinalizeCorrectly#1](../code-quality/codesnippet/VisualBasic/ca1816-call-gc-suppressfinalize-correctly_1.vb)]
[!code-csharp[FxCop.Usage.CallGCSuppressFinalizeCorrectly#1](../code-quality/codesnippet/CSharp/ca1816-call-gc-suppressfinalize-correctly_1.cs)]

## <a name="example-that-satisfies-ca1816"></a>Exemplo que satisfaça CA1816

Este exemplo mostra um método que corretamente chamadas <xref:System.GC.SuppressFinalize%2A?displayProperty=nameWithType> , passando [this (c#)](/dotnet/csharp/language-reference/keywords/this) ou [Me (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass#me).

[!code-vb[FxCop.Usage.CallGCSuppressFinalizeCorrectly2#1](../code-quality/codesnippet/VisualBasic/ca1816-call-gc-suppressfinalize-correctly_2.vb)]
[!code-csharp[FxCop.Usage.CallGCSuppressFinalizeCorrectly2#1](../code-quality/codesnippet/CSharp/ca1816-call-gc-suppressfinalize-correctly_2.cs)]

## <a name="related-rules"></a>Regras relacionadas

- [CA2215: métodos Dispose devem chamar o descarte da classe base](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)
- [CA2216: os tipos descartáveis devem declarar o finalizador](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

## <a name="see-also"></a>Consulte também

- [Padrão de descarte](/dotnet/standard/design-guidelines/dispose-pattern)