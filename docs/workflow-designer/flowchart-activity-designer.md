---
title: Designer de fluxo de trabalho - Designer de atividade do fluxograma
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Statements.Flowchart.UI
- System.Activities.Statements.FlowStep.UI
- System.Activities.Core.Presentation.FlowStart.UI
ms.assetid: d5af2276-5215-4138-880a-cf2b90bbf3a0
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3468e4e09f8e31ae6b3e8bf7a49b7a1c368b3e73
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49877680"
---
# <a name="flowchart-activity-designer"></a>Designer de atividade do fluxograma

A atividade de <xref:System.Activities.Statements.Flowchart> é usada para criar fluxos de trabalho que definem e gerencia controles de fluxo complexos. Um <xref:System.Activities.Statements.Flowchart> podem ser criados no código ou usando o Designer de fluxo de trabalho. Este tópico documenta a experiência de Designer de fluxo de trabalho. O designer de atividade de fluxo de trabalho do Designer de fluxo de trabalho permite aos desenvolvedores criar fluxos de trabalho de uma maneira natural.

## <a name="the-flowchart-activity"></a>A atividade do fluxograma

<xref:System.Activities.Statements.Flowchart> especifica <xref:System.Activities.Statements.Flowchart.StartNode%2A> exclusivo que é executado quando o fluxo de trabalho inicia e usa uma rede de <xref:System.Activities.Statements.Flowchart.Nodes%2A> associado para criar loop arbitrários ou para desviar o fluxo de execução como em qualquer outro lugar no fluxo de trabalho a um determinado momento.

### <a name="using-the-flowchart-activity-designer"></a>Usando o designer de atividade do fluxograma

O **fluxograma** designer de atividade pode ser encontrado na **fluxograma** categoria dos **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas**guia no Designer de fluxo de trabalho. Como alternativa, selecione **caixa de ferramentas** da **exibição** menus ou pressione **Ctrl**+**Alt** + **X**.

O **fluxograma** designer de atividade pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que os designers de atividade são colocados normalmente, como uma atividade raiz ou como o filho de outra atividade de fluxo de controle. Se o **fluxograma** designer de atividade é descartado em uma superfície de Designer de fluxo de trabalho em branco, ele cria um <xref:System.Activities.Statements.Flowchart> atividade, que, por padrão, apresenta-se em uma exibição expandida na qual é o nó inicial que inicia a execução representado como uma bola verde. Se o **fluxograma** designer de atividade é descartado em outra atividade de fluxo de controle, apresenta-se em uma exibição minimizada que pode ser expandida clicando duas vezes o **fluxograma** designer de atividade. Qualquer atividade na **caixa de ferramentas** podem ser arrastados diretamente para o **fluxograma** designer de atividade, incluindo outras atividades de fluxo de controle.

Após arrastar vários designers de atividade para a tela do Designer de fluxo de trabalho, o <xref:System.Activities.Activity> objetos que representam podem ser vinculados juntos para especificar a ordem de execução. Para criar um link entre uma atividade de origem e uma atividade de destino, o mouse sobre o designer de atividade de origem e quadradas alças aparecem em cada lado deles. Clique em uma das alças de quadradas e arraste-a segurando o botão do mouse na uma das alças que aparece de maneira similar ao redor de atividade de destino para passa sobre ele com o mouse. Liberar o botão do mouse e um link é criado entre essas duas atividades que é representado como uma seta do designer de origem para o designer de destino.

### <a name="flowchart-activity-properties"></a>Propriedades de atividade do fluxograma

A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.Flowchart> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade ou na superfície de designer.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|Especifica o nome para exibição do designer de atividade no cabeçalho. O valor padrão é fluxograma. O valor pode ser editado na **propriedades** janela ou diretamente no cabeçalho do designer de atividade.<br /><br /> Embora não seja necessário <xref:System.Activities.Activity.DisplayName%2A> restrita, é uma prática recomendada usar um.|
|<xref:System.Activities.Statements.Flowchart.Variables%2A>|False|A coleção de variáveis que são definidos no escopo deste <xref:System.Activities.Statements.Flowchart> para compartilhar o estado através das atividades filhos.|
|<xref:System.Activities.Statements.Flowchart.StartNode%2A>|False|<xref:System.Activities.Statements.FlowNode> que é executado quando <xref:System.Activities.Statements.Flowchart> iniciar.|
|<xref:System.Activities.Statements.Flowchart.Nodes%2A>|False|Contém a coleção de objetos <xref:System.Activities.Statements.FlowNode> em <xref:System.Activities.Statements.Flowchart>.|

## <a name="see-also"></a>Consulte também

- [Fluxograma](../workflow-designer/flowchart-activity-designers.md)
- [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)
- [FlowSwitch\<T>](../workflow-designer/flowswitch-t-activity-designer.md)