---
title: Depurar passo a passo de opções (herdado) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- branch stepping
- stepping, options in workflow debugging
- debugging, stepping options
- debugging workflows, stepping options
- instance stepping
ms.assetid: 3e9e3041-68c7-4f16-9bd6-da5e5144744b
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: b7dfaa4fb659418c26d5aa0144fac4188ef4b16b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49899377"
---
# <a name="debug-stepping-options-legacy"></a>Opções de avançar de depuração (legados)
Este tópico descreve como depurar aplicativos de [!INCLUDE[wf](../includes/wf-md.md)] que têm atividades simultâneas em [!INCLUDE[wfd1](../includes/wfd1-md.md)]herdado. Use [!INCLUDE[wfd2](../includes/wfd2-md.md)] herdado quando você precisa definir como alvo [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)].  
  
 Quando você está depurando as atividades herdados que possuem a execução simultânea, como **ParallelActivity** ou **ConditionedActivityGroup**, você pode usar uma das duas opções a seguir para percorrer seu código .  
  
- **Avançar da ramificação.** Este modo de Avançar permite que você percorrer e depurar uma ramificação específica de uma atividade composta, tal como o **ParallelActivity** ou o **ConditionalActivityGroup** atividade. Quando você usa esta opção depuração, você não irá notar que uma alteração no controle ocorre devido à execução simultânea de outras atividades no fluxo de trabalho. As etapas do depurador somente com as atividades na ramificação atualmente selecionado quando outras atividades no fluxo de trabalho podem executar simultaneamente. Por exemplo, por padrão, a ramificação mais à esquerda em uma **ParallelActivity** atividade e a primeira atividade filho de um **ConditionedActivityGroup** atividade são usados para depuração. Se o usuário estiver interessado em depurar qualquer outra atividade de ramificação ou filhos, um ponto de interrupção explícito deve ser colocado na atividade de ramificação ou filho. Depuração continua naquela ramificação quando o ponto de interrupção é disparado.  
  
- **Avançar de instância.** Este modo de avançar permite que você entrar completamente e depurar executar simultaneamente atividades no fluxo de trabalho. Com essa opção, você observará que uma alteração no controle ocorre ao executar simultaneamente atividades é executado dentro de fluxo de trabalho.  
  
  Por padrão, a opção de avançar da ramificação é selecionada, e os usuários podem alternar entre as duas opções para depurar um fluxo de trabalho herdado.  
  
  Você deve selecionar a opção de avançar da instância ao depurar fluxos de trabalho herdados do computador de estado.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando fluxos de trabalho herdado](../workflow-designer/debugging-legacy-workflows.md)   
 [Como alterar a opção de executar a depuração em etapas (herdado)](../workflow-designer/how-to-change-the-debug-stepping-option-legacy.md)