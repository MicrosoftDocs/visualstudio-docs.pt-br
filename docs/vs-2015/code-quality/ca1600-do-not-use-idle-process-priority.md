---
title: 'CA1600: não usar prioridade de processo ocioso | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotUseIdleProcessPriority
- CA1600
helpviewer_keywords:
- CA1600
- DoNotUseIdleProcessPriority
ms.assetid: 9b0d073b-78b6-41be-8ef3-14692a735283
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 3f6233136dcf7f1db5d622a02419d33e0eedacf5
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545672"
---
# <a name="ca1600-do-not-use-idle-process-priority"></a>CA1600: Não usar prioridade de processo ociosa
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotUseIdleProcessPriority|
|CheckId|CA1600|
|Categoria|Microsoft. Mobility|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Essa regra ocorre quando os processos são definidos como `ProcessPriorityClass.Idle` .

## <a name="rule-description"></a>Descrição da Regra
 Não defina a prioridade do processo como Ocioso. Os processos que `System.Diagnostics.ProcessPriorityClass.Idle` ocuparão a CPU quando, caso contrário, ficarão ociosos e, portanto, bloquearão o modo de espera.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Definir processos como `ProcessPriorityClass.BelowNormal` .

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Essa regra deve ser suprimida somente quando a prioridade de processo ociosa é necessária e as considerações de mobilidade podem ser ignoradas com segurança.
