---
title: 'CA1717: Apenas enums FlagsAttribute devem ter nomes plurais | Microsoft Docs'
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
- CA1717
- OnlyFlagsEnumsShouldHavePluralNames
helpviewer_keywords:
- OnlyFlagsEnumsShouldHavePluralNames
- CA1717
ms.assetid: a6855d8b-d78a-42c1-834e-61c31f5572ed
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: fd02409bd3805544effd1d53f5be2318b03fea90
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49833441"
---
# <a name="ca1717-only-flagsattribute-enums-should-have-plural-names"></a>CA1717: apenas enums FlagsAttribute devem ter nomes plurais
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|OnlyFlagsEnumsShouldHavePluralNames|
|CheckId|CA1717|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 O nome de uma enumeração visível externamente termina em uma palavra no plural e a enumeração não está marcada com o <xref:System.FlagsAttribute?displayProperty=fullName> atributo.

## <a name="rule-description"></a>Descrição da Regra
 Convenções de nomenclatura determinam que um nome no plural para uma enumeração indica que mais de um valor da enumeração pode ser especificado simultaneamente. O <xref:System.FlagsAttribute> informa os compiladores que a enumeração deve ser tratada como um campo de bits que permite que operações bit a bit na enumeração.

 Se apenas um valor de uma enumeração pode ser especificado por vez, o nome da enumeração deve ser uma palavra no singular. Por exemplo, uma enumeração que define os dias da semana pode ser destinada para uso em um aplicativo onde você pode especificar vários dias. Esta enumeração deve ter o <xref:System.FlagsAttribute> e poderia ser chamado 'Dias'. Uma enumeração semelhante que permite que um único dia seja especificada não teria o atributo e pode ser chamado 'Day'.

 Convenções de nomenclatura de fornecem uma aparência comum para bibliotecas que direcionam o common language runtime. Isso reduz o tempo que é necessário para conhecer uma nova biblioteca de software e aumenta a confiança do cliente que a biblioteca foi desenvolvida por alguém que tenha experiência em desenvolvimento de código gerenciado.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Verifique o nome da enumeração uma palavra no singular ou adicionar o <xref:System.FlagsAttribute>.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso da regra se o nome terminar em uma palavra no singular.

## <a name="related-rules"></a>Regras relacionadas
 [CA1714: enums de sinalizadores devem ter nomes plurais](../code-quality/ca1714-flags-enums-should-have-plural-names.md)

 [CA1027: marcar enums com FlagsAttribute](../code-quality/ca1027-mark-enums-with-flagsattribute.md)

 [CA2217: não marcar enums com FlagsAttribute](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>Consulte também
 <xref:System.FlagsAttribute?displayProperty=fullName> [Design de enumeração](http://msdn.microsoft.com/library/dd53c952-9d9a-4736-86ff-9540e815d545)



