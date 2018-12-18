---
title: Designer de fluxo de trabalho - Designer de atividade de CompensableActivity
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Statements.CompensableActivity.UI
ms.assetid: e0340d89-d39e-4a52-8557-13e27040d7b5
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7257e7cc31e0503c7e466bbf4f8c9dd02e5fe15a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49836119"
---
# <a name="compensableactivity-activity-designer"></a>Designer de atividade de CompensableActivity

O **CompensableActivity** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.CompensableActivity> atividade.

## <a name="the-compensableactivity-activity"></a>A atividade de CompensableActivity
 <xref:System.Activities.Statements.CompensableActivity> define uma unidade de trabalho que pode ser compensado confirmada ou após a conclusão com êxito.

### <a name="using-the-compensableactivity-activity-designer"></a>Usando o designer de atividade de CompensableActivity
 O **CompensableActivity** designer de atividade pode ser encontrado na **transação** categoria de **caixa de ferramentas**. Para abrir **caixa de ferramentas**, selecione o **caixa de ferramentas** guia no lado esquerdo do Designer de fluxo de trabalho. Como alternativa, selecione **caixa de ferramentas** da **exibição** menus ou pressione **Ctrl**+**Alt** + **X**.

 O **CompensableActivity** designer de atividade pode ser arrastado de **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho. Você pode soltar o designer de atividade dentro de um <xref:System.Activities.Statements.Sequence>. Soltar o designer de atividade cria uma <xref:System.Activities.Statements.CompensableActivity> atividade com um padrão <xref:System.Activities.Activity.DisplayName%2A> de CompensableActivity. Editar o <xref:System.Activities.Activity.DisplayName%2A> valor do cabeçalho do **CompensableActivity** designer de atividade. Ele também pode ser editado na **DisplayName** caixa da grade de propriedade.

### <a name="the-compensableactivity-properties"></a>As propriedades de CompensableActivity
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.CompensableActivity> e descreve como elas são usadas no designer. O <xref:System.Activities.Activity.DisplayName%2A> e <xref:System.Activities.Activity%601.Result%2A> propriedade pode ser editada na grade de propriedade mas outras propriedades devem ser editadas na superfície de Designer de fluxo de trabalho.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável opcional de atividade de <xref:System.Activities.Statements.CompensableActivity> . O padrão é CompensableActivity.|
|<xref:System.Activities.Activity%601.Result%2A>|False|Especifica o valor de retorno de <xref:System.Activities.Statements.CompensableActivity>. Esta propriedade deve ser editada na grade de propriedade.|
|<xref:System.Activities.Statements.CompensableActivity.Body%2A>|verdadeiro|Especifica a atividade para que a compensação, cancelamento, e a lógica de confirmação são fornecidos. Para adicionar o <xref:System.Activities.Statements.CompensableActivity.Body%2A> atividade, soltar uma atividade de **caixa de ferramentas** para o **corpo** caixa no **CompensableActivity** designer de atividade. Adicione o texto de dica "Soltar atividade aqui".|
|<xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>|False|Especifica a atividade que é executada quando há um cancelamento. Para adicionar a atividade, soltar o designer de **caixa de ferramentas** para o **CancellationHandler** caixa no **CompensableActivity** designer de atividade. Adicione texto de dica "Descartar atividade aqui".|
|<xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>|False|Especifica a atividade a ser executada para compensar a atividade de <xref:System.Activities.Statements.CompensableActivity.Body%2A> . Esse manipulador pode ser chamado explicitamente usando a atividade de <xref:System.Activities.Statements.Compensate> .<br /><br /> Para adicionar a atividade, soltar o designer de atividade de **caixa de ferramentas** para o **CompensationHandler** caixa no **CompensableActivity** designer de atividade. Adicione texto de dica "Descartar atividade aqui".|
|<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A>|False|Especifica a atividade a ser executada para confirmar a atividade de <xref:System.Activities.Statements.CompensableActivity.Body%2A> . Esse manipulador pode ser chamado explicitamente usando a atividade de <xref:System.Activities.Statements.Confirm> .<br /><br /> Para adicionar a atividade, soltar o designer de atividade de **caixa de ferramentas** para o **ConfirmationHandler** caixa no **CompensableActivity** designer de atividade. Adicione texto de dica "Descartar atividade aqui".|

## <a name="see-also"></a>Consulte também

- [Transação](../workflow-designer/transaction-activity-designers.md)
- [CancellationScope](../workflow-designer/cancellationscope-activity-designer.md)
- [Compensar](../workflow-designer/compensate-activity-designer.md)
- [Confirmar](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)