---
title: 'CA1716: os identificadores não devem corresponder a palavras-chave'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- IdentifiersShouldNotMatchKeywords
- CA1716
helpviewer_keywords:
- IdentifiersShouldNotMatchKeywords
- CA1716
ms.assetid: 900cc8a1-1089-4069-a4ce-10b109ac4fab
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: cfaef87f8463c43c412c5db3c83a899fb22b4f66
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49862431"
---
# <a name="ca1716-identifiers-should-not-match-keywords"></a>CA1716: os identificadores não devem corresponder a palavras-chave

|||
|-|-|
|NomeDoTipo|IdentifiersShouldNotMatchKeywords|
|CheckId|CA1716|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa

Um nome de um namespace, um tipo ou membro viritual ou interface corresponde a uma palavra-chave reservada em uma linguagem de programação.

## <a name="rule-description"></a>Descrição da regra

Identificadores de namespaces, tipos e virtuais e os membros de interface não devem corresponder a palavras-chave que são definidas por linguagens que visam o common language runtime. Dependendo da linguagem que é usada e a palavra-chave, ambiguidades e erros do compilador podem dificultar a biblioteca usar.

Esta regra verifica em palavras-chave nos seguintes idiomas:

- Visual Basic

- C#

- C++/CLI

Comparação de maiusculas e minúsculas é usada para [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] comparação diferencia maiusculas de minúsculas e palavras-chave é usada para os outros idiomas.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Selecione um nome que não aparece na lista de palavras-chave.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Se você estiver convencido de que o identificador não confundir os usuários da API, e que a biblioteca é utilizável em todos os idiomas disponíveis no .NET Framework, você pode suprimir um aviso nessa regra.