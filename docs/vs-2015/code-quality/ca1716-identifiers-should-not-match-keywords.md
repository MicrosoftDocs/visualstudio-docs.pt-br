---
title: 'CA1716: Os identificadores não devem corresponder a palavras-chave | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- IdentifiersShouldNotMatchKeywords
- CA1716
helpviewer_keywords:
- IdentifiersShouldNotMatchKeywords
- CA1716
ms.assetid: 900cc8a1-1089-4069-a4ce-10b109ac4fab
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 000e28642a10c565e525b2714eed0d7abaca9340
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49858869"
---
# <a name="ca1716-identifiers-should-not-match-keywords"></a>CA1716: os identificadores não devem corresponder a palavras-chave
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|IdentifiersShouldNotMatchKeywords|
|CheckId|CA1716|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um nome de um namespace, um tipo ou membro viritual ou interface corresponde a uma palavra-chave reservada em uma linguagem de programação.

## <a name="rule-description"></a>Descrição da Regra
 Identificadores de namespaces, tipos e virtuais e os membros de interface não devem corresponder a palavras-chave que são definidas por linguagens que visam o common language runtime. Dependendo da linguagem que é usada e a palavra-chave, ambiguidades e erros do compilador podem dificultar a biblioteca usar.

 Esta regra verifica em palavras-chave nos seguintes idiomas:

- Visual Basic

- C#

- C++/CLI

  Comparação de maiusculas e minúsculas é usada para [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] comparação diferencia maiusculas de minúsculas e palavras-chave é usada para os outros idiomas.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Selecione um nome que não aparece na lista de palavras-chave.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Você pode suprimir um aviso nessa regra, se você estiver convencido de que o identificador não confundir os usuários da API, e que a biblioteca é utilizável em todos os idiomas disponíveis no [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].



