---
title: Designer de atividade Persist | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Persist.UI
ms.assetid: be8648dd-3eb9-4a50-8ec1-57a8be804692
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 628082fc5130a17a14b273b4d1e35e962cc5e394
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49209294"
---
# <a name="persist-activity-designer"></a>Persistir o designer de atividades
O **Persist** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.Persist> atividade.  
  
## <a name="the-persist-activity"></a>A atividade persistir  
 A atividade de <xref:System.Activities.Statements.Persist> salva um fluxo de trabalho em disco, se possível. A atividade de <xref:System.Activities.Statements.Persist> não pode ser executada em uma zona de não persistência como, por exemplo, em uma atividade de <xref:System.Activities.Statements.TransactionScope> . Se você usar uma atividade de <xref:System.Activities.Statements.Persist> em um escopo de não persistência, uma exceção é lançada em tempo de execução.  
  
### <a name="using-the-persist-activity-designer"></a>Usando o designer de atividade de persistir  
 O **Persist** designer de atividade pode ser encontrado na **tempo de execução** categoria dos **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas** guia (como alternativa, selecione **caixa de ferramentas** da **exibição** menu ou CTRL + ALT + X.)  
  
 O **Persist** designer de atividade pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície onde quer que as atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Isso cria uma <xref:System.Activities.Statements.Persist> atividade com um padrão **DisplayName** de persistência. O <xref:System.Activities.Activity.DisplayName%2A> pode ser editado no cabeçalho do **Persist** designer de atividade ou nos **DisplayName** caixa da grade de propriedade.  
  
### <a name="the-persist-properties"></a>As propriedades persistir  
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.Persist> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade e algumas delass podem ser editadas na superfície de [!INCLUDE[wfd2](../includes/wfd2-md.md)] .  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.Activities.Statements.Persist> . O padrão é persiste. Embora o nome para exibição não é necessário restrita, é uma prática recomendada usar um nome para exibição.|  
  
## <a name="see-also"></a>Consulte também  
 [tempo de execução](../workflow-designer/runtime-activity-designers.md)   
 [TerminateWorkflow](../workflow-designer/terminateworkflow-activity-designer.md)