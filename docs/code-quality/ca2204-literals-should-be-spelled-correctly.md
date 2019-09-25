---
title: 'CA2204: Literais devem ser escritos corretamente'
ms.date: 03/28/2018
ms.topic: reference
f1_keywords:
- Literals should be spelled correctly
- CA2204
- LiteralsShouldBeSpelledCorrectly
helpviewer_keywords:
- CA2204
ms.assetid: b0bbcbb6-c92d-4c14-8ef7-9c8b38c791a6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6763fd9f8999bd590511026f6571db6a747c43bc
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231850"
---
# <a name="ca2204-literals-should-be-spelled-correctly"></a>CA2204: Literais devem ser escritos corretamente

|||
|-|-|
|NomeDoTipo|LiteralsShouldBeSpelledCorrectly|
|CheckId|CA2204|
|Categoria|Microsoft.Usage|
|Alteração significativa|Sem interrupção|

## <a name="cause"></a>Causa

Uma cadeia de caracteres literal é passada como um argumento para um parâmetro localizável, ou para uma propriedade localizável, e a cadeia de caracteres contém uma ou mais palavras que não são reconhecidas pela biblioteca do verificador ortográfico da Microsoft.

## <a name="rule-description"></a>Descrição da regra

Essa regra verifica uma cadeia de caracteres literal que é passada como um valor para um parâmetro ou propriedade quando um ou mais dos seguintes casos é verdadeiro:

- O <xref:System.ComponentModel.LocalizableAttribute> atributo do parâmetro ou da propriedade é definido como true.

- O nome do parâmetro ou da propriedade contém "texto", "mensagem" ou "legenda".

- O nome da variável de cadeia de caracteres que é passada <xref:System.Console.Write%2A> para <xref:System.Console.WriteLine> um método ou é "value" ou "Format".

Essa regra analisa a cadeia de caracteres literal em palavras, a geração de tokens de palavras compostas e verifica a ortografia de cada palavra ou token. Para obter informações sobre o algoritmo de análise, [consulte CA1704: Os identificadores devem ser escritos](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)corretamente.

## <a name="language"></a>Idioma

Atualmente, o verificador ortográfico verifica apenas os dicionários de cultura baseados em inglês. Você pode alterar a cultura do seu projeto no arquivo de projeto, adicionando o elemento **CodeAnalysisCulture** .

Por exemplo:

```xml
<Project ...>
  <PropertyGroup>
    <CodeAnalysisCulture>en-AU</CodeAnalysisCulture>
```

> [!IMPORTANT]
> Se você definir a cultura como algo diferente de uma cultura baseada em inglês, essa regra de análise de código será silenciosamente desabilitada.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, corrija a grafia da palavra ou adicione a palavra a um dicionário personalizado. Para obter informações sobre como usar dicionários personalizados, [consulte Como: Personalize o dicionário](../code-quality/how-to-customize-the-code-analysis-dictionary.md)de análise de código.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Não suprima um aviso nessa regra. Palavras escritas corretamente reduzem a curva de aprendizado necessária para novas bibliotecas de software.

## <a name="related-rules"></a>Regras relacionadas

- [CA1704: Os identificadores devem ser escritos corretamente](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)
- [CA1703: As cadeias de caracteres de recurso devem ser digitadas corretamente](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)