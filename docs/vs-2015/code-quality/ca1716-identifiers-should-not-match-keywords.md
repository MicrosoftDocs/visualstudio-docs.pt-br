---
title: 'CA1716: identificadores não devem corresponder a palavras-chave | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- IdentifiersShouldNotMatchKeywords
- CA1716
helpviewer_keywords:
- IdentifiersShouldNotMatchKeywords
- CA1716
ms.assetid: 900cc8a1-1089-4069-a4ce-10b109ac4fab
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 67a3588a857a0eea7d338217f975ed593dfdad52
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543696"
---
# <a name="ca1716-identifiers-should-not-match-keywords"></a>CA1716: Identificadores não devem corresponder a palavras-chave
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|IdentifiersShouldNotMatchKeywords|
|CheckId|CA1716|
|Categoria|Microsoft. Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um nome de um namespace, um tipo ou um membro de interface ou viritual corresponde a uma palavra-chave reservada em uma linguagem de programação.

## <a name="rule-description"></a>Descrição da Regra
 Identificadores para namespaces, tipos e membros de interface e virtuais não devem corresponder a palavras-chave definidas por linguagens que se destinam ao Common Language Runtime. Dependendo do idioma usado e da palavra-chave, os erros e as ambiguidades do compilador podem tornar a biblioteca difícil de usar.

 Esta regra verifica as palavras-chave nos seguintes idiomas:

- Visual Basic

- C#

- C++/CLI

  A comparação que não diferencia maiúsculas de minúsculas é usada para [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] palavras-chave e a comparação diferencia maiúsculas de minúsculas é usada para os outros idiomas.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Selecione um nome que não apareça na lista de palavras-chave.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Você pode suprimir um aviso dessa regra se estiver convencido de que o identificador não confundirá os usuários da API e que a biblioteca pode ser usada em todos os idiomas disponíveis no [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] .
