---
title: 'CA1724: os nomes de tipo não devem corresponder a namespaces'
ms.date: 09/28/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- TypeNamesShouldNotMatchNamespaces
- CA1724
helpviewer_keywords:
- TypeNamesShouldNotMatchNamespaces
- CA1724
ms.assetid: 329af3b5-5600-4101-831d-531ab3eb7060
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: bf359ffcc098fa2b5653c28da302e2777216ea5b
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47860258"
---
# <a name="ca1724-type-names-should-not-match-namespaces"></a>CA1724: Os nomes de tipo não devem corresponder a namespaces

|||
|-|-|
|NomeDoTipo|TypeNamesShouldNotMatchNamespaces|
|CheckId|CA1724|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa

Um nome de tipo corresponde a um nome de namespace referenciado que tenha um ou mais tipos visíveis externamente. A comparação de nome não diferencia maiusculas de minúsculas.

## <a name="rule-description"></a>Descrição da regra

Nomes de tipo criados pelo usuário não devem corresponder a nomes de namespaces referenciados que têm tipos visíveis externamente. A violação dessa regra pode reduzir a usabilidade da biblioteca.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Renomear o tipo, de modo que ele não corresponder ao nome de um namespace referenciado que tenha tipos visíveis externamente.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Para novos desenvolvimentos, nenhum conhecidos ocorrem de cenários em que você deve suprimir um aviso nessa regra. Antes de você suprime o aviso, considere cuidadosamente como os usuários da sua biblioteca talvez estejam confusos pelas nome correspondente. Para o envio de bibliotecas, talvez você precise suprimir um aviso nessa regra.