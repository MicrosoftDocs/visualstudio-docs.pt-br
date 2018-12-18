---
title: Adicionar caixa de diálogo CorrelationInitializers | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- AddCorrelationInitializers.UI
ms.assetid: c0517467-d54a-4ee6-aef0-c19b96b6f395
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 4d4d69185bef36ab514c984716cc6606f6068fb4
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49275685"
---
# <a name="add-correlationinitializers-dialog-box"></a>Adicione a caixa de diálogo CorrelationInitializers
O **adicionar inicializadores de correlação** caixa de diálogo é usada em [!INCLUDE[wfd1](../includes/wfd1-md.md)] para configurar o **CorrelationInitializers** propriedades do <xref:System.ServiceModel.Activities.Send>, <xref:System.ServiceModel.Activities.Receive>, <xref:System.ServiceModel.Activities.SendReply>, e <xref:System.ServiceModel.Activities.ReceiveReply> atividades. [!INCLUDE[crabout](../includes/crabout-md.md)] os designers de atividade que usam essa caixa, consulte o [envie](../workflow-designer/send-activity-designer.md), [Receive](../workflow-designer/receive-activity-designer.md), [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md), e [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md) tópicos.  
  
 Inicializadores de correlação na coleção especificada com esta caixa de diálogo pode inicializar a consulta com base, o contexto, o contexto de retorno de chamada, ou se correlaciona de solicitação de resposta entre as atividades de mensagem.  
  
 A tabela a seguir descreve os elementos de (UI) de interface do usuário para o **adicionar inicializadores de correlação** caixa de diálogo.  
  
|Elemento da Interface do Usuário|Descrição|  
|----------------|-----------------|  
|**Adicionar inicializador**|Clique o **initialize adicionar** caixa para adicionar um inicializador adicional à coleção.|  
|**Tipo de correlação**|Especifica o tipo de inicializador de correlação. Há quatro tipos a escolher:<br /><br /> 1.  Um inicializador de correlação de retorno de chamada para especificar <xref:System.ServiceModel.Activities.CallbackCorrelationInitializer>.<br />2.  Um inicializador de correlação de contexto para especificar <xref:System.ServiceModel.Activities.CorrelationInitializer>.<br />3.  Um inicializador de correlação de solicitação de resposta para especificar <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer>.<br />4.  Um inicializador de correlação de consulta para especificar <xref:System.ServiceModel.Activities.QueryCorrelationInitializer>.<br /><br /> Para editar o **CorrelationType**<br /><br /> 1.  Guia para a linha específica na **adicionar inicializador** DataGrid.<br />2.  Pressione Ctrl + Tab para definir o foco para **CorrelationTypeComboBox**<br />3.  Pressione Alt + seta para baixo para pop-up do **ComboBox** e editá-lo.|  
|**Consultas XPath**|Um par chave/valor que contém as consultas usadas para extrair dados de correlação das mensagens de entrada e saída. Esta lista só é válido para usar <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> tipos.|  
  
## <a name="to-launch-the-add-correlation-initializers-dialog-box"></a>Para iniciar a caixa de diálogo de inicializadores de adicionar correlação  
 O **adicionar inicializadores de correlação** caixa de diálogo é usada pela **enviar**, **Receive**, **ReceiveAndSendReply**, e  **SendAndReceiveReply** designers. Acessá-lo é semelhante em cada caso e os casos envolvendo o **Receive** designer é usado aqui para ilustrar o procedimento.  
  
 O **Receive** designer de atividade pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície onde quer que as atividades são colocadas em geral. Isso cria uma atividade de <xref:System.ServiceModel.Activities.Receive> com <xref:System.Activities.Activity.DisplayName%2A> padrão Receive. Selecione o **Receive** designer de atividade e clique no botão de reticências ao lado do texto (coleção) para o **CorrelationInitializers** propriedade na grade de propriedade para o **adicionar Inicializadores de correlação** caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar caixa de diálogo correlação](http://msdn.microsoft.com/en-us/9e41a149-e8ab-41b1-8886-ea06a63041b6)   
 [Caixa de diálogo Inicializar Correlação](../workflow-designer/initialize-correlation-dialog-box.md)