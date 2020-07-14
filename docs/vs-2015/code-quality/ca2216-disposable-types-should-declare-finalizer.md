---
title: 'CA2216: tipos descartáveis devem declarar finalizador | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DisposableTypesShouldDeclareFinalizer
- CA2216
helpviewer_keywords:
- CA2216
- DisposableTypesShouldDeclareFinalizer
ms.assetid: 0cabcc5e-b526-452b-8c2a-0cbe3b93c0ef
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5268cb90544088742c6fda7c751bab943503cacc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534466"
---
# <a name="ca2216-disposable-types-should-declare-finalizer"></a>CA2216: Tipos descartáveis devem declarar o finalizador
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DisposableTypesShouldDeclareFinalizer|
|CheckId|CA2216|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo que implementa <xref:System.IDisposable?displayProperty=fullName> e tem campos que sugerem o uso de recursos não gerenciados, não implementa um finalizador conforme descrito pelo <xref:System.Object.Finalize%2A?displayProperty=fullName> .

## <a name="rule-description"></a>Descrição da Regra
 Uma violação dessa regra será relatada se o tipo descartável contiver campos dos seguintes tipos:

- <xref:System.IntPtr?displayProperty=fullName>

- <xref:System.UIntPtr?displayProperty=fullName>

- <xref:System.Runtime.InteropServices.HandleRef?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implemente um finalizador que chama seu <xref:System.IDisposable.Dispose%2A> método.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se o tipo não <xref:System.IDisposable> for implementado com a finalidade de liberar recursos não gerenciados.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola essa regra.

 [!code-csharp[FxCop.Usage.DisposeNoFinalize#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.DisposeNoFinalize/cs/FxCop.Usage.DisposeNoFinalize.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2115: Chamar GC.KeepAlive ao usar recursos nativos](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md)

 [CA1816: Chamar GC.SuppressFinalize corretamente](../code-quality/ca1816-call-gc-suppressfinalize-correctly.md)

 [CA1049: Tipos com recursos nativos devem ser descartáveis](../code-quality/ca1049-types-that-own-native-resources-should-be-disposable.md)

## <a name="see-also"></a>Consulte Também
 <xref:System.IDisposable?displayProperty=fullName> <xref:System.IntPtr?displayProperty=fullName>
 <xref:System.Runtime.InteropServices.HandleRef?displayProperty=fullName>
 <xref:System.UIntPtr?displayProperty=fullName>
 <xref:System.Object.Finalize%2A?displayProperty=fullName>
 [Padrão de descarte](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
