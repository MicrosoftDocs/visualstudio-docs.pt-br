---
title: Designer de fluxo de trabalho - Adicionar caixa de diálogo CorrelationInitializers
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- AddCorrelationInitializers.UI
ms.assetid: c0517467-d54a-4ee6-aef0-c19b96b6f395
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 724c4e3ac911e5fda62304a08565937f38425368
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49948948"
---
# <a name="add-correlationinitializers-dialog-box"></a>Adicione a caixa de diálogo CorrelationInitializers

O **adicionar inicializadores de correlação** caixa de diálogo é usada no Designer de fluxo de trabalho para configurar a **CorrelationInitializers** propriedades do <xref:System.ServiceModel.Activities.Send>, <xref:System.ServiceModel.Activities.Receive>, <xref:System.ServiceModel.Activities.SendReply>, e <xref:System.ServiceModel.Activities.ReceiveReply> atividades. Para obter mais informações sobre os designers de atividade que use essa caixa, consulte o [envie](../workflow-designer/send-activity-designer.md), [Receive](../workflow-designer/receive-activity-designer.md), [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md), e [SendAndReceiveReply ](../workflow-designer/sendandreceivereply-template-designer.md) tópicos.

Os inicializadores de correlação na coleção especificada com essa caixa de diálogo podem inicializar as seguintes correlações entre as atividades de mensagem:

- com base em consulta
- contexto
- contexto do retorno de chamada
- solicitação-resposta

A tabela a seguir descreve os elementos de (UI) de interface do usuário para o **adicionar inicializadores de correlação** caixa de diálogo:

|Elemento da Interface do Usuário|Descrição|
|-|-----------------|
|**Adicionar inicializador**|Clique o **initialize adicionar** caixa para adicionar um inicializador adicional à coleção.|
|**Tipo de correlação**|Especifica o tipo de inicializador de correlação. Há quatro tipos a escolher:<br /><br /> 1. Um inicializador de correlação de retorno de chamada para especificar <xref:System.ServiceModel.Activities.CallbackCorrelationInitializer>.<br />2. Um inicializador de correlação de contexto para especificar <xref:System.ServiceModel.Activities.CorrelationInitializer>.<br />3. Um inicializador de correlação de solicitação de resposta para especificar <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer>.<br />4. Um inicializador de correlação de consulta para especificar <xref:System.ServiceModel.Activities.QueryCorrelationInitializer>.<br /><br /> Para editar o **CorrelationType**<br /><br /> 1. Guia para a linha específica na **adicionar inicializador** DataGrid.<br />2. Para definir o foco **CorrelationTypeComboBox**, pressione **Ctrl**+**guia**.<br />3. Pressione Alt + seta para baixo para pop-up do **ComboBox** e editá-lo.|
|**Consultas XPath**|Um par chave/valor que contém as consultas usadas para extrair dados de correlação das mensagens de entrada e saída. Esta lista só é válido para usar <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> tipos.|

## <a name="to-launch-the-add-correlation-initializers-dialog-box"></a>Para iniciar a caixa de diálogo de inicializadores de adicionar correlação

 O **adicionar inicializadores de correlação** caixa de diálogo é usada pela **enviar**, **Receive**, **ReceiveAndSendReply**, e  **SendAndReceiveReply** designers. Acessá-lo é semelhante em cada caso e os casos envolvendo o **Receive** designer é usado aqui para ilustrar o procedimento.

 O **Receive** designer de atividade pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que as atividades são colocadas. Descartando o **Receive** designer de atividade cria uma <xref:System.ServiceModel.Activities.Receive> atividade com um padrão <xref:System.Activities.Activity.DisplayName%2A> de recebimento. Selecione o **Receive** designer de atividade e clique no botão de reticências ao lado do texto (coleção) para o **CorrelationInitializers** propriedade na grade de propriedade para o **adicionar Inicializadores de correlação** caixa de diálogo.

## <a name="see-also"></a>Consulte também

- [Adicionar caixa de diálogo correlação](http://msdn.microsoft.com/en-us/9e41a149-e8ab-41b1-8886-ea06a63041b6)
- [Caixa de diálogo Inicializar Correlação](../workflow-designer/initialize-correlation-dialog-box.md)