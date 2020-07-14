---
title: 'CA1027: marcar enums com FlagsAttribute | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MarkEnumsWithFlags
- CA1027
helpviewer_keywords:
- CA1027
- MarkEnumsWithFlags
ms.assetid: 249e882c-8cd1-4c00-a2de-7b6bdc1849ff
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 774279dd05bd14c34df7f1d450f00599812d6a5b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544502"
---
# <a name="ca1027-mark-enums-with-flagsattribute"></a>CA1027: Marcar enumerações com FlagsAttribute
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|MarkEnumsWithFlags|
|CheckId|CA1027|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Os valores de uma enumeração pública são potências de duas ou são combinações de outros valores que são definidos na enumeração e o <xref:System.FlagsAttribute?displayProperty=fullName> atributo não está presente. Para reduzir os falsos positivos, essa regra não relata uma violação das enumerações que têm valores contíguos.

## <a name="rule-description"></a>Descrição da Regra
 Uma enumeração é um tipo de valor que define um conjunto de constantes nomeadas relacionadas. Aplica-se <xref:System.FlagsAttribute> a uma enumeração quando suas constantes nomeadas podem ser combinadas de uma significativa. Por exemplo, considere uma enumeração dos dias da semana em um aplicativo que controla quais recursos do dia estão disponíveis. Se a disponibilidade de cada recurso for codificada usando a enumeração que está <xref:System.FlagsAttribute> presente, qualquer combinação de dias poderá ser representada. Sem o atributo, somente um dia da semana pode ser representado.

 Para campos que armazenam enumerações combináveis, os valores de enumeração individuais são tratados como grupos de bits no campo. Portanto, esses campos são, às vezes, chamados de *campos de bits*. Para combinar valores de enumeração para armazenamento em um campo de bits, use os operadores condicionais boolianos. Para testar um campo de bits para determinar se um valor de enumeração específico está presente, use os operadores lógicos boolianos. Para um campo de bits armazenar e recuperar valores de enumeração combinados corretamente, cada valor definido na enumeração deve ser uma potência de dois. A menos que isso seja feito, os operadores lógicos boolianos não poderão extrair os valores de enumeração individuais que são armazenados no campo.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, adicione <xref:System.FlagsAttribute> à enumeração.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir um aviso dessa regra se você não quiser que os valores de enumeração sejam combináveis.

## <a name="example"></a>Exemplo
 No exemplo a seguir, `DaysEnumNeedsFlags` é uma enumeração que atende aos requisitos para usar o <xref:System.FlagsAttribute> , mas não o tem. A `ColorEnumShouldNotHaveFlag` enumeração não tem valores que são potências de dois, mas especifica incorretamente <xref:System.FlagsAttribute> . Isso viola a regra [CA2217: não marque enums com FlagsAttribute](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md).

 [!code-csharp[FxCop.Design.EnumFlags#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.EnumFlags/cs/FxCop.Design.EnumFlags.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2217: Não marcar enumerações com FlagsAttribute](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>Consulte Também
 <xref:System.FlagsAttribute?displayProperty=fullName>
