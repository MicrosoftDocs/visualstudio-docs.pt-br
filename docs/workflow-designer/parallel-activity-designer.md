---
title: Designer de fluxo de trabalho - Designer de atividade paralela
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Statements.Parallel.UI
ms.assetid: 0306dc3b-075a-4091-ac3a-96486fbabed5
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 76e0d7646645c7d86859de7f79ff22a46131c4a5
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49863757"
---
# <a name="parallel-activity-designer"></a>Designer paralelo de atividades

A atividade de <xref:System.Activities.Statements.Parallel> executa uma coleção de filhos atividades simultaneamente.

## <a name="the-parallel-activity"></a>A atividade paralela

A atividade de <xref:System.Activities.Statements.Parallel> armazena as atividades filho em uma coleção de <xref:System.Activities.Statements.Parallel.Branches%2A> . Use a atividade de <xref:System.Activities.Statements.Parallel> em vez de atividade de <xref:System.Activities.Statements.Sequence> se algumas das atividades filho podem ir ociosa.

O <xref:System.Activities.Statements.Parallel> atividade tem um <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> propriedade que contém um usuário especificado a expressão do Visual Basic. A atividade de <xref:System.Activities.Statements.Parallel> avalia essa propriedade após cada ramificação completa. Se for avaliada como **verdadeira**, em seguida, a <xref:System.Activities.Statements.Parallel> atividade é concluído sem executar outros ramificações. Se o <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> não é avaliada como **verdadeira**, em seguida, a <xref:System.Activities.Statements.Parallel> atividade é concluída quando todas as suas atividades filho forem concluídas.

### <a name="using-the-parallel-activity-designer"></a>Usando o designer paralelo de atividades

Acesso a **paralelas** designer de atividade na **fluxo de controle** categoria dos **caixa de ferramentas**.

O **paralelas** designer de atividade pode ser arrastado da **caixa de ferramentas** e ignorados sobre a superfície do Designer de fluxo de trabalho onde quer que os designers de atividade são colocados normalmente, por exemplo, dentro de um **Sequência** designer de atividade. Depois de soltá-la para o Designer de fluxo de trabalho, ele cria um <xref:System.Activities.Statements.Parallel> atividade, que, por padrão, contém um <xref:System.Activities.Activity.DisplayName%2A> de **paralela**

Para adicionar uma atividade para o <xref:System.Activities.Statements.Parallel.Branches%2A> coleção de atividade paralela, arraste outro designer de atividade do **caixa de ferramentas** e solte-o triângulo no **paralela** designer de atividade. Os triângulos flanqueiam as atividades contidas em ramificações. As atividades adicionais podem ser adicionadas repetindo este procedimento. As atividades podem ser reordenadas arrastando e soltando-os dentro de **paralela** designer de atividade.

### <a name="parallel-activity-properties-in-the-workflow-designer"></a>Propriedades paralelas de atividade em Designer de Fluxo de Trabalho

A tabela a seguir mostra as propriedades paralelas de atividade e descreve como elas são usadas no designer.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|Especifica o nome amigável para exibição do designer de atividade no cabeçalho. O valor padrão é **paralela**. O valor pode ser editado no, opcionalmente, o **propriedades** grade ou diretamente no cabeçalho do designer de atividade.|
|<xref:System.Activities.Statements.Parallel.Branches%2A>|verdadeiro|Contém a coleção de atividades filhos sejam executadas.|
|<xref:System.Activities.Statements.Parallel.CompletionCondition%2A>|False|Avaliado após uma ramificação completa. Se for avaliada como **verdadeira**, então o agendada ramificações é cancelado. Se essa propriedade não está definida ou é avaliada como **falsos**, a atividade é concluída quando todas as suas atividades filho forem concluídas. O valor padrão é **nulo**.|

## <a name="see-also"></a>Consulte também

- [Sequência](../workflow-designer/sequence-activity-designer.md)
- [ParallelForEach\<T>](../workflow-designer/parallelforeach-t-activity-designer.md)
- [Fluxo de Controle](../workflow-designer/control-flow-activity-designers.md)