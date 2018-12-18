---
title: Se o Designer de atividade | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Statements.If.UI
ms.assetid: 930a8fa2-db98-43e9-ad6d-a85cc7a6519a
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: fee98f4b95d626e429662d20501541c3241a9b2e
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49244225"
---
# <a name="if-activity-designer"></a>Se designer de atividades
A atividade de <xref:System.Activities.Statements.If> avalia uma condição e executa uma atividade dependendo dos resultados da avaliação. Esta atividade é mais útil ao usar um estilo modelando procedural de programação. Uma atividade de <xref:System.Activities.Statements.If> pode ser aninhadas dentro de uma atividade de <xref:System.Activities.Statements.Sequence> ou uma atividade de <xref:System.Activities.Statements.Parallel> , por exemplo. Se você estiver usando uma atividade de <xref:System.Activities.Statements.Flowchart> , considere usar uma atividade de <xref:System.Activities.Statements.FlowDecision> em vez disso.  
  
## <a name="if-properties-in-the-workflow-designer"></a>Se as propriedades em Designer de Fluxo de Trabalho  
 A tabela a seguir mostra as propriedades mais úteis de atividade de <xref:System.Activities.Statements.If> e descreve como usá-los no designer.  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Statements.If.Condition%2A>|verdadeiro|A condição que determina que atividade filho para executar. Para definir a <xref:System.Activities.Statements.If.Condition%2A>, digite um [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] expressão na **condição** caixa no **se** atividade designer ou na grade de propriedade.|  
|<xref:System.Activities.Statements.If.Else%2A>|False|A atividade a executar se a <xref:System.Activities.Statements.If.Condition%2A> está **falso**. Para adicionar uma atividade que é executada pelo <xref:System.Activities.Statements.If.Else%2A> ramificar, soltar uma atividade do **caixa de ferramentas** para o **Else** caixa no **se** designer de atividade com o texto de dica " Soltar atividade aqui".|  
|<xref:System.Activities.Statements.If.Then%2A>|False|A atividade a executar se a <xref:System.Activities.Statements.If.Condition%2A> está **verdadeiro**. Para adicionar uma atividade que é executada pelo <xref:System.Activities.Statements.If.Then%2A> ramificar, soltar uma atividade do **caixa de ferramentas** para o **, em seguida,** caixa no **se** designer de atividade com o texto de dica " Soltar atividade aqui".|  
  
## <a name="see-also"></a>Consulte também  
 [Sequência](../workflow-designer/sequence-activity-designer.md)   
 [Paralelo](../workflow-designer/parallel-activity-designer.md)   
 [Fluxo de Controle](../workflow-designer/control-flow-activity-designers.md)