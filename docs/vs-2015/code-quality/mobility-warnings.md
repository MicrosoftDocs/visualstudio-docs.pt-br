---
title: Avisos de mobilidade | Microsoft Docs
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
- vs.codeanalysis.MobilityRules
helpviewer_keywords:
- managed code analysis warnings, mobility warnings
- mobility warnings
- warnings, mobility
ms.assetid: 9808054c-593b-4fc3-92cc-1fc45f41569c
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 6e73864234604f22ec15340740442505fec3e078
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49270069"
---
# <a name="mobility-warnings"></a>Avisos de mobilidade
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Avisos de mobilidade oferecem suporte ao uso de energia eficiente.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Regra|Descrição|  
|----------|-----------------|  
|[CA1600: não usar a prioridade de processo ociosa](../code-quality/ca1600-do-not-use-idle-process-priority.md)|Não defina a prioridade do processo como Ocioso. Os processos que têm System.Diagnostics.ProcessPriorityClass.Idle ocuparão a CPU quando estariam ociosos e, assim, bloquearão a espera.|  
|[CA1601: não usar temporizadores que impeçam alterações no estado de energia](../code-quality/ca1601-do-not-use-timers-that-prevent-power-state-changes.md)|A atividade periódica de alta frequência manterá a CPU ocupada e interferirá nos temporizadores ociosos que economizam energia e desligam monitores e discos rígidos.|



