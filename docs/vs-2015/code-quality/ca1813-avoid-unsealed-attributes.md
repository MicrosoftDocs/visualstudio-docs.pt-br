---
title: 'CA1813: Evitar atributos não lacrados | Microsoft Docs'
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
- CA1813
- AvoidUnsealedAttributes
helpviewer_keywords:
- CA1813
- AvoidUnsealedAttributes
ms.assetid: f5e31b4c-9f8b-49e1-a2a8-bb5f1140729a
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 97eeacdb0753b0e1b3c42ba83245ba6ace9734d7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49830535"
---
# <a name="ca1813-avoid-unsealed-attributes"></a>CA1813: evitar atributos não lacrados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|AvoidUnsealedAttributes|
|CheckId|CA1813|
|Categoria|Microsoft.Performance|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público herda <xref:System.Attribute?displayProperty=fullName>, não é abstrato e não está lacrado (`NotInheritable` no Visual Basic).

## <a name="rule-description"></a>Descrição da Regra
 A biblioteca de classes do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] fornece métodos para recuperar atributos personalizados. Por padrão, esses métodos pesquisam a hierarquia de herança do atributo; Por exemplo <xref:System.Attribute.GetCustomAttribute%2A?displayProperty=fullName> procura o tipo de atributo especificado ou qualquer tipo de atributo que estende o tipo de atributo especificado. A validação do atributo elimina a pesquisa por meio da hierarquia de herança e pode melhorar o desempenho.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, lacre o tipo de atributo ou torná-lo abstrata.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra. Você deve fazer isso somente se você estiver definindo uma hierarquia de atributo e não é possível lacrar o atributo ou torná-lo abstrata.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um atributo personalizado que atende a essa regra.

 [!code-csharp[FxCop.Performance.AttributesSealed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.AttributesSealed/cs/FxCop.Performance.AttributesSealed.cs#1)]
 [!code-vb[FxCop.Performance.AttributesSealed#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.AttributesSealed/vb/FxCop.Performance.AttributesSealed.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1019: definir acessadores para argumentos de atributo](../code-quality/ca1019-define-accessors-for-attribute-arguments.md)

 [CA1018: marcar atributos com AttributeUsageAttribute](../code-quality/ca1018-mark-attributes-with-attributeusageattribute.md)

## <a name="see-also"></a>Consulte também
 [Atributos](http://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b)



