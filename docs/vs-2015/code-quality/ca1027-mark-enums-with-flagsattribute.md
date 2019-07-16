---
title: 'CA1027: Marcar enums com FlagsAttribute | Microsoft Docs'
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 6603e0869a9eb7947735c52a4c438b39d64b9140
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157708"
---
# <a name="ca1027-mark-enums-with-flagsattribute"></a>CA1027: Marcar enumerações com FlagsAttribute
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|MarkEnumsWithFlags|
|CheckId|CA1027|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Os valores de uma enumeração pública são potências de dois ou são combinações de outros valores que são definidos na enumeração, e o <xref:System.FlagsAttribute?displayProperty=fullName> atributo não estiver presente. Para reduzir os falsos positivos, essa regra não relata uma violação para enumerações que têm valores contíguos.

## <a name="rule-description"></a>Descrição da Regra
 Uma enumeração é um tipo de valor que define um conjunto de constantes nomeadas relacionadas. Aplicar <xref:System.FlagsAttribute> a uma enumeração quando suas constantes nomeadas podem ser combinadas de maneira significativa. Por exemplo, considere uma enumeração dos dias da semana em um aplicativo que mantém o controle de recursos do qual dia estão disponíveis. Se a disponibilidade de cada recurso é codificada usando a enumeração que tem <xref:System.FlagsAttribute> presente, qualquer combinação de dias pode ser representado. Sem o atributo, somente um dia da semana pode ser representado.

 Para campos que armazenam as enumerações combináveis, os valores de enumeração individuais são tratados como grupos de bits no campo. Portanto, esses campos são às vezes chamados de *campos de bit*. Para combinar os valores de enumeração para o armazenamento em um campo de bits, use os operadores condicionais Boolean. Para testar um campo de bits para determinar se um valor de enumeração específica está presente, use os operadores lógicos Boolean. Para um campo de bits armazenar e recuperar valores de enumeração combinados corretamente, cada valor que é definido na enumeração deve ser uma potência de dois. A menos que isso for verdadeiro, os operadores lógicos boolianos não poderá extrair valores de enumeração individuais que são armazenados no campo.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, adicionar <xref:System.FlagsAttribute> à enumeração.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprima um aviso nessa regra, se você não quiser que os valores de enumeração a ser combináveis.

## <a name="example"></a>Exemplo
 No exemplo a seguir `DaysEnumNeedsFlags` é uma enumeração que atende aos requisitos para usar <xref:System.FlagsAttribute>, mas não a possui. O `ColorEnumShouldNotHaveFlag` enumeração não tem valores que são potências de dois, mas especifica incorretamente <xref:System.FlagsAttribute>. Isso viola a regra [CA2217: Não marcar enums com FlagsAttribute](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md).

 [!code-csharp[FxCop.Design.EnumFlags#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.EnumFlags/cs/FxCop.Design.EnumFlags.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2217: Não marcar enums com FlagsAttribute](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>Consulte também
 <xref:System.FlagsAttribute?displayProperty=fullName>
