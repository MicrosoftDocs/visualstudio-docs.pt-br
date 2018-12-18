---
title: 'CA1720: os identificadores não devem conter nomes de tipo'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1720
- IdentifiersShouldNotContainTypeNames
helpviewer_keywords:
- IdentifiersShouldNotContainTypeNames
- CA1720
ms.assetid: c95ee48f-f23a-45f0-ac9e-a3c1ecfabdea
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 32abf9a2c11a8381b5f204a2388a85f7fd5d8230
ms.sourcegitcommit: 1abb9cf4c3ccb90e3481ea8079272c98aad12875
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50143119"
---
# <a name="ca1720-identifiers-should-not-contain-type-names"></a>CA1720: os identificadores não devem conter nomes de tipo

|||
|-|-|
|NomeDoTipo|IdentifiersShouldNotContainTypeNames|
|CheckId|CA1720|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 O nome de um parâmetro em um membro visível externamente contém um nome de tipo de dados.

 -ou-

 O nome de um membro visível externamente contém um nome de tipo de dados específicos de idioma.

## <a name="rule-description"></a>Descrição da regra
 Nomes de parâmetros e membros são melhor usados para se comunicar seu significado que to descrevem seu tipo, que deve ser fornecido pelas ferramentas de desenvolvimento. Para nomes de membros, se um nome de tipo de dados deve ser usado, usam um nome independente de linguagem em vez de um idioma específico. Por exemplo, em vez do c# tipo nome 'int', use o nome do tipo de dados independente de idioma, Int32.

 Cada token discreto no nome do parâmetro ou membro é verificado em relação os seguintes nomes de tipo de dados específicos de idioma, no diferenciando maiusculas de minúsculas:

- Bool

- WChar

- Int8

- UInt8

- Abreviado

- UShort

- int

- UInt

- Inteiro

- UInteger

- Long

- ULong

- Não assinado

- Assinado

- Float

- float32

- float64

Além disso, os nomes de um parâmetro também são verificados em relação os seguintes nomes de tipo de dados independente de idioma, diferenciando maiusculas de minúsculas:

- Objeto

- obj

- Boolean

- Char

- Cadeia de Caracteres

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

- Simples

- Duplo

- Decimal

- Guid

## <a name="how-to-fix-violations"></a>Como corrigir violações
 **Se disparado em relação a um parâmetro:**

 Substitua o identificador de tipo de dados no nome do parâmetro com um termo que melhor descreve seu significado ou um termo mais genérico, como 'value'.

 **Se disparado em relação a um membro:**

 Substitua o identificador de tipo de dados específicos de idioma no nome do membro com um termo que melhor descreve seu significado, um equivalente independente da linguagem ou um termo mais genérico, como 'value'.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Uso ocasional de nomes de parâmetro e de membros com base no tipo pode ser apropriado. No entanto, para novos desenvolvimentos, nenhum conhecidos ocorrem de cenários em que você deve suprimir um aviso nessa regra. Para bibliotecas que foram enviados anteriormente, você pode ter que suprimir um aviso nessa regra.

## <a name="related-rules"></a>Regras relacionadas
 [CA1709: os identificadores devem ter maiúsculas e minúsculas corretas](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

 [CA1708: os identificadores devem ser diferentes além de maiúsculas de minúsculas](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

 [CA1707: os identificadores não devem conter sublinhados](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)

 [CA1719: os nomes de parâmetro não devem corresponder aos nomes de membro](../code-quality/ca1719-parameter-names-should-not-match-member-names.md)
