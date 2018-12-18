---
title: Designer de modelo de ReceiveAndSendReply | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.ReceiveAndSendReply.UI
- System.ServiceModel.Activities.SendReply.UI
ms.assetid: d1d9a058-df7e-48f5-a2e7-3caeeba7eaa6
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 52d52d95ea6efe66e4888bdb81a9ce86633e8c11
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49935361"
---
# <a name="receiveandsendreply-template-designer"></a>Designer do modelo de ReceiveAndSendReply
O **ReceiveAndSendReply** modelo é usado para criar um par de pré-compilação configurado <xref:System.ServiceModel.Activities.Receive> e <xref:System.ServiceModel.Activities.SendReply> as atividades dentro de um <xref:System.Activities.Statements.Sequence> atividade que são correlacionadas como parte de uma troca de mensagens de solicitação/resposta padrão no servidor.  

## <a name="the-receiveandsendreply-template"></a>O modelo de ReceiveAndSendReply  
 Adicionando **ReceiveAndSendReply** modelo faz três coisas além de criar o <xref:System.ServiceModel.Activities.Receive> e <xref:System.ServiceModel.Activities.SendReply> atividades com um <xref:System.Activities.Statements.Sequence> atividade:  

1.  Configurar <xref:System.ServiceModel.Activities.Receive.OperationName%2A>, propriedades de <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> de atividade de <xref:System.ServiceModel.Activities.Receive> .  

2.  Associa a propriedade de <xref:System.ServiceModel.Activities.SendReply.Request%2A> de atividade de <xref:System.ServiceModel.Activities.Receive> a atividade de <xref:System.ServiceModel.Activities.Send> .  

3.  Cria <xref:System.ServiceModel.Activities.CorrelationHandle> como um variável na atividade pai.  

### <a name="using-the-receiveandsendreply-template-designer"></a>Usando o designer do modelo de ReceiveAndSendReply  
 O **ReceiveAndSendReply** designer de atividade pode ser encontrado na **Messaging** categoria dos **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas**  na guia [!INCLUDE[wfd2](../includes/wfd2-md.md)] (como alternativa, selecione **barra de ferramentas** do **exibição** menu, ou CTRL + ALT + X.)  

 O **ReceiveAndSendReply** designer de atividade pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície onde quer que as atividades são colocadas em geral. Isso cria uma <xref:System.ServiceModel.Activities.Receive> atividades que podem ser configuradas com o **enviar** designer de atividade e correlacionado <xref:System.ServiceModel.Activities.SendReply> que podem ser configurados com o designer de SendReplyToReceive.  

 [!INCLUDE[crabout](../includes/crabout-md.md)] usando o **Receive** designer para configurar a <xref:System.ServiceModel.Activities.Receive> atividade, consulte o [Receive](../workflow-designer/receive-activity-designer.md) tópico.  

 [!INCLUDE[crabout](../includes/crabout-md.md)] usando o **SendReplyToReceive** designer para configurar o <xref:System.ServiceModel.Activities.SendReply> atividade, consulte a seção a seguir.  

### <a name="properties-of-sendreply"></a>Propriedades de SendReply  
 A tabela a seguir mostra as propriedades de <xref:System.ServiceModel.Activities.SendReply> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedades e alguns podem ser editados na superfície do designer de [!INCLUDE[wfd2](../includes/wfd2-md.md)] .  


|                               Nome da Propriedade                                | Necessária |                                                                                                                                                                                                                                                                                                                                                      Uso                                                                                                                                                                                                                                                                                                                                                       |
|----------------------------------------------------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              <xref:System.Activities.Activity.DisplayName%2A>              |  False   |                                                                                                                                                                                            O nome amigável opcional de atividade de <xref:System.ServiceModel.Activities.SendReply> . O padrão é SendReplyToReceive.<br /><br /> Embora o uso de um valor não padrão para <xref:System.Activities.Activity.DisplayName%2A> amigável não é necessário restrita, é uma prática recomendada usar um valor.                                                                                                                                                                                             |
|         <xref:System.ServiceModel.Activities.SendReply.Request%2A>         |   verdadeiro   | Fazer referência a <xref:System.ServiceModel.Activities.Receive> a atividade emparelhada com esta atividade de <xref:System.ServiceModel.Activities.SendReply> . Essa propriedade não deve ser **nulo**. <xref:System.ServiceModel.Activities.Receive> e as atividades de <xref:System.ServiceModel.Activities.SendReply> são usados juntos no servidor para modelar um padrão de mensagem de solicitação/resposta. Esta propriedade especifica que a atividade de <xref:System.ServiceModel.Activities.Send> é emparelhada. No designer, você não pode editar esta propriedade como é associada automaticamente a atividade de <xref:System.ServiceModel.Activities.Send> de que você criou a atividade de <xref:System.ServiceModel.Activities.SendReply> . |
|         <xref:System.ServiceModel.Activities.SendReply.Content%2A>         |  False   |                       Especifica o conteúdo de mensagem ou de parâmetro para receber. Pode ser uma atividade de <xref:System.ServiceModel.Activities.ReceiveMessageContent> ou uma atividade de <xref:System.ServiceModel.Activities.ReceiveParametersContent> . Editar esta propriedade clicando no botão de elipse ao lado de **conteúdo** campo na grade de propriedade ou clicando no **definir...** botão ao lado de **conteúdo** do rótulo no **Receive** superfície do designer de atividade. Ambos exibe a **definição de conteúdo** caixa de diálogo. [!INCLUDE[crabout](../includes/crabout-md.md)] como usar essa caixa, consulte o [caixa de diálogo de definição de conteúdo](../workflow-designer/content-definition-dialog-box.md) tópico.                       |
| <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> |  False   |            Especifica a coleção de objetos de <xref:System.ServiceModel.Activities.CorrelationInitializer> que inicializam vários objetos de <xref:System.ServiceModel.Activities.CorrelationHandle> que configuram esta atividade de <xref:System.ServiceModel.Activities.Receive> dentro de fluxo de trabalho. Clique no botão de reticências ao lado de <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> propriedade na grade de propriedades para abrir o **adicionar inicializadores de correlação** caixa de diálogo. [!INCLUDE[crabout](../includes/crabout-md.md)] usando esta caixa, consulte o [caixa de diálogo Adicionar CorrelationInitializers](../workflow-designer/add-correlationinitializers-dialog-box.md) tópico.            |
|         <xref:System.ServiceModel.Activities.SendReply.Action%2A>          |  False   |                                                                                                                                                                                                                                              Especifica o cabeçalho da ação de mensagem. Se não é explicitamente definida, seu valor por padrão:<br /><br /> <strong>https://tempuri.org/{service namespace de contrato} / {nome do contrato de serviço} / {nome da operação}</strong>                                                                                                                                                                                                                                              |
|    <xref:System.ServiceModel.Activities.SendReply.PersistBeforeSend%2A>    |  False   |                                                                                                                                                                                                                                                                                          Especifica se a instância de fluxo de trabalho deve ser persistentes antes que a mensagem de resposta que é enviada. O valor padrão é **false**.                                                                                                                                                                                                                                                                                           |

## <a name="see-also"></a>Consulte também  
 [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)   
 [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)   
 [Receber](../workflow-designer/receive-activity-designer.md)   
 [Enviar](../workflow-designer/send-activity-designer.md)   
 [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)   
 [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)