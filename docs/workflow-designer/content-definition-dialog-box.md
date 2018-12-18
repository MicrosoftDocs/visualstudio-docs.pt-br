---
title: Designer de fluxo de trabalho - caixa de diálogo de definição de conteúdo
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- MessageContent.UI
ms.assetid: 7e4237c3-90a1-4149-bd8a-3643d1dde0df
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f8307db1858ba50d209e456dc17ddd36dcaab722
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49870765"
---
# <a name="content-definition-dialog-box"></a>Caixa de diálogo de conteúdo da definição

O **definição de conteúdo** caixa de diálogo é usada no Designer de fluxo de trabalho para configurar a **conteúdo** propriedades do <xref:System.ServiceModel.Activities.Send>, <xref:System.ServiceModel.Activities.Receive>, <xref:System.ServiceModel.Activities.SendReply>, e <xref:System.ServiceModel.Activities.ReceiveReply> atividades. Para obter mais informações sobre os designers de atividade que use essa caixa, consulte o [envie](../workflow-designer/send-activity-designer.md), [Receive](../workflow-designer/receive-activity-designer.md), [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md), e [SendAndReceiveReply ](../workflow-designer/sendandreceivereply-template-designer.md) tópicos.

A tabela a seguir descreve os elementos de (UI) de interface do usuário para o **inicializar correlação** caixa de diálogo:

|Elemento da Interface do Usuário|Descrição|
|-|-----------------|
|**Message**|Especifica o conteúdo de mensagem com o **dados da mensagem** caixa de texto de expressão e o tipo usando o **tipo de mensagem** caixa de listagem suspensa. Por padrão, o **definição de conteúdo** usa o <xref:System.ServiceModel.Activities.ReceiveMessageContent>, que espera um <xref:System.ServiceModel.Channels.Message> ou um tipo na definição do serviço de fluxo de trabalho de contrato de mensagem.|
|**Parâmetros**|Clique o **parâmetros** botão de opção usar <xref:System.ServiceModel.Activities.ReceiveParametersContent>, que espera um contrato de dados. Use a grade de dados para definir uma coleção genérica de pares chave/valor de <xref:System.Activities.OutArgument> cujos valores são atribuídos aos parâmetros variáveis no fluxo de trabalho atual.|

O **definição de conteúdo** caixa de diálogo é usada pela **enviar**, **Receive**, **ReceiveAndSendReply**, e  **SendAndReceiveReply** designers. Acessá-lo é semelhante em cada caso e exemplos de receptor são usados aqui para ilustrar o procedimento.

O **Receive** designer de atividade pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que as atividades são colocadas em geral. Isso cria uma atividade de <xref:System.ServiceModel.Activities.Receive> com <xref:System.Activities.Activity.DisplayName%2A> padrão Receive. Selecione o **Receive** designer de atividade e clique no botão de reticências ao lado do texto (conteúdo) para o **conteúdo** propriedade na grade de propriedade para o **definiçãodeconteúdo**caixa de diálogo.

O conteúdo pode ser especificado dentro de **mensagem** seção para um <xref:System.ServiceModel.Activities.ReceiveMessageContent> atividade ou dentro o **parâmetro** seção para um <xref:System.ServiceModel.Activities.ReceiveParametersContent> atividade.

## <a name="see-also"></a>Consulte também

- [Ajuda da interface do usuário do Designer de Fluxo de Trabalho](../workflow-designer/workflow-designer-ui-help.md)