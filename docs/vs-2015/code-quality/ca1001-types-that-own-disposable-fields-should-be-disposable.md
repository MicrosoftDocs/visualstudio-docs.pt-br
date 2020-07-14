---
title: 'CA1001: tipos que possuem campos descartáveis devem ser descartáveis | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1001
- TypesThatOwnDisposableFieldsShouldBeDisposable
helpviewer_keywords:
- CA1001
- TypesThatOwnDisposableFieldsShouldBeDisposable
ms.assetid: c85c126c-2b16-4505-940a-b5ddf873fb22
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: dab4532f082bd81eaa7b812eb038c5957636d453
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548311"
---
# <a name="ca1001-types-that-own-disposable-fields-should-be-disposable"></a>CA1001: Tipos com campos descartáveis devem ser descartáveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|TypesThatOwnDisposableFieldsShouldBeDisposable|
|CheckId|CA1001|
|Categoria|Microsoft. Design|
|Alteração Significativa|Não separável – se o tipo não estiver visível fora do assembly.<br /><br /> Quebra-se o tipo é visível fora do assembly.|

## <a name="cause"></a>Causa
 Uma classe declara e implementa um campo de instância que é um <xref:System.IDisposable?displayProperty=fullName> tipo e a classe não implementa <xref:System.IDisposable> .

## <a name="rule-description"></a>Descrição da Regra
 Uma classe implementa a <xref:System.IDisposable> interface para descartar os recursos não gerenciados que ele possui. Um campo de instância que é um <xref:System.IDisposable> tipo indica que o campo possui um recurso não gerenciado. Uma classe que declara que um <xref:System.IDisposable> campo é indiretamente proprietário de um recurso não gerenciado e deve implementar a <xref:System.IDisposable> interface. Se a classe não possui diretamente nenhum recurso não gerenciado, ela não deve implementar um finalizador.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implemente <xref:System.IDisposable> e, a partir do <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> método, chame o <xref:System.IDisposable.Dispose%2A> método do campo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma classe que viola a regra e uma classe que cumpre a regra implementando <xref:System.IDisposable> . A classe não implementa um finalizador porque a classe não possui diretamente nenhum recurso não gerenciado.

 [!code-csharp[FxCop.Design.DisposableFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.DisposableFields/cs/FxCop.Design.DisposableFields.cs#1)]
 [!code-vb[FxCop.Design.DisposableFields#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.DisposableFields/vb/FxCop.Design.DisposableFields.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2213: Campos descartáveis devem ser descartados](../code-quality/ca2213-disposable-fields-should-be-disposed.md)

 [CA2216: Tipos descartáveis devem declarar o finalizador](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)

 [CA2215: Métodos Dispose devem chamar o descarte da classe base](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)

 [CA1049: Tipos com recursos nativos devem ser descartáveis](../code-quality/ca1049-types-that-own-native-resources-should-be-disposable.md)
