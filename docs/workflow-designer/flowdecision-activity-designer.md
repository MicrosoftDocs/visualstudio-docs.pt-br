---
title: Designer de fluxo de trabalho - Designer de atividade de FlowDecision
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Statements.FlowDecision.UI
ms.assetid: 4a49edc3-3662-4b7b-812e-0a5ba00d6c94
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4a87c5c9ebe1b3eed2c3c569e508c5b76ce6845d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49818985"
---
# <a name="flowdecision-activity-designer"></a>Designer de atividade de FlowDecision

O nó de <xref:System.Activities.Statements.FlowDecision> é um nó condicional que fornece uma ramificação para o fluxo de controle em uma das duas alternativas com base em se uma condição especificada é satisfeita. Se o fluxo requer mais de duas ramificações, use <xref:System.Activities.Statements.FlowSwitch%601> em vez disso.

## <a name="the-flowdecision-node"></a>O nó de FlowDecision

Use <xref:System.Activities.Statements.FlowDecision> quando o fluxo pode ser transformada em dois caminhos. Um nó de <xref:System.Activities.Statements.FlowDecision> tem <xref:System.Activities.Statements.FlowDecision.Condition%2A> e <xref:System.Activities.Statements.FlowNode> associados a cada um dos dois resultados possíveis: <xref:System.Activities.Statements.FlowDecision.True%2A> ou <xref:System.Activities.Statements.FlowDecision.False%2A>. <xref:System.Activities.Statements.FlowDecision.Condition%2A> é avaliado e o valor da avaliação determina <xref:System.Activities.Statements.FlowNode> a seguir seja processado dentro de <xref:System.Activities.Statements.Flowchart>.

### <a name="using-the-flowdecision-designer"></a>Utilizando o designer de FlowDecision

O **FlowDecision** designer pode ser encontrada na **fluxograma** categoria dos **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas** guia no Designer de fluxo de trabalho. Como alternativa, selecione **caixa de ferramentas** da **exibição** menus ou pressione **Ctrl**+**Alt** + **X**.

O **FlowDecision** designer pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho dentro de um **fluxograma** designer de atividade. Isso cria uma <xref:System.Activities.Statements.FlowDecision> rotulado **decisão** dentro de <xref:System.Activities.Statements.Flowchart> atividade. Passe o mouse sobre o designer e o **verdadeira** e **False** alças de quadradas para os dois ramificações aparecem.

Após arrastar o **FlowDecision** designer e outros designers na **fluxograma**, os nós podem ser associados juntos para especificar a ordem de execução. Para criar um vínculo entre um nó de origem (incluindo o **verdadeira** e **falso** ramificações da **FlowDecision**) e um nó de destino, o mouse sobre o designer do nó de origem e quadradas alças aparecem em cada lado dele. Clique em uma das alças de quadradas e arraste-a segurando o botão do mouse na uma das alças que aparece de maneira similar ao redor do nó de destino quando você o mouse sobre ele. Liberar o botão do mouse e um link é criado no meio esses dois nós que é representado como uma seta do designer de origem para o designer de destino.

A expressão que indica o <xref:System.Activities.Statements.FlowDecision.Condition%2A> podem ser digitados em de **condição** caixa da **propriedades** janela clicando em que o texto de dica que informa "Digite uma expressão de VB".

### <a name="the-flowdecision-properties"></a>As propriedades de FlowDecision

A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.FlowDecision> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade ou na superfície de designer.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Statements.FlowDecision.Condition%2A>|verdadeiro|A condição que determina que caminho o controle de fluxo leva.|
|<xref:System.Activities.Statements.FlowDecision.True%2A>|False|O caminho tomada pelo controle de fluxo se <xref:System.Activities.Statements.FlowDecision.Condition%2A> estiver satisfeito.|
|<xref:System.Activities.Statements.FlowDecision.False%2A>|False|O caminho tomada pelo controle de fluxo se <xref:System.Activities.Statements.FlowDecision.Condition%2A> não estiver satisfeito.|

## <a name="see-also"></a>Consulte também

- [Fluxograma](../workflow-designer/flowchart-activity-designers.md)
- [Fluxograma](../workflow-designer/flowchart-activity-designer.md)
- [FlowSwitch\<T>](../workflow-designer/flowswitch-t-activity-designer.md)