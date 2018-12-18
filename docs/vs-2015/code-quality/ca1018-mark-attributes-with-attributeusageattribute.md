---
title: 'CA1018: Marcar atributos com AttributeUsageAttribute | Microsoft Docs'
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
- CA1018
- MarkAttributesWithAttributeUsage
helpviewer_keywords:
- CA1018
- MarkAttributesWithAttributeUsage
ms.assetid: 6ab70ec0-220f-4880-af31-45067703133c
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 277a9ff1db0001613bbd8c389b286c130ab17748
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49906137"
---
# <a name="ca1018-mark-attributes-with-attributeusageattribute"></a>CA1018: marcar atributos com AttributeUsageAttribute
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|MarkAttributesWithAttributeUsage|
|CheckId|CA1018|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 O <xref:System.AttributeUsageAttribute?displayProperty=fullName> atributo não está presente no atributo personalizado.

## <a name="rule-description"></a>Descrição da Regra
 Quando você define um atributo personalizado, marcá-la usando <xref:System.AttributeUsageAttribute> para indicar onde no código-fonte do atributo personalizado pode ser aplicado. O significado e o uso desejado de um atributo determinarão seus locais válidos no código. Por exemplo, você pode definir um atributo que identifica a pessoa a quem é responsável por manter e aprimorar a cada tipo em uma biblioteca e responsabilidade sempre é atribuída no nível do tipo. Nesse caso, os compiladores devem habilitar o atributo em classes, enumerações e interfaces, mas não devem habilitá-lo em métodos, eventos ou propriedades. Procedimentos e as políticas organizacionais determinaria se o atributo deve ser habilitado em assemblies.

 O <xref:System.AttributeTargets?displayProperty=fullName> enumeração define os destinos que você pode especificar para um atributo personalizado. Se você omitir <xref:System.AttributeUsageAttribute>, o atributo personalizado será válido para todos os destinos, conforme definido pelo `All` valor <xref:System.AttributeTargets> enumeração.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, especificar destinos para o atributo usando <xref:System.AttributeUsageAttribute>. Consulte o exemplo a seguir.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Você deve corrigir uma violação dessa regra, em vez de excluir a mensagem. Mesmo se o atributo herda <xref:System.AttributeUsageAttribute>, o atributo deve estar presente para simplificar a manutenção do código.

## <a name="example"></a>Exemplo
 O exemplo a seguir define dois atributos. `BadCodeMaintainerAttribute` omite incorretamente a <xref:System.AttributeUsageAttribute> instrução, e `GoodCodeMaintainerAttribute` implementa corretamente o atributo que é descrito anteriormente nesta seção. Observe que a propriedade `DeveloperName` é necessária para a regra de criação [CA1019: definir acessadores para argumentos de atributo](../code-quality/ca1019-define-accessors-for-attribute-arguments.md) e está incluído para integridade.

 [!code-csharp[FxCop.Design.AttributeUsage#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeUsage/cs/FxCop.Design.AttributeUsage.cs#1)]
 [!code-vb[FxCop.Design.AttributeUsage#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeUsage/vb/FxCop.Design.AttributeUsage.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1019: definir acessadores para argumentos de atributo](../code-quality/ca1019-define-accessors-for-attribute-arguments.md)

 [CA1813: evitar atributos não lacrados](../code-quality/ca1813-avoid-unsealed-attributes.md)

## <a name="see-also"></a>Consulte também
 [Atributos](http://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b)



