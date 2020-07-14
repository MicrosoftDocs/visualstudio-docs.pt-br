---
title: 'CA1032: Implementar construtores de exceção padrão | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1032
- ImplementStandardExceptionConstructors
helpviewer_keywords:
- CA1032
- ImplementStandardExceptionConstructors
ms.assetid: a8623c56-273a-4c95-8d83-95911a042be7
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 61b0157200ddff4cb8335118b30832a0c8950f65
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542279"
---
# <a name="ca1032-implement-standard-exception-constructors"></a>CA1032: Implementar construtores de exceção padrão
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ImplementStandardExceptionConstructors|
|CheckId|CA1032|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo é ampliado <xref:System.Exception?displayProperty=fullName> e não declara todos os construtores necessários.

## <a name="rule-description"></a>Descrição da Regra
 Os tipos de exceção devem implementar os seguintes construtores:

- NewException público ()

- NewException público (cadeia de caracteres)

- NewException público (cadeia de caracteres, exceção)

- NewException protegidos ou privados (SerializationInfo, StreamingContext)

  Deixar de fornecer o conjunto completo de construtores pode dificultar o tratamento correto das exceções. Por exemplo, o construtor que tem a assinatura `NewException(string, Exception)` é usado para criar exceções que são causadas por outras exceções. Sem esse construtor, você não pode criar e lançar uma instância de sua exceção personalizada que contém uma exceção interna (aninhada), que é o código gerenciado que deve ser feito nessa situação. Os três primeiros construtores de exceção são públicos por convenção. O quarto construtor é protegido em classes sem lacre e privado em classes lacradas. Para obter mais informações, consulte [CA2229: implemente construtores de serialização](../code-quality/ca2229-implement-serialization-constructors.md)

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, adicione os construtores ausentes à exceção e verifique se eles têm a acessibilidade correta.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra quando a violação é causada pelo uso de um nível de acesso diferente para os construtores públicos.

## <a name="example"></a>Exemplo
 O exemplo a seguir contém um tipo de exceção que viola essa regra e um tipo de exceção que é implementado corretamente.

 [!code-csharp[FxCop.Design.ExceptionMultipleCtors#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionMultipleCtors/cs/FxCop.Design.ExceptionMultipleCtors.cs#1)]
