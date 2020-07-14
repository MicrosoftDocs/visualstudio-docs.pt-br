---
title: 'CA1018: marcar atributos com AttributeUsageAttribute | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1018
- MarkAttributesWithAttributeUsage
helpviewer_keywords:
- CA1018
- MarkAttributesWithAttributeUsage
ms.assetid: 6ab70ec0-220f-4880-af31-45067703133c
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 256fc281b27c483f1dda0317f7d2695fa36c47f8
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535051"
---
# <a name="ca1018-mark-attributes-with-attributeusageattribute"></a>CA1018: Marcar atributos com AttributeUsageAttribute
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|MarkAttributesWithAttributeUsage|
|CheckId|CA1018|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 O <xref:System.AttributeUsageAttribute?displayProperty=fullName> atributo não está presente no atributo personalizado.

## <a name="rule-description"></a>Descrição da Regra
 Quando você define um atributo personalizado, marque-o usando <xref:System.AttributeUsageAttribute> para indicar onde no código-fonte o atributo personalizado pode ser aplicado. O significado e o uso desejado de um atributo determinarão seus locais válidos no código. Por exemplo, você pode definir um atributo que identifica a pessoa responsável por manter e aprimorar cada tipo em uma biblioteca, e essa responsabilidade sempre é atribuída no nível de tipo. Nesse caso, os compiladores devem habilitar o atributo em classes, enumerações e interfaces, mas não devem habilitá-lo em métodos, eventos ou propriedades. Procedimentos e políticas organizacionais ditariam se o atributo deveria ser habilitado em assemblies.

 A <xref:System.AttributeTargets?displayProperty=fullName> enumeração define os destinos que você pode especificar para um atributo personalizado. Se você omitir <xref:System.AttributeUsageAttribute> , seu atributo personalizado será válido para todos os destinos, conforme definido pelo `All` valor de <xref:System.AttributeTargets> enumeração.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, especifique destinos para o atributo usando <xref:System.AttributeUsageAttribute> . Veja os exemplos a seguir.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Você deve corrigir uma violação dessa regra em vez de excluir a mensagem. Mesmo que o atributo herde <xref:System.AttributeUsageAttribute> , o atributo deve estar presente para simplificar a manutenção do código.

## <a name="example"></a>Exemplo
 O exemplo a seguir define dois atributos. `BadCodeMaintainerAttribute`omite incorretamente a <xref:System.AttributeUsageAttribute> instrução e `GoodCodeMaintainerAttribute` implementa corretamente o atributo descrito anteriormente nesta seção. Observe que a propriedade `DeveloperName` é exigida pela regra de design [CA1019: definir acessadores para argumentos de atributo](../code-quality/ca1019-define-accessors-for-attribute-arguments.md) e está incluído para fins de integridade.

 [!code-csharp[FxCop.Design.AttributeUsage#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeUsage/cs/FxCop.Design.AttributeUsage.cs#1)]
 [!code-vb[FxCop.Design.AttributeUsage#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeUsage/vb/FxCop.Design.AttributeUsage.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1019: Definir acessadores para argumentos de atributo](../code-quality/ca1019-define-accessors-for-attribute-arguments.md)

 [CA1813: Evitar atributos não selados](../code-quality/ca1813-avoid-unsealed-attributes.md)

## <a name="see-also"></a>Consulte Também
 [Atributos](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b)
