---
title: 'CA1057: sobrecargas de URI de cadeia de caracteres chamam sobrecargas de System. URI | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1057
- StringUriOverloadsCallSystemUriOverloads
helpviewer_keywords:
- StringUriOverloadsCallSystemUriOverloads
- CA1057
ms.assetid: ef1e983e-9ca7-404b-82d7-65740ba0ce20
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: bcdb4d8333b0a4d2d06580d882cf736d4527eca4
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539523"
---
# <a name="ca1057-string-uri-overloads-call-systemuri-overloads"></a>CA1057: Sobrecargas de URI da cadeia de caracteres chamam sobrecargas System.Uri
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|StringUriOverloadsCallSystemUriOverloads|
|CheckId|CA1057|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo declara sobrecargas de método que diferem apenas pela substituição de um parâmetro de cadeia de caracteres por um <xref:System.Uri?displayProperty=fullName> parâmetro, e a sobrecarga que usa o parâmetro de cadeia de caracteres não chama a sobrecarga que usa o <xref:System.Uri> parâmetro.

## <a name="rule-description"></a>Descrição da Regra
 Como as sobrecargas diferem somente pela cadeia de caracteres/ <xref:System.Uri> parâmetro, presume-se que a cadeia de caracteres represente um URI (Uniform Resource Identifier). Uma representação de cadeia de caracteres de um URI está propensa a erros de análise e de codificação, e pode resultar em vulnerabilidades de segurança. A <xref:System.Uri> classe fornece esses serviços de maneira segura e segura. Para colher os benefícios da <xref:System.Uri> classe, a sobrecarga da cadeia de caracteres deve chamar a <xref:System.Uri> sobrecarga usando o argumento string.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Reimplemente o método que usa a representação de cadeia de caracteres do URI para que ele crie uma instância da <xref:System.Uri> classe usando o argumento string e, em seguida, passe o <xref:System.Uri> objeto para a sobrecarga que tem o <xref:System.Uri> parâmetro.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se o parâmetro da cadeia de caracteres não representar um URI.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma sobrecarga de cadeia de caracteres implementada corretamente.

 [!code-cpp[FxCop.Design.CallUriOverload#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.CallUriOverload/cpp/FxCop.Design.CallUriOverload.cpp#1)]
 [!code-csharp[FxCop.Design.CallUriOverload#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CallUriOverload/cs/FxCop.Design.CallUriOverload.cs#1)]
 [!code-vb[FxCop.Design.CallUriOverload#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.CallUriOverload/vb/FxCop.Design.CallUriOverload.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2234: Passar objetos System.Uri em vez de cadeias de caracteres](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)

 [CA1056: Propriedades de URI não devem ser cadeias de caracteres](../code-quality/ca1056-uri-properties-should-not-be-strings.md)

 [CA1054: Parâmetros de URI não devem ser cadeias de caracteres](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)

 [CA1055: Valores de retorno de URI não devem ser cadeias de caracteres](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)
