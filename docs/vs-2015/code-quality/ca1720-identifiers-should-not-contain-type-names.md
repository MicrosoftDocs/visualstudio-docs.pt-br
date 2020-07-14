---
title: 'CA1720: identificadores não devem conter nomes de tipo | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1720
- IdentifiersShouldNotContainTypeNames
helpviewer_keywords:
- IdentifiersShouldNotContainTypeNames
- CA1720
ms.assetid: c95ee48f-f23a-45f0-ac9e-a3c1ecfabdea
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f6d228b0fbf5507ba135f9ddc35d6d8b161f0011
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534843"
---
# <a name="ca1720-identifiers-should-not-contain-type-names"></a>CA1720: Identificadores não devem conter nomes de tipos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|IdentifiersShouldNotContainTypeNames|
|CheckId|CA1720|
|Categoria|Microsoft. Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 O nome de um parâmetro em um membro visível externamente contém um nome de tipo de dados.

 -ou-

 O nome de um membro visível externamente contém um nome de tipo de dados específico a um idioma.

## <a name="rule-description"></a>Descrição da Regra
 Os nomes de parâmetros e membros são mais usados para comunicar seu significado do que descrever seu tipo, que deve ser fornecido pelas ferramentas de desenvolvimento. Para nomes de membros, se um nome de tipo de dados precisar ser usado, use um nome independente de idioma em vez de um idioma específico. Por exemplo, em vez do nome do tipo C# "int", use o nome do tipo de dados independente de linguagem, Int32.

 Cada token discreto no nome do parâmetro ou membro é verificado em relação aos seguintes nomes de tipo de dados específicos de idioma, de maneira não diferencia maiúsculas de minúsculas:

- Bool

- WChar

- Int8

- UInt8

- Short

- UShort

- Int

- UInt

- Integer

- UInteger

- long

- ULong

- Não assinado

- Com sinal

- Float

- Float32

- Float64

  Além disso, os nomes de um parâmetro também são verificados em relação aos seguintes nomes de tipos de dados independentes de idioma, de maneira não diferencia maiúsculas de minúsculas:

- Objeto

- Obj

- Boolean

- Char

- String

- SByte

- Byte

- UByte

- Int16

- UInt16

- Int32

- UInt32

- Int64

- UInt64

- IntPtr

- PTR

- Ponteiro

- UInptr

- UPtr

- UPointer

- Single

- Double

- Decimal

- Guid

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 **Se for acionado em um parâmetro:**

 Substitua o identificador de tipo de dados no nome do parâmetro por um termo que melhor descreva seu significado ou um termo mais genérico, como ' value '.

 **Se for acionado em relação a um membro:**

 Substitua o identificador de tipo de dados específico do idioma no nome do membro por um termo que melhor descreva seu significado, um equivalente independente de idioma ou um termo mais genérico, como ' value '.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 O uso ocasional do parâmetro baseado em tipo e dos nomes de membros pode ser apropriado. No entanto, para o novo desenvolvimento, nenhum cenário conhecido ocorre onde você deve suprimir um aviso dessa regra. Para bibliotecas que foram enviadas anteriormente, talvez seja necessário suprimir um aviso dessa regra.

## <a name="related-rules"></a>Regras relacionadas
 [CA1709: Identificadores devem ter maiúsculas e minúsculas corretas](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708: Identificadores devem ser diferentes em algo além das maiúsculas e minúsculas](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

 [CA1707: Identificadores não devem conter sublinhados](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)

 [CA1719: Nomes de parâmetros não devem corresponder a nomes de membros](../code-quality/ca1719-parameter-names-should-not-match-member-names.md)
