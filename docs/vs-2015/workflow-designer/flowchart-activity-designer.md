---
title: Designer de atividade do fluxograma | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Flowchart.UI
- System.Activities.Statements.FlowStep.UI
- System.Activities.Core.Presentation.FlowStart.UI
ms.assetid: d5af2276-5215-4138-880a-cf2b90bbf3a0
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: 67bebeec9c2d88ba1912bc50b27e38f8278e7e3f
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49226233"
---
# <a name="flowchart-activity-designer"></a>Designer de atividade do fluxograma
A atividade de <xref:System.Activities.Statements.Flowchart> é usada para criar fluxos de trabalho que definem e gerencia controles de fluxo complexos. <xref:System.Activities.Statements.Flowchart> pode ser criado em código ou usando [!INCLUDE[wfd2](../includes/wfd2-md.md)]. Este tópico documenta a experiência de [!INCLUDE[wfd2](../includes/wfd2-md.md)] . O designer de atividade do fluxo de trabalho [!INCLUDE[wfd1](../includes/wfd1-md.md)] permite aos desenvolvedores para criar fluxos de trabalho em uma maneira natural.  
  
## <a name="the-flowchart-activity"></a>A atividade do fluxograma  
 <xref:System.Activities.Statements.Flowchart> especifica <xref:System.Activities.Statements.Flowchart.StartNode%2A> exclusivo que é executado quando o fluxo de trabalho inicia e usa uma rede de <xref:System.Activities.Statements.Flowchart.Nodes%2A> associado para criar loop arbitrários ou para desviar o fluxo de execução como em qualquer outro lugar no fluxo de trabalho a um determinado momento.  
  
### <a name="using-the-flowchart-activity-designer"></a>Usando o designer de atividade do fluxograma  
 O **fluxograma** designer de atividade pode ser encontrado na **fluxograma** categoria dos **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas**guia de [!INCLUDE[wfd2](../includes/wfd2-md.md)] (como alternativa, selecione **barra de ferramentas** do **exibição** menu ou CTRL + ALT + X.)  
  
 O **fluxograma** designer de atividade pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície onde quer que os designers de atividade são colocados normalmente, como uma atividade raiz ou como o filho de outra atividade de fluxo de controle. Se o **fluxograma** designer de atividade é solto em um espaço em branco [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície, ele cria um <xref:System.Activities.Statements.Flowchart> atividade, que, por padrão, apresenta-se em uma exibição expandida na qual é o nó inicial que inicia a execução representado como uma bola verde. Se o **fluxograma** designer de atividade é descartado em outra atividade de fluxo de controle, apresenta-se em uma exibição minimizada que pode ser expandida clicando duas vezes o **fluxograma** designer de atividade. Qualquer atividade na **caixa de ferramentas** podem ser arrastados diretamente para o **fluxograma** designer de atividade, incluindo outras atividades de fluxo de controle.  
  
 Após arrastar vários designers de atividade na tela de [!INCLUDE[wfd2](../includes/wfd2-md.md)] , os objetos de <xref:System.Activities.Activity> representam podem ser associados juntos para especificar ordem de execução. Para criar um link entre uma atividade de origem e uma atividade de destino, o mouse sobre o designer de atividade de origem e quadradas alças aparecem em cada lado deles. Clique em uma das alças de quadradas e arraste-a segurando o botão do mouse na uma das alças que aparece de maneira similar ao redor de atividade de destino para passa sobre ele com o mouse. Liberar o botão do mouse e um link é criado entre essas duas atividades que é representado como uma seta do designer de origem para o designer de destino.  
  
### <a name="flowchart-activity-properties"></a>Propriedades de atividade do fluxograma  
 A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.Flowchart> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade ou na superfície de designer.  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|Especifica o nome para exibição do designer de atividade no cabeçalho. O valor padrão é fluxograma. O valor pode ser editado na **propriedades** janela ou diretamente no cabeçalho do designer de atividade.<br /><br /> Embora não seja necessário <xref:System.Activities.Activity.DisplayName%2A> restrita, é uma prática recomendada usar um.|  
|<xref:System.Activities.Statements.Flowchart.Variables%2A>|False|A coleção de variáveis que são definidos no escopo deste <xref:System.Activities.Statements.Flowchart> para compartilhar o estado através das atividades filhos.|  
|<xref:System.Activities.Statements.Flowchart.StartNode%2A>|False|<xref:System.Activities.Statements.FlowNode> que é executado quando <xref:System.Activities.Statements.Flowchart> iniciar.|  
|<xref:System.Activities.Statements.Flowchart.Nodes%2A>|False|Contém a coleção de objetos <xref:System.Activities.Statements.FlowNode> em <xref:System.Activities.Statements.Flowchart>.|  
  
## <a name="see-also"></a>Consulte também  
 [Fluxograma](../workflow-designer/flowchart-activity-designers.md)   
 [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)   
 [FlowSwitch\<T>](../workflow-designer/flowswitch-t-activity-designer.md)