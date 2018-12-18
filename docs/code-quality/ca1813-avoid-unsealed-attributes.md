---
title: 'CA1813: evitar atributos não lacrados'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1813
- AvoidUnsealedAttributes
helpviewer_keywords:
- CA1813
- AvoidUnsealedAttributes
ms.assetid: f5e31b4c-9f8b-49e1-a2a8-bb5f1140729a
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 45804f08ea25ab8582d28632baf07abea24e0406
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47859478"
---
# <a name="ca1813-avoid-unsealed-attributes"></a>CA1813: evitar atributos não lacrados

|||
|-|-|
|NomeDoTipo|AvoidUnsealedAttributes|
|CheckId|CA1813|
|Categoria|Microsoft.Performance|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa

Um tipo público herda <xref:System.Attribute?displayProperty=fullName>, não é abstrato e não está lacrado (`NotInheritable` no Visual Basic).

## <a name="rule-description"></a>Descrição da regra

A biblioteca de classes do .NET Framework fornece métodos para recuperar atributos personalizados. Por padrão, esses métodos pesquisam a hierarquia de herança do atributo. Por exemplo, <xref:System.Attribute.GetCustomAttribute%2A?displayProperty=fullName> procura o tipo de atributo especificado ou qualquer tipo de atributo que estende o tipo de atributo especificado. A validação do atributo elimina a pesquisa por meio da hierarquia de herança e pode melhorar o desempenho.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, lacre o tipo de atributo ou torná-lo abstrata.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

É seguro suprimir um aviso nessa regra. Suprimir somente se você estiver definindo uma hierarquia de atributo e não é possível lacrar o atributo ou torná-lo abstrata.

## <a name="example"></a>Exemplo

O exemplo a seguir mostra um atributo personalizado que atende a essa regra.

[!code-csharp[FxCop.Performance.AttributesSealed#1](../code-quality/codesnippet/CSharp/ca1813-avoid-unsealed-attributes_1.cs)]
[!code-vb[FxCop.Performance.AttributesSealed#1](../code-quality/codesnippet/VisualBasic/ca1813-avoid-unsealed-attributes_1.vb)]

## <a name="related-rules"></a>Regras relacionadas

- [CA1019: definir acessadores para argumentos de atributo](../code-quality/ca1019-define-accessors-for-attribute-arguments.md)
- [CA1018: marcar atributos com AttributeUsageAttribute](../code-quality/ca1018-mark-attributes-with-attributeusageattribute.md)

## <a name="see-also"></a>Consulte também

- [Atributos](/dotnet/standard/design-guidelines/attributes)