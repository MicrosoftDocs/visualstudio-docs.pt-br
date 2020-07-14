---
title: 'CA1701: as palavras compostas da cadeia de recursos devem estar em maiúsculas e minúsculas Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ResourceStringCompoundWordsShouldBeCasedCorrectly
- CA1701
helpviewer_keywords:
- CA1701
- ResourceStringCompoundWordsShouldBeCasedCorrectly
ms.assetid: 4ddbe09f-24b8-4c47-9373-a06f4487ca0d
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 7c1c3b0fd6cf3a25d5db9e3039d4dc5d8364a18e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544099"
---
# <a name="ca1701-resource-string-compound-words-should-be-cased-correctly"></a>CA1701: Palavras compostas de cadeia de caracteres de recurso devem ter maiúsculas e minúsculas corretas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ResourceStringCompoundWordsShouldBeCasedCorrectly|
|CheckId|CA1701|
|Categoria|Microsoft. Naming|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Uma cadeia de caracteres de recurso contém uma palavra composta que não parece estar em maiúsculas corretamente.

## <a name="rule-description"></a>Descrição da Regra
 Cada palavra na cadeia de caracteres de recurso é dividida em tokens baseados em maiúsculas e minúsculas. Cada combinação contígua de dois tokens é verificada pela biblioteca do verificador ortográfico da Microsoft. Se reconhecidas, as palavras produzirão uma violação da regra. Exemplos de palavras compostas que causam uma violação são "CheckSum" e "MultiPart", que devem ser totais como "Checksum" e "multipart", respectivamente. Devido ao uso comum anterior, várias exceções são incorporadas à regra, e várias palavras únicas são sinalizadas, como "Toolbar" e "filename", que devem ser maiúsculas e minúsculas como duas palavras distintas. Neste exemplo, "ToolBar" e "FileName" seriam sinalizados.

 As convenções de nomenclatura fornecem uma aparência comum para as bibliotecas direcionadas ao Common Language Runtime. Isso reduz a curva de aprendizado necessária para novas bibliotecas de software e aumenta a confiança do cliente de que a biblioteca foi desenvolvida por alguém que tenha experiência no desenvolvimento de código gerenciado.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Altere a palavra de forma que ela fique correta.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se ambas as partes da palavra composta forem reconhecidas pelo dicionário ortográfico e a intenção for usar duas palavras.

 Você também pode adicionar palavras compostas a um dicionário personalizado para o verificador ortográfico. As palavras no dicionário personalizado não causam violações. Para obter mais informações, consulte [como: personalizar o dicionário de análise de código](../code-quality/how-to-customize-the-code-analysis-dictionary.md).

## <a name="related-rules"></a>Regras relacionadas
 [CA1702: Palavras compostas devem ter maiúsculas e minúsculas corretas](../code-quality/ca1702-compound-words-should-be-cased-correctly.md)

 [CA1709: Identificadores devem ter maiúsculas e minúsculas corretas](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708: Identificadores devem ser diferentes em algo além das maiúsculas e minúsculas](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

## <a name="see-also"></a>Consulte Também
 [Diretrizes de nomenclatura](https://msdn.microsoft.com/library/fc076d66-9b5f-42d3-aa65-61d970c794a3) de [convenções de capitalização](https://msdn.microsoft.com/library/4c4ea526-9203-486f-b72d-29d61c5b3c6d)
