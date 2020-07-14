---
title: 'CA2234: passe objetos System. Uri em vez de cadeias de caracteres | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PassSystemUriObjectsInsteadOfStrings
- CA2234
helpviewer_keywords:
- CA2234
- PassSystemUriObjectsInsteadOfStrings
ms.assetid: 14616b37-74c4-4286-b051-115d00aceb5f
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0ce5c076260886def089118a4d7211d75e0185c0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545204"
---
# <a name="ca2234-pass-systemuri-objects-instead-of-strings"></a>CA2234: Passar objetos System.Uri em vez de cadeias de caracteres
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|PassSystemUriObjectsInsteadOfStrings|
|CheckId|CA2234|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 É feita uma chamada a um método que tem um parâmetro de cadeia de caracteres cujo nome contém "URI", "URI", "urn", "urn", "URL" ou "URL"; e o tipo declarativo do método contém uma sobrecarga de método correspondente que tem um <xref:System.Uri?displayProperty=fullName> parâmetro.

## <a name="rule-description"></a>Descrição da Regra
 Um nome de parâmetro é dividido em tokens com base na Convenção do camel case e, em seguida, cada token é verificado para ver se ele é igual a "URI", "URI", "urn", "urn", "URL" ou "URL". Se houver uma correspondência, presume-se que o parâmetro represente um URI (Uniform Resource Identifier). Uma representação de cadeia de caracteres de um URI está propensa a erros de análise e de codificação, e pode resultar em vulnerabilidades de segurança. A <xref:System.Uri> classe fornece esses serviços de maneira segura e segura. Quando há uma opção entre duas sobrecargas que diferem apenas em relação à representação de um URI, o usuário deve escolher a sobrecarga que usa um <xref:System.Uri> argumento.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, chame a sobrecarga que usa o <xref:System.Uri> argumento.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se o parâmetro da cadeia de caracteres não representar um URI.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método, `ErrorProne` , que viola a regra e um método, `SaferWay` , que chama corretamente a <xref:System.Uri> sobrecarga.

 [!code-cpp[FxCop.Usage.PassUri#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.PassUri/cpp/FxCop.Usage.PassUri.cpp#1)]
 [!code-csharp[FxCop.Usage.PassUri#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.PassUri/cs/FxCop.Usage.PassUri.cs#1)]
 [!code-vb[FxCop.Usage.PassUri#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.PassUri/vb/FxCop.Usage.PassUri.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1057: Sobrecargas de URI da cadeia de caracteres chamam sobrecargas System.Uri](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)

 [CA1056: Propriedades de URI não devem ser cadeias de caracteres](../code-quality/ca1056-uri-properties-should-not-be-strings.md)

 [CA1054: Parâmetros de URI não devem ser cadeias de caracteres](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)

 [CA1055: Valores de retorno de URI não devem ser cadeias de caracteres](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)
