---
title: 'CA2204: os literais devem ser escritos corretamente | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- Literals should be spelled correctly
- CA2204
- LiteralsShouldBeSpelledCorrectly
helpviewer_keywords:
- CA2204
ms.assetid: b0bbcbb6-c92d-4c14-8ef7-9c8b38c791a6
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ecf829251cbeab600cb95f8f0c0b0173cd7338d4
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546270"
---
# <a name="ca2204-literals-should-be-spelled-correctly"></a>CA2204: Literais devem ser escritos corretamente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|LiteralsShouldBeSpelledCorrectly|
|CheckId|CA2204|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um método passa uma cadeia de caracteres literal para que é usada em um parâmetro ou propriedade que requer uma cadeia de caracteres localizada e a cadeia de caracteres literal contém uma ou mais palavras que não são reconhecidas pela biblioteca do verificador ortográfico da Microsoft.

## <a name="rule-description"></a>Descrição da Regra
 Essa regra verifica uma cadeia de caracteres literal que é passada como um valor para um parâmetro ou propriedade quando um ou mais dos seguintes casos é verdadeiro:

- O <xref:System.ComponentModel.LocalizableAttribute> atributo do parâmetro ou da propriedade é definido como true.

- O nome do parâmetro ou da propriedade contém "texto", "mensagem" ou "legenda".

- O nome do parâmetro de cadeia de caracteres que é passado para um método Console. Write ou console. WriteLine é "value" ou "Format".

  Essa regra analisa a cadeia de caracteres literal em palavras, a geração de tokens de palavras compostas e verifica a ortografia de cada palavra/token. Para obter informações sobre o algoritmo de análise, consulte [CA1704: identificadores devem ser escritos corretamente](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md).

  Por padrão, a versão em inglês (EN) do verificador ortográfico é usada.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, corrija a grafia da palavra ou adicione a palavra a um dicionário personalizado. Para obter informações sobre como usar dicionários personalizados, consulte [como: personalizar o dicionário de análise de código](../code-quality/how-to-customize-the-code-analysis-dictionary.md).

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra. Palavras escritas corretamente reduzem a curva de aprendizado necessária para novas bibliotecas de software.

## <a name="related-rules"></a>Regras relacionadas
 [CA1704: Identificadores devem ser escritos corretamente](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)

 [CA1703: Cadeias de caracteres de recurso devem ser escritas corretamente](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md)
