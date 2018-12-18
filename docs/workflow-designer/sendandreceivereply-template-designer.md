---
title: Designer de fluxo de trabalho - Designer de modelo de SendAndReceiveReply
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.ServiceModel.Activities.SendAndReceiveReply.UI
- System.ServiceModel.Activities.ReceiveReply.UI
ms.assetid: 818a8c84-6593-416d-b016-1d91b85ffb68
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 22cdd114a11ff9d1b3b162009cc77d83aec1fd83
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49858960"
---
# <a name="sendandreceivereply-template-designer"></a>Designer do modelo de SendAndReceiveReply

O **SendAndReceiveReply** modelo é usado para criar um par de pré-compilação configurado <xref:System.ServiceModel.Activities.Send> e <xref:System.ServiceModel.Activities.ReceiveReply> atividades. As atividades são parte de um <xref:System.Activities.Statements.Sequence> atividade e são correlacionadas como parte de um padrão de troca de mensagem de solicitação/resposta no cliente.

## <a name="the-sendandreceivereply-template"></a>O modelo de SendAndReceiveReply

Adicionando o **SendAndReceiveReply** modelo faz três coisas além de criar o <xref:System.ServiceModel.Activities.Send> e <xref:System.ServiceModel.Activities.ReceiveReply> as atividades dentro de um <xref:System.Activities.Statements.Sequence> atividade:

- Configura a <xref:System.ServiceModel.Activities.Send.OperationName%2A> e <xref:System.ServiceModel.Activities.Send.ServiceContractName%2A> propriedades do <xref:System.ServiceModel.Activities.Send> atividade.

- Associa a propriedade de <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A> de atividade de <xref:System.ServiceModel.Activities.ReceiveReply> a atividade de <xref:System.ServiceModel.Activities.Send> .

- Cria <xref:System.ServiceModel.Activities.CorrelationHandle> como um variável na atividade pai.

### <a name="use-the-sendandreceivereply-template-designer"></a>Use o Designer de modelo de SendAndReceiveReply

Acesso a **SendAndReceiveReply** designer de atividade na **Messaging** categoria dos **caixa de ferramentas**. O **SendAndReceiveReply** designer de atividade pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que as atividades são colocadas em geral. Soltar o designer de atividade cria uma <xref:System.ServiceModel.Activities.Send> atividades que podem ser configuradas com o **enviar** designer de atividade e correlacionado <xref:System.ServiceModel.Activities.ReceiveReply> que podem ser configurados com o **ReceiveReplyForSend** designer.

Para obter mais informações sobre como usar o **envie** designer para configurar a <xref:System.ServiceModel.Activities.Send> atividade, consulte [enviar](../workflow-designer/send-activity-designer.md).

### <a name="properties-of-receivereply"></a>Propriedades de ReceiveReply

A tabela a seguir mostra o <xref:System.ServiceModel.Activities.ReceiveReply> propriedades e descreve como eles são usados no designer. Essas propriedades podem ser editadas na grade de propriedades e alguns podem ser editados na superfície de Designer de fluxo de trabalho.


| Nome da Propriedade | Necessária | Uso |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | False | O nome amigável opcional de atividade de <xref:System.ServiceModel.Activities.ReceiveReply> . O padrão é ReceiveReplyForSend.<br /><br /> Embora o uso de um valor não padrão para amigável <xref:System.Activities.Activity.DisplayName%2A> não é estritamente necessária, é melhor usar um valor. |
| <xref:System.ServiceModel.Activities.ReceiveReply.Request%2A> | verdadeiro | Fazer referência a <xref:System.ServiceModel.Activities.Send> a atividade emparelhada com esta atividade de <xref:System.ServiceModel.Activities.ReceiveReply> . Essa propriedade não deve ser **nulo**. <xref:System.ServiceModel.Activities.Send> e as atividades de <xref:System.ServiceModel.Activities.ReceiveReply> são usados juntos no cliente para modelar um padrão de mensagem de solicitação/resposta. Esta propriedade especifica que a atividade de <xref:System.ServiceModel.Activities.Send> é emparelhada. No designer, você não pode editar essa propriedade porque ele é automaticamente associado para o <xref:System.ServiceModel.Activities.Send> atividade do qual você criou o <xref:System.ServiceModel.Activities.ReceiveReply> atividade. |
| <xref:System.ServiceModel.Activities.ReceiveReply.Content%2A> | False | Especifica o conteúdo de mensagem ou de parâmetro para receber. Pode ser uma atividade de <xref:System.ServiceModel.Activities.ReceiveMessageContent> ou uma atividade de <xref:System.ServiceModel.Activities.ReceiveParametersContent> . Editar esta propriedade clicando no botão de reticências próximo à **conteúdo** campo na grade de propriedade ou clicando o **definir** lado a **conteúdo** rótulos no **Receive** superfície do designer de atividade. Ambos exibe a **definição de conteúdo** caixa de diálogo. Para obter mais informações sobre como usar essa caixa, consulte [caixa de diálogo de definição de conteúdo](../workflow-designer/content-definition-dialog-box.md). |
| <xref:System.ServiceModel.Activities.ReceiveReply.CorrelationInitializers%2A> | False | Especifica a coleção de objetos de <xref:System.ServiceModel.Activities.CorrelationInitializer> que inicializam vários objetos de <xref:System.ServiceModel.Activities.CorrelationHandle> que configuram esta atividade de <xref:System.ServiceModel.Activities.Receive> dentro de fluxo de trabalho. Clique no botão de reticências ao lado de <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> propriedade na grade de propriedades para abrir o **adicionar inicializadores de correlação** caixa de diálogo. Para obter mais informações sobre como usar essa caixa, consulte [caixa de diálogo Adicionar CorrelationInitializers](../workflow-designer/add-correlationinitializers-dialog-box.md). |
| <xref:System.ServiceModel.Activities.ReceiveReply.Action%2A> | False | Especifica o cabeçalho da ação de mensagem. Se ele não foi explicitamente definido, seu valor padrão é:<br /><br /> <strong>https://tempuri.org/{service namespace de contrato} / {nome do contrato de serviço} / {nome da operação}.</strong> |

## <a name="see-also"></a>Consulte também

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [Receber](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [Enviar](../workflow-designer/send-activity-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)