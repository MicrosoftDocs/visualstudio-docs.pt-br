---
title: Depurando fluxos de trabalho de um computador remoto (herdado) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- workflows, debugging remotely
- debugging workflows, remotely
- remote debugging, workflows
- debugging, remote
ms.assetid: 44eaec8f-9959-4ae7-a374-670946f933c1
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 2b3627b6d62b1f4d237c2f2013d332be56b58fc6
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49191565"
---
# <a name="debugging-workflows-from-a-remote-computer-legacy"></a>Fluxos de trabalho de depuração de um computador remoto (legados)
Este tópico descreve como depurar aplicativos herdadas remotos de [!INCLUDE[wf](../includes/wf-md.md)] que são criados com [!INCLUDE[wfd1](../includes/wfd1-md.md)]herdado. Use [!INCLUDE[wfd2](../includes/wfd2-md.md)] herdado quando seu aplicativo precisa definir como alvo [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)].  
  
 Quando você instala [!INCLUDE[vs_current_long](../includes/vs-current-long-md.md)], uma das opções de instalação do componente é instalar o [!INCLUDE[vs_current_long](../includes/vs-current-long-md.md)] do depurador para [!INCLUDE[wf](../includes/wf-md.md)]. Isso instala os componentes de depuração remota. Esses componentes de depuração remota devem ser instalados no computador que você está definido para depuração remota de fluxo de trabalho.  
  
 Além disso, o assembly que contém a definição de fluxo de trabalho de fluxo de trabalho herdado que você está depurando em um computador remoto deve ser instalado no cachê global de assemblies (GAC) do computador local que você está depurando de. Por exemplo, se um fluxo de trabalho herdado está em execução em um computador remoto A, e você depurá-lo do computador local B, a definição de fluxo de trabalho deve estar presente no GAC do computador B. Isso permite que o designer para desserializar e exibir no computador B a marcação de fluxo de trabalho do fluxo de trabalho que está executando remotamente no computador A. Para obter mais informações sobre o cache de assembly global, consulte a biblioteca MSDN.  
  
 depuração remota de[!INCLUDE[wf2](../includes/wf2-md.md)] funciona da mesma que a depuração remota para outros componentes de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] . Para obter mais informações, consulte [!INCLUDE[vs_current_long](../includes/vs-current-long-md.md)] depuração remota na biblioteca MSDN.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando fluxos de trabalho herdados](../workflow-designer/debugging-legacy-workflows.md)