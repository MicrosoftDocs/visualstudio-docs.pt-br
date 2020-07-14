---
title: 'CA1406: Evite argumentos Int64 para clientes Visual Basic 6 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidInt64ArgumentsForVB6Clients
- CA1406
helpviewer_keywords:
- AvoidInt64ArgumentsForVB6Clients
- CA1406
ms.assetid: d5d0d3fc-f105-43da-be5b-923ab023309c
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b6ab93c24cd97d498ae886c7a9184fd4a5f111f1
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534908"
---
# <a name="ca1406-avoid-int64-arguments-for-visual-basic-6-clients"></a>CA1406: Evitar argumentos Int64 para clientes do Visual Basic 6
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AvoidInt64ArgumentsForVB6Clients|
|CheckId|CA1406|
|Categoria|Microsoft. Interoperability|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo marcado especificamente como visível para Component Object Model (COM) declara um membro que usa um <xref:System.Int64?displayProperty=fullName> argumento.

## <a name="rule-description"></a>Descrição da Regra
 Os clientes COM do Visual Basic 6 não podem acessar inteiros de 64 bits.

 Por padrão, os itens a seguir são visíveis para COM: assemblies, tipos públicos, membros de instância pública em tipos públicos e todos os membros de tipos de valor público. No entanto, para reduzir os falsos positivos, essa regra exige que a visibilidade COM do tipo seja explicitamente declarada; o assembly contentor deve ser marcado com o <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> definido como `false` e o tipo deve ser marcado com o <xref:System.Runtime.InteropServices.ComVisibleAttribute> definido como `true` .

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra para um parâmetro cujo valor sempre pode ser expresso como um integral de 32 bits, altere o tipo de parâmetro para <xref:System.Int32?displayProperty=fullName> . Se o valor do parâmetro puder ser maior do que pode ser expresso como um integral de 32 bits, altere o tipo de parâmetro para <xref:System.Decimal?displayProperty=fullName> . Observe que <xref:System.Single?displayProperty=fullName> e <xref:System.Double?displayProperty=fullName> perdem a precisão nos intervalos superiores do tipo de <xref:System.Int64> dados. Se o membro não for destinado a ser visível para COM, marque-o com o <xref:System.Runtime.InteropServices.ComVisibleAttribute> conjunto como `false` .

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se for certo que Visual Basic 6 clientes COM não acessarão o tipo.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra.

 [!code-csharp[FxCop.Interoperability.LongArgument#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.LongArgument/cs/FxCop.Interoperability.LongArgument.cs#1)]
 [!code-vb[FxCop.Interoperability.LongArgument#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.LongArgument/vb/FxCop.Interoperability.LongArgument.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1413: Evitar campos não públicos em tipos de valor visíveis no COM](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)

 [CA1407: Evitar membros estáticos em tipos visíveis no COM](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)

 [CA1017: Marcar assemblies com ComVisibleAttribute](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>Consulte Também
 Interoperação com o [tipo de dados Long](https://msdn.microsoft.com/library/b4770c34-1804-4f8c-b512-c10b0893e516) [de código não gerenciado](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
