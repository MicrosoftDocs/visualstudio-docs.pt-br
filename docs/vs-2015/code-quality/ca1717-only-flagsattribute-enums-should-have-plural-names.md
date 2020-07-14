---
title: 'CA1717: somente enumerações FlagsAttribute devem ter nomes no plural | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1717
- OnlyFlagsEnumsShouldHavePluralNames
helpviewer_keywords:
- OnlyFlagsEnumsShouldHavePluralNames
- CA1717
ms.assetid: a6855d8b-d78a-42c1-834e-61c31f5572ed
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c58c218991226a954185853097dc81da36c69ed6
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543683"
---
# <a name="ca1717-only-flagsattribute-enums-should-have-plural-names"></a>CA1717: Apenas enumerações FlagsAttribute devem ter nomes no plural
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|OnlyFlagsEnumsShouldHavePluralNames|
|CheckId|CA1717|
|Categoria|Microsoft. Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 O nome de uma enumeração visível externamente termina em uma palavra do plural e a enumeração não é marcada com o <xref:System.FlagsAttribute?displayProperty=fullName> atributo.

## <a name="rule-description"></a>Descrição da Regra
 As convenções de nomenclatura ditam que um nome no plural para uma enumeração indica que mais de um valor da enumeração pode ser especificado simultaneamente. O <xref:System.FlagsAttribute> informa aos compiladores que a enumeração deve ser tratada como um campo de bits que permite operações bit a bit na enumeração.

 Se apenas um valor de uma enumeração puder ser especificado por vez, o nome da enumeração deverá ser uma palavra singular. Por exemplo, uma enumeração que define os dias da semana pode ser destinada a uso em um aplicativo em que você pode especificar vários dias. Essa enumeração deve ter <xref:System.FlagsAttribute> e pode ser chamada ' Days '. Uma enumeração semelhante que permite que apenas um único dia seja especificado não teria o atributo e poderia ser chamada ' Day '.

 As convenções de nomenclatura fornecem uma aparência comum para as bibliotecas direcionadas ao Common Language Runtime. Isso reduz o tempo necessário para aprender uma nova biblioteca de software e aumenta a confiança do cliente de que a biblioteca foi desenvolvida por alguém que tenha experiência no desenvolvimento de código gerenciado.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Torne o nome da enumeração uma palavra singular ou adicione o <xref:System.FlagsAttribute> .

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso da regra se o nome terminar em uma palavra singular.

## <a name="related-rules"></a>Regras relacionadas
 [CA1714: Enumerações de sinalizador devem ter nomes no plural](../code-quality/ca1714-flags-enums-should-have-plural-names.md)

 [CA1027: Marcar enumerações com FlagsAttribute](../code-quality/ca1027-mark-enums-with-flagsattribute.md)

 [CA2217: Não marcar enumerações com FlagsAttribute](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>Consulte Também
 <xref:System.FlagsAttribute?displayProperty=fullName>[Design de enumeração](https://msdn.microsoft.com/library/dd53c952-9d9a-4736-86ff-9540e815d545)
