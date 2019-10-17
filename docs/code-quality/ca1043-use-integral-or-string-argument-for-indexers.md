---
title: 'CA1043: usar argumento integral ou da cadeia de caracteres para indexadores'
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1043
- UseIntegralOrStringArgumentForIndexers
helpviewer_keywords:
- CA1043
- UseIntegralOrStringArgumentForIndexers
ms.assetid: d7f14b9e-2220-4f80-b6b8-48c655a05701
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 10424344abc52d4911b7caf60e02b03e6ed6e96f
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72446629"
---
# <a name="ca1043-use-integral-or-string-argument-for-indexers"></a>CA1043: usar argumento integral ou da cadeia de caracteres para indexadores

|||
|-|-|
|NomeDoTipo|UseIntegralOrStringArgumentForIndexers|
|CheckId|CA1043|
|Categoria|Microsoft. Design|
|Alteração significativa|Quebra|

## <a name="cause"></a>Causa

Um tipo contém um indexador que usa um tipo de índice diferente de <xref:System.Int32?displayProperty=fullName>, <xref:System.Int64?displayProperty=fullName>, <xref:System.Object?displayProperty=fullName> ou <xref:System.String?displayProperty=fullName>.

Por padrão, essa regra só examina os tipos público e protegido, mas isso é [configurável](#configurability).

## <a name="rule-description"></a>Descrição da regra

Indexadores, ou seja, propriedades indexadas, devem usar tipos inteiros ou de cadeia de caracteres para o índice. Esses tipos são normalmente usados para indexar estruturas de dados e aumentar a usabilidade da biblioteca. O uso do tipo <xref:System.Object> deve ser restrito a esses casos em que o inteiro ou o tipo de cadeia de caracteres específico não pode ser especificado em tempo de design. Se o design exigir outros tipos para o índice, reconsidere se o tipo representa um armazenamento de dados lógico. Se não representar um armazenamento de dados lógico, use um método.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, altere o índice para um tipo inteiro ou de cadeia de caracteres ou use um método em vez do indexador.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Suprimir um aviso desta regra somente após considerar atentamente a necessidade do indexador não padrão.

## <a name="configurability"></a>Configurabilidade

Se você estiver executando essa regra por meio de [analisadores do FxCop](install-fxcop-analyzers.md) (e não com a análise herdada), poderá configurar em quais partes de sua base de código executar essa regra, com base em sua acessibilidade. Por exemplo, para especificar que a regra deve ser executada somente na superfície da API não pública, adicione o seguinte par chave-valor a um arquivo. editorconfig em seu projeto:

```ini
dotnet_code_quality.ca1043.api_surface = private, internal
```

Você pode configurar essa opção apenas para essa regra, para todas as regras ou para todas as regras nesta categoria (Design). Para obter mais informações, consulte [Configurar analisadores de FxCop](configure-fxcop-analyzers.md).

## <a name="example"></a>Exemplo

O exemplo a seguir mostra um indexador que usa um índice <xref:System.Int32>.

[!code-csharp[FxCop.Design.IntegralOrStringIndexers#1](../code-quality/codesnippet/CSharp/ca1043-use-integral-or-string-argument-for-indexers_1.cs)]
[!code-cpp[FxCop.Design.IntegralOrStringIndexers#1](../code-quality/codesnippet/CPP/ca1043-use-integral-or-string-argument-for-indexers_1.cpp)]
[!code-vb[FxCop.Design.IntegralOrStringIndexers#1](../code-quality/codesnippet/VisualBasic/ca1043-use-integral-or-string-argument-for-indexers_1.vb)]

## <a name="related-rules"></a>Regras relacionadas

- [CA1023: os indexadores não devem ser multidimensionais](../code-quality/ca1023-indexers-should-not-be-multidimensional.md)
- [CA1024: usar propriedades quando apropriado](../code-quality/ca1024-use-properties-where-appropriate.md)
