---
title: 'CA1049: tipos que tenham recursos nativos devem ser descartáveis'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1049
- TypesThatOwnNativeResourcesShouldBeDisposable
helpviewer_keywords:
- TypesThatOwnNativeResourcesShouldBeDisposable
- CA1049
ms.assetid: 084e587d-0e45-4092-b767-49eed30d6a35
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- cplusplus
ms.openlocfilehash: f9a2eeb032951df86d38075220c14fe98488edef
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45551984"
---
# <a name="ca1049-types-that-own-native-resources-should-be-disposable"></a>CA1049: tipos que tenham recursos nativos devem ser descartáveis

|||
|-|-|
|NomeDoTipo|TypesThatOwnNativeResourcesShouldBeDisposable|
|CheckId|CA1049|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa

Faz referência a um tipo de um <xref:System.IntPtr?displayProperty=fullName> campo, uma <xref:System.UIntPtr?displayProperty=fullName> campo, ou um <xref:System.Runtime.InteropServices.HandleRef?displayProperty=fullName> campo, mas não implementa <xref:System.IDisposable?displayProperty=fullName>.

## <a name="rule-description"></a>Descrição da regra

Esta regra pressupõe que <xref:System.IntPtr>, <xref:System.UIntPtr>, e <xref:System.Runtime.InteropServices.HandleRef> campos armazenam ponteiros para recursos não gerenciados. Os tipos que alocam recursos não gerenciados devem implementar <xref:System.IDisposable> para permitir que os chamadores liberem esses recursos sob demanda e reduzir os tempos de vida dos objetos que contêm os recursos.

O padrão de design recomendado para limpar recursos não gerenciados é fornecer implícito e um meio explícito para liberar esses recursos usando o <xref:System.Object.Finalize%2A?displayProperty=fullName> método e o <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> método, respectivamente. O coletor de lixo chama o <xref:System.Object.Finalize%2A> método de um objeto em algum momento indeterminado depois que o objeto é determinado como não é mais acessível. Depois de <xref:System.Object.Finalize%2A> é chamado, mais a coleta de lixo é necessário para liberar o objeto. O <xref:System.IDisposable.Dispose%2A> método permite que o chamador liberar recursos sob demanda, mais cedo do que os recursos seriam liberados se deixada para o coletor de lixo explicitamente. Depois que os recursos não gerenciados, ele limpa <xref:System.IDisposable.Dispose%2A> deve chamar o <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> método para permitir que o coletor de lixo Saiba que <xref:System.Object.Finalize%2A> não tem mais a ser chamado; isso elimina a necessidade para a coleta de lixo adicionais e reduz o tempo de vida do objeto.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, implementar <xref:System.IDisposable>.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra, se o tipo não faz referência a um recurso não gerenciado. Caso contrário, não suprima um aviso nessa regra porque falhar ao implementar <xref:System.IDisposable> pode fazer com que os recursos não gerenciados para se tornar indisponível ou subutilizados.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que implementa <xref:System.IDisposable> para limpar um recurso não gerenciado.

 [!code-csharp[FxCop.Design.UnmanagedResources#1](../code-quality/codesnippet/CSharp/ca1049-types-that-own-native-resources-should-be-disposable_1.cs)]
 [!code-vb[FxCop.Design.UnmanagedResources#1](../code-quality/codesnippet/VisualBasic/ca1049-types-that-own-native-resources-should-be-disposable_1.vb)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2115: chamar GC.KeepAlive durante o uso de recursos nativos](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md)

 [CA1816: chamar GC.SuppressFinalize corretamente](../code-quality/ca1816-call-gc-suppressfinalize-correctly.md)

 [CA2216: os tipos descartáveis devem declarar o finalizador](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

 [CA1001: tipos que têm campos descartáveis devem ser descartáveis](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md)

## <a name="see-also"></a>Consulte também

- [Limpando recursos não gerenciados](/dotnet/standard/garbage-collection/unmanaged)
- [Padrão de descarte](/dotnet/standard/design-guidelines/dispose-pattern)