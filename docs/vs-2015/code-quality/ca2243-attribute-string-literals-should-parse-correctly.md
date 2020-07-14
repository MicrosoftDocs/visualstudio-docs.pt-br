---
title: 'CA2243: literais de cadeia de caracteres de atributo devem ser analisados corretamente | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2243
- AttributeStringLiteralsShouldParseCorrectly
helpviewer_keywords:
- AttributeStringLiteralsShouldParseCorrectly
- CA2243
ms.assetid: bfadb366-379d-4ee4-b17b-c4a09bf1106b
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 09e932651576f9b6d595657ad024b8f2697ad016
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535740"
---
# <a name="ca2243-attribute-string-literals-should-parse-correctly"></a>CA2243: Literais de cadeias de caracteres de atributo devem ser analisados corretamente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AttributeStringLiteralsShouldParseCorrectly|
|CheckId|CA2243|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 O parâmetro literal da cadeia de caracteres de um atributo não é analisado corretamente para uma URL, GUID ou versão.

## <a name="rule-description"></a>Descrição da Regra
 Como os atributos são derivados de <xref:System.Attribute?displayProperty=fullName> , e os atributos são usados no momento da compilação, somente valores constantes podem ser passados para seus construtores. Os parâmetros de atributo que devem representar URLs, GUIDs e versões não podem ser digitados como <xref:System.Uri?displayProperty=fullName> , <xref:System.Guid?displayProperty=fullName> e <xref:System.Version?displayProperty=fullName> , porque esses tipos não podem ser representados como constantes. Em vez disso, eles devem ser representados por cadeias de caracteres.

 Como o parâmetro é digitado como uma cadeia de caracteres, é possível que um parâmetro formatado incorretamente possa ser passado no momento da compilação.

 Essa regra usa uma heurística de nomenclatura para localizar parâmetros que representam um URI (Uniform Resource Identifier), um GUID (identificador global exclusivo) ou uma versão e verifica se o valor passado está correto.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Altere a cadeia de caracteres do parâmetro para uma URL, GUID ou versão formada corretamente.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se o parâmetro não representar uma URL, GUID ou versão.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra o código para o AssemblyFileVersionAttribute que viola essa regra.

 [!code-csharp[FxCop.Usage.AttributeStringLiteralsShouldParseCorrectly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.AttributeStringLiteralsShouldParseCorrectly/cs/FxCop.Usage.AttributeStringLiteralsShouldParseCorrectly.cs#1)]

 A regra é disparada pelo seguinte:

- Parâmetros que contêm ' version ' e não podem ser analisados para System. Version.

- Parâmetros que contêm ' GUID ' e não podem ser analisados como System. GUID.

- Parâmetros que contêm ' URI ', ' urn ' ou ' URL ' e não podem ser analisados para System. Uri.

## <a name="see-also"></a>Consulte Também
 [CA1054: Parâmetros de URI não devem ser cadeias de caracteres](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)
