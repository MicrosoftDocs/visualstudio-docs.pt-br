---
title: Designer de atividade FlowDecision | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Statements.FlowDecision.UI
ms.assetid: 4a49edc3-3662-4b7b-812e-0a5ba00d6c94
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 7109b779cf33d226f44853e3f67c8609bd42fc1b
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49212882"
---
# <a name="flowdecision-activity-designer"></a>Designer de atividade de FlowDecision
O nó de <xref:System.Activities.Statements.FlowDecision> é um nó condicional que fornece uma ramificação para o fluxo de controle em uma das duas alternativas com base em se uma condição especificada é satisfeita. Se o fluxo requer mais de duas ramificações, use <xref:System.Activities.Statements.FlowSwitch%601> em vez disso.  
  
## <a name="the-flowdecision-node"></a>O nó de FlowDecision  
 Use <xref:System.Activities.Statements.FlowDecision> quando o fluxo pode ser transformada em dois caminhos. Um nó de <xref:System.Activities.Statements.FlowDecision> tem <xref:System.Activities.Statements.FlowDecision.Condition%2A> e <xref:System.Activities.Statements.FlowNode> associados a cada um dos dois resultados possíveis: <xref:System.Activities.Statements.FlowDecision.True%2A> ou <xref:System.Activities.Statements.FlowDecision.False%2A>. <xref:System.Activities.Statements.FlowDecision.Condition%2A> é avaliado e o valor da avaliação determina <xref:System.Activities.Statements.FlowNode> a seguir seja processado dentro de <xref:System.Activities.Statements.Flowchart>.  
  
### <a name="using-the-flowdecision-designer"></a>Utilizando o designer de FlowDecision  
 O **FlowDecision** designer pode ser encontrada na **fluxograma** categoria dos **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas** Guia de [!INCLUDE[wfd2](../includes/wfd2-md.md)] (como alternativa, selecione **barra de ferramentas** da **exibição** menu, ou CTRL + ALT + X.)  
  
 O **FlowDecision** designer pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície dentro de um **fluxograma** designer de atividade. Isso cria uma <xref:System.Activities.Statements.FlowDecision> rotulado **decisão** dentro de <xref:System.Activities.Statements.Flowchart> atividade. Passe o mouse sobre o designer e o **verdadeira** e **False** alças de quadradas para os dois ramificações aparecem.  
  
 Após arrastar o **FlowDecision** designer e outros designers na **fluxograma**, os nós podem ser associados juntos para especificar a ordem de execução. Para criar um vínculo entre um nó de origem (incluindo o **verdadeira** e **falso** ramificações da **FlowDecision**) e um nó de destino, o mouse sobre o designer do nó de origem e quadradas alças aparecem em cada lado dele. Clique em uma das alças de quadradas e arraste-a segurando o botão do mouse na uma das alças que aparece de maneira similar ao redor do nó de destino quando você o mouse sobre ele. Liberar o botão do mouse e um link é criado no meio esses dois nós que é representado como uma seta do designer de origem para o designer de destino.  
  
 A expressão que indica o <xref:System.Activities.Statements.FlowDecision.Condition%2A> podem ser digitados em de **condição** caixa da **propriedades** janela clicando em que o texto de dica que informa "Digite uma expressão de VB".  
  
### <a name="the-flowdecision-properties"></a>As propriedades de FlowDecision  
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.FlowDecision> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade ou na superfície de designer.  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Statements.FlowDecision.Condition%2A>|verdadeiro|A condição que determina que caminho o controle de fluxo leva.|  
|<xref:System.Activities.Statements.FlowDecision.True%2A>|False|O caminho tomada pelo controle de fluxo se <xref:System.Activities.Statements.FlowDecision.Condition%2A> estiver satisfeito.|  
|<xref:System.Activities.Statements.FlowDecision.False%2A>|False|O caminho tomada pelo controle de fluxo se <xref:System.Activities.Statements.FlowDecision.Condition%2A> não estiver satisfeito.|  
  
## <a name="see-also"></a>Consulte também  
 [Fluxograma](../workflow-designer/flowchart-activity-designers.md)   
 [Fluxograma](../workflow-designer/flowchart-activity-designer.md)   
 [FlowSwitch\<T>](../workflow-designer/flowswitch-t-activity-designer.md)