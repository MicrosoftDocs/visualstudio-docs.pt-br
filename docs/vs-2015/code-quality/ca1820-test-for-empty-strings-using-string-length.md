---
title: 'CA1820: Teste para cadeias de caracteres vazias usando o comprimento da cadeia de caracteres | Microsoft Docs'
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: bebd3b78881f9e1a2f4908ea667f80cbd7b98dd6
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58925684"
---
# <a name="ca1820-test-for-empty-strings-using-string-length"></a>CA1820: Testar para verificar se há cadeias de caracteres vazias usando o tamanho da cadeia de caracteres
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|TestForEmptyStringsUsingStringLength|
|CheckId|CA1820|
|Categoria|Microsoft.Performance|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Uma cadeia de caracteres é comparado com a cadeia de caracteres vazia usando <xref:System.Object.Equals%2A?displayProperty=fullName>.

## <a name="rule-description"></a>Descrição da Regra
 Comparando cadeias de caracteres usando o <xref:System.String.Length%2A?displayProperty=fullName> propriedade ou o <xref:System.String.IsNullOrEmpty%2A?displayProperty=fullName> método é significativamente mais rápido do que usar <xref:System.Object.Equals%2A>. Isso ocorre porque <xref:System.Object.Equals%2A> executa significativamente mais instruções MSIL que ambos <xref:System.String.IsNullOrEmpty%2A> ou o número de instruções executadas para recuperar o <xref:System.String.Length%2A> propriedade de valor e compará-la como zero.

 Você deve estar ciente que <xref:System.Object.Equals%2A> e <xref:System.String.Length%2A> = = 0 se comportam de forma diferente para cadeias de caracteres nulas. Se você tentar obter o valor de <xref:System.String.Length%2A> propriedade em uma cadeia de caracteres nula, o common language runtime lançará uma <xref:System.NullReferenceException?displayProperty=fullName>. Se você realizar uma comparação entre uma cadeia de caracteres nula e a cadeia de caracteres vazia, o common language runtime não lançar uma exceção; a comparação retorna `false`. Testando null não afeta significativamente o desempenho relativo dessas duas abordagens. Ao direcionar [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)], use o <xref:System.String.IsNullOrEmpty%2A> método. Caso contrário, use o <xref:System.String.Length%2A> = = comparação sempre que possível.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere a comparação para usar o <xref:System.String.Length%2A> propriedade e teste para a cadeia de caracteres nula. Se o objetivo [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)], use o <xref:System.String.IsNullOrEmpty%2A> método.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, se o desempenho não for um problema.

## <a name="example"></a>Exemplo
 O exemplo a seguir ilustra as técnicas diferentes que são usadas para procurar uma cadeia de caracteres vazia.

 [!code-csharp[FxCop.Performance.StringTest#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.StringTest/cs/FxCop.Performance.StringTest.cs#1)]
