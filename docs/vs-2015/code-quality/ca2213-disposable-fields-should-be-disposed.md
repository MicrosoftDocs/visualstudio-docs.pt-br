---
title: 'CA2213: Os campos descartáveis devem ser descartados | Microsoft Docs'
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
- DisposableFieldsShouldBeDisposed
- CA2213
helpviewer_keywords:
- CA2213
- DisposableFieldsShouldBeDisposed
ms.assetid: e99442c9-70e2-47f3-b61a-d8ac003bc6e5
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: b4e59dd35ab1f787dcaada5448443e35efc1f6c9
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49910480"
---
# <a name="ca2213-disposable-fields-should-be-disposed"></a>CA2213: os campos descartáveis devem ser descartados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|DisposableFieldsShouldBeDisposed|
|CheckId|CA2213|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Um tipo que implementa <xref:System.IDisposable?displayProperty=fullName> declara campos que são de tipos que também implementam <xref:System.IDisposable>. O <xref:System.IDisposable.Dispose%2A> método do campo não é chamado pelo <xref:System.IDisposable.Dispose%2A> método do tipo declarativo.

## <a name="rule-description"></a>Descrição da Regra
 Um tipo é responsável para o descarte de todos os seus recursos não gerenciados; Isso é realizado pela implementação <xref:System.IDisposable>. Esta regra verifica para ver se um tipo descartável `T` declara um campo `F` que é uma instância de um tipo descartável `FT`. Para cada campo `F`, a regra tenta localizar uma chamada para `FT.Dispose`. A regra procura os métodos chamados pela `T.Dispose`e um nível inferior (os métodos chamados pelos métodos chamados `FT.Dispose`).

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, chame <xref:System.IDisposable.Dispose%2A> nos campos que são de tipos que implementam <xref:System.IDisposable> se você é responsável por alocar e liberar os recursos não gerenciados mantidos pelo campo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, se você não é responsável por liberar os recursos mantidos pelo campo, ou se a chamada para <xref:System.IDisposable.Dispose%2A> ocorre em um nível mais profundo de chamada que as verificações de regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo `TypeA` que implementa <xref:System.IDisposable> (`FT` na discussão previosu).

 [!code-csharp[FxCop.Usage.IDisposablePattern#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposablePattern/cs/FxCop.Usage.IDisposablePattern.cs#1)]

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo `TypeB` que viola essa regra ao declarar um campo `aFieldOfADisposableType` (`F` na discussão anterior) como um tipo descartável (`TypeA`) e não chamando <xref:System.IDisposable.Dispose%2A> no campo. `TypeB` corresponde ao `T` na discussão anterior.

 [!code-csharp[FxCop.Usage.IDisposableFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.IDisposableFields/cs/FxCop.Usage.IDisposableFields.cs#1)]

## <a name="see-also"></a>Consulte também
 <xref:System.IDisposable?displayProperty=fullName> [Padrão de descarte](http://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)



