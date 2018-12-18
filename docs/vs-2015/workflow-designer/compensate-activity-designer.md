---
title: Designer de atividade Compensate | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Compensate.UI
ms.assetid: 7347c947-bfff-4bad-becd-5cd23e7b24cd
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: ae01f59e6d1b1c9d9e0baa4214a693b3e6d390d8
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49245928"
---
# <a name="compensate-activity-designer"></a>Compense o designer de atividades
O **Compensate** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.Compensate> atividade.  
  
## <a name="the-compensate-activity"></a>A atividade de compesação  
 A atividade de <xref:System.Activities.Statements.Compensate> chama explicitamente <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> para uma atividade contida em <xref:System.Activities.Statements.CompensableActivity>. Se a atividade de <xref:System.Activities.Statements.Compensate> não é usada dentro de <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>, <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>, ou <xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> de <xref:System.Activities.Statements.CompensableActivity>, então você deve especificar a propriedade de <xref:System.Activities.Statements.Compensate.Target%2A> .  
  
 <xref:System.Activities.Statements.CompensationToken> especificado por <xref:System.Activities.Statements.Compensate.Target%2A> fornece um meio para confirmar ou compensar explicitamente <xref:System.Activities.Statements.CompensableActivity> uma vez que <xref:System.Activities.Statements.CompensableActivity.Body%2A> de <xref:System.Activities.Statements.CompensableActivity> terminou com êxito.  
  
### <a name="using-the-compensate-activity-designer"></a>Usando o designer de atividade de compesação  
 O **Compensate** designer de atividade pode ser encontrado na **transação** categoria da **caixa de ferramentas**, que é acessado clicando o **dacaixadeferramentas** guia no lado esquerdo do [!INCLUDE[wfd2](../includes/wfd2-md.md)] (como alternativa, selecione **barra de ferramentas** do **exibição** menu, ou CTRL + ALT + X.)  
  
 O **Compensate** designer de atividade pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície onde quer que as atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Isso cria uma atividade de <xref:System.Activities.Statements.Compensate> com <xref:System.Activities.Activity.DisplayName%2A> padrão Compensate. O <xref:System.Activities.Activity.DisplayName%2A> valor pode ser editado no cabeçalho do **Compensate** designer de atividade ou nos **DisplayName** caixa da grade de propriedade.  
  
### <a name="the-compensate-properties"></a>As propriedades de compesação  
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.CancellationScope> e descreve como elas são usadas no designer. A propriedade de <xref:System.Activities.Activity.DisplayName%2A> pode ser editada na grade de propriedade ou na superfície de [!INCLUDE[wfd2](../includes/wfd2-md.md)] , mas a propriedade de <xref:System.Activities.Statements.Compensate.Target%2A> deve ser editada na grade de propriedade.  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|Especifica o nome amigável opcional de atividade de <xref:System.Activities.Statements.Compensate> . O padrão é compensa.|  
|<xref:System.Activities.Statements.Compensate.Target%2A>|verdadeiro|Especifica <xref:System.Activities.InArgument%601> que contém <xref:System.Activities.Statements.CompensationToken> para esta atividade de <xref:System.Activities.Statements.Compensate> .|  
  
## <a name="see-also"></a>Consulte também  
 [Transação](../workflow-designer/transaction-activity-designers.md)   
 [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)   
 [Designer de atividade Compensate](../workflow-designer/compensate-activity-designer.md)   
 [Confirmar](../workflow-designer/confirm-activity-designer.md)   
 [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)