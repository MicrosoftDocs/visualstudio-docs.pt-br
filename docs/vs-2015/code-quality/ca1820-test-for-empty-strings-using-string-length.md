---
title: 'CA1820: teste para cadeias de caracteres vazias usando comprimento da cadeia | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- TestForEmptyStringsUsingStringLength
- CA1820
helpviewer_keywords:
- TestForEmptyStringsUsingStringLength
- CA1820
ms.assetid: da1e70c8-b1dc-46b9-8b8f-4e6e48339681
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 296eb6407e3ce63b0eb28ff86c215c12ec724ce9
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545308"
---
# <a name="ca1820-test-for-empty-strings-using-string-length"></a>CA1820: Testar para verificar se há cadeias de caracteres vazias usando o tamanho da cadeia de caracteres
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|TestForEmptyStringsUsingStringLength|
|CheckId|CA1820|
|Categoria|Microsoft. performance|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Uma cadeia de caracteres é comparada com a cadeia de caracteres vazia usando <xref:System.Object.Equals%2A?displayProperty=fullName> .

## <a name="rule-description"></a>Descrição da Regra
 Comparar cadeias de caracteres usando a <xref:System.String.Length%2A?displayProperty=fullName> propriedade ou o <xref:System.String.IsNullOrEmpty%2A?displayProperty=fullName> método é significativamente mais rápido do que usar o <xref:System.Object.Equals%2A> . Isso ocorre porque <xref:System.Object.Equals%2A> o executa significativamente mais instruções MSIL do que um <xref:System.String.IsNullOrEmpty%2A> ou o número de instruções executadas para recuperar o <xref:System.String.Length%2A> valor da propriedade e compará-lo com zero.

 Você deve estar ciente de que <xref:System.Object.Equals%2A> e <xref:System.String.Length%2A> = = 0 se comporta de forma diferente para cadeias de caracteres nulas. Se você tentar obter o valor da <xref:System.String.Length%2A> propriedade em uma cadeia de caracteres nula, a Common Language Runtime lançará um <xref:System.NullReferenceException?displayProperty=fullName> . Se você executar uma comparação entre uma cadeia de caracteres nula e a cadeia de caracteres vazia, a Common Language Runtime não lançará uma exceção; a comparação retorna `false` . O teste de NULL não afeta significativamente o desempenho relativo dessas duas abordagens. Ao direcionar [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] , use o <xref:System.String.IsNullOrEmpty%2A> método. Caso contrário, use a <xref:System.String.Length%2A> comparação = = sempre que possível.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere a comparação para usar a <xref:System.String.Length%2A> propriedade e o teste para a cadeia de caracteres nula. Se estiver direcionando [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] , use o <xref:System.String.IsNullOrEmpty%2A> método.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se o desempenho não for um problema.

## <a name="example"></a>Exemplo
 O exemplo a seguir ilustra as diferentes técnicas que são usadas para procurar uma cadeia de caracteres vazia.

 [!code-csharp[FxCop.Performance.StringTest#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.StringTest/cs/FxCop.Performance.StringTest.cs#1)]
