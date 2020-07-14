---
title: 'CA1308: Normalizar cadeias de caracteres para maiúsculas | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1308
- NormalizeStringsToUppercase
helpviewer_keywords:
- NormalizeStringsToUppercase
- CA1308
ms.assetid: 7e9a7457-3f93-4938-ac6f-1389fba8d9cc
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c068fcda7d03ae91435c040d2110d632668d832a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538730"
---
# <a name="ca1308-normalize-strings-to-uppercase"></a>CA1308: Normalizar cadeias de caracteres em maiúsculas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|NormalizeStringsToUppercase|
|CheckId|CA1308|
|Categoria|Microsoft. Globalization|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Uma operação normaliza uma cadeia de caracteres para minúsculas.

## <a name="rule-description"></a>Descrição da Regra
 As cadeias de caracteres devem ser normalizadas em maiúsculas. Um pequeno grupo de caracteres, quando são convertidos em minúsculas, não pode fazer uma viagem de ida e volta. Fazer uma viagem de ida e volta significa converter os caracteres de uma localidade em outra localidade que representa dados de caracteres de forma diferente e, em seguida, recuperar com precisão os caracteres originais dos caracteres convertidos.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Altere as operações que convertem cadeias de caracteres em minúsculas para que as cadeias de caracteres sejam convertidas em maiúsculas. Por exemplo, altere `String.ToLower(CultureInfo.InvariantCulture)` para `String.ToUpper(CultureInfo.InvariantCulture)`.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir uma mensagem de aviso quando você não está tomando decisão de segurança com base no resultado (por exemplo, quando você a exibe na interface do usuário).

## <a name="see-also"></a>Consulte Também
 [Avisos de globalização](../code-quality/globalization-warnings.md)
