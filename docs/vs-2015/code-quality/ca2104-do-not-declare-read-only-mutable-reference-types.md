---
title: 'CA2104: Não declare tipos de referência mutáveis somente leitura | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotDeclareReadOnlyMutableReferenceTypes
- CA2104
helpviewer_keywords:
- CA2104
- DoNotDeclareReadOnlyMutableReferenceTypes
ms.assetid: 81b83ee5-4db5-4be0-9f8d-90b53894ec3b
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ff42cc2b8543fe8e1cf980a3574ae15922febf9b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85521037"
---
# <a name="ca2104-do-not-declare-read-only-mutable-reference-types"></a>CA2104: Não declarar tipos de referência mutáveis somente leitura
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotDeclareReadOnlyMutableReferenceTypes|
|CheckId|CA2104|
|Categoria|Microsoft.Security|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo visível externamente contém um campo somente leitura visível externamente que é um tipo de referência mutável.

## <a name="rule-description"></a>Descrição da Regra
 Um tipo mutável é um tipo cujos dados da instância podem ser modificados. A <xref:System.Text.StringBuilder?displayProperty=fullName> classe é um exemplo de um tipo de referência mutável. Ele contém membros que podem alterar o valor de uma instância da classe. Um exemplo de um tipo de referência imutável é a <xref:System.String?displayProperty=fullName> classe. Depois de ter sido instanciado, seu valor nunca pode ser alterado.

 O modificador somente leitura ([ReadOnly](https://msdn.microsoft.com/library/2f8081f6-0de2-4903-898d-99696c48d2f4) em C#, [ReadOnly](https://msdn.microsoft.com/library/e868185d-6142-4359-a2fd-a7965cadfce8) em [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] e [const](https://msdn.microsoft.com/library/b21c0271-1ad0-40a0-b21c-5e812bba0318) em c++) em um campo de tipo de referência (ponteiro em c++) impede que o campo seja substituído por uma instância diferente do tipo de referência. No entanto, o modificador não impede que os dados da instância do campo sejam modificados por meio do tipo de referência.

 Os campos de matriz somente leitura são isentos dessa regra, mas, em vez disso, causam uma violação dos [campos CA2105: array não devem ser somente leitura](../code-quality/ca2105-array-fields-should-not-be-read-only.md) .

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, remova o modificador somente leitura ou, se uma alteração significativa for aceitável, substitua o campo por um tipo imutável.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se o tipo de campo for imutável.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma declaração de campo que causa uma violação dessa regra.

 [!code-cpp[FxCop.Security.MutableReferenceTypes#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.MutableReferenceTypes/cpp/FxCop.Security.MutableReferenceTypes.cpp#1)]
 [!code-csharp[FxCop.Security.MutableReferenceTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.MutableReferenceTypes/cs/FxCop.Security.MutableReferenceTypes.cs#1)]
 [!code-vb[FxCop.Security.MutableReferenceTypes#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.MutableReferenceTypes/vb/FxCop.Security.MutableReferenceTypes.vb#1)]
