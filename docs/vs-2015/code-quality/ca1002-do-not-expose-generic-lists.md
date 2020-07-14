---
title: 'CA1002: não expor listas genéricas | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotExposeGenericLists
- CA1002
helpviewer_keywords:
- CA1002
- DoNotExposeGenericLists
ms.assetid: 5caac810-1a79-47df-a27b-c46c5040bf34
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 6fcc4ae2a07eb7b1f155d6c65020e2c1a9ddc9f2
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546842"
---
# <a name="ca1002-do-not-expose-generic-lists"></a>CA1002: Não expor listas genéricas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotExposeGenericLists|
|CheckId|CA1002|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo contém um membro visível externamente que é um <xref:System.Collections.Generic.List%601?displayProperty=fullName> tipo, retorna um <xref:System.Collections.Generic.List%601?displayProperty=fullName> tipo ou cuja assinatura inclui um <xref:System.Collections.Generic.List%601?displayProperty=fullName> parâmetro.

## <a name="rule-description"></a>Descrição da Regra
 <xref:System.Collections.Generic.List%601?displayProperty=fullName>é uma coleção genérica que é projetada para desempenho e não para herança. <xref:System.Collections.Generic.List%601?displayProperty=fullName>Não contém membros virtuais que facilitam a alteração do comportamento de uma classe herdada. As coleções genéricas a seguir são projetadas para herança e devem ser expostas em vez de <xref:System.Collections.Generic.List%601?displayProperty=fullName> .

- <xref:System.Collections.ObjectModel.Collection%601?displayProperty=fullName>

- <xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=fullName>

- <xref:System.Collections.ObjectModel.KeyedCollection%602?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere o <xref:System.Collections.Generic.List%601?displayProperty=fullName> tipo para uma das coleções genéricas projetadas para herança.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprimir um aviso dessa regra, a menos que o assembly que gera esse aviso não seja uma biblioteca reutilizável. Por exemplo, seria seguro suprimir esse aviso em um aplicativo ajustado para o desempenho em que um benefício de desempenho foi obtido do uso de listas genéricas.

## <a name="related-rules"></a>Regras relacionadas
 [CA1005: Evitar parâmetros excessivos em tipos genéricos](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1010: Coleções devem implementar uma interface genérica](../code-quality/ca1010-collections-should-implement-generic-interface.md)

 [CA1000: Não declarar membros estáticos em tipos genéricos](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1006: Não aninhar tipos genéricos em assinaturas de membro](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004: Métodos genéricos devem fornecer um parâmetro de tipo](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1003: Usar instâncias do manipulador de eventos genérico](../code-quality/ca1003-use-generic-event-handler-instances.md)

 [CA1007: Usar genéricos quando apropriado](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>Consulte Também
 [Genéricos](https://msdn.microsoft.com/library/75ea8509-a4ea-4e7a-a2b3-cf72482e9282)
