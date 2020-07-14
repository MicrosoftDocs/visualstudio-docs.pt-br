---
title: 'CA2004: remover chamadas para GC. KeepAlive | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- RemoveCallsToGCKeepAlive
- CA2004
helpviewer_keywords:
- RemoveCallsToGCKeepAlive
- CA2004
ms.assetid: bc543b5b-23eb-4b45-abc2-9325cd254ac2
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 53fa5f61cb7c503502956831452bc3eca1a9fece
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85521193"
---
# <a name="ca2004-remove-calls-to-gckeepalive"></a>CA2004: Remover as chamadas a GC.KeepAlive
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|RemoveCallsToGCKeepAlive|
|CheckId|CA2004|
|Categoria|Microsoft. confiabilidade|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 As classes usam `SafeHandle` , mas ainda contêm chamadas para `GC.KeepAlive` .

## <a name="rule-description"></a>Descrição da Regra
 Se você estiver convertendo para `SafeHandle` uso, remova todas as chamadas para `GC.KeepAlive` (Object). Nesse caso, as classes não devem chamar `GC.KeepAlive` , supondo que elas não tenham um finalizador, mas que dependam `SafeHandle` do para concluir o identificador do sistema operacional para elas.  Embora o custo de deixar em uma chamada para `GC.KeepAlive` pode ser insignificante como medido pelo desempenho, a percepção de que uma chamada `GC.KeepAlive` é necessária ou suficiente para resolver um problema de tempo de vida que pode não existir mais torna o código mais difícil de manter.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Remova as chamadas para `GC.KeepAlive` .

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Você pode suprimir esse aviso somente se não estiver tecnicamente correto para converter para `SafeHandle` uso em sua classe.
