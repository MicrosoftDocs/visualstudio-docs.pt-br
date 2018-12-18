---
title: 'CA1701: as palavras compostas da cadeia de caracteres do recurso devem ter maiúsculas e minúsculas corretas'
ms.date: 03/28/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ResourceStringCompoundWordsShouldBeCasedCorrectly
- CA1701
helpviewer_keywords:
- CA1701
- ResourceStringCompoundWordsShouldBeCasedCorrectly
ms.assetid: 4ddbe09f-24b8-4c47-9373-a06f4487ca0d
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ecc558cb9c069c19b545434afe0a851130fdb300
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31915651"
---
# <a name="ca1701-resource-string-compound-words-should-be-cased-correctly"></a>CA1701: as palavras compostas da cadeia de caracteres do recurso devem ter maiúsculas e minúsculas corretas

|||
|-|-|
|NomeDoTipo|ResourceStringCompoundWordsShouldBeCasedCorrectly|
|CheckId|CA1701|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Não recentes|

## <a name="cause"></a>Causa

Uma cadeia de caracteres de recurso contém uma palavra composta que parece não ter maiusculas e minúsculas corretamente.

## <a name="rule-description"></a>Descrição da regra

Cada palavra na cadeia de caracteres de recurso é dividida em tokens com base em maiusculas e minúsculas. Cada combinação contígua de dois tokens é verificada pela biblioteca do verificador ortográfico da Microsoft. Se reconhecidas, as palavras produzirão uma violação da regra. São exemplos de palavras compostas que causam uma violação de "CheckSum" e "MultiPart", que deve ter maiusculas e minúsculas como "Checksum" e "Multipart", respectivamente. Devido ao uso comum anterior, várias exceções são incorporadas a regra e várias palavras únicas são sinalizadas como "Ferramentas" e "Filename", que deve ter maiusculas e minúsculas como duas palavras diferentes. Neste exemplo, "Ferramentas" e "FileName" será sinalizado.

Convenções de nomenclatura fornecem uma aparência comum para bibliotecas de destino do common language runtime. Isso reduz a curva de aprendizado que é necessário para novas bibliotecas de software e aumenta a confiança do cliente que a biblioteca foi desenvolvida por uma pessoa com experiência em desenvolvimento de código gerenciado.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Altere a palavra para que ele é maiusculas e minúsculas corretas.

## <a name="change-the-dictionary-language"></a>Alterar o idioma do dicionário

Por padrão, a versão em inglês (en) do verificador ortográfico é usada. Se você quiser alterar o idioma do verificador ortográfico, você poderá fazê-lo adicionando um dos seguintes atributos para o *AssemblyInfo.cs* ou *AssemblyInfo* arquivo:

- Use <xref:System.Reflection.AssemblyCultureAttribute> para especificar a cultura se os recursos estão em um assembly satélite.
- Use <xref:System.Resources.NeutralResourcesLanguageAttribute> para especificar o *cultura neutra* do seu assembly se os recursos estão no mesmo assembly como o seu código.

> [!IMPORTANT]
> Se você definir a cultura para algo diferente de uma cultura baseada em inglês, esta regra de análise de código silenciosamente está desabilitada.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

É seguro suprimir um aviso de que essa regra se ambas as partes da palavra composta reconhecidas pelo dicionário de ortografia e a intenção é usar duas palavras.

Você também pode adicionar palavras compostas de um dicionário personalizado para o verificador ortográfico. Palavras no dicionário personalizado não causam violações. Para obter mais informações, consulte [como: personalizar o dicionário de análise de código](../code-quality/how-to-customize-the-code-analysis-dictionary.md).

## <a name="related-rules"></a>Regras relacionadas

- [CA1702: palavras compostas devem ter maiúsculas e minúsculas corretas](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)
- [CA1709: os identificadores devem ter maiúsculas e minúsculas corretas](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)
- [CA1708: os identificadores devem ser diferentes além de maiúsculas de minúsculas](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

## <a name="see-also"></a>Consulte também

- [Convenções de maiúsculas e minúsculas](/dotnet/standard/design-guidelines/capitalization-conventions)
- [Diretrizes de nomenclatura](/dotnet/standard/design-guidelines/naming-guidelines)