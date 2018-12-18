---
title: 'CA1019: definir acessadores para argumentos de atributo'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1019
- DefineAccessorsForAttributeArguments
helpviewer_keywords:
- CA1019
- DefineAccessorsForAttributeArguments
ms.assetid: 197f2378-3c43-427e-80de-9ec25006c05c
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 2e095c862edc5d7b68e1a6c55ada90a425b7e64f
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45550447"
---
# <a name="ca1019-define-accessors-for-attribute-arguments"></a>CA1019: definir acessadores para argumentos de atributo

|||
|-|-|
|NomeDoTipo|DefineAccessorsForAttributeArguments|
|CheckId|CA1019|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Em seu construtor, um atributo define argumentos que não têm propriedades correspondentes.

## <a name="rule-description"></a>Descrição da regra
 Os atributos podem definir argumentos obrigatórios que devem ser especificados quando você aplica o atributo a um destino. Eles também são conhecidos como argumentos posicionais porque são fornecidos a construtores de atributos como parâmetros posicionais. Para cada argumento obrigatório, o atributo também deve fornecer uma propriedade somente leitura correspondente de forma que o valor do argumento possa ser recuperado no tempo de execução. Esta regra verifica que, para cada parâmetro de construtor, você definiu a propriedade correspondente.

 Os atributos também podem definir argumentos opcionais, que também são conhecidos como argumentos nomeados. Esses argumentos são fornecidos a construtores de atributo por nome e devem ter uma propriedade de leitura/gravação correspondente.

 Para argumentos obrigatórios e opcionais, as propriedades correspondentes e os parâmetros do construtor devem usar o mesmo nome, mas diferenciam maiusculas de minúsculas. Usem o casing Pascal propriedades maiusculas/minúsculas e maiusculas e minúsculas de concatenação de uso de parâmetros.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, adicione uma propriedade somente leitura para cada parâmetro de construtor que não tenha uma.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Suprima um aviso nessa regra, se você não quiser que o valor do argumento obrigatório a ser recuperável.

## <a name="custom-attributes-example"></a>Exemplo de atributos personalizados

O exemplo a seguir mostra dois atributos que definem um parâmetro (posicional) obrigatório. A primeira implementação do atributo está definida incorretamente. A implementação do segundo está correta.

[!code-csharp[FxCop.Design.AttributeAccessors#1](../code-quality/codesnippet/CSharp/ca1019-define-accessors-for-attribute-arguments_1.cs)]
[!code-vb[FxCop.Design.AttributeAccessors#1](../code-quality/codesnippet/VisualBasic/ca1019-define-accessors-for-attribute-arguments_1.vb)]

## <a name="positional-and-named-arguments"></a>Argumentos posicionais e nomeados

Argumentos posicionais e nomeados deixar claro para os consumidores da sua biblioteca quais argumentos são obrigatórios para o atributo e quais argumentos são opcionais.

O exemplo a seguir mostra uma implementação de um atributo que tem argumentos posicionais e nomeados:

[!code-csharp[FxCop.Design.AttributeAccessorsNamed#1](../code-quality/codesnippet/CSharp/ca1019-define-accessors-for-attribute-arguments_2.cs)]

O exemplo a seguir mostra como aplicar o atributo personalizado a duas propriedades:

[!code-csharp[FxCop.Design.AttributeAccessorsNamedApplied#1](../code-quality/codesnippet/CSharp/ca1019-define-accessors-for-attribute-arguments_3.cs)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1813: evitar atributos não lacrados](../code-quality/ca1813-avoid-unsealed-attributes.md)

## <a name="see-also"></a>Consulte também
 [Atributos](/dotnet/standard/design-guidelines/attributes)