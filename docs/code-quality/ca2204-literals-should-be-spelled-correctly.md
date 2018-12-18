---
title: 'CA2204: os literais do recurso devem ter a ortografia correta'
ms.date: 03/28/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6f86658978a105c1fa4f3c4602b5c838f4c80726
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31918417"
---
# <a name="ca2204-literals-should-be-spelled-correctly"></a>CA2204: os literais do recurso devem ter a ortografia correta

|||
|-|-|
|NomeDoTipo|LiteralsShouldBeSpelledCorrectly|
|CheckId|CA2204|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separáveis|

## <a name="cause"></a>Causa

Uma cadeia de caracteres literal é passada como um argumento para um parâmetro localizável, ou a uma propriedade localizável, e a cadeia de caracteres contém uma ou mais palavras que não são reconhecidas pela biblioteca do verificador ortográfico do Microsoft.

## <a name="rule-description"></a>Descrição da regra

Esta regra verifica se uma cadeia de caracteres literal que é passada como um valor para um parâmetro ou a propriedade quando um ou mais dos casos a seguir forem verdadeiras:

- O <xref:System.ComponentModel.LocalizableAttribute> atributo do parâmetro ou propriedade é definido como true.

- O nome de parâmetro ou a propriedade contém "Text", "Mensagem" ou "Legenda".

- O nome da variável de cadeia de caracteres que é passada para um <xref:System.Console.Write%2A> ou <xref:System.Console.WriteLine> método é "valor" ou "formato".

Esta regra analisa a cadeia de caracteres literal em palavras, tokens palavras compostas e verifica a ortografia de cada palavra ou token. Para obter informações sobre o algoritmo de análise, consulte [CA1704: os identificadores devem ser grafados corretamente](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md).

## <a name="language"></a>Idioma

O verificador ortográfico verifica atualmente apenas em dicionários de cultura baseada em inglês. Você pode alterar a cultura do seu projeto no arquivo de projeto, adicionando o **CodeAnalysisCulture** elemento.

Por exemplo:

```xml
<Project ...>
  <PropertyGroup>
    <CodeAnalysisCulture>en-AU</CodeAnalysisCulture>
```

> [!IMPORTANT]
> Se você definir a cultura para algo diferente de uma cultura baseada em inglês, esta regra de análise de código silenciosamente está desabilitada.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação desta regra, corrija a ortografia da palavra ou adicionar a palavra ao dicionário personalizado. Para obter informações sobre como usar os dicionários personalizados, consulte [como: personalizar o dicionário de análise de código](../code-quality/how-to-customize-the-code-analysis-dictionary.md).

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Não suprima um aviso nessa regra. Corretamente palavras reduzem a curva de aprendizado necessária para novas bibliotecas de software.

## <a name="related-rules"></a>Regras relacionadas

- [CA1704: os identificadores devem ter a ortografia correta](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)
- [CA1703: as cadeias de caracteres do recurso devem ter a ortografia correta](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)