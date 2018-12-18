---
title: Designers de atividade do sistema de mensagens | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 897e63cf-a42f-4edd-876f-c4ccfffaf6d6
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 254b8d819da8cd1d06d21699940c3b118aa75119
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49274749"
---
# <a name="messaging-activity-designers"></a>Designer de atividade de mensagem
Os designers de atividade de mensagem são usados para criar e configurar as atividades de mensagem que enviam e recebem mensagens de [!INCLUDE[indigo1](../includes/indigo1-md.md)] de dentro de um aplicativo de [!INCLUDE[wf](../includes/wf-md.md)] . [!INCLUDE[netfx40_long](../includes/netfx40-long-md.md)] apresenta cinco atividades de mensagem e [!INCLUDE[wfd1](../includes/wfd1-md.md)] fornece dois novos designer do modelo que permitem a você gerenciar a mensagem em um fluxo de trabalho. Os tópicos contidos nesta seção e listados na tabela a seguir fornecem orientação sobre como usar o designer de atividade e modelo de [!INCLUDE[wfd2](../includes/wfd2-md.md)] .  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Atividade de mensagem|Descrição|  
|----------------------|-----------------|  
|[CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)|Cria e configura uma atividade de <xref:System.ServiceModel.Activities.CorrelationScope> que fornece gerenciamento implícito de atividades filhos de mensagem com um objeto de <xref:System.ServiceModel.Activities.CorrelationHandle> .|  
|[InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)|Cria e configura uma atividade de <xref:System.ServiceModel.Activities.InitializeCorrelation> que é usada para inicializar correlação sem enviar e receber uma mensagem.|  
|[Receber](../workflow-designer/receive-activity-designer.md)|Cria e configura uma atividade de <xref:System.ServiceModel.Activities.Receive> que receberá uma mensagem de um serviço.|  
|[ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)|Cria um par de pré-compilação configurado <xref:System.ServiceModel.Activities.Send> e atividades de <xref:System.ServiceModel.Activities.ReceiveReply> dentro de uma atividade de <xref:System.Activities.Statements.Sequence> .|  
|[Enviar](../workflow-designer/send-activity-designer.md)|Cria e configura uma atividade de <xref:System.ServiceModel.Activities.Send> que enviar uma mensagem a um serviço.|  
|[SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)|Cria um par de pré-compilação configurado <xref:System.ServiceModel.Activities.Receive> e atividades de <xref:System.ServiceModel.Activities.SendReply> dentro de uma atividade de <xref:System.Activities.Statements.Sequence> .|  
|[TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)|Cria e configura uma atividade de <xref:System.ServiceModel.Activities.TransactedReceiveScope> que permite ao fluxo de transações em um fluxo de trabalho.|  
  
## <a name="reference"></a>Referência  
 <xref:System.Activities.Activity>  
  
 <xref:System.ServiceModel.Activities.CorrelationScope>  
  
 <xref:System.ServiceModel.Activities.Receive>  
  
 <xref:System.ServiceModel.Activities.Send>  
  
 <xref:System.ServiceModel.Activities.ReceiveReply>  
  
 <xref:System.ServiceModel.Activities.SendReply>  
  
 <xref:System.ServiceModel.Activities.TransactedReceiveScope>  
  
## <a name="related-sections"></a>Seções relacionadas  
 Para outros tipos de designer de atividade, consulte os seguintes tópicos.  
  
 [Fluxo de Controle](../workflow-designer/control-flow-activity-designers.md)  
  
 [Usando os designers de atividade](../workflow-designer/using-the-activity-designers.md)  
  
 [Fluxograma](../workflow-designer/flowchart-activity-designers.md)  
  
 [Tempo de execução](../workflow-designer/runtime-activity-designers.md)  
  
 [Primitives](../workflow-designer/primitives-activity-designers.md)  
  
 [Transação](../workflow-designer/transaction-activity-designers.md)  
  
 [Coleção](../workflow-designer/collection-activity-designers.md)  
  
 [Tratamento de erro](../workflow-designer/error-handling-activity-designers.md)  
  
## <a name="external-resources"></a>Recursos externos  
 [Usando os designers de atividade](../workflow-designer/using-the-activity-designers.md)