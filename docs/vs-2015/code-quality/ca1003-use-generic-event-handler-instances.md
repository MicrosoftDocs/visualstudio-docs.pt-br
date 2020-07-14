---
title: 'CA1003: usar instâncias de manipulador de eventos genéricas | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseGenericEventHandlerInstances
- CA1003
helpviewer_keywords:
- CA1003
- UseGenericEventHandlerInstances
ms.assetid: 402101b6-555d-4cf7-b223-1d9fdfaaf1cd
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ee0571e85a1d4ec9960e0235814fcb9d7adbd483
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539900"
---
# <a name="ca1003-use-generic-event-handler-instances"></a>CA1003: Usar instâncias do manipulador de eventos genérico
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|UseGenericEventHandlerInstances|
|CheckId|CA1003|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo contém um delegado que retorna void, cuja assinatura contém dois parâmetros (o primeiro objeto e o segundo tipo que pode ser atribuído a EventArgs) e os destinos de assembly que o contêm [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] .

## <a name="rule-description"></a>Descrição da Regra
 Antes [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] , para passar informações personalizadas para o manipulador de eventos, um novo delegado tinha de ser declarado que especificou uma classe que era derivada da <xref:System.EventArgs?displayProperty=fullName> classe. Isso não é mais verdade no [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] , que introduziu o <xref:System.EventHandler%601?displayProperty=fullName> delegado. Esse delegado genérico permite que qualquer classe derivada de <xref:System.EventArgs> para ser usada junto com o manipulador de eventos.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, remova o delegado e substitua seu uso usando o <xref:System.EventHandler%601?displayProperty=fullName> delegado. Se o delegado for gerado automaticamente pelo [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] compilador, altere a sintaxe da declaração de evento para usar o <xref:System.EventHandler%601?displayProperty=fullName> delegado.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um delegado que viola a regra. No [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] exemplo, os comentários descrevem como modificar o exemplo para atender à regra. Para o exemplo de C#, um exemplo a seguir mostra o código modificado.

 [!code-csharp[FxCop.Design.CustomEventHandler#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CustomEventHandler/cs/FxCop.Design.CustomEventHandler.cs#1)]
 [!code-vb[FxCop.Design.CustomEventHandler#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.CustomEventHandler/vb/FxCop.Design.CustomEventHandler.vb#1)]

## <a name="example"></a>Exemplo
 O exemplo a seguir remove a declaração delegate do exemplo anterior, que satisfaz a regra e substitui seu uso nos `ClassThatRaisesEvent` `ClassThatHandlesEvent` métodos e usando o <xref:System.EventHandler%601?displayProperty=fullName> delegado.

 [!code-csharp[FxCop.Design.GenericEventHandler#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.GenericEventHandler/cs/FxCop.Design.GenericEventHandler.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1005: Evitar parâmetros excessivos em tipos genéricos](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1010: Coleções devem implementar uma interface genérica](../code-quality/ca1010-collections-should-implement-generic-interface.md)

 [CA1000: Não declarar membros estáticos em tipos genéricos](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1002: Não expor listas genéricas](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006: Não aninhar tipos genéricos em assinaturas de membro](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004: Métodos genéricos devem fornecer um parâmetro de tipo](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1007: Usar genéricos quando apropriado](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>Consulte Também
 [Genéricos](https://msdn.microsoft.com/library/75ea8509-a4ea-4e7a-a2b3-cf72482e9282)
