---
title: Designer de fluxo de trabalho - Designer de modelo de ReceiveAndSendReply
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.ServiceModel.Activities.ReceiveAndSendReply.UI
- System.ServiceModel.Activities.SendReply.UI
ms.assetid: d1d9a058-df7e-48f5-a2e7-3caeeba7eaa6
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9c6b5a12b37509e6e5113c704ef2c3ff931ea32e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49886403"
---
# <a name="receiveandsendreply-template-designer"></a>Designer do modelo de ReceiveAndSendReply

O **ReceiveAndSendReply** modelo é usado para criar um par de pré-compilação configurado <xref:System.ServiceModel.Activities.Receive> e <xref:System.ServiceModel.Activities.SendReply> atividades. As atividades são parte de um <xref:System.Activities.Statements.Sequence> atividade e são correlacionadas como parte de um padrão de troca de mensagem de solicitação/resposta no servidor.

## <a name="the-receiveandsendreply-template"></a>O modelo de ReceiveAndSendReply

Adicionando um **ReceiveAndSendReply** modelo faz três coisas além de criar o <xref:System.ServiceModel.Activities.Receive> e <xref:System.ServiceModel.Activities.SendReply> atividades com um <xref:System.Activities.Statements.Sequence> atividade:

- Configura a <xref:System.ServiceModel.Activities.Receive.OperationName%2A> e <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> propriedades do <xref:System.ServiceModel.Activities.Receive> atividade.

- Associa a propriedade de <xref:System.ServiceModel.Activities.SendReply.Request%2A> de atividade de <xref:System.ServiceModel.Activities.Receive> a atividade de <xref:System.ServiceModel.Activities.Send> .

- Cria <xref:System.ServiceModel.Activities.CorrelationHandle> como um variável na atividade pai.

### <a name="use-the-receiveandsendreply-template-designer"></a>Use o designer de modelo de ReceiveAndSendReply

Acesso a **ReceiveAndSendReply** designer de atividade na **Messaging** categoria dos **caixa de ferramentas**. O **ReceiveAndSendReply** designer de atividade pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que as atividades são colocadas em geral. Soltar o designer de atividade cria uma <xref:System.ServiceModel.Activities.Receive> atividades que podem ser configuradas com o **enviar** designer de atividade e correlacionado <xref:System.ServiceModel.Activities.SendReply> que podem ser configurados com o designer de SendReplyToReceive.

Para obter mais informações sobre como usar o **Receive** designer para configurar a <xref:System.ServiceModel.Activities.Receive> atividade, consulte [Designer de atividade receber](../workflow-designer/receive-activity-designer.md).

### <a name="properties-of-sendreply"></a>Propriedades de SendReply

A tabela a seguir mostra as propriedades de <xref:System.ServiceModel.Activities.SendReply> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedades e alguns podem ser editados na superfície de Designer de fluxo de trabalho.


| Nome da Propriedade | Necessária | Uso |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | False | O nome amigável opcional de atividade de <xref:System.ServiceModel.Activities.SendReply> . O padrão é SendReplyToReceive.<br /><br /> Embora o uso de um valor não padrão para amigável <xref:System.Activities.Activity.DisplayName%2A> não é estritamente necessária, é melhor usar um valor. |
| <xref:System.ServiceModel.Activities.SendReply.Request%2A> | verdadeiro | Fazer referência a <xref:System.ServiceModel.Activities.Receive> a atividade emparelhada com esta atividade de <xref:System.ServiceModel.Activities.SendReply> . Essa propriedade não deve ser **nulo**. <xref:System.ServiceModel.Activities.Receive> e as atividades de <xref:System.ServiceModel.Activities.SendReply> são usados juntos no servidor para modelar um padrão de mensagem de solicitação/resposta. Esta propriedade especifica que a atividade de <xref:System.ServiceModel.Activities.Send> é emparelhada. No designer, você não pode editar essa propriedade porque ele é automaticamente associado para o <xref:System.ServiceModel.Activities.Send> atividade do qual você criou o <xref:System.ServiceModel.Activities.SendReply> atividade. |
| <xref:System.ServiceModel.Activities.SendReply.Content%2A> | False | Especifica o conteúdo de mensagem ou de parâmetro para receber. Pode ser uma atividade de <xref:System.ServiceModel.Activities.ReceiveMessageContent> ou uma atividade de <xref:System.ServiceModel.Activities.ReceiveParametersContent> . Editar esta propriedade clicando no botão de reticências próximo à **conteúdo** campo na grade de propriedade ou clicando o **definir** lado a **conteúdo** rótulo em que o  **Receber** superfície do designer de atividade. Ambos exibe a **definição de conteúdo** caixa de diálogo. Para obter mais informações sobre como usar essa caixa, consulte o [caixa de diálogo de definição de conteúdo](../workflow-designer/content-definition-dialog-box.md) tópico. |
| <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> | False | Especifica a coleção de objetos de <xref:System.ServiceModel.Activities.CorrelationInitializer> que inicializam vários objetos de <xref:System.ServiceModel.Activities.CorrelationHandle> que configuram esta atividade de <xref:System.ServiceModel.Activities.Receive> dentro de fluxo de trabalho. Clique no botão de reticências ao lado de <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> propriedade na grade de propriedades para abrir o **adicionar inicializadores de correlação** caixa de diálogo. Para obter mais informações sobre como usar essa caixa, consulte o [caixa de diálogo Adicionar CorrelationInitializers](../workflow-designer/add-correlationinitializers-dialog-box.md) tópico. |
| <xref:System.ServiceModel.Activities.SendReply.Action%2A> | False | Especifica o cabeçalho da ação de mensagem. Se ele não foi explicitamente definido, seu valor padrão é:<br /><br /> <strong>https://tempuri.org/{service namespace de contrato} / {nome do contrato de serviço} / {nome da operação}</strong> |
| <xref:System.ServiceModel.Activities.SendReply.PersistBeforeSend%2A> | False | Especifica se a instância de fluxo de trabalho deve ser persistentes antes que a mensagem de resposta que é enviada. O valor padrão é **false**. |

## <a name="see-also"></a>Consulte também

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [Receber](../workflow-designer/receive-activity-designer.md)
- [Enviar](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)