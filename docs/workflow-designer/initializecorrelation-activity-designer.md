---
title: Designer de fluxo de trabalho - Designer de atividade de InitializeCorrelation
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.ServiceModel.Activities.InitializeCorrelation.UI
ms.assetid: 4c54f34c-ee84-42a6-abb0-ec260c1ccb76
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7f72cb538018588ab11335be5a99fe86b5c474c3
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49879877"
---
# <a name="initializecorrelation-activity-designer"></a>Designer de atividade de InitializeCorrelation

O **InitializeCorrelation** designer de atividade é usado para criar e configurar um <xref:System.ServiceModel.Activities.InitializeCorrelation> atividade. O <xref:System.ServiceModel.Activities.InitializeCorrelation> atividade estabelece uma correlação entre mensagens antes de enviar ou recebê-los.

## <a name="the-initializecorrelation-activity"></a>A atividade de InitializeCorrelation

Uma atividade de <xref:System.ServiceModel.Activities.InitializeCorrelation> é usada para inicializar correlações sem enviar e receber uma mensagem. Correlação é inicializada normalmente ao enviar ou para receber uma mensagem. Se correlação deve ser estabelecida antes que uma mensagem ser enviada ou recebida, use <xref:System.ServiceModel.Activities.InitializeCorrelation> para inicializar correlação.

### <a name="using-the-initializecorrelation-activity-designer"></a>Usando o designer de atividade de InitializeCorrelation

Acesso a **InitializeCorrelation** designer de atividade na **Messaging** categoria dos **caixa de ferramentas**.

O **InitializeCorrelation** designer de atividade pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho. Soltar o designer de atividade cria uma <xref:System.ServiceModel.Activities.InitializeCorrelation> atividade com um padrão <xref:System.Activities.Activity.DisplayName%2A> de InitializeCorrelation. O <xref:System.Activities.Activity.DisplayName%2A> pode ser editado no cabeçalho do **InitializeCorrelation** designer de atividade ou nos **DisplayName** caixa do **propriedades** janela.

O <xref:System.ServiceModel.Activities.CorrelationHandle> pode ser especifica na **correlação** campo **as propriedades** janela no **InitializeCorrelation** superfície do designer de atividade.

Para exibir o **inicializar correlação** caixa de diálogo onde você pode especificar o identificador da correlação e os pares de chave-valor usados para inicializá-lo, selecione o botão de reticências ao lado de **CorrelationData** campo **propriedades** janela. Ou, selecione o texto de dica de "Modo de exibição..." sobre o **InitializeCorrelation** superfície do designer de atividade. Para obter mais informações sobre como usar essa caixa de diálogo, consulte a [caixa de diálogo do Editor de coleção de tipo](../workflow-designer/type-collection-editor-dialog-box.md) artigo.

### <a name="the-initializecorrelation-properties"></a>As propriedades de InitializeCorrelation

A tabela a seguir mostra o <xref:System.ServiceModel.Activities.InitializeCorrelation> propriedades e descreve como eles são usados no designer. Essas propriedades podem ser editadas na **propriedades** janela ou na superfície do Designer de fluxo de trabalho.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.ServiceModel.Activities.InitializeCorrelation> . O valor padrão é InitializeCorrelation.<br /><br /> Embora o uso de um valor não padrão para amigável <xref:System.Activities.Activity.DisplayName%2A> não é estritamente necessária, é recomendável.|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.Correlation%2A>|False|<xref:System.ServiceModel.Activities.CorrelationHandle> usado para associar atividades de fluxo de trabalho em correlação.|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>|False|Um dicionário de dados de correlação que se relacionam mensagens ao fluxo de trabalho instância.<br /><br /> Use o **inicializar correlação** caixa de diálogo para configurar o <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>. Para obter mais informações sobre o uso esta caixa de diálogo, consulte a [caixa de diálogo do Editor de coleção de tipo](../workflow-designer/type-collection-editor-dialog-box.md) artigo.|

## <a name="see-also"></a>Consulte também

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [Receber](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [Enviar](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)