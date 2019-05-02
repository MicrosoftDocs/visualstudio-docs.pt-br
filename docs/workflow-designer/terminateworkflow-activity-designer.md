---
title: Designer de fluxo de trabalho - Designer de atividade de TerminateWorkflow
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.TerminateWorkflow.UI
ms.assetid: 08e632ed-0724-4fb4-9df1-f8d443eaf0ac
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 662366e3b0c0558170c117104d20a1bcb6417615
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62434027"
---
# <a name="terminateworkflow-activity-designer"></a>Designer de atividade de TerminateWorkflow

O **TerminateWorkflow** designer de atividade é usado para criar e configurar um <xref:System.Activities.Statements.TerminateWorkflow> atividade.

## <a name="the-terminateworkflow-activity"></a>A atividade de TerminateWorkflow

A atividade de <xref:System.Activities.Statements.TerminateWorkflow> finaliza a execução de um fluxo de trabalho.

### <a name="using-the-terminateworkflow-activity-designer"></a>Usando o designer de atividade de TerminateWorkflow

O **TerminateWorkflow** designer de atividade pode ser encontrado na **tempo de execução** categoria dos **caixa de ferramentas**, que é acessado clicando o **dacaixadeferramentas** guia (como alternativa, selecione **caixa de ferramentas** da **exibição** menu ou CTRL + ALT + X.)

O **TerminateWorkflow** designer de atividade pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que as atividades são colocadas em geral, como em um <xref:System.Activities.Statements.Sequence>. Isso cria uma <xref:System.Activities.Statements.TerminateWorkflow> atividade com um padrão **DisplayName** de TerminateWorkflow. O <xref:System.Activities.Activity.DisplayName%2A> pode ser editado no cabeçalho do **TerminateWorkflow** designer de atividade ou nos **DisplayName** caixa da grade de propriedade.

### <a name="the-terminateworkflow-properties"></a>As propriedades de TerminateWorkflow

A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.TerminateWorkflow> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade e alguns deles podem ser editados na superfície do Designer de fluxo de trabalho.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|O nome amigável de atividade de <xref:System.Activities.Statements.TerminateWorkflow> . O padrão é TerminateWorkflow. Embora o nome para exibição não é necessário restrita, é uma prática recomendada usar um nome para exibição.|
|<xref:System.Activities.Statements.TerminateWorkflow.Exception%2A>|False|A exceção para indicar quando o fluxo de trabalho é encerrado. Defina essa propriedade na grade de propriedade.|
|<xref:System.Activities.Statements.TerminateWorkflow.Reason%2A>|False|A razão que explica como o fluxo de trabalho foi encerrado. Defina essa propriedade na grade de propriedade.|

## <a name="see-also"></a>Consulte também

- [Tempo de execução](../workflow-designer/runtime-activity-designers.md)
- [Persistir](../workflow-designer/persist-activity-designer.md)