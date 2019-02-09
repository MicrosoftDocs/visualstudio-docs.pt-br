---
title: Designer de fluxo de trabalho - Designer de atividade de CancellationScope
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.CancellationScope.UI
ms.assetid: 2c85d663-b219-4142-9866-7693ffd46379
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 43a818be208c7e07ef74a8f35923f3042bb8fad5
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55938157"
---
# <a name="cancellationscope-activity-designer"></a>Designer de atividade de CancellationScope

O **CancellationScope** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.CancellationScope> atividade.

## <a name="the-cancellationscope-activity"></a>A atividade de CancellationScope

A atividade de <xref:System.Activities.Statements.CancellationScope> permite que você especifique uma atividade para a lógica de execução e cancelar para a atividade.

### <a name="using-the-cancellationscope-activity-designer"></a>Usando o designer de atividade de CancellationScope

O **CancellationScope** designer de atividade pode ser encontrado na **transação** categoria de **caixa de ferramentas**. Para abrir **caixa de ferramentas**, selecione o **caixa de ferramentas** guia do Designer de fluxo de trabalho. Como alternativa, selecione **caixa de ferramentas** da **exibição** menus ou pressione **Ctrl**+**Alt** + **X**.

O **CancellationScope** designer de atividade pode ser arrastado de **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que as atividades são colocadas, como em um <xref:System.Activities.Statements.Sequence>. Descartando o **CancellationScope** designer de atividade cria uma <xref:System.Activities.Statements.CancellationScope> atividade com um padrão <xref:System.Activities.Activity.DisplayName%2A> de CancellationScope. Editar o <xref:System.Activities.Activity.DisplayName%2A> valor do cabeçalho do **CancellationScope** designer de atividade. Você também pode editá-lo na **DisplayName** caixa da grade de propriedade.

### <a name="the-cancellationscope-properties"></a>As propriedades de CancellationScope

A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.CancellationScope> e descreve como elas são usadas no designer. O <xref:System.Activities.Activity.DisplayName%2A> propriedade pode ser editada na grade de propriedade mas outras propriedades devem ser editadas na superfície do Designer de fluxo de trabalho.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável opcional de atividade de <xref:System.Activities.Statements.CancellationScope> . O padrão é CancellationScope. Embora o valor de <xref:System.Activities.Activity.DisplayName%2A> não é necessário restrita, é uma prática recomendada usar um.|
|<xref:System.Activities.Statements.CancellationScope.Body%2A>|verdadeiro|Especifica a atividade para que a lógica cancelar é fornecida. Para adicionar o <xref:System.Activities.Statements.CancellationScope.Body%2A> atividade, soltar uma atividade de **caixa de ferramentas** para o **corpo** caixa no **CancellationScope** designer de atividade. Adicione o texto da dica "Descartar atividade aqui".|
|<xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>|verdadeiro|Especifica a atividade que é executada se houver um cancelamento. Para adicionar o <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> atividade, soltar uma atividade de **caixa de ferramentas** para o **CancellationHandler** caixa no **CancellationScope** designer de atividade. Adicione o texto da dica "Descartar atividade aqui".|

## <a name="see-also"></a>Consulte também

- [Transação](../workflow-designer/transaction-activity-designers.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensar](../workflow-designer/compensate-activity-designer.md)
- [Confirmar](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)