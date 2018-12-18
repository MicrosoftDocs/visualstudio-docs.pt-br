---
title: 'CA1406: Evitar argumentos Int64 para clientes do Visual Basic 6 | Microsoft Docs'
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
- AvoidInt64ArgumentsForVB6Clients
- CA1406
helpviewer_keywords:
- AvoidInt64ArgumentsForVB6Clients
- CA1406
ms.assetid: d5d0d3fc-f105-43da-be5b-923ab023309c
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 81217588ab2f633ee7fc25d8036e7506a7de0364
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49878330"
---
# <a name="ca1406-avoid-int64-arguments-for-visual-basic-6-clients"></a>CA1406: evitar argumentos Int64 para clientes do Visual Basic 6
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|AvoidInt64ArgumentsForVB6Clients|
|CheckId|CA1406|
|Categoria|Microsoft.Interoperability|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo que é marcado especificamente como visível para COM Component Object Model () declara um membro que utiliza um <xref:System.Int64?displayProperty=fullName> argumento.

## <a name="rule-description"></a>Descrição da Regra
 Os clientes COM do Visual Basic 6 não podem acessar inteiros de 64 bits.

 Por padrão, a seguir é visível no COM: assemblies, tipos públicos, membros de instância pública em tipos públicos e todos os membros de tipos de valor público. No entanto, para reduzir os falsos positivos, essa regra exige a visibilidade de COM do tipo a ser declarado explicitamente; o assembly que contém deve ser marcado com o <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> definido como `false` e o tipo deve ser marcado com o <xref:System.Runtime.InteropServices.ComVisibleAttribute> definido como `true`.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra para um parâmetro cujo valor sempre pode ser expresso como um inteiro de 32 bits, altere o tipo de parâmetro para <xref:System.Int32?displayProperty=fullName>. Se o valor do parâmetro pode ser maior do que pode ser expresso como um inteiro de 32 bits, altere o tipo de parâmetro para <xref:System.Decimal?displayProperty=fullName>. Observe que ambos <xref:System.Single?displayProperty=fullName> e <xref:System.Double?displayProperty=fullName> perder a precisão em intervalos superiores do <xref:System.Int64> tipo de dados. Se o membro não deve ser visível para COM, marcá-la com o <xref:System.Runtime.InteropServices.ComVisibleAttribute> definido como `false`.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, se você tiver certeza de que os clientes COM do Visual Basic 6 não acessará o tipo.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra.

 [!code-csharp[FxCop.Interoperability.LongArgument#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.LongArgument/cs/FxCop.Interoperability.LongArgument.cs#1)]
 [!code-vb[FxCop.Interoperability.LongArgument#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.LongArgument/vb/FxCop.Interoperability.LongArgument.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1413: evitar campos não públicos em tipos de valor visíveis em COM](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)

 [CA1407: evitar membros estáticos em tipos visíveis em COM](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)

 [CA1017: marcar assemblies com ComVisibleAttribute](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>Consulte também
 [Interoperação com código não gerenciado](http://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258) [tipo de dados Long](http://msdn.microsoft.com/library/b4770c34-1804-4f8c-b512-c10b0893e516)



