---
title: 'CA1702: palavras compostas devem ter maiúsculas e minúsculas corretas'
ms.date: 03/28/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1702
- CompoundWordsShouldBeCasedCorrectly
helpviewer_keywords:
- CA1702
- CompoundWordsShouldBeCasedCorrectly
ms.assetid: 05481245-7ad8-48c3-a456-3aa44b6160a6
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4703c43c81df13432f45fb4ba519a02b39a839e0
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31917837"
---
# <a name="ca1702-compound-words-should-be-cased-correctly"></a>CA1702: palavras compostas devem ter maiúsculas e minúsculas corretas

|||
|-|-|
|NomeDoTipo|CompoundWordsShouldBeCasedCorrectly|
|CheckId|CA1702|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Acionado quando a quebra em assemblies.<br /><br /> Não quebra - quando disparado em parâmetros de tipo.|

## <a name="cause"></a>Causa

O nome de um identificador contém várias palavras e pelo menos uma das palavras parece ser uma palavra composta que não tem maiúsculas corretas.

## <a name="rule-description"></a>Descrição da regra

O nome do identificador é dividido em palavras com base em maiusculas e minúsculas. Cada combinação de duas palavras contígua é verificada pela biblioteca do verificador ortográfico do Microsoft. Se ele for reconhecido, o identificador produz uma violação da regra. São exemplos de palavras compostas que causam uma violação de "CheckSum" e "MultiPart", que deve ter maiusculas e minúsculas como "Checksum" e "Multipart", respectivamente. Devido ao uso comum anterior, várias exceções são incorporadas a regra e várias palavras únicas são sinalizadas, como "Ferramentas" e "Filename", que devem ter maiusculas e minúsculas como duas palavras distintas (nesse caso, "Ferramentas" e "FileName").

Convenções de nomenclatura fornecem uma aparência comum para bibliotecas de destino do common language runtime. Isso reduz a curva de aprendizado que é necessário para novas bibliotecas de software e aumenta a confiança do cliente que a biblioteca foi desenvolvida por uma pessoa com experiência em desenvolvimento de código gerenciado.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Altere o nome para que ele é maiusculas e minúsculas corretas.

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

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

É seguro suprimir um aviso de que essa regra se ambas as partes da palavra composta reconhecidas pelo dicionário de ortografia e a intenção é usar duas palavras.

## <a name="related-rules"></a>Regras relacionadas

- [CA1701: as palavras compostas da cadeia de caracteres de recurso devem ter maiúsculas e minúsculas corretas](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md)
- [CA1709: os identificadores devem ter maiúsculas e minúsculas corretas](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)
- [CA1708: os identificadores devem ser diferentes além de maiúsculas de minúsculas](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

## <a name="see-also"></a>Consulte também

- [Diretrizes de nomenclatura](/dotnet/standard/design-guidelines/naming-guidelines)
- [Convenções de maiúsculas e minúsculas](/dotnet/standard/design-guidelines/capitalization-conventions)