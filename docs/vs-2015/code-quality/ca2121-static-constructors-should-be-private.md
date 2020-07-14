---
title: 'CA2121: construtores estáticos devem ser privados | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2121
- StaticConstructorsShouldBePrivate
helpviewer_keywords:
- CA2121
- StaticConstructorsShouldBePrivate
ms.assetid: ee93c620-8fc1-4e47-866c-d389c3ca9f2e
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 7f95b33e1391ca755a6c0df261fa2bd05bd3c7a0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544307"
---
# <a name="ca2121-static-constructors-should-be-private"></a>CA2121: Construtores estáticos devem ser particulares
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|StaticConstructorsShouldBePrivate|
|CheckId|CA2121|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo tem um construtor estático que não é privado.

## <a name="rule-description"></a>Descrição da Regra
 Um construtor estático, também conhecido como Construtor de classe, é usado para inicializar um tipo. O sistema chama o construtor estático antes que a primeira instância do tipo seja criada ou que outros membros estáticos sejam referenciados. O usuário não tem controle sobre quando o construtor estático é chamado. Se não for privado, um construtor estático poderá ser chamado por um código diferente do sistema. Dependendo das operações realizadas no construtor, isso pode causar um comportamento inesperado.

 Essa regra é imposta pelos compiladores C# e Visual Basic .NET.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 As violações geralmente são causadas por uma das seguintes ações:

- Você definiu um construtor estático para seu tipo e não o tornaria privado.

- O compilador da linguagem de programação adicionou um construtor estático padrão ao seu tipo e não o torna particular.

  Para corrigir o primeiro tipo de violação, torne seu construtor estático privado. Para corrigir o segundo tipo, adicione um construtor estático privado ao seu tipo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprime essas violações. Se o design de seu software exigir uma chamada explícita para um construtor estático, é provável que o design contenha falhas graves e seja revisado.
