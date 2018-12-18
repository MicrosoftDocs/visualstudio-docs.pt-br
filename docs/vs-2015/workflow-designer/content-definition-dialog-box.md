---
title: Caixa de diálogo Definição de conteúdo | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- MessageContent.UI
ms.assetid: 7e4237c3-90a1-4149-bd8a-3643d1dde0df
caps.latest.revision: 3
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 0c0fffed6bbb8d9690f96679d910d5ac4a3b631e
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49176106"
---
# <a name="content-definition-dialog-box"></a>Caixa de diálogo de conteúdo da definição
O **definição de conteúdo** caixa de diálogo é usada em [!INCLUDE[wfd1](../includes/wfd1-md.md)] para configurar o **conteúdo** propriedades do <xref:System.ServiceModel.Activities.Send>, <xref:System.ServiceModel.Activities.Receive>, <xref:System.ServiceModel.Activities.SendReply>, e <xref:System.ServiceModel.Activities.ReceiveReply> atividades. [!INCLUDE[crabout](../includes/crabout-md.md)] os designers de atividade que usam essa caixa, consulte o [envie](../workflow-designer/send-activity-designer.md), [Receive](../workflow-designer/receive-activity-designer.md), [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md), e [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md) tópicos.  
  
 A tabela a seguir descreve os elementos de (UI) de interface do usuário para o **inicializar correlação** caixa de diálogo.  
  
|Elemento da Interface do Usuário|Descrição|  
|----------------|-----------------|  
|**Message**|Especifica o conteúdo de mensagem com o **dados da mensagem** caixa de texto de expressão e o tipo usando o **tipo de mensagem** caixa de listagem suspensa. Por padrão, o **definição de conteúdo** usa o <xref:System.ServiceModel.Activities.ReceiveMessageContent>, que espera um <xref:System.ServiceModel.Channels.Message> ou um tipo na definição do serviço de fluxo de trabalho de contrato de mensagem.|  
|**Parâmetros**|Clique o **parâmetros** botão de opção usar <xref:System.ServiceModel.Activities.ReceiveParametersContent>, que espera um contrato de dados. Use a grade de dados para definir uma coleção genérica de pares chave/valor de <xref:System.Activities.OutArgument> cujos valores são atribuídos aos parâmetros variáveis no fluxo de trabalho atual.|  
  
 O **definição de conteúdo** caixa de diálogo é usada pela **enviar**, **Receive**, **ReceiveAndSendReply**, e  **SendAndReceiveReply** designers. Acessá-lo é semelhante em cada caso e exemplos de receptor são usados aqui para ilustrar o procedimento.  
  
 O **Receive** designer de atividade pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície onde quer que as atividades são colocadas em geral. Isso cria uma atividade de <xref:System.ServiceModel.Activities.Receive> com <xref:System.Activities.Activity.DisplayName%2A> padrão Receive. Selecione o **Receive** designer de atividade e clique no botão de reticências ao lado do texto (conteúdo) para o **conteúdo** propriedade na grade de propriedade para o **definiçãodeconteúdo**caixa de diálogo.  
  
 O conteúdo pode ser especificado dentro de **mensagem** seção para um <xref:System.ServiceModel.Activities.ReceiveMessageContent> atividade ou dentro o **parâmetro** seção para um <xref:System.ServiceModel.Activities.ReceiveParametersContent> atividade.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda da interface do usuário do Designer de Fluxo de Trabalho](../workflow-designer/workflow-designer-ui-help.md)