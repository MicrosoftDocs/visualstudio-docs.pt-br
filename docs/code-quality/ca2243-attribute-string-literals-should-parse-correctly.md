---
title: 'CA2243: os literais da cadeia de caracteres de atributo devem ser analisados corretamente'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2243
- AttributeStringLiteralsShouldParseCorrectly
helpviewer_keywords:
- AttributeStringLiteralsShouldParseCorrectly
- CA2243
ms.assetid: bfadb366-379d-4ee4-b17b-c4a09bf1106b
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c6808520f3b28a2da8421394619550166d88d52d
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45551932"
---
# <a name="ca2243-attribute-string-literals-should-parse-correctly"></a>CA2243: os literais da cadeia de caracteres de atributo devem ser analisados corretamente

|||
|-|-|
|NomeDoTipo|AttributeStringLiteralsShouldParseCorrectly|
|CheckId|CA2243|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Parâmetro literal de cadeia de caracteres de um atributo não é analisado corretamente para uma URL, GUID ou versão.

## <a name="rule-description"></a>Descrição da regra
 Uma vez que os atributos derivados <xref:System.Attribute?displayProperty=fullName>e os atributos são usados em tempo de compilação, somente valores constantes que podem ser passados para seus construtores. Parâmetros de atributo que devem representar URLs, GUIDs e as versões não podem ser digitados como <xref:System.Uri?displayProperty=fullName>, <xref:System.Guid?displayProperty=fullName>, e <xref:System.Version?displayProperty=fullName>, porque esses tipos não podem ser representados como constantes. Em vez disso, eles devem ser representados por cadeias de caracteres.

 Como o parâmetro é tipado como uma cadeia de caracteres, é possível que um parâmetro formatado incorretamente pode ser passado em tempo de compilação.

 Essa regra usa uma heurística de nomenclatura para localizar parâmetros que representam um uniform resource identifier (URI), um identificador de GUID (global exclusivo) ou uma versão e verifica se o valor passado está correto.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Altere a cadeia de caracteres do parâmetro para uma URL, GUID ou versão está formado corretamente.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra, se o parâmetro não representar uma URL, GUID ou versão.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra o código para o AssemblyFileVersionAttribute que viola essa regra.

 [!code-csharp[FxCop.Usage.AttributeStringLiteralsShouldParseCorrectly#1](../code-quality/codesnippet/CSharp/ca2243-attribute-string-literals-should-parse-correctly_1.cs)]

 A regra é acionada pelos seguintes parâmetros:

- Parâmetros que contêm 'version' e não podem ser analisados para Version.

- Parâmetros que contêm 'guid' e não podem ser analisados para GUID.

- Parâmetros que contêm 'uri', 'urn' ou 'url' e não podem ser analisados para System. URI.

## <a name="see-also"></a>Consulte também

- [CA1054: os parâmetros de URI não devem ser cadeias de caracteres](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)