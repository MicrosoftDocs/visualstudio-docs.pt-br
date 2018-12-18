---
title: 'CA1308: normalizar cadeias de caracteres para maiúsculas'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1308
- NormalizeStringsToUppercase
helpviewer_keywords:
- NormalizeStringsToUppercase
- CA1308
ms.assetid: 7e9a7457-3f93-4938-ac6f-1389fba8d9cc
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5ebb31029dcc3ef88df776470afdeeb17cea601d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49949793"
---
# <a name="ca1308-normalize-strings-to-uppercase"></a>CA1308: normalizar cadeias de caracteres para maiúsculas

|||
|-|-|
|NomeDoTipo|NormalizeStringsToUppercase|
|CheckId|CA1308|
|Categoria|Microsoft.Globalization|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Uma operação normaliza uma cadeia de caracteres em minúsculas.

## <a name="rule-description"></a>Descrição da regra
 As cadeias de caracteres devem ser normalizadas em maiúsculas. Um pequeno grupo de caracteres, quando eles são convertidos em minúsculas, não é possível fazer uma viagem de ida e volta. Para fazer uma viagem de ida e volta o meio para converter os caracteres de uma localidade para outra localidade que representa dados de caracteres de forma diferente e, em seguida, com precisão recuperar os caracteres originais dos caracteres convertidos.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Altere as operações que convertem cadeias de caracteres em minúsculas, para que as cadeias de caracteres são convertidas em letras maiusculas em vez disso. Por exemplo, altere `String.ToLower(CultureInfo.InvariantCulture)` para `String.ToUpper(CultureInfo.InvariantCulture)`.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir uma mensagem de aviso quando você não estiver fazendo a decisão de segurança com base no resultado (por exemplo, quando você exibe na interface do usuário).

## <a name="see-also"></a>Consulte também
 [Avisos de globalização](../code-quality/globalization-warnings.md)