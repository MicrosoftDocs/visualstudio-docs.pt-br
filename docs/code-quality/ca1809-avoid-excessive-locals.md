---
title: 'CA1809: Evitar locais excessivos'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: reference
f1_keywords:
- CA1809
- AvoidExcessiveLocals
helpviewer_keywords:
- AvoidExcessiveLocals
- CA1809
ms.assetid: 5c81ea43-cb49-448f-980f-a1dd9764043c
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0824517aa7d5dc05f9a0297ca44cd235f5800653
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53904004"
---
# <a name="ca1809-avoid-excessive-locals"></a>CA1809: Evitar locais excessivos

|||
|-|-|
|NomeDoTipo|AvoidExcessiveLocals|
|CheckId|CA1809|
|Categoria|Microsoft.Performance|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um membro contiver mais de 64 variáveis locais, algumas das quais podem ser gerado pelo compilador.

## <a name="rule-description"></a>Descrição da regra
 Uma otimização de desempenho comum é armazenar um valor em um registro do processador, em vez de na memória, que é conhecido como *registro* o valor. O common language runtime considera até 64 variáveis locais para enregistration. Variáveis que não seja cancelado são colocadas na pilha e devem ser movidas para um registro antes de manipulação. Para permitir que a chance de que todas as variáveis locais obter cancelado, limite o número de variáveis locais a 64.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, Refatore a implementação para usar não mais do que 64 variáveis locais.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro para suprimir um aviso nessa regra, ou para desabilitar a regra, se o desempenho não for um problema.

## <a name="related-rules"></a>Regras relacionadas
 [CA1804: Remover locais não usados](../code-quality/ca1804-remove-unused-locals.md)