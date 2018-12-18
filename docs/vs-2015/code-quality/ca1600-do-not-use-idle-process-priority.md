---
title: 'CA1600: Não usar a prioridade de processo ociosa | Microsoft Docs'
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
- DoNotUseIdleProcessPriority
- CA1600
helpviewer_keywords:
- CA1600
- DoNotUseIdleProcessPriority
ms.assetid: 9b0d073b-78b6-41be-8ef3-14692a735283
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: f077774f67ca398d26746d0c375545e0cb641454
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49941848"
---
# <a name="ca1600-do-not-use-idle-process-priority"></a>CA1600: não usar a prioridade de processo ociosa
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|DoNotUseIdleProcessPriority|
|CheckId|CA1600|
|Categoria|Microsoft.Mobility|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Essa regra ocorre quando os processos são definidos como `ProcessPriorityClass.Idle`.

## <a name="rule-description"></a>Descrição da Regra
 Não defina a prioridade do processo como Ocioso. Os processos que têm `System.Diagnostics.ProcessPriorityClass.Idle` ocuparão a CPU quando estariam ocioso e, assim, bloquearão em espera.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Definir processos `ProcessPriorityClass.BelowNormal`.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Essa regra deve ser suprimida somente quando a prioridade de processo ociosa é necessária e considerações de mobilidade podem ser ignoradas com segurança.



