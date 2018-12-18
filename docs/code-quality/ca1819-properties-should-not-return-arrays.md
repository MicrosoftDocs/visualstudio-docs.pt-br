---
title: 'CA1819: as propriedades não devem retornar matrizes'
ms.date: 09/28/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PropertiesShouldNotReturnArrays
- CA1819
helpviewer_keywords:
- PropertiesShouldNotReturnArrays
- CA1819
ms.assetid: 85fcf312-57f8-438a-8b10-34441fe0bdeb
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 99fd9627c06b11dae9348a85f417cf152ac1c8c9
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47859027"
---
# <a name="ca1819-properties-should-not-return-arrays"></a>CA1819: as propriedades não devem retornar matrizes

|||
|-|-|
|NomeDoTipo|PropertiesShouldNotReturnArrays|
|CheckId|CA1819|
|Categoria|Microsoft.Performance|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa

Uma propriedade pública ou protegida em um tipo público retorna uma matriz.

## <a name="rule-description"></a>Descrição da regra

Matrizes retornadas por propriedades não são protegidos contra gravação, mesmo se a propriedade é somente leitura. Para manter a matriz à prova de adulteração, a propriedade deve retornar uma cópia da matriz. Normalmente, os usuários não entendem as implicações adversas no desempenho de chamar essa propriedade. Especificamente, elas podem usar a propriedade como uma propriedade indexada.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, verifique a propriedade de um método ou altere a propriedade para retornar uma coleção.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Você pode suprimir um aviso de que é gerado para uma propriedade de um atributo que é derivado de <xref:System.Attribute> classe. Atributos podem conter propriedades que retornam matrizes, mas não podem conter propriedades que retornam coleções.

Você pode suprimir o aviso se a propriedade for parte de um [o objeto de transferência de dados (DTO)](/previous-versions/msp-n-p/ff649585(v=pandp.10)) classe.

Caso contrário, não suprima um aviso nessa regra.

## <a name="example-violation"></a>Violação de exemplo

O exemplo a seguir mostra uma propriedade que viola essa regra:

[!code-csharp[FxCop.Performance.PropertyArrayViolation#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_1.cs)]
[!code-vb[FxCop.Performance.PropertyArrayViolation#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_1.vb)]

Para corrigir uma violação dessa regra, verifique a propriedade de um método ou altere a propriedade para retornar uma coleção em vez de uma matriz.

### <a name="change-the-property-to-a-method"></a>Altere a propriedade para um método

O exemplo a seguir corrige a violação, alterando a propriedade a um método:

[!code-vb[FxCop.Performance.PropertyArrayFixedMethod#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_2.vb)]
[!code-csharp[FxCop.Performance.PropertyArrayFixedMethod#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_2.cs)]

### <a name="change-the-property-to-return-a-collection"></a>Altere a propriedade para retornar uma coleção

O exemplo a seguir corrige a violação, alterando a propriedade para retornar um <xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=fullName>:

[!code-csharp[FxCop.Performance.PropertyArrayFixedCollection#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_3.cs)]
[!code-vb[FxCop.Performance.PropertyArrayFixedCollection#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_3.vb)]

## <a name="allow-users-to-modify-a-property"></a>Permitir que os usuários modificar uma propriedade

Você talvez queira permitir que o consumidor da classe modificar uma propriedade. O exemplo a seguir mostra uma propriedade de leitura/gravação que viola essa regra:

[!code-csharp[FxCop.Performance.PropertyModifyViolation#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_4.cs)]
[!code-vb[FxCop.Performance.PropertyModifyViolation#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_4.vb)]

O exemplo a seguir corrige a violação, alterando a propriedade para retornar um <xref:System.Collections.ObjectModel.Collection%601?displayProperty=fullName>:

[!code-vb[FxCop.Performance.PropertyModifyFixed#1](../code-quality/codesnippet/VisualBasic/ca1819-properties-should-not-return-arrays_5.vb)]
[!code-csharp[FxCop.Performance.PropertyModifyFixed#1](../code-quality/codesnippet/CSharp/ca1819-properties-should-not-return-arrays_5.cs)]

## <a name="related-rules"></a>Regras relacionadas

- [CA1024: usar propriedades quando apropriado](../code-quality/ca1024-use-properties-where-appropriate.md)