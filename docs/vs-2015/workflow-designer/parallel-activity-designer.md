---
title: Designer de atividade em paralelo | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Parallel.UI
ms.assetid: 0306dc3b-075a-4091-ac3a-96486fbabed5
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: f557eb013cb313321b336fb22fd1299e51faaa82
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49221553"
---
# <a name="parallel-activity-designer"></a>Designer paralelo de atividades
A atividade de <xref:System.Activities.Statements.Parallel> executa uma coleção de filhos atividades simultaneamente.  
  
## <a name="the-parallel-activity"></a>A atividade paralela  
 A atividade de <xref:System.Activities.Statements.Parallel> armazena as atividades filho em uma coleção de <xref:System.Activities.Statements.Parallel.Branches%2A> . Use a atividade de <xref:System.Activities.Statements.Parallel> em vez de atividade de <xref:System.Activities.Statements.Sequence> se algumas das atividades filho podem ir ociosa.  
  
 A atividade de <xref:System.Activities.Statements.Parallel> tem uma propriedade de <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> que contém uma expressão especificada usuário de [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] . A atividade de <xref:System.Activities.Statements.Parallel> avalia essa propriedade após cada ramificação completa. Se for avaliada como **verdadeira**, em seguida, a <xref:System.Activities.Statements.Parallel> atividade é concluído sem executar outros ramificações. Se o <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> não é avaliada como **verdadeira**, em seguida, a <xref:System.Activities.Statements.Parallel> atividade é concluída quando todas as suas atividades filho forem concluídas.  
  
### <a name="using-the-parallel-activity-designer"></a>Usando o designer paralelo de atividades  
 O **paralelas** designer de atividade pode ser encontrado na **fluxo de controle** categoria da **caixa de ferramentas**, que é acessado clicando o **caixa de ferramentas**guia no lado esquerdo do [!INCLUDE[wfd2](../includes/wfd2-md.md)] (como alternativa, selecione **barra de ferramentas** do **exibição** menu, ou CTRL + ALT + X.)  
  
 O **paralelas** designer de atividade pode ser arrastado da **caixa de ferramentas** e ser solto sobre a [!INCLUDE[wfd2](../includes/wfd2-md.md)] superfície onde quer que os designers de atividade são colocados normalmente, por exemplo, dentro de um **Sequência** designer de atividade. Após solto na [!INCLUDE[wfd2](../includes/wfd2-md.md)], ele cria um <xref:System.Activities.Statements.Parallel> atividade, que, por padrão, contém uma <xref:System.Activities.Activity.DisplayName%2A> de **paralela**  
  
 Para adicionar uma atividade para o <xref:System.Activities.Statements.Parallel.Branches%2A> coleção de atividade paralela, arraste outro designer de atividade do **caixa de ferramentas** e solte-o triângulo no **paralela** designer de atividade. Os triângulos flanqueiam as atividades contidas em ramificações. As atividades adicionais podem ser adicionadas repetindo este procedimento. As atividades podem ser reordenadas arrastando e soltando-os dentro de **paralela** designer de atividade.  
  
### <a name="parallel-activity-properties-in-the-workflow-designer"></a>Propriedades paralelas de atividade em Designer de Fluxo de Trabalho  
 A tabela a seguir mostra as propriedades paralelas de atividade e descreve como elas são usadas no designer.  
  
|Nome da Propriedade|Necessária|Uso|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|Especifica o nome amigável para exibição do designer de atividade no cabeçalho. O valor padrão é **paralela**. O valor pode ser editado no, opcionalmente, o **propriedades** grade ou diretamente no cabeçalho do designer de atividade.|  
|<xref:System.Activities.Statements.Parallel.Branches%2A>|verdadeiro|Contém a coleção de atividades filhos sejam executadas.|  
|<xref:System.Activities.Statements.Parallel.CompletionCondition%2A>|False|Avaliado após uma ramificação completa. Se for avaliada como **verdadeira**, então o agendada ramificações é cancelado. Se essa propriedade não está definida ou é avaliada como **falsos**, a atividade é concluída quando todas as suas atividades filho forem concluídas. O valor padrão é **nulo**.|  
  
## <a name="see-also"></a>Consulte também  
 [Sequência](../workflow-designer/sequence-activity-designer.md)   
 [ParallelForEach\<T >](../workflow-designer/parallelforeach-t-activity-designer.md)   
 [Fluxo de Controle](../workflow-designer/control-flow-activity-designers.md)