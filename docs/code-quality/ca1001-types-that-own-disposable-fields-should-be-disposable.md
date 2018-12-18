---
title: 'CA1001: tipos que tenham campos descartáveis devem ser descartáveis'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1001
- TypesThatOwnDisposableFieldsShouldBeDisposable
helpviewer_keywords:
- CA1001
- TypesThatOwnDisposableFieldsShouldBeDisposable
ms.assetid: c85c126c-2b16-4505-940a-b5ddf873fb22
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: a73acee1c01aba7a638d27c0e772e4fbf5e19384
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45546923"
---
# <a name="ca1001-types-that-own-disposable-fields-should-be-disposable"></a>CA1001: tipos que tenham campos descartáveis devem ser descartáveis

|||
|-|-|
|NomeDoTipo|TypesThatOwnDisposableFieldsShouldBeDisposable|
|CheckId|CA1001|
|Categoria|Microsoft.Design|
|Alteração Significativa|Sem quebra - se o tipo não é visível fora do assembly.<br /><br /> Quebrando - se o tipo é visível fora do assembly.|

## <a name="cause"></a>Causa
 Uma classe declara e implementa um campo de instância que é um <xref:System.IDisposable?displayProperty=fullName> tipo e a classe não implementa <xref:System.IDisposable>.

## <a name="rule-description"></a>Descrição da regra
 Uma classe implementa o <xref:System.IDisposable> interface para descartar os recursos não gerenciados que ele possui. Um campo de instância que é um <xref:System.IDisposable> tipo indica se o campo tem um recurso não gerenciado. Uma classe que declara um <xref:System.IDisposable> campo indiretamente possui um recurso não gerenciado e deve implementar o <xref:System.IDisposable> interface. Se a classe possui diretamente quaisquer recursos não gerenciados, ele não deve implementar um finalizador.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, implemente <xref:System.IDisposable> e para o <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> chamada de método a <xref:System.IDisposable.Dispose%2A> método do campo.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma classe que viola a regra e uma classe que satisfaz a regra com a implementação de <xref:System.IDisposable>. A classe não implementa um finalizador porque a classe não possui diretamente quaisquer recursos não gerenciados.

 [!code-vb[FxCop.Design.DisposableFields#1](../code-quality/codesnippet/VisualBasic/ca1001-types-that-own-disposable-fields-should-be-disposable_1.vb)]
 [!code-csharp[FxCop.Design.DisposableFields#1](../code-quality/codesnippet/CSharp/ca1001-types-that-own-disposable-fields-should-be-disposable_1.cs)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2213: os campos descartáveis devem ser descartados](../code-quality/ca2213-disposable-fields-should-be-disposed.md)

 [CA2216: os tipos descartáveis devem declarar o finalizador](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

 [CA2215: métodos Dispose devem chamar o descarte da classe base](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)

 [CA1049: tipos que tenham recursos nativos devem ser descartáveis](../code-quality/ca1049-types-that-own-native-resources-should-be-disposable.md)