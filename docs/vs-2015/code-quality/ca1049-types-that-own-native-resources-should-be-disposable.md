---
title: 'CA1049: Tipos que tenham recursos nativos devem ser descartáveis | Microsoft Docs'
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
- CA1049
- TypesThatOwnNativeResourcesShouldBeDisposable
helpviewer_keywords:
- TypesThatOwnNativeResourcesShouldBeDisposable
- CA1049
ms.assetid: 084e587d-0e45-4092-b767-49eed30d6a35
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: b99abcd66916568f125dc6d503a589ba0d17b35c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49921620"
---
# <a name="ca1049-types-that-own-native-resources-should-be-disposable"></a>CA1049: tipos que tenham recursos nativos devem ser descartáveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|TypesThatOwnNativeResourcesShouldBeDisposable|
|CheckId|CA1049|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Faz referência a um tipo de um <xref:System.IntPtr?displayProperty=fullName> campo, uma <xref:System.UIntPtr?displayProperty=fullName> campo, ou um <xref:System.Runtime.InteropServices.HandleRef?displayProperty=fullName> campo, mas não implementa <xref:System.IDisposable?displayProperty=fullName>.

## <a name="rule-description"></a>Descrição da Regra
 Esta regra pressupõe que <xref:System.IntPtr>, <xref:System.UIntPtr>, e <xref:System.Runtime.InteropServices.HandleRef> campos armazenam ponteiros para recursos não gerenciados. Os tipos que alocam recursos não gerenciados devem implementar <xref:System.IDisposable> para permitir que os chamadores liberem esses recursos sob demanda e reduzir os tempos de vida dos objetos que contêm os recursos.

 O padrão de design recomendado para limpar recursos não gerenciados é fornecer implícito e um meio explícito para liberar esses recursos usando o <xref:System.Object.Finalize%2A?displayProperty=fullName> método e o <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> método, respectivamente. O coletor de lixo chama o <xref:System.Object.Finalize%2A> método de um objeto em algum momento indeterminado depois que o objeto é determinado como não é mais acessível. Depois de <xref:System.Object.Finalize%2A> é chamado, mais a coleta de lixo é necessário para liberar o objeto. O <xref:System.IDisposable.Dispose%2A> método permite que o chamador liberar recursos sob demanda, mais cedo do que os recursos seriam liberados se deixada para o coletor de lixo explicitamente. Depois que os recursos não gerenciados, ele limpa <xref:System.IDisposable.Dispose%2A> deve chamar o <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName> método para permitir que o coletor de lixo Saiba que <xref:System.Object.Finalize%2A> não tem mais a ser chamado; isso elimina a necessidade para a coleta de lixo adicionais e reduz o tempo de vida do objeto.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implementar <xref:System.IDisposable>.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, se o tipo não faz referência a um recurso não gerenciado. Caso contrário, não suprima um aviso nessa regra porque falhar ao implementar <xref:System.IDisposable> pode fazer com que os recursos não gerenciados para se tornar indisponível ou subutilizados.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que implementa <xref:System.IDisposable> para limpar um recurso não gerenciado.

 [!code-csharp[FxCop.Design.UnmanagedResources#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.UnmanagedResources/cs/FxCop.Design.UnmanagedResources.cs#1)]
 [!code-vb[FxCop.Design.UnmanagedResources#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.UnmanagedResources/vb/FxCop.Design.UnmanagedResources.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2115: chamar GC.KeepAlive durante o uso de recursos nativos](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md)

 [CA1816: chamar GC.SuppressFinalize corretamente](../code-quality/ca1816-call-gc-suppressfinalize-correctly.md)

 [CA2216: os tipos descartáveis devem declarar o finalizador](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

 [CA1001: tipos que têm campos descartáveis devem ser descartáveis](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md)

## <a name="see-also"></a>Consulte também
  [Padrão de descarte](http://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)



