---
title: Designer de fluxo de trabalho - Designer de atividade de sequência
ms.date: 11/04/2016
ms.topic: reference
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Statements.Sequence.UI
ms.assetid: 51c8d3cb-4d43-458f-9631-b63755f9ac94
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 288e184f2ae2b4df74860a2cd8066d00e02a44c2
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49950583"
---
# <a name="sequence-activity-designer"></a>Arranje seqüencialmente o designer de atividades

A atividade de <xref:System.Activities.Statements.Sequence> contém uma coleção ordenada de atividades filhos que executa em ordem.

Outra maneira de executar um conjunto de atividades em ordem é usar uma atividade de <xref:System.Activities.Statements.Flowchart> . Considere o uso de [fluxograma](../workflow-designer/flowchart-activity-designer.md) quando você tiver uma ramificação simples ou um loop de fluxo do programa que você deseja modelagem esquematicamente.

## <a name="using-the-sequence-activity-designer"></a>Usando o designer de atividade de sequência

Para adicionar um <xref:System.Activities.Statements.Sequence> atividade, arraste o **sequência** designer de atividade dos **caixa de ferramentas** e solte-o para a superfície do Designer de fluxo de trabalho. Para adicionar uma atividade filho para esta <xref:System.Activities.Statements.Sequence> atividade, arraste alguma outra atividade do **caixa de ferramentas** e solte-a no triângulo na caixa com o texto de dica "Descartar atividade aqui".

### <a name="sequence-activity-properties-in-the-workflow-designer"></a>Propriedades de atividade da sequência em Designer de Fluxo de Trabalho

A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.Sequence> e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade ou na superfície de designer.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|Especifica o nome amigável do designer de atividade de <xref:System.Activities.Statements.Sequence> no cabeçalho. O valor padrão é sequência. O valor pode ser editado na grade de propriedade ou diretamente no cabeçalho do designer de atividade.<br /><br /> Embora não seja necessário <xref:System.Activities.Activity.DisplayName%2A> restrita, é uma prática recomendada usar um.|

## <a name="see-also"></a>Consulte também

- [Fluxograma](../workflow-designer/flowchart-activity-designer.md)
- [Fluxo de Controle](../workflow-designer/control-flow-activity-designers.md)