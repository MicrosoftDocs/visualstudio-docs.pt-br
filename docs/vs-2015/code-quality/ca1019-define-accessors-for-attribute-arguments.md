---
title: 'CA1019: definir acessadores para argumentos de atributo | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1019
- DefineAccessorsForAttributeArguments
helpviewer_keywords:
- CA1019
- DefineAccessorsForAttributeArguments
ms.assetid: 197f2378-3c43-427e-80de-9ec25006c05c
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ec9be9dae502ec48570a85576f483518ed0d75d6
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534947"
---
# <a name="ca1019-define-accessors-for-attribute-arguments"></a>CA1019: Definir acessadores para argumentos de atributo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DefineAccessorsForAttributeArguments|
|CheckId|CA1019|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Em seu construtor, um atributo define argumentos que não têm propriedades correspondentes.

## <a name="rule-description"></a>Descrição da Regra
 Os atributos podem definir argumentos obrigatórios que devem ser especificados quando você aplica o atributo a um destino. Eles também são conhecidos como argumentos posicionais porque são fornecidos a construtores de atributos como parâmetros posicionais. Para cada argumento obrigatório, o atributo também deve fornecer uma propriedade somente leitura correspondente de forma que o valor do argumento possa ser recuperado no tempo de execução. Essa regra verifica se, para cada parâmetro de construtor, você definiu a propriedade correspondente.

 Os atributos também podem definir argumentos opcionais, que também são conhecidos como argumentos nomeados. Esses argumentos são fornecidos a construtores de atributo por nome e devem ter uma propriedade de leitura/gravação correspondente.

 Para argumentos obrigatórios e opcionais, as propriedades correspondentes e os parâmetros do construtor devem usar o mesmo nome, mas com maiúsculas e minúsculas diferentes. As propriedades usam a capitalização de Pascal e os parâmetros usam o camel case.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, adicione uma propriedade somente leitura para cada parâmetro de construtor que não tenha um.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir um aviso dessa regra se você não quiser que o valor do argumento obrigatório seja recuperável.

## <a name="custom-attributes-example"></a>Exemplo de atributos personalizados

### <a name="description"></a>Descrição
 O exemplo a seguir mostra dois atributos que definem um parâmetro obrigatório (posicional). A primeira implementação do atributo está definida incorretamente. A segunda implementação está correta.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Design.AttributeAccessors#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeAccessors/cs/FxCop.Design.AttributeAccessors.cs#1)]
 [!code-vb[FxCop.Design.AttributeAccessors#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeAccessors/vb/FxCop.Design.AttributeAccessors.vb#1)]

## <a name="positional-and-named-arguments"></a>Argumentos posicionais e nomeados

### <a name="description"></a>Descrição
 Os argumentos posicionais e nomeados tornam-se claro para os consumidores da sua biblioteca quais argumentos são obrigatórios para o atributo e quais argumentos são opcionais.

 O exemplo a seguir mostra uma implementação de um atributo que tem argumentos posicionais e nomeados.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Design.AttributeAccessorsNamed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeAccessorsNamed/cs/FxCop.Design.AttributeAccessorsNamed.cs#1)]

### <a name="comments"></a>Comentários
 O exemplo a seguir mostra como aplicar o atributo personalizado a duas propriedades.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Design.AttributeAccessorsNamedApplied#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeAccessorsNamedApplied/cs/FxCop.Design.AttributeAccessorsNamedApplied.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1813: Evitar atributos não selados](../code-quality/ca1813-avoid-unsealed-attributes.md)

## <a name="see-also"></a>Consulte Também
 [Atributos](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b)
