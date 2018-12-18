---
title: 'CA2234: passar objetos System.Uri em vez de cadeias de caracteres'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PassSystemUriObjectsInsteadOfStrings
- CA2234
helpviewer_keywords:
- CA2234
- PassSystemUriObjectsInsteadOfStrings
ms.assetid: 14616b37-74c4-4286-b051-115d00aceb5f
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: fcc7994e67e268aff21af925632d2ee9cf102ff4
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45547149"
---
# <a name="ca2234-pass-systemuri-objects-instead-of-strings"></a>CA2234: passar objetos System.Uri em vez de cadeias de caracteres

|||
|-|-|
|NomeDoTipo|PassSystemUriObjectsInsteadOfStrings|
|CheckId|CA2234|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 É feita uma chamada para um método que tem um parâmetro de cadeia de caracteres cujo nome contém "uri", "Uri", "urn", "Urn", "url" ou "Url"; e o tipo de declaração do método contém uma sobrecarga do método correspondente que tenha um <xref:System.Uri?displayProperty=fullName> parâmetro.

## <a name="rule-description"></a>Descrição da regra
 Um nome de parâmetro é dividido em tokens com base na convenção camel case e, em seguida, cada token é verificado para ver se é igual a "uri", "Uri", "urn", "Urn", "url" ou "Url". Se houver uma correspondência, o parâmetro será assumido para representar um uniform resource identifier (URI). Uma representação de cadeia de caracteres de um URI está propensa a erros de análise e de codificação, e pode resultar em vulnerabilidades de segurança. O <xref:System.Uri> classe fornece esses serviços de maneira segura e protegida. Quando há uma escolha entre duas sobrecargas que diferem apenas em relação a representação de um URI, o usuário deve escolher a sobrecarga que utiliza um <xref:System.Uri> argumento.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, chame a sobrecarga que utiliza o <xref:System.Uri> argumento.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra, se o parâmetro de cadeia de caracteres não representa um URI.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método `ErrorProne`, que viola a regra e um método `SaferWay`, que chama corretamente o <xref:System.Uri> de sobrecarga.

 [!code-vb[FxCop.Usage.PassUri#1](../code-quality/codesnippet/VisualBasic/ca2234-pass-system-uri-objects-instead-of-strings_1.vb)]
 [!code-cpp[FxCop.Usage.PassUri#1](../code-quality/codesnippet/CPP/ca2234-pass-system-uri-objects-instead-of-strings_1.cpp)]
 [!code-csharp[FxCop.Usage.PassUri#1](../code-quality/codesnippet/CSharp/ca2234-pass-system-uri-objects-instead-of-strings_1.cs)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1057: as sobrecargas de URI da cadeia de caracteres chamam sobrecargas System.Uri](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)

 [CA1056: as propriedades de URI não devem ser cadeias de caracteres](../code-quality/ca1056-uri-properties-should-not-be-strings.md)

 [CA1054: os parâmetros de URI não devem ser cadeias de caracteres](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)

 [CA1055: os valores de retorno de URI não devem ser cadeias de caracteres](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)