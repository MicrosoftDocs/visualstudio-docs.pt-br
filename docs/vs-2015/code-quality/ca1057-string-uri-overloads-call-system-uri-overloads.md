---
title: 'Ca1057 as: Cadeia de caracteres chamam sobrecargas System. URI | Microsoft Docs'
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
- CA1057
- StringUriOverloadsCallSystemUriOverloads
helpviewer_keywords:
- StringUriOverloadsCallSystemUriOverloads
- CA1057
ms.assetid: ef1e983e-9ca7-404b-82d7-65740ba0ce20
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: e948e91a0559034e688e029eb5ba227a8dd343c2
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49920502"
---
# <a name="ca1057-string-uri-overloads-call-systemuri-overloads"></a>CA1057: as sobrecargas de URI da cadeia de caracteres chamam sobrecargas System.Uri
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|StringUriOverloadsCallSystemUriOverloads|
|CheckId|CA1057|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um tipo declara sobrecargas de método que diferem apenas pela substituição de um parâmetro de cadeia de caracteres com um <xref:System.Uri?displayProperty=fullName> parâmetro e a sobrecarga que utiliza o parâmetro de cadeia de caracteres não chama a sobrecarga que utiliza o <xref:System.Uri> parâmetro.

## <a name="rule-description"></a>Descrição da Regra
 Como as sobrecargas diferem apenas pela cadeia de caracteres /<xref:System.Uri> parâmetro, a cadeia de caracteres deve para representar um uniform resource identifier (URI). Uma representação de cadeia de caracteres de um URI está propensa a erros de análise e de codificação, e pode resultar em vulnerabilidades de segurança. O <xref:System.Uri> classe fornece esses serviços de maneira segura e protegida. Para obter os benefícios do <xref:System.Uri> classe, a sobrecarga de cadeia de caracteres deve chamar o <xref:System.Uri> usando o argumento de cadeia de caracteres de sobrecarga.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Reimplementar o método que usa a representação de cadeia de caracteres do URI para que ele cria uma instância das <xref:System.Uri> usando o argumento de cadeia de caracteres de classe e, em seguida, passa a <xref:System.Uri> objeto para a sobrecarga que tenha o <xref:System.Uri> parâmetro.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, se o parâmetro de cadeia de caracteres não representa um URI.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma sobrecarga de cadeia de caracteres implementado corretamente.

 [!code-cpp[FxCop.Design.CallUriOverload#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.CallUriOverload/cpp/FxCop.Design.CallUriOverload.cpp#1)]
 [!code-csharp[FxCop.Design.CallUriOverload#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CallUriOverload/cs/FxCop.Design.CallUriOverload.cs#1)]
 [!code-vb[FxCop.Design.CallUriOverload#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.CallUriOverload/vb/FxCop.Design.CallUriOverload.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2234: passar objetos System.Uri em vez de cadeias de caracteres](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)

 [CA1056: as propriedades de URI não devem ser cadeias de caracteres](../code-quality/ca1056-uri-properties-should-not-be-strings.md)

 [CA1054: os parâmetros de URI não devem ser cadeias de caracteres](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)

 [CA1055: os valores de retorno de URI não devem ser cadeias de caracteres](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)



