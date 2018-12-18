---
title: Designer de atividade de InitializeCorrelation | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.InitializeCorrelation.UI
ms.assetid: 4c54f34c-ee84-42a6-abb0-ec260c1ccb76
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 9dd9d622785fbfebd8560daf9bf459716381ddbf
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49234020"
---
# <a name="initializecorrelation-activity-designer"></a>Designer de atividade de InitializeCorrelation
O **InitializeCorrelation** designer de atividade é usado para criar e configurar um <xref:System.ServiceModel.Activities.InitializeCorrelation> atividade que é usada para estabelecer uma correlação entre mensagens antes de enviar ou recebê-los.  
  
## <a name="the-initializecorrelation-activity"></a>A atividade de InitializeCorrelation  
 Uma atividade de <xref:System.ServiceModel.Activities.InitializeCorrelation> é usada para inicializar correlações sem enviar e receber uma mensagem. Correlação é inicializada normalmente ao enviar ou para receber uma mensagem. Se correlação deve ser estabelecida antes que uma mensagem ser enviada ou recebida, use <xref:System.ServiceModel.Activities.InitializeCorrelation> para inicializar correlação.  
  
### <a name="using-the-initializecorrelation-activity-designer"></a>Usando o designer de atividade de InitializeCorrelation  
 O **InitializeCorrelation** designer de atividade pode ser encontrado na **Messaging** categoria dos **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas**  guia o [!INCLUDE[wfd2](../includes/wfd2-md.md)] (como alternativa, selecione **barra de ferramentas** do **exibição** menu ou CTRL + ALT + X.)  
  
 O **InitializeCorrelation** designer de atividade pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície. Isso cria uma <xref:System.ServiceModel.Activities.InitializeCorrelation> atividade com um padrão <xref:System.Activities.Activity.DisplayName%2A> de InitializeCorrelation.The <xref:System.Activities.Activity.DisplayName%2A> pode ser editado no cabeçalho dos **InitializeCorrelation** designer de atividade ou no  **DisplayName** caixa do **propriedades** janela.  
  
 O <xref:System.ServiceModel.Activities.CorrelationHandle> pode ser especifica na **correlação** campo **as propriedades** janela no **InitializeCorrelation** superfície do designer de atividade.  
  
 Clicar no botão de elipse além de **CorrelationData** campo **propriedades** janela ou o "modo de exibição..." Dica de texto em **InitializeCorrelation** superfície do designer de atividade exibe as **inicializar correlação** caixa de diálogo na qual você pode especificar o identificador da correlação e os pares chave-valor usados para inicializá-lo. [!INCLUDE[crabout](../includes/crabout-md.md)] usando esta caixa de diálogo, consulte a [caixa de diálogo do Editor de coleção de tipo](../workflow-designer/type-collection-editor-dialog-box.md) tópico.  
  
### <a name="the-initializecorrelation-properties"></a>As propriedades de InitializeCorrelation  
 A tabela a seguir mostra as propriedades de <xref:System.ServiceModel.Activities.InitializeCorrelation> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na **propriedades** janela ou no [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície.  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.ServiceModel.Activities.InitializeCorrelation> . O valor padrão é InitializeCorrelation.<br /><br /> Embora o uso de um valor não padrão para <xref:System.Activities.Activity.DisplayName%2A> amigável não é necessário restrita, é uma prática recomendada usar um valor.|  
|<xref:System.ServiceModel.Activities.InitializeCorrelation.Correlation%2A>|False|<xref:System.ServiceModel.Activities.CorrelationHandle> usado para associar atividades de fluxo de trabalho em correlação.|  
|<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>|False|Um dicionário de dados de correlação que se relacionam mensagens ao fluxo de trabalho instância.<br /><br /> Use o **inicializar correlação** caixa de diálogo para configurar o <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>. [!INCLUDE[crabout](../includes/crabout-md.md)] o uso esta caixa de diálogo, consulte a [caixa de diálogo do Editor de coleção de tipo](../workflow-designer/type-collection-editor-dialog-box.md) tópico.|  
  
## <a name="see-also"></a>Consulte também  
 [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)   
 [Receber](../workflow-designer/receive-activity-designer.md)   
 [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)   
 [Enviar](../workflow-designer/send-activity-designer.md)   
 [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)   
 [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)