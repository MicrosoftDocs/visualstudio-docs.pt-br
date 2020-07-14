---
title: 'CA1809: evitar locais em excesso | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1809
- AvoidExcessiveLocals
helpviewer_keywords:
- AvoidExcessiveLocals
- CA1809
ms.assetid: 5c81ea43-cb49-448f-980f-a1dd9764043c
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d39c8d9d09cf457738df87e3c2e6e109f7bc1696
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543852"
---
# <a name="ca1809-avoid-excessive-locals"></a>CA1809: Evitar locais excessivos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AvoidExcessiveLocals|
|CheckId|CA1809|
|Categoria|Microsoft. performance|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um membro contém mais de 64 variáveis locais, algumas das quais podem ser geradas pelo compilador.

## <a name="rule-description"></a>Descrição da Regra
 Uma otimização de desempenho comum é armazenar um valor em um registro de processador em vez de na memória, que é conhecido como *registrar* o valor. O Common Language Runtime considera até 64 variáveis locais para o registro. As variáveis que não são registradas são colocadas na pilha e devem ser movidas para um registro antes da manipulação. Para permitir a chance de que todas as variáveis locais sejam registradas, limite o número de variáveis locais a 64.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, refatore a implementação para usar no máximo 64 variáveis locais.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra ou desabilitar a regra, se o desempenho não for um problema.

## <a name="related-rules"></a>Regras relacionadas
 [CA1804: Remover locais não utilizados](../code-quality/ca1804-remove-unused-locals.md)
