---
title: 'CA1054: os parâmetros de URI não devem ser cadeias de caracteres | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1054
- UriParametersShouldNotBeStrings
helpviewer_keywords:
- CA1054
- UriParametersShouldNotBeStrings
ms.assetid: 8e99d72b-a658-47a7-8dd5-9784ce2c30b8
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: babef652bbfa55d6549cf0e43ddae0920b3ff302
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539484"
---
# <a name="ca1054-uri-parameters-should-not-be-strings"></a>CA1054: Parâmetros de URI não devem ser cadeias de caracteres
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|UriParametersShouldNotBeStrings|
|CheckId|CA1054|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo declara um método com um parâmetro de cadeia de caracteres cujo nome contém "URI", "URI", "urn", "urn", "URL" ou "URL" e o tipo não declara uma sobrecarga correspondente que usa um <xref:System.Uri?displayProperty=fullName> parâmetro.

## <a name="rule-description"></a>Descrição da Regra
 Essa regra divide o nome do parâmetro em tokens com base na Convenção do camel case e verifica se cada token é igual a "URI", "URI", "urn", "urn", "URL" ou "URL". Se houver uma correspondência, a regra assumirá que o parâmetro representa um URI (Uniform Resource Identifier). Uma representação de cadeia de caracteres de um URI está propensa a erros de análise e de codificação, e pode resultar em vulnerabilidades de segurança. Se um método usa uma representação de cadeia de caracteres de um URI, deve ser fornecida uma sobrecarga correspondente que usa uma instância da <xref:System.Uri> classe, que fornece esses serviços de maneira segura e segura.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, altere o parâmetro para um <xref:System.Uri> tipo; essa é uma alteração significativa. Como alternativa, forneça uma sobrecarga do método que usa um <xref:System.Uri> parâmetro; esta é uma alteração sem interrupção.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se o parâmetro não representar um URI.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo, `ErrorProne` , que viola essa regra e um tipo, `SaferWay` , que satisfaz a regra.

 [!code-cpp[FxCop.Design.UriNotString#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.UriNotString/cpp/FxCop.Design.UriNotString.cpp#1)]
 [!code-csharp[FxCop.Design.UriNotString#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.UriNotString/cs/FxCop.Design.UriNotString.cs#1)]
 [!code-vb[FxCop.Design.UriNotString#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.UriNotString/vb/FxCop.Design.UriNotString.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1056: Propriedades de URI não devem ser cadeias de caracteres](../code-quality/ca1056-uri-properties-should-not-be-strings.md)

 [CA1055: Valores de retorno de URI não devem ser cadeias de caracteres](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)

 [CA2234: Passar objetos System.Uri em vez de cadeias de caracteres](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)

 [CA1057: Sobrecargas de URI da cadeia de caracteres chamam sobrecargas System.Uri](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)
