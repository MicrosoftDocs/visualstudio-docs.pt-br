---
title: Designer de atividade de TerminateWorkflow | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Statements.TerminateWorkflow.UI
ms.assetid: 08e632ed-0724-4fb4-9df1-f8d443eaf0ac
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 67681982c9c8d77df77242be5c07679f3b0d24ff
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49225689"
---
# <a name="terminateworkflow-activity-designer"></a>Designer de atividade de TerminateWorkflow
O **TerminateWorkflow** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.TerminateWorkflow> atividade.  
  
## <a name="the-terminateworkflow-activity"></a>A atividade de TerminateWorkflow  
 A atividade de <xref:System.Activities.Statements.TerminateWorkflow> finaliza a execução de um fluxo de trabalho.  
  
### <a name="using-the-terminateworkflow-activity-designer"></a>Usando o designer de atividade de TerminateWorkflow  
 O **TerminateWorkflow** designer de atividade pode ser encontrado na **tempo de execução** categoria dos **caixa de ferramentas**, que é acessado clicando o **dacaixadeferramentas** guia (como alternativa, selecione **caixa de ferramentas** da **exibição** menu ou CTRL + ALT + X.)  
  
 O **TerminateWorkflow** designer de atividade pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície onde quer que as atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Isso cria uma <xref:System.Activities.Statements.TerminateWorkflow> atividade com um padrão **DisplayName** de TerminateWorkflow. O <xref:System.Activities.Activity.DisplayName%2A> pode ser editado no cabeçalho do **TerminateWorkflow** designer de atividade ou nos **DisplayName** caixa da grade de propriedade.  
  
### <a name="the-terminateworkflow-properties"></a>As propriedades de TerminateWorkflow  
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.TerminateWorkflow> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade e algumas delass podem ser editadas na superfície de [!INCLUDE[wfd2](../includes/wfd2-md.md)] .  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.Activities.Statements.TerminateWorkflow> . O padrão é TerminateWorkflow. Embora o nome para exibição não é necessário restrita, é uma prática recomendada usar um nome para exibição.|  
|<xref:System.Activities.Statements.TerminateWorkflow.Exception%2A>|False|A exceção para indicar quando o fluxo de trabalho é encerrado. Defina essa propriedade na grade de propriedade.|  
|<xref:System.Activities.Statements.TerminateWorkflow.Reason%2A>|False|A razão que explica como o fluxo de trabalho foi encerrado. Defina essa propriedade na grade de propriedade.|  
  
## <a name="see-also"></a>Consulte também  
 [tempo de execução](../workflow-designer/runtime-activity-designers.md)   
 [Persistir](../workflow-designer/persist-activity-designer.md)