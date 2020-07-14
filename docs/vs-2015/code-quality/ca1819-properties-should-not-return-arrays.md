---
title: 'CA1819: as propriedades não devem retornar matrizes | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PropertiesShouldNotReturnArrays
- CA1819
helpviewer_keywords:
- PropertiesShouldNotReturnArrays
- CA1819
ms.assetid: 85fcf312-57f8-438a-8b10-34441fe0bdeb
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a96d2164cbd6c03cb0d191b2d0c3c4607468209c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545321"
---
# <a name="ca1819-properties-should-not-return-arrays"></a>CA1819: Propriedades não devem retornar matrizes
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|PropertiesShouldNotReturnArrays|
|CheckId|CA1819|
|Categoria|Microsoft. performance|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Uma propriedade pública ou protegida em um tipo público retorna uma matriz.

## <a name="rule-description"></a>Descrição da Regra
 As matrizes retornadas por propriedades não são protegidas por gravação, mesmo que a propriedade seja somente leitura. Para manter a matriz à prova de adulteração, a propriedade deve retornar uma cópia da matriz. Normalmente, os usuários não compreenderão as implicações adversas no desempenho de chamar uma propriedade assim. Especificamente, eles podem usar a propriedade como uma propriedade indexada.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, torne a propriedade um método ou altere a propriedade para retornar uma coleção.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Os atributos podem conter propriedades que retornam matrizes, mas não podem conter propriedades que retornem coleções. Você pode suprimir um aviso que é gerado para uma propriedade de um atributo que é derivada do [System. Attribute] (<!-- TODO: review code entity reference <xref:assetId:///System.Attribute?qualifyHint=False&amp;autoUpgrade=True>  -->classes. Caso contrário, não omita um aviso dessa regra.

## <a name="example-violation"></a>Violação de exemplo

### <a name="description"></a>Descrição
 O exemplo a seguir mostra uma propriedade que viola essa regra.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Performance.PropertyArrayViolation#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayViolation/cs/FxCop.Performance.PropertyArrayViolation.cs#1)]
 [!code-vb[FxCop.Performance.PropertyArrayViolation#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayViolation/vb/FxCop.Performance.PropertyArrayViolation.vb#1)]

### <a name="comments"></a>Comentários
 Para corrigir uma violação dessa regra, torne a propriedade um método ou altere a propriedade para retornar uma coleção em vez de uma matriz.

## <a name="change-the-property-to-a-method-example"></a>Alterar a propriedade para um exemplo de método

### <a name="description"></a>Descrição
 O exemplo a seguir corrige a violação alterando a propriedade para um método.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Performance.PropertyArrayFixedMethod#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayFixedMethod/cs/FxCop.Performance.PropertyArrayFixedMethod.cs#1)]
 [!code-vb[FxCop.Performance.PropertyArrayFixedMethod#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayFixedMethod/vb/FxCop.Performance.PropertyArrayFixedMethod.vb#1)]

## <a name="return-a-collection-example"></a>Retornar um exemplo de coleção

### <a name="description"></a>Descrição
 O exemplo a seguir corrige a violação alterando a propriedade para retornar um

 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=fullName>.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Performance.PropertyArrayFixedCollection#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayFixedCollection/cs/FxCop.Performance.PropertyArrayFixedCollection.cs#1)]
 [!code-vb[FxCop.Performance.PropertyArrayFixedCollection#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyArrayFixedCollection/vb/FxCop.Performance.PropertyArrayFixedCollection.vb#1)]

## <a name="allowing-users-to-modify-a-property"></a>Permitindo que os usuários modifiquem uma propriedade

### <a name="description"></a>Descrição
 Talvez você queira permitir que o consumidor da classe modifique uma propriedade. O exemplo a seguir mostra uma propriedade de leitura/gravação que viola essa regra.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Performance.PropertyModifyViolation#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyModifyViolation/cs/FxCop.Performance.PropertyModifyViolation.cs#1)]
 [!code-vb[FxCop.Performance.PropertyModifyViolation#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyModifyViolation/vb/FxCop.Performance.PropertyModifyViolation.vb#1)]

### <a name="comments"></a>Comentários
 O exemplo a seguir corrige a violação alterando a propriedade para retornar um <xref:System.Collections.ObjectModel.Collection%601?displayProperty=fullName> .

### <a name="code"></a>Código
 [!code-csharp[FxCop.Performance.PropertyModifyFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyModifyFixed/cs/FxCop.Performance.PropertyModifyFixed.cs#1)]
 [!code-vb[FxCop.Performance.PropertyModifyFixed#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.PropertyModifyFixed/vb/FxCop.Performance.PropertyModifyFixed.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1024: Usar propriedades quando apropriado](../code-quality/ca1024-use-properties-where-appropriate.md)
