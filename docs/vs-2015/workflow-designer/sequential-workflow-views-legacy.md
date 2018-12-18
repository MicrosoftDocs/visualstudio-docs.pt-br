---
title: Modos de exibição do fluxo de trabalho sequencial (herdado) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sequential workflow views
- sequential workflows, views
ms.assetid: 135f24b9-1b37-442b-9ef8-f0f2108a3212
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 1ac9d10ddb687063de8c45296bc879854a0979a4
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49248723"
---
# <a name="sequential-workflow-views-legacy"></a>Exibições sequenciais de fluxo de trabalho (legados)
[!INCLUDE[vs2010](../includes/vs2010-md.md)] fornece [!INCLUDE[wfd1](../includes/wfd1-md.md)] herdado que pode ser usado para direcionar [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)].  
  
 [!INCLUDE[wfd2](../includes/wfd2-md.md)] fornece uma maneira de criar aplicativos graficamente de [!INCLUDE[wf](../includes/wf-md.md)] usando a interface do usuário e de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] . aplicativos de[!INCLUDE[wf](../includes/wf-md.md)] são compostos das etapas do processo de fluxo de trabalho chamadas atividades. Para criar um fluxo de trabalho, compor atividades na superfície de design arrastando seus respectivos Designer de atividade de **caixa de ferramentas** na superfície de design.  
  
 Quando você cria um fluxo de trabalho sequencial, o que é um [SequentialWorkflowActivity](http://go.microsoft.com/fwlink?LinkID=65040), três modos de exibição do fluxo de trabalho estão disponíveis. Essas exibições são acessíveis a partir de **fluxo de trabalho** menu e, no menu de contexto na superfície de design.  
  
 A tabela a seguir lista o nome e a descrição de cada uma.  
  
|Opção de menu/guia|Descrição|  
|----------------------|-----------------|  
|**Exibição SequentialWorkflow**|Com o botão direito a superfície de design e selecione o **exibição SequentialWorkflow** opção no menu de contexto para exibir o **fluxo de trabalho sequencial** exibição, que mostra a atividade com base em gráfica representação de fluxo de trabalho sequencial. Ou selecione **exibição SequentialWorkflow** da **fluxo de trabalho** menu.|  
|**Exibir manipulador de cancelamento**|Com o botão direito a superfície de design e selecione o **exibir manipulador de cancelamento** opção no menu de contexto para exibir o **sequencial de fluxo de trabalho** exibir, que mostra o [CancellationHandlerActivity ](http://go.microsoft.com/fwlink?LinkID=65050) atividade associada com o fluxo de trabalho. Ou selecione **exibir manipulador de cancelamento** da **fluxo de trabalho** menu.|  
|**Exibir manipulador de falha**|Com a superfície de design e selecione o botão direito a **manipulador de falha de exibição** opção no menu de contexto para exibir o **falhas** exibir, que mostra as [FaultHandlersActivity](http://go.microsoft.com/fwlink?LinkID=65055) atividade associada com o fluxo de trabalho. Ou selecione **manipulador de falha de exibição** da **fluxo de trabalho** menu.|  
  
 Para obter mais informações sobre modos semelhantes, consulte [modos de exibição de atividade (herdado)](../workflow-designer/activity-views-legacy.md).  
  
## <a name="see-also"></a>Consulte também  
 [Modos de exibição de atividade (herdado)](../workflow-designer/activity-views-legacy.md)   
 [Criando projetos herdados de fluxo de trabalho](../workflow-designer/creating-legacy-workflow-projects.md)   
 [Modos de criação de fluxo de trabalho](http://go.microsoft.com/fwlink?LinkID=65014)