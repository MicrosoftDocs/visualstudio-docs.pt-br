---
title: 'CA2213: os campos descartáveis devem ser descartados'
ms.date: 11/05/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DisposableFieldsShouldBeDisposed
- CA2213
helpviewer_keywords:
- CA2213
- DisposableFieldsShouldBeDisposed
ms.assetid: e99442c9-70e2-47f3-b61a-d8ac003bc6e5
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: be06c9bf38ec360cedc858d92a84b1f89c662856
ms.sourcegitcommit: bccb05b5b4e435f3c1f7c36ba342e7d4031eb398
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51220626"
---
# <a name="ca2213-disposable-fields-should-be-disposed"></a>CA2213: os campos descartáveis devem ser descartados

|||
|-|-|
|NomeDoTipo|DisposableFieldsShouldBeDisposed|
|CheckId|CA2213|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa

Um tipo que implementa <xref:System.IDisposable?displayProperty=fullName> declara campos que são de tipos que também implementam <xref:System.IDisposable>. O <xref:System.IDisposable.Dispose%2A> método do campo não é chamado pelo <xref:System.IDisposable.Dispose%2A> método do tipo declarativo.

## <a name="rule-description"></a>Descrição da regra

Um tipo é responsável pelo descarte de todos os seus recursos não gerenciados. Regra CA2213 verifica para ver se um tipo descartável (ou seja, uma que implementa <xref:System.IDisposable>) `T` declara um campo `F` que é uma instância de um tipo descartável `FT`. Para cada campo `F` que foi atribuído a um objeto criado localmente dentro de métodos ou inicializadores do tipo recipiente `T`, a regra tenta localizar uma chamada para `FT.Dispose`. A regra procura os métodos chamados pela `T.Dispose` e um nível inferior (ou seja, os métodos chamados pelos métodos chamados `FT.Dispose`).

> [!NOTE]
> CA2213 de regra é acionada somente para os campos que são atribuídos a um objeto descartável criado localmente em inicializadores e métodos do tipo recipiente. Se o objeto é criado ou atribuído fora do tipo `T`, a regra não é acionado. Isso reduz o ruído para casos em que o tipo recipiente não possui a responsabilidade para o descarte do objeto.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, chame <xref:System.IDisposable.Dispose%2A> nos campos que são de tipos que implementam <xref:System.IDisposable>.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

É seguro suprimir um aviso nessa regra, se você não é responsável para liberar os recursos mantidos pelo campo, ou se a chamada para <xref:System.IDisposable.Dispose%2A> ocorre em um nível mais profundo de chamada que as verificações de regra.

## <a name="example"></a>Exemplo

O trecho a seguir mostra um tipo `TypeA` que implementa <xref:System.IDisposable>.

[!code-csharp[FxCop.Usage.IDisposablePattern#1](../code-quality/codesnippet/CSharp/ca2213-disposable-fields-should-be-disposed_1.cs)]

O trecho a seguir mostra um tipo `TypeB` que viola a regra CA2213 ao declarar um campo `aFieldOfADisposableType` como um tipo descartável (`TypeA`) e não chamando <xref:System.IDisposable.Dispose%2A> no campo.

[!code-csharp[FxCop.Usage.IDisposableFields#1](../code-quality/codesnippet/CSharp/ca2213-disposable-fields-should-be-disposed_2.cs)]

## <a name="see-also"></a>Consulte também

- <xref:System.IDisposable?displayProperty=fullName>
- [Padrão de descarte](/dotnet/standard/design-guidelines/dispose-pattern)