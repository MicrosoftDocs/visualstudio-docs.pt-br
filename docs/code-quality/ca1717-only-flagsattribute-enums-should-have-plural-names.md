---
title: 'CA1717: Apenas enumerações FlagsAttribute devem ter nomes no plural'
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1717
- OnlyFlagsEnumsShouldHavePluralNames
helpviewer_keywords:
- OnlyFlagsEnumsShouldHavePluralNames
- CA1717
ms.assetid: a6855d8b-d78a-42c1-834e-61c31f5572ed
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2d760802422773b3713fa7ea08ce0ce7a191f418
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69547120"
---
# <a name="ca1717-only-flagsattribute-enums-should-have-plural-names"></a>CA1717: Apenas enumerações FlagsAttribute devem ter nomes no plural

|||
|-|-|
|NomeDoTipo|OnlyFlagsEnumsShouldHavePluralNames|
|CheckId|CA1717|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa

O nome de uma enumeração termina em uma palavra plural e a enumeração não é marcada com o <xref:System.FlagsAttribute?displayProperty=fullName> atributo.

Por padrão, essa regra só examina enumerações visíveis externamente, mas isso é [configurável](#configurability).

## <a name="rule-description"></a>Descrição da regra

As convenções de nomenclatura ditam que um nome no plural para uma enumeração indica que mais de um valor da enumeração pode ser especificado simultaneamente. O <xref:System.FlagsAttribute> informa aos compiladores que a enumeração deve ser tratada como um campo de bits que permite operações bit a bit na enumeração.

Se apenas um valor de uma enumeração puder ser especificado por vez, o nome da enumeração deverá ser uma palavra singular. Por exemplo, uma enumeração que define os dias da semana pode ser destinada a uso em um aplicativo em que você pode especificar vários dias. Essa enumeração deve ter <xref:System.FlagsAttribute> e pode ser chamada ' Days '. Uma enumeração semelhante que permite que apenas um único dia seja especificado não teria o atributo e poderia ser chamada ' Day '.

As convenções de nomenclatura fornecem uma aparência comum para as bibliotecas direcionadas ao Common Language Runtime. Isso reduz o tempo necessário para aprender uma nova biblioteca de software e aumenta a confiança do cliente de que a biblioteca foi desenvolvida por alguém que tenha experiência no desenvolvimento de código gerenciado.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Torne o nome da enumeração uma palavra singular ou adicione o <xref:System.FlagsAttribute>.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

É seguro suprimir um aviso da regra se o nome terminar em uma palavra singular.

## <a name="configurability"></a>Configurabilidade

Se você estiver executando essa regra por meio de analisadores do [FxCop](install-fxcop-analyzers.md) (e não com a análise herdada), poderá configurar em quais partes de sua base de código executar essa regra, com base em sua acessibilidade. Por exemplo, para especificar que a regra deve ser executada somente na superfície da API não pública, adicione o seguinte par chave-valor a um arquivo. editorconfig em seu projeto:

```ini
dotnet_code_quality.ca1717.api_surface = private, internal
```

Você pode configurar essa opção apenas para essa regra, para todas as regras ou para todas as regras nesta categoria (nomenclatura). Para obter mais informações, consulte [Configurar analisadores de FxCop](configure-fxcop-analyzers.md).

## <a name="related-rules"></a>Regras relacionadas

- [CA1714: Enumerações de sinalizadores devem ter nomes no plural](../code-quality/ca1714-flags-enums-should-have-plural-names.md)
- [CA1027: Marcar enums com FlagsAttribute](../code-quality/ca1027-mark-enums-with-flagsattribute.md)
- [CA2217: Não marcar enums com FlagsAttribute](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

## <a name="see-also"></a>Consulte também

- <xref:System.FlagsAttribute?displayProperty=fullName>
- [Design de enumeração](/dotnet/standard/design-guidelines/enum)