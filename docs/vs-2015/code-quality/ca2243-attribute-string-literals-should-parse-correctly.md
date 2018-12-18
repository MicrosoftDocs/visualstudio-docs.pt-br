---
title: 'CA2243: Literais de cadeia de caracteres de atributo devem ser analisados corretamente | Microsoft Docs'
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
- CA2243
- AttributeStringLiteralsShouldParseCorrectly
helpviewer_keywords:
- AttributeStringLiteralsShouldParseCorrectly
- CA2243
ms.assetid: bfadb366-379d-4ee4-b17b-c4a09bf1106b
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 3155006ecfc0e65365f23a6e09f6ec23e9d0e12d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49914730"
---
# <a name="ca2243-attribute-string-literals-should-parse-correctly"></a>CA2243: os literais da cadeia de caracteres de atributo devem ser analisados corretamente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|AttributeStringLiteralsShouldParseCorrectly|
|CheckId|CA2243|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Parâmetro literal de cadeia de caracteres de um atributo não é analisado corretamente para uma URL, GUID ou versão.

## <a name="rule-description"></a>Descrição da Regra
 Uma vez que os atributos derivados <xref:System.Attribute?displayProperty=fullName>e os atributos são usados em tempo de compilação, somente valores constantes que podem ser passados para seus construtores. Parâmetros de atributo que devem representar URLs, os GUIDs e as versões não podem ser digitados como <xref:System.Uri?displayProperty=fullName>, <xref:System.Guid?displayProperty=fullName>, e <xref:System.Version?displayProperty=fullName>, porque esses tipos não podem ser representados como constantes. Em vez disso, eles devem ser representados por cadeias de caracteres.

 Como o parâmetro é tipado como uma cadeia de caracteres, é possível que um parâmetro formatado incorretamente pode ser passado em tempo de compilação.

 Essa regra usa uma heurística de nomenclatura para localizar parâmetros que representam um uniform resource identifier (URI), um identificador de GUID (global exclusivo) ou uma versão e verifica se o valor passado está correto.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Altere a cadeia de caracteres do parâmetro para uma URL, GUID ou versão está formado corretamente.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, se o parâmetro não representar uma URL, GUID ou versão.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra o código para o AssemblyFileVersionAttribute que viola essa regra.

 [!code-csharp[FxCop.Usage.AttributeStringLiteralsShouldParseCorrectly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.AttributeStringLiteralsShouldParseCorrectly/cs/FxCop.Usage.AttributeStringLiteralsShouldParseCorrectly.cs#1)]

 A regra é disparada pelo seguinte:

-   Parâmetros que contêm 'version' e não podem ser analisados para Version.

-   Parâmetros que contêm 'guid' e não podem ser analisados para GUID.

-   Parâmetros que contêm 'uri', 'urn' ou 'url' e não podem ser analisados para System. URI.

## <a name="see-also"></a>Consulte também
 [CA1054: os parâmetros de URI não devem ser cadeias de caracteres](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)



