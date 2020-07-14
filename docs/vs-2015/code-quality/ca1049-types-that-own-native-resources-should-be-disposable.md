---
title: 'CA1049: tipos que possuem recursos nativos devem ser descartáveis | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1049
- TypesThatOwnNativeResourcesShouldBeDisposable
helpviewer_keywords:
- TypesThatOwnNativeResourcesShouldBeDisposable
- CA1049
ms.assetid: 084e587d-0e45-4092-b767-49eed30d6a35
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 49c56b98e3be01675c2c21cd11c2961dd75f4877
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546803"
---
# <a name="ca1049-types-that-own-native-resources-should-be-disposable"></a>CA1049: Tipos com recursos nativos devem ser descartáveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|TypesThatOwnNativeResourcesShouldBeDisposable|
|CheckId|CA1049|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo referencia um <xref:System.IntPtr?displayProperty=fullName> campo, um <xref:System.UIntPtr?displayProperty=fullName> campo ou um <xref:System.Runtime.InteropServices.HandleRef?displayProperty=fullName> campo, mas não implementa <xref:System.IDisposable?displayProperty=fullName> .

## <a name="rule-description"></a>Descrição da Regra
 Essa regra pressupõe que <xref:System.IntPtr> os <xref:System.UIntPtr> campos, e <xref:System.Runtime.InteropServices.HandleRef> armazenam ponteiros para recursos não gerenciados. Tipos que alocam recursos não gerenciados devem <xref:System.IDisposable> ser implementados para permitir que os chamadores liberem esses recursos sob demanda e reduzam os tempos de vida dos objetos que contêm os recursos.

 O padrão de design recomendado para limpar recursos não gerenciados é fornecer um meio implícito e explícito para liberar esses recursos usando o <xref:System.Object.Finalize%2A?displayProperty=fullName> método e o <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> método, respectivamente. O coletor de lixo chama o <xref:System.Object.Finalize%2A> método de um objeto em algum momento indeterminado depois que o objeto não é mais acessível. Depois <xref:System.Object.Finalize%2A> que é chamado, uma coleta de lixo adicional é necessária para liberar o objeto. O <xref:System.IDisposable.Dispose%2A> método permite que o chamador libere explicitamente os recursos sob demanda, antes que os recursos sejam liberados se deixados para o coletor de lixo. Depois de limpar os recursos não gerenciados, o <xref:System.IDisposable.Dispose%2A> deve chamar o <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> método para permitir que o coletor de lixo saiba que <xref:System.Object.Finalize%2A> não precisa mais ser chamado; isso elimina a necessidade de coleta de lixo adicional e reduz o tempo de vida do objeto.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implemente <xref:System.IDisposable> .

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se o tipo não fizer referência a um recurso não gerenciado. Caso contrário, não omita um aviso dessa regra porque a falha na implementação <xref:System.IDisposable> pode fazer com que os recursos não gerenciados se tornem indisponíveis ou subutilizados.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que implementa <xref:System.IDisposable> para limpar um recurso não gerenciado.

 [!code-csharp[FxCop.Design.UnmanagedResources#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.UnmanagedResources/cs/FxCop.Design.UnmanagedResources.cs#1)]
 [!code-vb[FxCop.Design.UnmanagedResources#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.UnmanagedResources/vb/FxCop.Design.UnmanagedResources.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2115: Chamar GC.KeepAlive ao usar recursos nativos](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md)

 [CA1816: Chamar GC.SuppressFinalize corretamente](../code-quality/ca1816-call-gc-suppressfinalize-correctly.md)

 [CA2216: Tipos descartáveis devem declarar o finalizador](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

 [CA1001: Tipos com campos descartáveis devem ser descartáveis](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md)

## <a name="see-also"></a>Consulte Também
  [Padrão de descarte](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
