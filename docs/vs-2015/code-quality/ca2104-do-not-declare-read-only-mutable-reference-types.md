---
title: 'CA2104: Não declarar tipos de referência mutáveis somente leitura | Microsoft Docs'
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
- DoNotDeclareReadOnlyMutableReferenceTypes
- CA2104
helpviewer_keywords:
- CA2104
- DoNotDeclareReadOnlyMutableReferenceTypes
ms.assetid: 81b83ee5-4db5-4be0-9f8d-90b53894ec3b
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 66248e6920c879932204ddb25a40820720adfd84
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49877433"
---
# <a name="ca2104-do-not-declare-read-only-mutable-reference-types"></a>CA2104: não declarar tipos de referência mutáveis somente leitura
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|DoNotDeclareReadOnlyMutableReferenceTypes|
|CheckId|CA2104|
|Categoria|Microsoft.Security|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um tipo visível externamente contém um campo somente leitura visível externamente que é um tipo de referência mutável.

## <a name="rule-description"></a>Descrição da Regra
 Um tipo mutável é um tipo cujos dados da instância podem ser modificados. O <xref:System.Text.StringBuilder?displayProperty=fullName> classe é um exemplo de um tipo de referência mutável. Ele contém membros que podem alterar o valor de uma instância da classe. Um exemplo de um tipo de referência imutável é o <xref:System.String?displayProperty=fullName> classe. Depois que tiver sido instanciado, seu valor nunca pode ser alterados.

 O modificador somente leitura ([readonly](http://msdn.microsoft.com/library/2f8081f6-0de2-4903-898d-99696c48d2f4) em c#, [ReadOnly](http://msdn.microsoft.com/library/e868185d-6142-4359-a2fd-a7965cadfce8) na [!INCLUDE[vbprvb](../includes/vbprvb-md.md)], e [const](http://msdn.microsoft.com/library/b21c0271-1ad0-40a0-b21c-5e812bba0318) em C++) em um tipo de referência campo (ponteiro em C++) impede que o campo que está sendo substituído por uma instância diferente do tipo de referência. No entanto, o modificador não impede que os dados da instância do campo que está sendo modificado por meio do tipo de referência.

 Campos de matriz somente leitura são isentos dessa regra, mas em vez disso, causar uma violação do [CA2105: campos de matriz não devem ser somente leitura](../code-quality/ca2105-array-fields-should-not-be-read-only.md) regra.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, remova o modificador somente leitura ou, se uma alteração significativa é aceitável, substitua o campo com um tipo imutável.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, se o tipo de campo é imutável.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma declaração de campo que faz com que uma violação dessa regra.

 [!code-cpp[FxCop.Security.MutableReferenceTypes#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.MutableReferenceTypes/cpp/FxCop.Security.MutableReferenceTypes.cpp#1)]
 [!code-csharp[FxCop.Security.MutableReferenceTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.MutableReferenceTypes/cs/FxCop.Security.MutableReferenceTypes.cs#1)]
 [!code-vb[FxCop.Security.MutableReferenceTypes#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.MutableReferenceTypes/vb/FxCop.Security.MutableReferenceTypes.vb#1)]



