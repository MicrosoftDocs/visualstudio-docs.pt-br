---
title: Designer de fluxo de trabalho - Designer de atividade de StateMachine
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- StateMachine Designer
- System.Activities.Statements.StateMachine.UI
ms.assetid: 474d5fb3-1049-4b3f-bc6b-7524dbbe1672
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 59b1a194f4f301bd3080820b56c89044315c66e7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62809387"
---
# <a name="statemachine-activity-designer"></a>Designer de atividade de StateMachine

A atividade de <xref:System.Activities.Statements.StateMachine> contém uma coleção de estados e modelos de fluxos de trabalho usando o paradigma familiar do computador de estado.

## <a name="using-the-statemachine-activity-designer"></a>Usando o designer de atividade de StateMachine

Para adicionar um <xref:System.Activities.Statements.StateMachine> atividade, arraste o **StateMachine** designer de atividade dos **máquina de estado** seção o **caixa de ferramentas** e solte-o para o Designer de fluxo de trabalho superfície. Para adicionar um estado filho para esta <xref:System.Activities.Statements.StateMachine> atividade, arraste um <xref:System.Activities.Statements.State> ou <xref:System.Activities.Core.Presentation.FinalState> da **caixa de ferramentas** e solte-o no **StateMachine**.

### <a name="statemachine-activity-properties-in-the-workflow-designer"></a>Propriedades de atividade de StateMachine em Designer de Fluxo de Trabalho

A tabela a seguir mostra as propriedades de <xref:System.Activities.Statements.StateMachine> que podem ser definidas usando o designer de fluxo de trabalho e descreve como elas são usadas no designer. Essas propriedades podem ser editadas na grade de propriedade e alguns podem ser editados na superfície de designer.

|Nome da Propriedade|Necessária|Uso|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|Especifica o nome amigável do designer de atividade de <xref:System.Activities.Statements.StateMachine> no cabeçalho. O valor padrão é **StateMachine**. O valor pode ser editado na grade de propriedade ou diretamente no cabeçalho do designer de atividade. <xref:System.Activities.Activity.DisplayName%2A> é usado em navegação de rastreamento que é exibida na parte superior do designer de fluxo de trabalho.<br /><br /> Embora não seja necessário <xref:System.Activities.Activity.DisplayName%2A> restrita, é uma prática recomendada usar um.|

## <a name="see-also"></a>Consulte também

- [Fluxograma](../workflow-designer/flowchart-activity-designer.md)
- [Fluxo de Controle](../workflow-designer/control-flow-activity-designers.md)