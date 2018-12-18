---
title: Designer de atividade do Designer de fluxo de trabalho - Confirm
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Statements.Confirm.UI
ms.assetid: c753b67b-b0e7-462a-bb4e-ba8db04a078d
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9f6823b564b7ec3da1585810c27db2f97c1b16ae
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49906527"
---
# <a name="confirm-activity-designer"></a>Confirme que o designer de atividades

O **Confirm** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.Confirm> atividade.

## <a name="the-confirm-activity"></a>A atividade de confirmação
 A atividade de <xref:System.Activities.Statements.Confirm> chama explicitamente <xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> para uma atividade contida em <xref:System.Activities.Statements.CompensableActivity>. Se a atividade de <xref:System.Activities.Statements.Confirm> não é usada dentro de <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>, <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>, ou <xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> de <xref:System.Activities.Statements.CompensableActivity>, então você deve especificar a propriedade de <xref:System.Activities.Statements.Confirm.Target%2A> .

 <xref:System.Activities.Statements.CompensationToken> especificado por <xref:System.Activities.Statements.Compensate.Target%2A> fornece um meio para confirmar ou compensar explicitamente <xref:System.Activities.Statements.CompensableActivity> uma vez que <xref:System.Activities.Statements.CompensableActivity.Body%2A> de <xref:System.Activities.Statements.CompensableActivity> terminou com êxito.

### <a name="using-the-confirm-activity-designer"></a>Usando o designer de atividade de confirmação
 O **Confirm** designer de atividade pode ser encontrado no **transação** categoria do **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas**guia no lado esquerdo do Designer de fluxo de trabalho. Como alternativa, selecione **caixa de ferramentas** da **exibição** menus ou pressione **Ctrl**+**Alt** + **X**.

 O **Confirm** designer de atividade pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que as atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Isso cria uma atividade de <xref:System.Activities.Statements.Confirm> com <xref:System.Activities.Activity.DisplayName%2A> padrão Confirmar. O <xref:System.Activities.Activity.DisplayName%2A> valor pode ser editado no cabeçalho do **confirmar** designer de atividade ou nos **DisplayName** caixa da grade de propriedade.

### <a name="the-confirm-properties"></a>As propriedades de confirmação
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.Confirm> e descreve como elas são usadas no designer. O <xref:System.Activities.Activity.DisplayName%2A> propriedade pode ser editada na grade de propriedade ou na superfície do Designer de fluxo de trabalho, mas o <xref:System.Activities.Statements.Confirm.Target%2A> propriedade deve ser editada na grade de propriedade.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|Especifica o nome amigável opcional de atividade de <xref:System.Activities.Statements.CancellationScope> . O padrão é confirma.|
|<xref:System.Activities.Statements.Confirm.Target%2A>|verdadeiro|Especifica <xref:System.Activities.InArgument%601> que contém <xref:System.Activities.Statements.CompensationToken> para esta atividade de <xref:System.Activities.Statements.Confirm> .|

## <a name="see-also"></a>Consulte também

- [Transação](../workflow-designer/transaction-activity-designers.md)
- [CancellationScope](../workflow-designer/cancellationscope-activity-designer.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensar](../workflow-designer/compensate-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)