---
title: 'CA1714: os enums de sinalizadores devem ter nomes plurais'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- FlagsEnumsShouldHavePluralNames
- CA1714
helpviewer_keywords:
- CA1714
- FlagsEnumsShouldHavePluralNames
ms.assetid: 95ef5b43-7681-49e9-a5a3-ac0357cf1be7
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: dc24a758d5c3c124267e4c967c6eb4afd1364cc2
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49871544"
---
# <a name="ca1714-flags-enums-should-have-plural-names"></a>CA1714: os enums de sinalizadores devem ter nomes plurais

|||
|-|-|
|NomeDoTipo|FlagsEnumsShouldHavePluralNames|
|CheckId|CA1714|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Uma enumeração pública tem o <xref:System.FlagsAttribute?displayProperty=fullName> e seu nome não termina em '.

## <a name="rule-description"></a>Descrição da regra
 Tipos que são marcados com <xref:System.FlagsAttribute> têm nomes que estão no plurais porque o atributo indica que mais de um valor pode ser especificado. Por exemplo, uma enumeração que define os dias da semana pode ser destinada para uso em um aplicativo onde você pode especificar vários dias. Esta enumeração deve ter o <xref:System.FlagsAttribute> e poderia ser chamado 'Dias'. Uma enumeração semelhante que permite que um único dia seja especificada não teria o atributo e pode ser chamado 'Day'.

 Convenções de nomenclatura de fornecem uma aparência comum para bibliotecas que direcionam o common language runtime. Isso reduz a curva de aprendizado que é necessário para novas bibliotecas de software e aumenta a confiança do cliente que a biblioteca foi desenvolvida por alguém que tenha experiência em desenvolvimento de código gerenciado.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Verifique o nome da enumeração uma palavra no plural ou remova o <xref:System.FlagsAttribute> atributo se vários valores de enumeração não devem ser especificados simultaneamente.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir uma violação, se o nome é uma palavra no plural, mas não termina com do '. Por exemplo, se a enumeração de vários dias que foi descrita anteriormente foram nomeada 'DaysOfTheWeek', isso violaria a lógica da regra, mas não sua intenção. Tais violações devem ser suprimidas.

## <a name="related-rules"></a>Regras relacionadas
 [CA1027: marcar enums com FlagsAttribute](../code-quality/ca1027-mark-enums-with-flagsattribute.md)

 [CA2217: não marcar enums com FlagsAttribute](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>Consulte também

- <xref:System.FlagsAttribute?displayProperty=fullName>
- [Design de enumeração](/dotnet/standard/design-guidelines/enum)