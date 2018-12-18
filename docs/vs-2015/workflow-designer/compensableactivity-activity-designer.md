---
title: Designer de atividade de CompensableActivity | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Statements.CompensableActivity.UI
ms.assetid: e0340d89-d39e-4a52-8557-13e27040d7b5
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 670d3e92b24e35979074df3817611ceff692f59d
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49290440"
---
# <a name="compensableactivity-activity-designer"></a>Designer de atividade de CompensableActivity
O **CompensableActivity** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.CompensableActivity> atividade.  
  
## <a name="the-compensableactivity-activity"></a>A atividade de CompensableActivity  
 <xref:System.Activities.Statements.CompensableActivity> define uma unidade de trabalho que pode ser compensado confirmada ou após a conclusão com êxito.  
  
### <a name="using-the-compensableactivity-activity-designer"></a>Usando o designer de atividade de CompensableActivity  
 O **CompensableActivity** designer de atividade pode ser encontrado na **transação** categoria dos **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas**  guia no lado esquerdo do [!INCLUDE[wfd2](../includes/wfd2-md.md)] (como alternativa, selecione **barra de ferramentas** do **exibição** menu, ou CTRL + ALT + X.)  
  
 O **CompensableActivity** designer de atividade pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície onde quer que as atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Isso cria uma atividade de <xref:System.Activities.Statements.CompensableActivity> com <xref:System.Activities.Activity.DisplayName%2A> padrão de CompensableActivity. O <xref:System.Activities.Activity.DisplayName%2A> valor pode ser editado no cabeçalho do **CompensableActivity** designer de atividade ou nos **DisplayName** caixa da grade de propriedade.  
  
### <a name="the-compensableactivity-properties"></a>As propriedades de CompensableActivity  
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.CompensableActivity> e descreve como elas são usadas no designer. A propriedade de <xref:System.Activities.Activity.DisplayName%2A> e de <xref:System.Activities.Activity%601.Result%2A> pode ser editada na grade de propriedade mas outras propriedades devem ser editadas na superfície de [!INCLUDE[wfd2](../includes/wfd2-md.md)] .  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável opcional de atividade de <xref:System.Activities.Statements.CompensableActivity> . O padrão é CompensableActivity.|  
|<xref:System.Activities.Activity%601.Result%2A>|False|Especifica o valor de retorno de <xref:System.Activities.Statements.CompensableActivity>. Esta propriedade deve ser editada na grade de propriedade.|  
|<xref:System.Activities.Statements.CompensableActivity.Body%2A>|verdadeiro|Especifica a atividade para que a compensação, cancelamento, e a lógica de confirmação são fornecidos. Para adicionar o <xref:System.Activities.Statements.CompensableActivity.Body%2A> atividade, soltar uma atividade do **caixa de ferramentas** no **corpo** caixa no **CompensableActivity** designer de atividade com o texto de dica "Drop atividade aqui".|  
|<xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>|False|Especifica a atividade que é executado no caso de cancelamento. Para adicionar a atividade, soltar o designer do **caixa de ferramentas** para o **CancellationHandler** caixa no **CompensableActivity** designer de atividade com o texto de dica "Drop Atividade aqui".|  
|<xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>|False|Especifica a atividade a ser executada para compensar a atividade de <xref:System.Activities.Statements.CompensableActivity.Body%2A> . Esse manipulador pode ser chamado explicitamente usando a atividade de <xref:System.Activities.Statements.Compensate> .<br /><br /> Para adicionar a atividade, soltar o designer de atividade do **caixa de ferramentas** para o **CompensationHandler** caixa no **CompensableActivity** designer de atividade com o texto de dica " Soltar atividade aqui".|  
|<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A>|False|Especifica a atividade a ser executada para confirmar a atividade de <xref:System.Activities.Statements.CompensableActivity.Body%2A> . Esse manipulador pode ser chamado explicitamente usando a atividade de <xref:System.Activities.Statements.Confirm> .<br /><br /> Para adicionar a atividade, soltar o designer de atividade do **caixa de ferramentas** para o **ConfirmationHandler** caixa no **CompensableActivity** designer de atividade com o texto de dica " Soltar atividade aqui".|  
  
## <a name="see-also"></a>Consulte também  
 [Transação](../workflow-designer/transaction-activity-designers.md)   
 [CancellationScope](../workflow-designer/cancellationscope-activity-designer.md)   
 [Compensar](../workflow-designer/compensate-activity-designer.md)   
 [Confirmar](../workflow-designer/confirm-activity-designer.md)   
 [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)