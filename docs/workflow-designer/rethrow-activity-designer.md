---
title: Designer de fluxo de trabalho - Designer de atividade de relançar
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Rethrow.UI
ms.assetid: 9cfa2eda-395f-4cf3-9154-83fadd4f7452
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 558ff5a36d172b8cd1fef0b811d1eaa920b90c6d
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55913870"
---
# <a name="rethrow-activity-designer"></a>Designer de atividade de Relançar

O **relançar** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.Rethrow> atividade.

## <a name="the-rethrow-activity"></a>A atividade de relançar

A atividade de <xref:System.Activities.Statements.Rethrow> lança uma exceção lançada anteriormente. Esta atividade somente pode ser usada em um manipulador de <xref:System.Activities.Statements.Catch> na atividade de <xref:System.Activities.Statements.TryCatch> .

### <a name="use-the-rethrow-activity-designer"></a>Use o Designer de atividade de relançar

Acesso a **relançar** designer de atividade na **tratamento de erros** categoria dos **caixa de ferramentas**. O **relançar** designer de atividade pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que as atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Soltar o designer de atividade cria uma <xref:System.Activities.Statements.Rethrow> atividade com um padrão **DisplayName** throw. O <xref:System.Activities.Activity.DisplayName%2A> valor pode ser editado no cabeçalho do **relançar** designer de atividade, ou nos **DisplayName** caixa da grade de propriedade.

### <a name="the-rethrow-properties"></a>As propriedades de relançar

A tabela a seguir mostra o <xref:System.Activities.Statements.Rethrow> propriedades e descreve como eles são usados no designer:

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|Especifica o nome amigável opcional de atividade de <xref:System.Activities.Statements.Rethrow> . O padrão é Relançar.|

## <a name="see-also"></a>Consulte também

- [Coleção](../workflow-designer/collection-activity-designers.md)
- [Throw](../workflow-designer/throw-activity-designer.md)
- [TryCatch](../workflow-designer/trycatch-activity-designer.md)